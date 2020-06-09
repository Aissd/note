1、变量提升

```
var web = 'google.cn';
console.log(web);
var class = 'google'; // 这里会报错，因为用了class关键字

但结果是，连web都不会输出，而是报了个class的语义错误。
原因是var存在变量提升，即解析器在代码执行前会分析一遍代码，当分析到class时发现错误，就立马抛出错误来；
```

```
console.log(web);
var web = 'google.cn';

结果输出的是 undefined
原因是解析器在代码执行前会分析一遍代码
```

2、暂时性死区（要使用之前必须声明，否则报错）

```
let web = 'facebook.com';
function fn() {
	console.log(web);
	let web = 'google.com'; // 报错，let不存在变量提升，需要先声明再使用
}
fn();
```

3、let 有块级作用域，var没有

let 不允许重复声明

```
let a = 1;
let a = 2; // 报错
```

```
// let有块级作用域
{
	let a = '123'; 
}
console.log(a); // 报错，Uncaught ReferenceError: a is not defined
```

```
3）var无块级作用域
{
	var a = '123';
}
console.log(a); // 123
```

4、arguments不是数组类型 

5、箭头函数

​	1）不适合在事件处理的匿名函数（this问题）

​	2）不适合在递归中使用（没有函数名）

​	3）箭头函数中的this指向的是上下文（即父级作用域中的this）

6、函数与方法中this的的不同

​	1）如果函数为对象的方法（类方法），this就是当前对象

​	2）如果函数只是普通函数，this就是window

7、改变this指针

```
 // 方法一，通过常量保留this指针
let obj = {
	site: 'abc',
	list: [1,2,3],
	show: function() {
		let self = this;
		return this.list.map(function(value) {
			return `{self.site}-${value}`;
		});
	}
};

 // 方法二，传递函数第二个参数
 let obj = {
	site: 'abc',
	list: [1,2,3],
	show: function() {
		let self = this;
		return this.list.map(function(value) {
			return `{this.site}-${value}`; // 2）这里的this就是map函数第二个参数传进来的this
		}, this); // 1）这里，把show方法的this传进去
	}
};
```

