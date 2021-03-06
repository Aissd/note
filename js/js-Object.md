### Object.freeze()
> 冻结对象 -  不允许删除，修改，追加属性，定义对象特征，遍历

```
const obj = {
	host: 'http://localhost',
	port: 80
};
Object.freeze(obj);
obj.port = 8080; // 无法修改，但不会报错，如果需要有提示，可以使用严格模式 "use strict" 声明。
```

```
Object.isFrozen(user); // 判断是否处于冻结状态
```

### Object.hasOwnProperty()
> 检测当前属性是否为对象的私有属性 - 不查找原型链

### attr in object
> 查找当前对象和原型链

### Object.setPrototypeOf(a, b) - 把b改成a的原型
> 改变原型  - a的原型链指向b
```
let obj1 = { name: 'xxx' };
let obj2 = { age: 18 };
obj1.__proto__ = obj2; // obj1的原型指向obj2
等价于
Object.setPrototypeOf(obj1, obj2);

// 获取obj1原型
Object.getPrototypeOf(obj1);
```

### Object.getPrototypeof
> 查找原型（父亲）

```
let obj = {};
Object.getPrototypeof(obj);
```

### enumerable: true
> Object的属性特征 - 这样可以被遍历，Object.keys输出来；

### configurable: true
> Object的属性特征 - 这样可以被删除或者是修改配置
> 控制不允许向对象添加属性

```
const user = {};
Object.preventExtensions(user);
user.site = 'aaa'; // 无法添加，严格模式下会报错

if(Object.isExtensible(user)) {} // 可以用这个判断是否可以添加属性
```

### Object.seal(user); 
> 封闭对象 - 不允许删除属性，追加属性，定义对象特征

```
Object.isSealed(); // 判断对象是否处于封闭状态
```

### Object.getOwnPropertyDescriptors(user)
> 获取对象的属性特征

### 对象的属性访问器

```
// 访问器伪造属性：
let obj = {
	list: [
		{price: 10},
		{price: 20},
		{price: 30},
		{price: 40}
	],
	get total() {
		return this.list.reduce((total, item) => total + item, 0);
	}
};

console.log(obj.total); // 100
```

### 创建一个没有原型的对象

```
// 第一次参数是指定的原型，传null则没有
let obj = Object.create(null, {
	name: {
		value: 'hd'
	}
});
console.log(obj);
```

### 一般是实例调用

```
function User() {}
let user = new User();
user.__proto__.view = function() {
	console.log('123');
}
```

### prototype一般是对象（Object，Function...）调用

```
User.prototype.show = function() {
	console.log('abc');
}
```

```
let o = {};
o.__proto__ == Object.prototype; // true
```

### 给对象设置原型

```
let hd = { name: 'hd' };
let parent = { name: 'parent' };
Object.setPrototype(hd, parent); // 给hd设置原型，为parent
```

### super	

```
super == this.__proto__
```

### in
> 检测当前对象是否存在某个属性（包括原型链上的）

### Object.assign()
> 合并对象（浅拷贝）

```
let name = { name: 'xxx' };
let age = { age: 18 };
let obj = Object.assign(name, age);
// 等价于
let res = Object.assign(obj, name, age);
// 等价于
let obj = {...name, ...age};
```

### super关键字
> 获取原型上的属性

```
let obj1 = {
	age: 9,
	name: 'jw'
}

let obj2 = {
	name: 'zfpx',
	getPName() {
		return super.name
	},
	__proto__: obj1
};
console.log(obj2.getPName()); // 'jw'
```

### Object.defineProperty

### Object.valueOf
> 返回该对象的原始值