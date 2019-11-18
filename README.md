Search Word:
<input type="text" name="word" id="word" value="word">
<button onclick="return search();">search</button>
<br/>
<button onclick="return reset();">reset</button><br/>
<br/>
<div id="content">
<br/>
</div>
<script>

if (localStorage.getItem("dictionary")) {
	var dictionary = JSON.parse(window.localStorage.getItem("dictionary"));
	var content = "";
	for (var key in dictionary) {
		content += "<a href='https://www.google.com/search?&q=define:'"+key+"'>"+key+"</a><br/>"
	}
	//alert(content);
	document.getElementById("content").innerHTML = content;
}
function reset( ) {
	var dictionary = {};
	window.localStorage.setItem("dictionary", JSON.stringify(dictionary));
}
function search( ) {
    if (!localStorage.getItem("dictionary")) {
       reset();
    }
	var dictionary = JSON.parse(window.localStorage.getItem("dictionary"));
	var entry = document.getElementById('word').value.trim();
	if (entry =='')
	{
		return;
	}
	if (!dictionary[ entry ] )
	{
		dictionary[ entry ] = entry;
		
		window.localStorage.setItem("dictionary", JSON.stringify(dictionary));
		document.getElementById("content").innerHTML = document.getElementById("content").innerHTML.concat("<a href='https://www.google.com/search?&q=define:'").concat(entry).concat("'>").concat(entry).concat("</a><br/>");
	}
	
	
	
	window.location = "https://www.google.com/search?&q=define:" + entry;
}
</script>
