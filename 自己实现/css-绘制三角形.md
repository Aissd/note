对border形成的最大的误解，就是认为元素的border是有四个矩形边框拼接而成的。



实际上元素的border是由四个三角形组合而成的

```
div {
    width: 0;
    height: 0;
    border: 40px solid;
    border-color: orange blue red green;
}
效果图如下：
```

![img](https://upload-images.jianshu.io/upload_images/9397803-d69e514577bcca5e.png?imageMogr2/auto-orient/strip|imageView2/2/w/160/format/webp)

因此，要取得各个角度的三角形，只需把其他三个方向的border-color设置为白色或者透明色即可。