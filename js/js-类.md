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
function User() {} // 既是函数也是对象
User.show = function() { // 静态函数
	console.log('User.static.method');
}
User.site = 'hdcms.com'; // 静态属性

function Admin() {}
Admin.__proto__ = User; // Admin的__proto__属性指向User
Admin.show(); // User.static.method
console.log(Admin.site); // hdcms.com
```

```
class User {
	static show() {
		console.log('User.static.show');
	}
	site: 'hdcms.com'
}

class Admin extends User {}
Admin.show(); // User.static.method
consoloe.dir(Admin.site); // hdcms.com
```

9、instanceof 检测原型链

![image-20200611122303778](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20200611122303778.png)

```
function User() {}
function Admin() {}
Admin.prototype = Object.create(User.prototype);
let hd = new Admin();

console.log(hd instanceof Admin); // true - Admin在hd的原型链上
console.log(hd instanceof User); // true - User在hd的原型链上
console.log(hd.__proto__ == Admin.prototype); // true - hd的__proto__与Admin的原型是同一个
console.log(hd.__proto__.__proto__ == Admin.prototype.__proto__); // true
console.log(Admin.prototype.__proto__.__proto__.__proto__); // null - 原型链到头了

查找是否在原型链上
function checkPrototype(obj, constructor) {
	if(!obj.__proto__) return false;
	if(obj.__proto__ == constructor.prototype) return true;
	return checkPrototype(obj.__proto__, constructor);
}

console.log(checkPrototype(hd, Admin)); // true
console.log(checkPrototype(hd, User)); // true
```

10、isPrototypeOf 检测继承关系

```
let a = {};
let b = {
	__proto__: a // 继承a
};
let c = {
	__proto__: b // 继承b
};
console.log(a.isPrototypeOf(b)); // true - b是不是由a实现的（a是否存在于b的原型链上）
console.log(a.isPrototypeOf(c)); // true - c是不是由a实现的（a是否存在于c的原型链上）
console.log(c.isPrototypeOf(a)); // false - a是不是有c实现的（c是否存在于a的原型链上）
```

```
class Common {}
class User extends Common {}
class Admin extends User {} 
let hd = new Admin();
console.log(Admin.prototype.isPrototypeOf(hd)); // true - hd是不是有Admin的原型实现的（Admin的原型是否存在于hd的原型上）
console.log(Common.prototype.isPrototypeOf(hd)); // true - hd是不是有Common的原型实现的（Common的原型是否存在于hd的原型上）
```

11、使用原型增强内置类的实现（增强，扩充内置类）

```
// 原型方式实现
function Arr(...args) {
	args.forEach(item => this.push(item)); // 把数据都放进Arr
	// 扩充 - 获取数组第一个元素
	this.first = function() {
		return this[0];
	}
	// 扩充 - 获取数组中的最大值
	this.max = function() {
		return this.sort((a, b) => b - a)[0];
	}
}

Arr.prototype = Object.create(Array.prototype); // Arr继承内置的Array
let hd = new Arr(99, 1, 2, 3, 4, 56, 195);
console.log(hd.max()); // 195
console.log(hd.first()); // 99
```

12、使用class增强内置类的实现

```
class Arr extends Array {
	constructor(...args) { // 若没有传入参数，可以不写这个构造函数
		super(...args);
	}
	first() {
		return this[0];
	}
	max() {
		return this.sort((a, b) => b - a)[0];
	}
}

let hd = new Arr(99, 1, 2, 3, 4, 56, 195);
console.log(hd.max()); // 195
console.log(hd.first()); // 99
```

13、mixin混合模式使用技巧（类似多继承）

```
let Tool = {
	max(key) {
		return this.data.sort((a, b) => b[key] - a[key])[0];
	}
}
let Arr = {
	count(key) {
		this.data.reduce((t, c) => t + c[key], 0);
	}
}
class Lesson {
	constructor(lessons) {
		this.lessons = lessons;
	}
	get data() {
		return this.lessons;
	}
}

const data = [
	{ name: 'js', price: 100, click: 188 },
	{ name: 'mysql', price: 212, click" 34 },
	{ name: 'vue.js', price: 98, click: 89 }
];

Object.assign(Lesson.prototype, Tool, Arr); // 原型也是对象，往Lesson.prototype添加Tool

let hd = new Lesson(data);
console.log(hd.max('price')); // { name: 'mysql', price: 212, click" 34 }
console.log(hd.count('price')); // 410
```

