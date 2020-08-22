https://www.w3cschool.cn/less/

1、变量

```
标识符
	less中以@开头表示变量
插值
	@direction: left;
	.my-padding {
		padding-@{direction}: 20px;
	}
```

2、注释

```
以//开头的注释，不会显示到css文件中
以/**/包裹的注释会被显示到css文件中
```

