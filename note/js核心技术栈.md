1、js中的技术类型

```
1）基本数据类型
	number string boolean null undefined symbol bigint
2）引用数据类型
	object function
```

2、一些类型转换

```
！！ 若在计算表达式里，只要左右有一项是object或者是string，就会做字符串拼接

1）object + 0；// 对象会转换为字符串（toString）；
2）1 + null； // null会转化为0
3）1 + undefined； // undefined会转化为NaN
4）1 + NaN； // 任何类型和NaN做运算都会变为NaN
5）1 + true； // true会转换成1
6）1 - '12px'; // NaN
7）[].toString(); // '' - 在数学运算中会转换成空字符串
8）{}.toString(); // '[object Object]' - 在数学运算中会转换成


问题：为什么结果会不一样
1 + {}; // '1[object Object]'
{} + 1; // 1
```

3、把其他数据类型转换为number类型

```
1、特定需要转换为number的：
	1）Number(val); // 转换失败，会变成NaN - Number('1.2.1') - NaN
	2）parseInt(val)/parseFloat(val)
2、隐式转换（浏览器内部默认要先转换为number进行计算的）
	1）isNaN(val)
	2）数学运算（特殊情况：+在出现字符串的情况下是字符串拼接）
	3）在==比较的时候，有些值需要转换为数组再进行比较
```

4、把其他数据类型转换为字符串

```
1、能使用的办法
	1）toString()
	2）String()
2、隐式转换（一般都是调用其toString）
	1）加号运算的时候，如果某一边出现字符串，则是字符串拼接；
	2）把对象转为数字，需要先toString()转换为字符串，再去转换为数字；
	3）基于alert/confirm/promp/document.write...这些方式输出内容，都是内容先转为字符串，然后再输出的
	
```

5、把其他数据类型转换为布尔

```
1、基于以下方式可以把其他数据类型转换为布尔
	1）!转换为布尔值后取反
	2）!!转换为布尔类型
	3）Boolean(val)
2、隐式转换
	1）在循环或者条件判断中，条件处理的结果就是布尔类型
	
规则：
只有0,NaN,null,undefined,空字符串这五个值会变成布尔值的false，其余都是true
```

6、在==比较过程中，数据转换的规则：

```
1、类型一样的几个特殊点：
	1）{}=={}：false // 对象比较的是堆内存的地址
	2）[]==[]：false // 比较的是堆内存的地址
	3）NaN==NaN：false // NaN跟谁都不相等
2、类型不一样的转换规则
	1）null==undefined：true // 但是换成===结果是false（类型不一致）剩下null/undefined和其他任何数据类型都不相等；
	2）字符串==对象 // 要把对象转换成字符串
	3）剩下如果==两边数据类型不一致，都是需要转换为数组再进行比较

注意：等号优先级是比较低
1）[] == false; // true // == 比较，两边类型不一，先转换为数字类型。[]先转为字符串，变空字符串，再转数字类型，变成0；false转换为数字0，0==0相等，为true；
2）![] == false; // true // == 比较，由于优先级低，左侧也是表达式，先执行左侧，[]转换为true，取反则为false，false == false，所以为true
```

7、对象转字符串

```
1）会先调valueOf() 取原始值，如果没有，则调toString()
```

8、parseInt转换过程

```
1）parseInt(val); // 把val转换为数字（内核机制：需要把val先变为字符串，然后从字符串左侧第一个字符查找，把找到的有效数字字符转换为数字，直到遇到一个非有效数字字符为止）
2）parseInt(val, n); // 把val看作n进制数据，最后 转换为十进制
	n不写，默认是10，特殊情况字符串是以0X开头的，默认是16进制；
	n范围（2~36之间），不在这个之间的，除了0和10一样，剩下结果都是NaN
	
let arr = [10.18, 0, 10, 25, 23];
arr = arr.map(parseInt);
console.log(arr);

arr.map((item, index)=>{});
parseInt(10.18, 0);
	=> parseInt('10.18', 0);
	=> 0和10一样，是10进制的意思，即'10.18'转换成10进制，取整，即为10；
parseInt(0,1);
	=>parseInt('0', 1);
	=>0不在范围内，即为NaN
parseInt(10,2);
	=> parseInt('10', 2);
	=> 看做二进制，'10'这个二进制转换成十进制
	=> 0*2^0 + 1*2^1 => 0 + 2，即为2
parseInt(25,3);
	=> parseInt('25', 3);
	=> 看做三进制，由于三进制只有012，只有2符合，所以是把'2'这个三进制转换成十进制
	=> 2*3^0，结果为2
parseInt(23,4);
	=> parseInt('23', 4);
	=> 看做四进制，'23'这个4进制转换成十进制
	=> 3*4^0+2*4^1 = 3 + 8，结果为11
```

9、ECStack执行环境栈

```
概念：
1）EC(G) - 全局执行上下文
2）VO(G) - 全局变量对象
```

10、赋值

```
1、带有成员访问的要优先处理：
let a = { n: 1 };
let b = a;
a.x = a = { n: 2 }; // a.x先处理，先把{n:2}赋值给a.x；然后再{n:2}赋值给a
console.log(a.x); // undefined // 访问不存在的成员属性，返回undefined
console.log(b); // {n:1,x:{n:2}}
```

11、声明和定义

```
声明：创建变量
定义：给变量赋值
```

12、变量提升 - 在当前上下文，代码运行之前，会把所有带var变量进行声明，function进行声明或定义

```
变量提升：当前上下文执行前，会把var/function声明或者定义，带var的只声明，带function声明+定义；如果遇到了{}（块级作用域），新老浏览器标签不一致（为了向下兼容ES3，向上兼容ES6）
1）IE浏览器<=10：
	不管{}（块级作用域），function声明+定义，不存在块级作用域（全部都是全局）；
2）新版浏览器
	{}中的function，在全局下只声明不定义；
	{}中出现function/let/const会创建一个块级上下文
```

```
举个栗子：
var a = 0;
if(true) {
	a = 1;
	function a() {};
	a = 21;
	console.log(a);
}
console.log(a);

<= 10的IE浏览器：
1、var a = 0;
2、a = 1;
3、function a() {};
4、a = 21;
5、console.log(a); // 21
6、console.log(a); // 21

新版浏览器：
1、var a;function a; // 变量提升
2、a = 1;
3、function a() {}; // 遇到function，创建一个块级上下文，会把该代码之前所有对a的操作映射给全局一份，后面的都认为是私有的）
4、1中变量提升的a变成1;
5、a = 21; // 私有的
6、console.log(a); // 21，这是私有的
7、console.log(a); // 1，这是全局的
```

```
es6的块级作用域：
1）ES6中存在块级作用域，(只要{} - 除了对象之外的大括号，出现let，const，function，if...)
2）有一种情况也会产生：
	2.1）函数有形参赋值了默认值（至少一个）
	2.2）函数体中右单独声明过某个变量（var声明）
这样在函数运行的时候会产生两个上下文
	第一个：函数执行形成的私有上下文EX(FUNC) // 作用域链/形参赋值...
	第二个：函数体大括号抱起来的块级上次文EC（BLOCK）
```

13、new 原理

```
1、创建一个实例对象
// let obj = {};
// obj.__proto__ = X.prototype; // IE不支持
let obj = Object.create(X.prototype);
2、把方法执行，让里面的this指向实例对象
3、分析返回结果：返回结果是引用类型的（对象/函数）则当前返回结果；
if(result !== null && /^(object|function)$/.test(typeof result)) return result;
return obj; // 返回结果是基本类型或无返回值，则返回实例对象


function _new(Func, ...args) {
	// 1、创建一个实例对象
		// 1.1、IE不兼容
	// let obj = {};
	// obj.__proto__ = Func.prototype;
		// 1.2、IE不兼容
		// Object.setPrototypeOf(obj, Func.prototype);
		// 1.3、兼容IE
	let obj = Object.create(Func.prototype);
	// 2、把方法执行，让里面的this指向实例对象
	let result = Func.call(obj, ...args);
	// 3、分析返回结果
		// 3.1、返回结果是引用类型的（对象/函数）则当前返回结果；
	if(result !== null && /^(object|function)$/.test(typeof result)) return result;
		// 3.2、返回结果是基本类型或无返回值，则返回实例对象
	return obj;
}
```

14、手写call方法

```
~ function() {
	// context -> this要指向的上下文
	function change(context, ...args) {
		// this => func
		context = context = undefined ? window : context;
		let type = typeof context;
		if(!/^(object|function)$/.test(type)) {
			if(/^(symbol|bigint)$/.test(type)) { // symbol不是一个构造函数
				context = Object(context);
			} else {
				context = new context.constructor(context); // call和apply会自动调用
			}
		}
		let key = Symbol('key'), result; // 避免冲突
		context[key] = this;
		result = context[key](...args);
		delete context[key]; // 移除不会再使用的
		return result;
	}
	Function.prototype.change = change;
}();
```

15、手写bind（返回一个函数）

```
~ function() {
	// context -> this要指向的上下文
	function bind(context, ...args) {
		// this => func
		let _this = this;
		context = context = undefined ? window : context;
		let type = typeof context;
		if(!/^(object|function)$/.test(type)) {
			if(/^(symbol|bigint)$/.test(type)) { // symbol不是一个构造函数
				context = Object(context);
			} else {
				context = new context.constructor(context); // call和apply会自动调用
			}
			return function anonymous(...innerArgs) { 
				_this.call(context, ...args.concat(innerArgs));
			}
		}
	}
	Function.prototype.bind = bind;
}();
```

