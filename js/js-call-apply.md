1、call 和 apply

Function.prototype.call(thisArg, arg1, arg2, ...)

Function.prototype.apply(thisArg, [arg1, arg2, ...])

第一个参数thisArg就是要改变this指针的对象，后面的就是要传递的参数

区别就是apply接收的是数组，call接收的是一个个的参数；

共同点是，会立即执行。

```
let lisi = { name: '李四' };
function User() {
	console.log(this.name);
}
User.call(lisi); // 李四 - 会把lisi传递给User构造函数的this，从而改变this的指针，然后立即执行，输出this.name
User.apply();
```

注意：不需要改变this时，传null即可

2、bind

Function.prototype.bind()

不会立即执行

```
function hd(a, b) {
	return this.f + a + b;
}

（第一种传参方式）
let func = hd.bind({ f: 1 }, 2, 3); // 返回的是一个新函数（{ f : 1 }传递给了hd的this）
console.log(func()); // 6 这样才会调用

（第二种传参方式）
let func = hd.bind({ f: 1 }); // 返回的是一个新函数
console.log(func(2, 3)); // 6 这样才会调用
```

