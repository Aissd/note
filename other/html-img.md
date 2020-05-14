1、设置宽高属性，保留空间，避免没加载完的时候只显示一条线；

2、用css隐藏图片

```
img {
	display: none;
}
```

上面的内容不会阻止浏览器加载图片，即使它在视觉上是隐藏的。原因是被认为是被替换的元素，所以我们无法控制它加载的内容。

3、可访问性问题

HTML图片应该通过将alt属性设置为有意义的描述来访问。

4、响应式的图片集：

​	4.1）srcset属性：根据屏幕宽度的不同，出现多个图片的大小。这个选择只能由浏览器来挑选合适的图片，而我们并没有控制权。

```
<img src="small.jpg" srcset="medium.jpg 500w, large.jpg 800w" alt="" />
```

​	4.2）HTML Picture 元素

	<picture>
	    <source srcset="large.jpg" media="(min-width: 800px)" />
	    <source srcset="medium.jpg" media="(min-width: 500px)" />
	    <img src="small.jpg" />
	</picture>
5、调整图片的大小：使用的一个伟大的东西就是object-fit和object-position属性。它们让我们可以控制的内容如何调整大小和位置，就像CSS背景图片一样

```
img {
	object-fit: cover;
	object-position: 50% 50%;
}
```

6、CSS背景图片

​	1）如何使用CSS背景图片

```
<div class="element">Some content</div>
.element {    background: url('cool.jpg');}
```

​	2）多重背景

	.element {
		background: url('cool-1.jpg'), url('cool-2.jpg');
	}
​	3）隐藏图像：如果未使用CSS设置图片，则不会下载该图片

```
@media (min-width: 700px) {
    .element {
        background: url('cool-1.jpg');
    }
}
```

7、可访问性问题：如果使用不正确，背景图片可能会影响可访问性。例如，将其用于文章中的大拇指，这对文章至关重要

​	1）css背景图，右击无法保存图片的

8、伪元素：可以使用伪元素与CSS背景图片一起使用，例如，在图片的顶部显示一个叠加元素。对于 ``，除非我们为覆盖层添加一个单独的元素，否则无法做到这一点（右上角或者左上角的角标）

9、SVG：

​	1）不影响质量的前提下进行缩放

​	2）在SVG中，可以嵌入JPG,PNG或SVG图像

    <svg width="200" height="200">
        <image href="cheesecake.jpg" height="100%" width="100%" preserveAspectRatio="xMidYMid slice" />
    </svg>
​		preserveAspectRatio？这就是保持SVG全宽和全高的图像原因，而不被拉伸或压缩。

​		这与 CSS 中的 object-fit: cover 或 background-size: cover 非常相似。

​	3）可以添加<title>和<desc>标签

    <svg width="200" height="200">
    	<title>A photo of blueberry Cheescake</title>
        <desc>A meaningful description about the image</desc>	    		      						<image href="cheesecake.jpg" preserveAspectRatio="xMidYMid slice" />
    </svg>

10、网站标志

​	1）LOGO

```
<a href="#">
    <img src="logo.svg" alt="Nature Food" />
</a>
```

​	2）一个响应式的标志

```
<a class="logo" href="/">
    <picture>
    	<source media="(min-width: 1350px)" srcset="sm-logo--full.svg" />
    	<img src="sm-logo.svg" alt="Smashing Magazine" />
    </picture>
</a>
```

```
.logo {
	display: inline-block;
	width: 45px;
}
@media (min-width: 1350px) {
	.logo {
		width: 180px;
  	}
}
```

​	3）用户头像

​		3.1）使用HTML ``与 ``的使用方法

​		要添加一个内边框，我们不能使用内嵌框阴影，因为它在图片上不起作用。解决的办法是将头像包裹在 ``中，并为内边框添加一个专用元素。

​	通过在 上设置一个10%的黑色边框，我们可以确保边框与暗色图像融合，只有在图像颜色较浅的情况下，边框才会显现出来。

```
<div class="avatar-wrapper">
	<img class="avatar" src="shadeed2.jpg" alt="A photo of Ahmad Shadeed">
	<div class="avatar-border"></div>
</div>
.avatar-wrapper {  
	position: relative;
	width: 150px;
	height: 150px;
}
.avatar-border {  
	position: absolute;
	left: 0;
	top: 0;
	width: 100%;
	height: 100%;
	border-radius: 50%;
	border: 2px solid rgba(0, 0, 0, 0.1);
}
```

​			3.2）一个带有CSS背景的

​			用来显示头像，那可能意味着头像是装饰性的。我想起了一个用例，那就是散落在页面中的随机头像

```
<div class="avatar" style="--img-url: url(shadeed2.jpg)"></div>
.avatar {
	background: var(--img-url) center/cover;
	width: 150px;
	height: 150px;
	border-radius: 50%;
	box-shadow: inset 0 0 0 2px rgba(#000, 0.1);
}
```

4）有图标的输入框

    <p>
        <label for="name">Full name</label>
        <input type="text" id="name" />
    </p>
    
    input {
        background-color: #fff;
        background-image:url ('user.svg');
        background-size: 20px 20px;
        background-position: left 10px center;
        background-repeat: no-repeat;
    }
5）CSS印刷

​	5.1）避免使用图片作为CSS背景

​		当一个图片作为CSS背景被包含时，它将不会被打印出来，而是会出现一个空位。

​		使用HTML比较安全，因为它的打印不会有任何问题。