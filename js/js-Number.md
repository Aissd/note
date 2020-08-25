1、isNaN检测的机制

```
1）首先检验当前要检验的值是否为有效数字类型，如果不是，浏览器会默认的把值转换为数字类型；
	1.1)把非数字类型的值转换为数字：
		1.1.1）其他基本类型转换为数字：直接使用Number()这个方法转换
		1.1.2）
			字符串转数字
                Number('13px'); // NaN =>如果当前字符串中出现任意一个非有效数字字符，结果为NaN
                isNaN('13px'); // true
                Number('13.5'); // 可识别小数
                Number('13.5.5'); // NaN
             布尔值转数字
                 Number(true); // 1
                 Number(false); // 0
             其他
                 Number(null); // 0
                 Number(undefined); // NaN
             对象
             	({}).toString(); // "[object Object]" - Number({}); // NaN
             数组
             	[12,23].toString(); // "12,23" - Number([12,23]); // NaN
             	[12].toString(); // "12" - Number([12]); // 12
             	[].toString(); // "" - Number([]); // 0
             正则
             	/^$/.toString(); // "/^$/" - Number(/^$/); // NaN
             
		1.1.3）把引用数据类型值转换为数字：先把引用值调取toString转换为字符串，然后再把字符串调取Number转换为数字。
2）当前检测的值已经是数字类型，是有效数字返回false，不是返回true（数字类型中只有NaN不是有效数字，其余都是有效数字）
```

2、Number() , parseInt() , parseFloat() 区别

```
区别在于字符串转换分析上：
	Number()：出现任意非有效数字字符，结果就是NaN
	parseInt()：把一个字符串中的整数部分解析出来（从字符串最左字符开始查找有效数字字符，并且转为数字。但遇到一个非有效数字字符，查找结束。）
	parseFloat()：那一个字符串中小数（浮点数）部分解析出来
	
	parseInt('13.5px'); // 13
	parseInt('width: 13.5px'); // NaN
	parseFloat('13.5px'); // 13.5
```

3、NaN的比较

```
console.log(NaN == NaN); // false - NaN和谁都不相等，包括自己
```

4、检测是否为一个有效数字：

```
if(!isNaN(num)) {
	// 检验是否为有效数字，只有这一种方案
}
```

5、最大安全数字

```
Number.MAX_SAFE_INTEGER

超过最大安全数字来进行运算就不准确了
可以转为bigint类型来处理

9007199254740991n

typeof 9007199254740991n; // "bigint" 
```

6、数字类型有几个特殊的值

```
1）NaN - 非有效数字
2）Infinity - 无穷大，大于任何数值
3）-Infinity - 无穷小，小于任何数值
```

7、number和boolean用==比较时，会把boolean转换为number再比较值

```
for(let i = 0; i < 3; i++) {
	// 0: false, 1:true, 2:true
	if(i % 3) {
		if(i % 3 == true) { // 需要把布尔转化为数字再比较
			// 1
		} else {
			// 2
		}
	} else {
		// 0
	}
}
```

