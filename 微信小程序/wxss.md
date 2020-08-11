1、使用背景图片

```
background: url(./img/x.png) no-repeat; // 这样是不行的

解决方法：
1）使用网络图片；
2）把图片转成base64：background: url(转换之后的base64字符串) no-repeat;
3）利用流布局，设置z-index层级，将image标签置于底层
```

