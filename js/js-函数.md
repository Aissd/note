1、函数提升

```
hd(); // houdunren.com 函数会提升

function hd() {
	console.log('houdunren.com');
}

var hd = function() {
	console.log('后盾人');
}
```

2、函数是对象

```
hd instanceof Object; // true
```

3、立即执行函数 - 立即执行，无需调用

```
;(function(window) {
	// 私有作用域，外界访问不到
	function hd() {
		console.log('hd');
	}
	function cmd() {
		console.log('cmd');
	}
	window.temp = { hd, cmd }; // 对外暴露
})(window);
```

4、当函数执行是，会开辟出一块新的内存地址，多次执行就开辟多个；