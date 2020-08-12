1、:nth-child(n)：当前容器所有子元素中的第n个

```
.box li:nth-child(1) {} // box容器所有子元素中的第一个并且标签名是li
```

2、:nth-of-type(n)：先给当前容器按照某一个标签名进行分组，获取分组中的第n个

```
.box li:nth-of-type(1) {} // 先获取box中所有的li，再获取li中的第一个
```

3、even 偶数，odd奇数

4、三行一组，分别是红绿蓝

```
3n + 1; // 3个为1组的第一个
3n + 2; // 3个为1组的第二个
3n + 3; // 即 3n，3个为1组的第三个

.box li:nth-of-type(3n + 1) {
	color: red;
}
.box li:nth-of-type(3n + 2) {
	color: green;
}
.box li:nth-of-type(3n) {
	color: blue;
}
```

5、:first-of-type

6、:last-of-type

7、:nth-last-child(n)

8、:nth-last-of-type(n)

9、:nth-last-of-type(n)

10、:first-child

11、:last-child