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



6、多个动画

animation-name: xxx,yyy ;

animation-duration: 4s, 2s;

animation-name: xxx,yyy,zzz; xxx用4s，yyy用2s，zzz用4s // 重头计算

若xxx与yyy有相同的动画动作，放在后面的yyy的动画动作权重更高

animation-iteration-count: 1, 2, 3 // 动画播放次数



7、transform: scale(0) // 缩放成0，等同于消失



8、不是所有属性都能产生动画，比如border的solid变成double，宽度的auto变成300px，因为他们没有明确的中间值

9、animation-direction动画方向四种模式

normal 0%- 100%，100%瞬间回到0%

reverse 100% - 0%，0%瞬间回到100%

alternate 0%- 100%，100%逐渐回到0%

alternate 100% - 0%，0%逐渐回到100%

10、animation-fill-mode: forwards; // 保留到100%帧的状态



11、animation-fill-mode: backwards; // 当动画没动的时候，使用起始值状态



12、currentColor，css3的关键字，获取使用该关键字的元素（如果没有就是最近的父元素）的color属性的颜色值；



13、emmit 

div{$}*8 -> 生成出8个div，且每个div有数字序号1-8



14、

animation-timing-function: steps(4, start); // 起始就运动，所以第一个step不可见，从第二个step开始，最后一个step可见

animation-timing-function: steps(4, end); // 起始就是初始，开始可见，从第一个step开始，最后一个step不可见