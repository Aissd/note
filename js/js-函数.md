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

箭头函数没有变量提升

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

5、箭头函数

```
1）不适合在事件处理的匿名函数（this问题）
2）不适合在递归中使用（没有函数名）
3）箭头函数中的this指向的是上下文（即父级作用域中的this）
```

6、arguments不是数组类型 

```
typeof arguments; // object
```

7、call和apply的区别是什么？哪个性能更好一些？

```
1）call和apply是Function原型上的方法，每个Function的实例都可以调原型上的这两个方法；
2）这两个方法执行的目的都是改变函数中的this指向；
3）区别在于call的参数是一个一个传递的，而apply的参数是以数组形式传递的
相类似的还有方法bind， bind也是用来改变函数中的this指向，bind没有把函数立即执行，只是预先改变this

性能上，传三个以内参数差不多，三个以上时，call的性能更佳。

fn.call(obj, 10, 20, 30);
fn.apply(obj, [10, 20, 30]);
```

8、回调函数

```
回调函数中的this一般都是window
```

