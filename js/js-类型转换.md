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

