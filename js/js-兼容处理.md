### event
```
window.addEventListener('click', function(ev) {
	var e = ev || window.event; // window.event是IE引入的属性
	var tar = e.target || e.srcElement; // 当前事件的源，e.srcElement是IE的一种规范
	var tagName = tar.tagName.toLowerCase();
}, false);
```