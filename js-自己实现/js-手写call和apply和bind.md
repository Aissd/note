### Function.prototype.call() -  call

#### 特点
* 可以改变当前函数的this
* 绑定后立即函数执行
* 可传入多个参数【apply需要传入一个数组】
```
function fn() { console.log(this); }
fn.call(); // 不传参数时，this指向window

fn.call('hello'); // String {'hello'}
```
> 常见面试题
```
function fn1() { console.log(1); }
function fn2() { console.log(2); }
fn1.call(fn2); // 1
fn1.call.call(fn2); // 2 => 如果多个call会让call方法执行，并且把call中的this变成fn2
```

```
原理：
let obj = {};
function fn() { 
	console.log(this); 
};

obj.$$ = fn;
obj.$$(); // => this为obj本身
fn(); // => this为window
```


### 手写call - 方法一：
```
Function.prototype.myCall = function call(context, fn) {
	// context => obj
	// this => fn
	// args => 传进去的参数
}
```
### 手写call - 方法二：
```
// context - 上下文，没传则指向window
Function.prototype.myCall = function(context) {
	context = context ? Object(context) : window; // Object(context) => 避免传入一个字符串'hello'，使得this='hello'这种错误的语法
	context.fn = this;
	let args = [];
	for(let i = 1; i < arguments.length; i++) {
		args.push('arguments[' + i + ']');
	}
	// 利用数组的totring的特性 => [1,2].toString(); // '1,2'
	let r = eval('context.fn(' + args + ')'); // 执行函数
	delete context.fn; // 释放内存
	return r; // 返回fn的return值，fn无显示return时则是undefined
}
```

### 手写apply - 方法一：
```
Function.prototype.myApply = function(context, args) {
	context = context ? Object(context) : window;
	context.fn = this;
	if(!args) {
		return context.fn();
	}
	let r = eval('context.fn(' + i + ')');
	delete context.fn;
	return r;
}
```

### Function.prototype.bind - bind
```
let obj = {
	name: 'jw'
}
function fn() {
	console.log(this.name); // 直接在外面调用fn，输出的是undefined，因为this指向的是window
}
let bindFn = fn.bind(obj); // 把fn绑定到obj上，this指向了obj，返回的是一个绑定后的方法，bindFn并不会自动执行
bindFn(); // 'jw'
```
### bind的特点
> 1）bind方法可以绑定this指向
> 2）bind方法返回一个绑定后的新函数（高阶函数），并拥有指定的this值和初始参数
> 3）如果返回的绑定函数被new了，当前函数的this就是当前实例

### 手写bind - 方法一：
```
Function.prototype.myBind = function(context) {
	let that = this;
	let bindArgs = Array.prototype.slice.call(arguments, 1); // 获取传入的其他参数，从第二个开始截取到最后（第一个是上下文），返回一个新的数组
	function Fn() {};
	function fBound() {
		let args = Array.prototype.slice.call(arguments);
		return that.apply(this instanceof fBound ? this : context, bindArgs);
	}
	Fn.prototype = this.prototype;
	fBound.prototype = new Fn();
	return fBound
}
```