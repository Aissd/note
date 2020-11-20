### 语法
1）区分大小写
2）标识符
	2.1）第一个字符必须是字母，下划线，或美元符号；
	2.2）剩下的其他字符可以是字母，下划线，美元符号或数字
	2.3）关键字，保留字，true，false，null不能作为标识符

### 变量提升

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

### 暂时性死区（要使用之前必须声明，否则报错）

> 如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。

```
let web = 'facebook.com';
function fn() {
	console.log(web);
	let web = 'google.com'; // 报错，let不存在变量提升，需要先声明再使用
}
fn();

暂时性死区，意味着typeof不再是百分百安全的操作：
typeof x; // Uncaught ReferenceError: x is not defined
let x = 10;

typeof y; // 'undefined'
var y = 10;
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

### let 有块级作用域，var没有

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

> let、const禁止重复声明

```
let b = 10;
let b = 20; // 抛出重复声明错误

var c = 10;
let c = 10; // 抛出重复声明错误

let d = 10;
var d = 10; // 抛出重复声明错误

function fn(x) {
	let x = 10; // 重复声明
}
```

> ES3开始，try/catch结构在catch分局中具有块作用域

```
try {
    throw undefined;
} catch(a) {
    a = 2;
    console.log(a); // 2
}
console.log(a); // 报未定义错误
```

### 提升机制

* 1）先声明再赋值；
* 2）函数声明和var声明都会被提升；
* 3）函数会首先被提升

### const定义的变量是一个常量，必须初始化，且初始化之后不能修改绑定（string，number，boolean...）

> 但允许修改引用类型的值（object，array）

### 变量的赋值可分为三个阶段：
* 创建变量，在内存中开辟空间；
* 初始化变量，将变量初始化为undefined；
* 真正赋值
关于let，var，function
* let的【创建】过程被提升了，但是初始化没有提升
* var的【创建】和【初始化】都被提升了
* function的【创建】，【初始化】和赋值都被提升了