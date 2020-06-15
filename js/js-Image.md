

```
function loadImage(src, resolve, reject) {
	let image = new Image();
	image.src = src;
	image.onload = () => {
		resolve();
	}
	image.onerror = reject;
}

loadImage('xxx.png', image => {
	document.body.appendChild(image);
}, () => {
	console.log('加载失败')
})
```

