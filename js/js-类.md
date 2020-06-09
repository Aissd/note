1、class原理（使用的是原型机制）

```
// 类方式 - 默认使用严格模式
class User {
	constructor(name) { // 为类的属性初始化
		this.name = name;
	}
	show() {} // 自动把show方法添加到原型上去 - 为不可枚举
}

// 判断User的构造函数是否等于User原型的constructor
console.log(User === User.prototype.constructor); // true

let u = new User();

// 打印出这个对象（而不是原型链）的所有方法
console.log(Object.getOwnPropertyNames(u)); // ['name'] 

// 打印出原型链的所有方法
console.log(Object.getOwnPropertyNames(User.prototype)); // ['constructor', 'show']
```

```
// 构造函数方式
function Hd(name) {
	this.name = name;
}
Hd.prototype.show = function() {} // 手动把show方法添加到原型上去 - 可枚举

// 判断Hd的构造函数是否等于Hd原型的constructor
console.log(Hd === Hd.prototype.constructor); // true

let h = new Hd();

// 打印出这个对象（而不是原型链）的所有方法
console.log(Object.getOwnPropertyNames(h)); // ['name'] 

// 打印出原型链的所有方法
console.log(Object.getOwnPropertyNames(Hd.prototype)); // ['constructor', 'show'] 
```

2、静态属性

```
class Request {
	static host = 'http://www.google.cn'; // 静态属性，为类所有，共用的属性
	api(url) {
		return Request.host + `/${url}`;
	}
}

let obj = new Request();
console.log(obj.api('article'));
```

3、静态方法实现原理

```
function User() {}
User.show = function() {
	console.log('static.show')
}
```

