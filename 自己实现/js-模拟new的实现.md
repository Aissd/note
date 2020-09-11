### 原生new的使用
```
function Animal(type) {
	this.type = type; // 实例上的属性
}
Animal.prototype.say = function() {
	console.log('say');
}
let animal = new Animal('哺乳类');
console.log(animal.type); // '哺乳类'
animal.say(); // 'say'
```
### 手写模拟new的实现
```
function Animal(type) {
	this.type = type; // 实例上的属性
}
Animal.prototype.say = function() {
	console.log('say');
}

function mockNew() {
	let Constructor = [].shift.call(arguments); // shift =>移除arguments的第一位，返回被移除的元素，也就是new时传入的第一个参数=>类，即Constructor=>类，剩余的arguments就是其他的参数
	let obj = {}; // new之后返回的结果
	obj.__proto__ = Constructor.prototype; // 改变原型链指向，实现公共继承
	let r = Constructor.apply(obj, arguments); // 若构造函数返回的是一个引用类型，需要把该应用类型返回，否则返回obj
	return r instanceof Object ? r : obj;
}
let animal = mockNew(Animal, '哺乳类');
console.log(animal.type); // '哺乳类'
animal.say(); // 'say'
```