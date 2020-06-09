注意：

​	1）不是所有属性都能产生动画，比如border的solid变成double，宽度的auto变成300px，因为他们没有明确的中间值

1、animation-name（动画名称）

```
// 多个动画
animation-name: xxx, yyy;

// 若xxx与yyy有相同的动画动作，放到后面的yyy的动画动作权重更高
animation-name: xxx, yyy, zzz;
animation-iteration-count: 1, 2, 3;
animation-duration: 4s, 2s; // 动画有三个，但动画时间只有两个，会重头计算，即：则xxx用4s，yyy用2s，zzz用4s
```

2、animation-duration（动画时长）

```
animation-duration: 0s; // 默认，表示无动画
// 单位为s（秒）或ms（毫秒），无单位的值无效
```

3、animation-iteration-count（动画运行次数）

```
animation-iteration-count: 1; // 默认一次
animation-iteration-count: infinite; // 无限循环
// 可以定义成小数，播放部分动画
```

4、animation-direction（动画方向）

```
animation-direction: normal; 	       // 0% - 100%，然后从100%瞬间回到0%；
animation-direction: reverse;           // 100% - 0%，然后从0%瞬间回到100%；
animation-direction: alternate;    	   // 0% - 100%，然后从100%逐渐回到0%；
animation-direction: alternate-reverse; // 100% - 0%，然后从0%逐渐回到100%；
```

5、animation-fill-mode（）

```
animation-fill-mode: forwards; // 保留到100%帧的状态
animation-fill-mode: backwards; // 当动画没动的时候，使用起始值的状态
```

6、animation-timing-function（）

```
animation-timing-function: steps(4, start); // 起始就运动，所有第一个step不可见，从第二个step开始，最后一个step可见

animation-timing-function: steps(4, end); // 起始就是初始，开始可见，从第一个step开始，最后一个step不可见
```

