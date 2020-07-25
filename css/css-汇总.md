1、opacity: 0;visibility: hidden; display: none; 的区别

```
1）opacity: 0; 该元素隐藏，但不会改变页面布局；若该元素已绑定事件，点击仍然会触发；
2）visibility: hidden; 该元素隐藏，但不会改变页面布局；点击也不会触发事件；
3）display: none; 该元素隐藏，且会改变页面布局；
```

2、BFC（Block Formatting Context）（块格式化上下文）

```
2.1、创建BFC的方式：
1）根元素（html）
2）浮动元素（元素的float不是none）
3）绝对定位元素（元素的position为absolute或fixed）
4）行内块级元素（元素的display为inline-block）
5）表格单元格（元素的display为table-cell-HTML表格单元格默认为该值）
6）overflow值不为visible的块元素
7）弹性元素（display为flex或inline-flex元素的直接子元素）
8）网格元素（display为grid或inline-grid元素的直接子元素）
2.2、BFC的效果
建立一个隔离空间，断绝空间内外元素相互作用
	1）内部的盒子会在垂直方向一个接一个排列（可以看作BFC中有一个常规流）；
	2）处于同一个BFC中的元素相互影响，可能会发生margin collapse；
	3）每个元素的margin box的左边，与容器块border box的左边相接触（对于从左往右的格式化，否则相反）。即使存在浮动也是如此；
	4）BFC就是页面上的一个隔离独立容器，容器里面的子元素不会影响到外面的元素，反之亦然
	5）计算BFC的高度时，考虑BFC所包含的所有元素，连浮动元素也参与计算
	6）浮动盒区域不叠加到BFC上
```

