

1、transform-origin（改变被转换元素的位置）

```
transform-origin: 50% 50% 0; // x-axis yaxis z-axis

对应的值可以是：（相对于元素左上角的位置）
x-axis: left，center，right，length，%
y-axis: top，center，bottom，length，%
z-axis: length
```

2、

http://houdunren.gitee.io/note/css/12%20%E5%8F%98%E5%BD%A2%E5%8A%A8%E7%94%BB.html#%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86

1、行内元素不产生变形效果，将其转为inline-block和block以及弹性元素时都可以产生变化效果；

```
<style>
    span {
        display: inline-block; /* 去掉就无效了 */
        transition: 2s;
        transform: translateX(100px) translateX(50px);
        width: 100px;
        height: 100px;
        background: #9b59b6;
    }

    span:hover {
        transition: 2s;
        transform: translateX(100px);
    }
</style>

<span>hdcms</span>
```

css进阶之动画

https://zhuanlan.zhihu.com/p/50910069

2、transition只能做单个动作，如果动画包含多个动作，那就需要animation

3、transform直译为变换，它和动画无关，transition是一个状态到另一个状态的变化过程，而transform仅仅是静止的最终状态。

4、transform原点位于元素中心

css元素默认的坐标系，原点在左上角；

transform变换原点位于元素中心；

5、perspective（透视），可简单理解为眼睛离屏幕的距离

6、transform: scale(0) // 缩放成0，等同于消失

