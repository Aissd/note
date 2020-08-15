null 和 undefined

```
1）都代表空或者没有
2）null：空对象指针
3）undefined：未定义

区别：
	null一般都是意料之中的没有（通俗理解为人为手动先赋值为null，后面程序中会再次给它赋值）

	undefined：代表的没有一般不是人为手动控制的，大部分都是浏览器自主为空（后面可以赋值也可以不赋值）
```



为什么typeof null 为 'object'

```
因为二进制以000开头的是obj

null则全是0，所以被误认为是object

这是引擎解析的一个bug
```

