```
%scroll {
  overflow-x: hidden;
  overflow-y: auto;
  &::-webkit-scrollbar {
        /*滚动条整体样式*/
        width: 5px;
        /*高宽分别对应横竖滚动条的尺寸*/
        height: 5px;
  }
  &::-webkit-scrollbar-thumb {
        /*滚动条里面小方块*/
        border-radius: 5px;
        box-shadow: inset 0 0 5px rgba(47, 203, 235, .5);
        background: rgba(47, 203, 235, .5);
  }
  &::-webkit-scrollbar-track {
        /*滚动条里面轨道*/
        box-shadow: inset 0 0 5px rgba(255, 255, 255, 0.1);
        border-radius: 0;
        background: rgba(255, 255, 255, 0.1);
  }
}
```

1、用阴影做边框

```
box-shadow: 0 0 1px #2685E5 inset;
```

2、css变量

```
:root {
  --main-bg-color: brown;
}
.one {
  background-color: var(--main-bg-color);
}
.two {
  background-color: var(--main-bg-color);
}
```

​	通过在:root伪类上设置自定义属性，然后在整个文档需要的地方使用，可以减少这样的重复性。

3、清除浮动

```
// 清除浮动
.clearfix:after {
    content: "\00A0";
    display: block;
    visibility: hidden;
    width: 0;
    height: 0;
    clear: both;
    font-size: 0;
    line-height: 0;
    overflow: hidden;
}
.clearfix {
    zoom: 1;
}
```

4、垂直水平居中

```
/* 绝对定位方式且已知宽高 */
position: absolute;
top: 50%;
left: 50%;
margin-top: -3em;
margin-left: -7em;
width: 14em;
height: 6em;

/* 绝对丁文 + 未知宽高 + translate */
position: absolute;
left: 50%;
top: 50%;
transform: translate(-50%, -50%);
//需要补充浏览器前缀

/* flex - （未知宽高） */
display: flex;
align-items: center;
justify-content: center;
```

5、文本末尾添加省略号

```
/* 宽度固定，适合单行显示... */
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;

/* 宽度不固定，适合多行以及移动端显示 */
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 3; /* 多少行 */
-webkit-box-orient: vertical;
```

6、文本的模糊效果

```
color: transparent;
text-shadow: 0 0 2px rgba(0, 0, 0, 0.5);
```

7、简洁的loading动画效果

```
.loading:after {
    display: inline-block;
    overflow: hidden;
    vertical-align: bottom;
    content: "\2026";
    -webkit-animation: ellipsis 2s infinite;
}

// 动画部分
@-webkit-keyframes ellipsis {
    from { width: 2px; }
    to { width: 15px; }
}
```

8、自定义文本选中样式

```
// 注意只能修改这两个属性 字体颜色 选中背景颜色
element::selection {
    color: green;
    background-color: pink;
}
element::-moz-selection {
    color: green;
    background-color: pink;
}
```

9、字体颜色渐变

```
background: linear-gradient(to right, red, blue);
-webkit-background-clip: text;
color: transparent;
```

10、滚动条样式 - chrome

```
%scroll {
	overflow-x: hidden;
	overflow-y: auto;
    &::-webkit-scrollbar {
        /*滚动条整体样式*/
        width: 5px;
        /*高宽分别对应横竖滚动条的尺寸*/
        height: 5px;
    }
    &::-webkit-scrollbar-thumb {
        /*滚动条里面小方块*/
        border-radius: 5px;
        box-shadow: inset 0 0 5px rgba(47, 203, 235, .5);
        background: rgba(47, 203, 235, .5);
    }
    &::-webkit-scrollbar-track {
        /*滚动条里面轨道*/
        box-shadow: inset 0 0 5px rgba(255, 255, 255, 0.1);
        border-radius: 0;
        background: rgba(255, 255, 255, 0.1);
	}
}
```

11、class前缀选择器

```
[class^="btn-"] {}
```

12、currentColor，css3的关键字，获取使用该关键字的元素（如果没有就是最近的父元素）的color属性的颜色值；