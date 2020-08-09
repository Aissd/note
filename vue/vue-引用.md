1、图片：

​	1）vue标签里引用：

```
1.1）require("@/assets/icon/jinggai.png")
1.2）<img src="@/assets/images/play@2x.png" alt="播放按钮" class="btn-play" />
```

​	2）sass使用：

```
2.1）background: url("../../assets/img/lg_img.png") no-repeat right center;
2.2）background: url(~@/assets/img/newIndex/bg.png) no-repeat center/contain;
```

2、样式：

​	1）style标签里

```
@import "~@/scss/pageStyle/indexMapModel.scss";
@import "./indexMapModel.scss";
```



3、js

