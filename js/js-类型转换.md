数据转换：

```
1）显性转换：Boolean(),Number(),String()
2）隐式转换：四则运算，==，判断语句if
```

1、String转换为Number

```
1、parseInt()：解析一个字符串，从位置0开始查看每个字符，直到找到第一个非有效的字符位置，最后返回一个整数。
	1）parseInt(string, 10); // 默认十进制
	2）parseInt('11', 2); // 转为二进制

2、parseFloat(string)：
	1）parseFloat('123456red'); // 123456
	2）parseFloat('11.2'); // 11.2
	3）parseFloat('11.22.33'); // 11.22
3、Number
```





2、把其他数据类型转换为number类型

```
发生的情况
1）isNaN检测的时候：当检测的值不是数字类型，浏览器会自己调用Number方法把它先转换为数字，然后再检测是否有有效数字；
	1.1）isNaN('3'); // false
		Number('3') => 3
		isNaN(3) => false

	1.2）isNaN('3px'); // true
		Number('3px') => NaN
		isNaN(NaN) => true

2）基于parseInt/parseFloat/Number去手动转换数字类型
3）数学运算： + - * / %，但是 + 不仅仅是数学运算，还可能是字符串拼接
	3.1）'3'-1; // 2
		Number('3') => 3
		3-1; // 2

	3.2）'3px'-1; // NaN
		Number('3px') => NaN
		NaN - 1 => NaN

	3.3）'3px'+1; // '3px1'
	3.4）var i = '3';
		i=i+1; // '31'
		i+=1; // '31'
		i++; // 4（i++就是单纯的数学运算，已经摒弃掉字符串拼接规则）
		++i; // 4
4）在基于 == 比较的时候，有时候也会把其他值转换为数字类型
```

```
转换规律
1）转换方法：
Number（浏览器自行转换都是基于这个方法完成的）

1.1）把字符串转换为数字：
	只要遇到一个非有效数字字符，结果就是NaN
	'' => 0; // 空字符串
	' ' => 0; // 空格（Space）
	'\n' => 0; // 换行符（Enter）
	'\t' => 0; // 制表符（Tab）
1.2）把布尔值转换为数字：
	true => 1
	false => 0
1.3）把没有转换为数字
	null => 0
	undefined => NaN
1.4）把引用类型转换为数字
	首先都先转换为字符串（toString），然后再转换为数字（Number）
```

3、把其他类型转换为字符串

```
发生的情况
1）基于alert/confirm/prompt/document.write等方法输出内容的时候，会把输出的值转换为字符串，然后再输出
	alert(1); // '1'
2）基于 + 进行字符串拼接的时候
3）把引用类型值转换为数字的时候，首先会转换为字符串，然后再转换为数字
4）给对象设置属性名，如果不是字符串，首先转换为字符串，然后再当做属性存储到对象中（对象的属性只能是数字或者字符串）
5）手动调用toString/toFixed/join/String等方法的时候，也是为了转换为字符串
	var n = Math.PI; // 获取圆周率
	n.toFixed(2); // '3.14'
	
	var arr = [12,23,34];
	ary.join('+'); // '12+23+34'
```

```
转换规律
	调用的方法：toString/String
	除了对象，都是单/双引号包裹
	[] => ''
	[13]=> '13'
	[12, 23] => '12,23'
	
	{name:'xxx'} => '[object Object]'
	{} => '[object Object]'
	不管是啥样的普通对象，最后结果都一样
	
	new Date().toString() => Web Aug 19 2020 12:48:44 GMT+0800（中国标准时间）
	/\.is$/.toString() => '/\.is$/'
	Math.toString() => '[object Math]'
	Date.toString() => 'function Date() { [native code] }'
```

4、把其他类型转换为布尔类型

```
发生情况
1）基于!/!!/Boolean等方法转换
2）条件判断中的条件最后都会转换为布尔类型
	if(n) {
		// => 把n的值转换为布尔校验条件真假
	}
	if('3px' + 3) {
		// => 先计算表达式的结果为'3px3'，把结果转换为布尔值，为true，条件成立
	}
```

```
转换规律
只有0/NaN/''/null/undefined 等五个值转换为布尔值为false，其他都是转换为true

特殊情况：
1）数学运算和字符串拼接 + 
	当表达式中出现字符串，就是字符串拼接，否则就是数学运算
	
	1+true; // 2（数学运算）
	'1'+true; // 1true（字符串拼接）
	[12]+10; // '1210'（虽然现在没看见字符串，但是引用类型转换为数字，首先会转换为字符串，所以变为字符串拼接）
	({}+10); // '[object Object]10' 
	{}+10; // 10 （这个和以上说的没有半毛钱关系，因为根本就不是数学运算，也不是字符串拼接，它是两部分代码，一部分是{}，代表一个代码块【块级作用域】，+10才是操作，等同于0+10，所以结果为10【严格写法应该是{};+10;】）
	{}+true; // 1
	{}+[]; // 0
	{}+{}; // '[object Object][object Object]'
	
2）特殊情况: == 在进行比较的时候，如果左右两边的数据类型不一样，则先转为相同的类型，再进行比较
	对象==对象; // 不一定相等，因为对象操作的是引用地址，地址不相同则不同
	{}=={}; // false
	[]==[]; // false
	var o1={};
	var o2=o1;
	o1==o2; // true

不同情况的比较，都是把其他值转换为数字，然后再进行比较
对象==数字：把对象转换为数字
对象==布尔：把对象转换为数字，把布尔值也转换为数字
对象==字符串：把对象转换为数字，把字符串也转换为数字
字符串==数字：把字符串转换为数字
字符串==布尔：把字符串转换为数字，把布尔值转换为数字
布尔==数字：把布尔值转换为数字

null == undefined; // true
null === undefined; // false
null === null; // true
undefined === undefined; // true
null && undefined和其他值都不相等

NaN==NaN; false
NaN和谁都不相等，包括自己

1 == true; // false
1 == false; // false
2 == true; // false （规律不要混淆，这里是把true变为数字1）

[] == false; // true （都转换为数字0 == 0;） 
![] == false; // true（先算![]，把数组转换为布尔取反=>false => false == false）
[] == []; //
[] == true; // false（都转换为数字0 == 1）
![] == true; // false
```

思考题

```
12+true+false+null+undefined+[]+'珠峰'+null+undefined+[]+true

12+true
13+false
13+null
13+undefined
NaN+[]
'NaN'+'珠峰'
...
```

