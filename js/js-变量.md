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

