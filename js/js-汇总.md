1、js运行环境（也叫执行上下文）

```
1）全局：js执行的默认环境，若是浏览器，则会创建window对象；同时还是var声明全局变量的载体；
2）函数：每当一个函数被调用时都会创建一个函数上下文；且同一个函数被多次调用，都会创建一个新的上下文；
3）eval：eval函数执行内部代码创建上下文【不推荐】
```

2、js执行上下文（也叫执行栈或调用栈）

```
1）在js中，用栈的方式来管理执行上下文，称为执行栈（函数调用栈），遵循“先进后出，后进先出”的顺序存储。
2）在该栈中，
	处于最底部的就是我们最开始创建的全局执行上下文对象；
	处于栈顶的，就是当前正在执行的上下文。其他上下文处于等待的状态，这是因为js是单线程所致。
3）栈的执行流程：
	3.1）入栈：代码执行时，上下文被创建，并被压入栈中；
	3.2）执行：被压入的上下文处于栈顶，为当前的执行上下文。当这个函数被调用完成之后，当前的执行上下文被销毁；
	3.3）出栈：当前的执行上下文被销毁后会从栈顶被弹出，称为出栈，紧接着下一个上下文开始执行

参考地址：https://juejin.im/post/5e72e405f265da57112650bc
```

3、自定义错误处理

```
class ParamError extends Error {
	constructor(msg) {
		super(msg);
		this.name = 'ParamError';
	}
}

使用：
throw new ParamError('参数错误');
```

4、noscript标签的作用

```
用来定义在脚本未执行时的替代内容（文本）
可以用来检测浏览器是否支持脚本，若不支持脚本则可以显示noscript里的
```

5、reflow（回流）和repaint（重绘）

```
下面情况会导致回流发生：
1）改变窗口大小；
2）改变文字大小；
3）内容改变，如用户在输入框中敲字
4）激活伪类，如hover
5）操作class属性
6）计算offsetWidth和offsetHeight
7）设置style属性
https://www.cnblogs.com/Peng2014/p/4687218.html
```

6、import

```
import 命令是编译阶段执行的，在代码运行之前。
因此被导入的模块会先运行，而导入模块的文件会后执行。

这是commonJS中require()和import之间的区别，使用require()，你可以在运行代码时根据需要加载依赖项。

commonjs模块输出的是一个值的拷贝；es6模块输出的是值的引用；
commonjs模块是运行时加载的；es5模块是编译时输出接口；
commonjs模块是单个值导出，es6可以导出多个；
commonjs是动态语法，可以写在判断里；es6module静态语法只能写在顶层；
commonjs的this是当前模块，es6module的this是undefined

import 在生产环境下，会自动去除掉没用的代码
tree-shaking把没用到的代码，自动删除掉
es6模块会把结果放到default

test.js:
let sum = (a,b) => {
	return a + b;
}

export default {
	sum
}
a.js:
let calc from './test.js';
console.log(calc.sum(1,2));
let calc = require('./test.js');
console.log(calc.default.sum(1,2));
```

7、if , else if , else

```
不管在条件判断中写什么，最后总要把具体其计算出true/false来判断条件是否成立（把其他类型的值转换为布尔类型，只有0/NaN/''/null/undefined是false，其余都是true）
```

8、

```
在js中，+ - * / % 都是数学运算，除 + 以外，其余运算符在运算的时候，如果遇到了非数字类型的值，首先会转换为数字类型（Number()），然后再进行运算

+ 在js中除了数学相加，还有字符串拼接的作用（如果运算中遇到了字符串，则为字符串拼接，而不是数学相加）

{}+'str'; // NaN
[]+'str'; // 'str'
null+'str'; // 'nullstr'
undefined+'str'; // 'undefinedstr'
```

```
> < >= <= 这些是数学比较，遇到非数字类型的值，首先会转换为数字类型（Number），然后再进行运算

({}) > 5; // false
'str' > 5; // false
```

9、null代表的是空对象指针（没有指向任何的内存空间）， typeof null; // "object"

10、typeof检测数组/正则/对象，最后返回的都是"object"，因此无法细分对象

11、三元运算符

```
1）如果三元运算符中的某一部分不需要做任何的处理，用null/undefined/void 0 占位即可；
var num = 12;
num > 10 ? num++ : null;
2）如果需要执行多项操作，把其用小括号包裹起来，每条操作语句用逗号分隔；
var num = 12;
num >= 12 ? (num++, num *= 10) : null;
```

```
思考题：
var num = 12;
if(num > 0) {
	if(num < 10) {
		num++;
	} else {
		num--;
	}
} else {
	if(num == 0) {
		num++;
		num=num/10;
	}
}
改成三元运算符：
var num = 12;
num > 0 ? (num<10?num++:num--) : (num==0?(num++, num/=10):null);
```

12、n++ 和 n +=1完全一样吗？

```
如果操作的对象是字符串，则不同
var n = '10';
n++; // 11
n+=1; // '101'
如果遇到非有效数字做运算，则为NaN
```

13、switch

```
switch是强校验
```

14、for循环中的关键字：continue ， break

```
continue; // 结束本轮循环（循环体中continue后面的代码将不再执行），继续执行下一轮循环
break; // 强制结束整个循环，不做任何处理

思考题：
for(var i = 1; i <= 10; i += 2) {
	if(i <= 5) {
		i++;
		continue;
	} else {
		i -= 2;
		break;
	}
	i--;
	console.log(i);
}
console.log(i);
```

15、alert - 输出的都是字符串

16、赋值操作 = 

```
先走 = 左边的
let a = { n: 1 };
a.x = a = { n: 2 }; // 现在a的堆存中写x，之后开辟新的堆内存{n:2}，再关联
// a.x = a; a = { n: 2 };
```

17、js可以运行的环境

```
1）浏览器（内核/引擎）
2）webview
3）node.js
```

18、连等赋值，以右侧先运算

```
1）连等赋值，以右侧先运算
	a = b = 10;
	1.1）b = 10;
	1.2）a = 10;
2）但某些操作的优先级很高，比如a.x成员访问，它的优先级是19，比等号赋值搞，所以优先
	a.x = b = 10;
	2.1）a.x = 10;
    2.2）b = 10;
```

