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

4、class属性继承的原理

```
// 原型链方式
function User(name) {
	this.name = name;
}

function Admin(name) {
	User.call(this, name);
}

Admin.prototype = Object.create(User.prototype); // Admin的原型指向User的原型（继承）
Admin.prototype.show = function() {}; // 在Admin的原型上添加show方法，跟在User的原型上添加效果一致；
let hd = new Admin('后盾人'); // 实例
console.log(hd);
```

```
// class方式
class User() {
	constructor(name) {
		this.name = name;
	}
}

class Admin extends User {
	constructor(name) {
		super(name); // 调用父级的constructor
	}
}

let hd = new Admin('后盾人');
console.log(hd);
```

5、类的方法继承原理

6、super原理分析

```
// class 方式
class User {
	show() {
		consol.log(this.name);
	}
}
class Admin extends User {
	constructor(name) {
		super();
		this.name = name;
	}
	show() {
		super.show(); // 调用父级的show方法
		console.log('admin.show')
	}
}

console.dir(Admin);
let hd = new Admin('后盾人');
hd.show();
```

```
//
let hd = {
	name: 'hd.name',
	show() {
		console.log(this.name);
	}
};
let xj = {
	__proto__: hd, // 原型继承hd
	name: 'xj.name',
	show() { // 要用super，必须这么写，show: function() {}  这样会报错
		super.show(); // 调用父级的方法
		// this.__proto__.show.call(this); // 改变调用show时的this为xj // 如果这么写，两层是没问题的，多层的话，this到第三层就不对了
		// this.__proto__.show(); // 如果这么写，打印出来的是hd.name，则错误，继承只是用父级的方法，但该方法打印出来的name需要的是当前的对象才对
	}
};
xj.show();
```

7、为什么子类的constructor要调用super

```
function User(name) {
	this.name = name;
}
// call - 单个属性时
function Admin(name) {
	User.call(this, name); // 没有这句，输出来的hd是个继承了User的空对象而已，没有name属性
}
// 多个属性时
// function Admin(...args) {
//     User.apply(this, args); // 没有这句，输出来的hd是个继承了User的空对象而已，没有name属性
//     User.call(this, ...args); // call的写法
// }

Admin.prototype = Object.create(User.prototype);
let hd = new Admin('后盾人');
console.log(hd);
```

```
class User {
	constructor(name) {
		this.name = name;
	}
}

class Admin extends User {
	constructor(...args) {
		super(...args); // 若显性的写了constructor，那必须使用super()调用父类的构造函数，并传递参数
		this.site = 'houdunren.com'; // 且如果要重写属性，那必须先调用super()，不然优先级比父级的同名属性低，会被覆盖
	}
}

let hd = new Admin('后盾人');
console.log(hd);
```

8、静态继承 原理

```

```

