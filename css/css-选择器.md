### :nth-child(n)：当前容器所有子元素中的第n个

```
.box li:nth-child(1) {} // box容器所有子元素中的第一个并且标签名是li
```

### :nth-of-type(n)：先给当前容器按照某一个标签名进行分组，获取分组中的第n个

```
.box li:nth-of-type(1) {} // 先获取box中所有的li，再获取li中的第一个
```

### even 偶数，odd奇数

### 三行一组，分别是红绿蓝

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

### :first-of-type

### :last-of-type

### :nth-last-child(n)

### :nth-last-of-type(n)

### :nth-last-of-type(n)

### :first-child

### :last-child

> 父元素的最后一个子元素

### [class^="btn-"] {}