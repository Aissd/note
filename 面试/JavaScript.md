### 前端的存储有几种方式，这些方式的区别是什么

### js有哪些数据类型

### js跳出循环有哪些方法

### 数组去重的方法

### 下面的代码打印什么内容
```
f2();
var num = 123;
function f1() {
	console.log(num); // 结果A
}
function f2() {
	var num = 456;
	f1();
}
console.log(num); // 结果B
```

### call和apply的区别是什么
都是Function原型上的方法，每个函数作为Function的实例，都可以调取原型上的call和apply，ta们都是用来改变this指向的。唯一区别就是call不固定参数，要求一个个传入，apply参数固定，把参数以数组形式传入。会立即执行。

3个以内参数，两个性能差不多，3个以上，call性能比apply的好

bind不会立即执行

### 箭头函数与普通函数的区别

1、箭头函数语法更简洁
2、箭头函数没有自己的this，ta里面的this是继承函数所处上下文中的this（使用call/apply等都无法改变this指向）