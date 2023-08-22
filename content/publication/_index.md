---
title: Publications 
# View.
#   1 = List
#   2 = Compact
#   3 = Card
#   4 = Citation
view: 4

# Optional header image (relative to `static/img/` folder).
header:
  caption: ""
  image: ""
---
<div>
<i class="far fa-file-alt pub-icon" aria-hidden="true"></i>
Total: <p id="counter"></p>
</div>

<script language="javascript">
	document.body.onchange = function(){
        alert("ciao");
	var counter = document.getElementById("counter");
	var pubs = document.getElementsByClassName("pub-list-item");
	counter.textContent = pubs.length;
	}
</script>