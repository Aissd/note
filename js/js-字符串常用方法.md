字符串常用方法

```
字符串是基本数据类型，字符串的每一次操作都是值直接的进行操作，不像数组一样是基于空间地址来操作的，所以不存在原有字符串是否改变这一说，肯定都是不变的。
```

1、charAt/charCodeAt

```
charAt
1）作用：charAt根据索引获取指定位置的字符，
2）参数：索引（无则默认是0）
3）返回：指定索引对应的字符串（无则为空字符串）

与字符串根据索引取值相比的区别：当索引不存在时
let str = 'zys';
str[100]; // undefined => 运行的机制和对象是一样的
str.charAt(100); // ''

charCodeAt
1）作用：不仅仅获取字符，它获取的是字符串对应的Unicode编码值（ASC II码值)
2）参数：索引（无则默认是0）
3）返回：指定缩影对应的ASC II码值（超出索引范围则为NaN）

str.charCodeAt(0); // 122 => z的ASC II码值 （对应的十进制编码）
String.fromCharCode返回的是编码对应的字符
String.fromCharCode(122); // 'z'
```

2、indexOf/ lastIndexOf

3、slice

```
作用：str.slice(n,m)从索引n开始找到索引为m处（不包含m），把找到的字符当做新字符返回
```

4、substring

```
和slice语法一模一样。
唯一区别在于：
slice支持负数索引，而substring不支持负数索引（n和m均是负数，返回空字符串）
```

5、substr

```
也是字符串截取方法，用法是：
str.substr(n,m)，从索引n开始截取m个字符

区别：和substring一样，第二个参数不传，截取到末尾，但它支持第一个索引为负数，负数也是总长度+负数索引
```

6、toUpperCase/toLowerCase

```
实现字符大小写转换
```

7、split

```
和数组中的join相对应，数组中的join是把数组们一项按照指定的连接符变为字符串，而split是把字符串按照指定的分隔符，拆分成数组中每一项
```

8、replace

```
1）作用：替换字符串中的原有字符
2）参数：原有字符，要替换的新字符
3）返回：替换后的字符串

在不使用正则的情况下，每执行一次replace只能替换一个
```

练习：

```
1、时间字符串格式化：
时间字符串"2018-4-4 16:26:8"，基于这个字符串获取到"04月04日 16时26分"
```

时间字符串格式化

```
~function(pro) {
	pro.formatTime = function(template) {
		template = template || '{0}年{1}月{2}日 {3}时{4}分{5}秒';
		var ary = this.match(/\d+/g);
		template = template.replace(/\{(\d+)\}/g, function() {
			var n = arguments[1],
				val = ary[n] || '0';
			Number(val) < 10 ? val = '0' + val : null;
			return val;
		});
		return template;
	}
}(String.prototype);

var str = '2020-8-21 07:9:1';
str.formatTime();  // "2020年08月21日 007时09分01秒"
str.formatTime('{1}月{2}日 {3}时{4}分'); // "08月21日 07时09分"
str.formatTime('{0}-{1}-{2}'); // "2020-08-21"
```

9、endsWith
```
// 该方法区分大小写
'./main.js'.endsWith('.js'); // true
```
```
// 原理
if (!String.prototype.endsWith) {
	// search - 要判断的字符串
	// this_len - 判断的结尾条件
	String.prototype.endsWith = function(search, this_len) {
		if (this_len === undefined || this_len > this.length) {
			this_len = this.length;
		}
		return this.substring(this_len - search.length, this_len) === search;
	};
}
```

10、startsWith
```
// 该方法区分大小写
'./main.js'.startsWith('.'); // true
```