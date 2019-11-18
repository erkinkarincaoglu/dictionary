
Search:
<input type="text" name="word" id="word" value="word">
<button onclick="return search();">search</button>
<br/>
<button onclick="return reset();">clear</button><br/>
<br/>
<div id="content">
</div>
<script>

if (localStorage.getItem("dictionary")) {
	var dictionary = JSON.parse(window.localStorage.getItem("dictionary"));
	var content = [];
	for (var key in dictionary) {
		content.push ( createWordLink(key) );
	}
	for (var i=content.length-1;i>=0;i--) {
		document.getElementById("content").innerHTML +=content[i];
	}
}
function reset( ) {
	window.localStorage.setItem("dictionary", "{}");
	location.reload(true);
}

function createWordLink(entry) {
	return "<a href='https://www.google.com/search?q=define:".concat(entry).concat("'>").concat(entry).concat("</a><br/>");
}
function search( ) {
	var entry = document.getElementById('word').value.trim();
	if (!entry) {
		return;
	}
	var dictionary = JSON.parse( localStorage.getItem("dictionary") ? localStorage.getItem("dictionary") : "{}");
	if (!dictionary[ entry ] )
	{
		dictionary[ entry ] = entry;
		window.localStorage.setItem("dictionary", JSON.stringify(dictionary));
		document.getElementById("content").innerHTML = createWordLink(entry).concat(document.getElementById("content").innerHTML);
	}
	window.location = "https://www.google.com/search?&q=define:" + entry;
}
</script>
