* 来源：JavaScript设计模式与开发实践

### 惰性加载函数

- 做一些兼容处理，不可避免一些嗅探工作，比如在各个浏览器中能够通用的事件绑定函数addEvent。

```
var addEvent = function(elem, type, handler) {
	if (window.addEventListener) {
		// 函数内部重写这个函数，重写之后的函数即是期望的addEvent函数
		// 在下一次进入addEvent函数的时候就不再存在条件分支语句
		addEvent = function(elem, type, handler) {
			elem.addEventListener(type, handler, false);
		}
	} else if (window.attachEvent) {
		addEvent = function(elem, type, handler) {
			elem.attachEvent('on' + type, handler);
		}
	}
	addEvent(elem, type, handler);
};
```

### 柯里化

### 去柯里化

### 函数节流

### 分时函数

- 创建好友列表，通常有成百上千个好友，若好友用一个节点来表示，当页面渲染这个列表时，可能需要一次性往页面创建成百上千个节点。容易造成浏览器卡顿甚至假死。

- 解决方案之一是下面的timeChunk函数，让创建节点的工作分批进行，比如把1秒钟创建1000个节点改为每隔200毫秒创建8个节点

```
// array - 创建节点时需要用到的数据
// fn - 封装了创建节点逻辑的函数
// count - 每一批创建节点的数量
var timeChunk = function(array, fn, count) {
	var obj, t;
	var len = array.length;
	var start = function() {
		for (var i = 0; i < Math.min(count || 1, array.length); i++) {
			var obj = array.shift();
			fn(obj);
		}
	}
	return function() {
		t = setInterval(function() {
			if (array.length === 0) { // 如果全部节点都已经被创建好
				return clearInterval(t);
			}
			start();
		}, 200); // 分批执行的时间间隔，也可以用参数的形式传入
	}
};
```