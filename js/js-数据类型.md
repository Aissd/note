1、typeof

```
1）底层机制：直接在计算机底层基于数据类型的值（二进制）进行检测
2）typeof null "object"，对象存储在计算机中，都是以000开始的二进制存储，null也是，所以检测出来是对象
3）typeof 普通对象/数组对象/正则对象/日期对象 "object"


```

2、instanceof - 检测当前实例是否属于这个类

```
1）底层机制：只要当前类出现在实例的原型链上，结果都是true

let arr = [];
console.log(arr instanceof Array); // true
console.log(arr instanceof RegExp); // false
console.log(arr instanceof Object); // true

2）由于可以肆意修改原型的指向，所以检测出来的结果是不准的
function Fn() {
	this.x = 100;
}
Fn.prototype = Object.create(Array.prototype);
let f = new Fn;
console.log(f instanceof Array);

3）instanceof 不能检测基本数据类型
console.log(1 instance Number); // false

// 实例，要监测的类
function instance_of(example, classFunc) {
	// 实例.__protp__ === 类.prototype;
	// 类的原型
	let classFuncPrototype = classFunc.prototype,
		proto = Object.getPrototypeOf(example); // example.__proto__ （ie不支持）
	while(true) {
		if(proto === null) {
			// Object.prototype.__proto__ => null
			return false;
		}
		if(proto === classFuncPrototype) {
			// 查找过程中发现有，则证明实例是这个类的一个实例
			return true;
		}
		proto = Object.getPrototypeOf(proto);
	}
}

let arr = [];
console.log(instance_of(arr, Array);
```

3、constructor  - 

```
1）支持检测基本类型
let arr = [];
console.log(arr.constructor === Array); // true
console.log(arr.constructor === RegExp); // false
console.log(arr.constructor === Object); // false
let n = 1;
console.log(n.constructor === Number); // true

2）constructor可以随便改，所以也不准
Number.prototype.constructor == 'AA';
let n = 1;
console.log(n.constructor === Number); // false
```

4、Object.prototype.toString.call([value]); - 标准检测数据类型的办法 - 返回当前实例所属类的信息

```
let obj = { name: '珠峰培训' };
alert(obj); // 会调用toString [object Object]
// obj.toString(); => [object Object] 通过找到Object原型链上的toString方法

推测：是不是只要把Object.prototype.toString执行，让它里面的this变为要监测的值，那就能返回当前值所属类的信息
// "[object Number/String/Boolean/Null/Undefined/Symbol/Object/Array/Regex/Function/Date/NaN]"
Object.prototype.toString.call(1); 
Object.prototype.toString.call(NaN);
Object.prototype.toString.call('');
Object.prototype.toString.call(true);
Object.prototype.toString.call([]);
Object.prototype.toString.call(/^$/);
Object.prototype.toString.call(new Date());
Object.prototype.toString.call(undefined);
Object.prototype.toString.call(null);
Object.prototype.toString.call(Symbol('xx'));
Object.prototype.toString.call(function() {});
Object.prototype.toString.call(BigInt);
Object.prototype.toString.call(Error);
```

5、

```
基本数据类型是按值操作
引用数据类型是按地址来操作
```

