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

只有块级作用域内存在let 、const关键字声明的变量，js会将该变量声明移入暂时性死区中，访问暂时性死区的变量会触发运行时的错误。只有执行let、const变量声明语句之后，该变量声明才会从暂时性死区移除，才可正常访问。

```
let web = 'facebook.com';
function fn() {
	console.log(web);
	let web = 'google.com'; // 报错，let不存在变量提升，需要先声明再使用
}
fn();
```

```
var tmp = 10;
if(true) {
	tmp = 20; // 试图访问暂时性死区的变量，报错
	let tmp;
}

function fn(x=y, y=2) {
	return [x,y];
}
fn(); // 报错
```

3、let 有块级作用域，var没有

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

```
{
    var a = 10;
}
{
    let a = 20;
    ++a;
    console.log(a); // 21
}
console.log(a); // 10
```

let、const禁止重复声明

```
let b = 10;
let b = 20; // 抛出重复声明错误

var c = 10;
let c = 10; // 抛出重复声明错误

let d = 10;
var d = 10; // 抛出重复声明错误
```

ES3开始，try/catch结构在catch分局中具有块作用域

```
try {
    throw undefined;
} catch(a) {
    a = 2;
    console.log(a); // 2
}
console.log(a); // 报未定义错误
```

4、提升机制

```
1）先声明再赋值；
2）函数声明和var声明都会被提升；
3）函数会首先被提升
```

5、const定义的变量是一个常量，必须初始化，且初始化之后不能修改绑定（string，number，boolean...）

但允许修改值（object，array）

