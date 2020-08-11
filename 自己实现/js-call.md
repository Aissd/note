call

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



```
Function.prototype.myCall = function call(context, fn) {
	// context => obj
	// this => fn
	// args => 传进去的参数
}
```

