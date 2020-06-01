1、栅格布局

```
display: grid; // 块级的，独占一行
grid-template-rows: 20% 20% 20% 20% 20%; // 5份，每份20%
grid-template-columns: 50% 50%; // 2份，每份50%
```

```
display: inline-grid; // 内联的
```

2、重复绘制

```
grid-template-rows: repeat(3, 1fr); // 3份，每份等比例分布
grid-template-columns: repeat(3, 1fr); // 3份，每份等比例分布
```

3、自动填充尺寸

```
width: 300px;
height: 300px; 
grid-template-rows: repeat(auto-fill, 100px); // 按每行100px，自动填充满300px的宽
grid-template-columns: repeat(auto-fill, 100px); // 按每列100px，自动填充满300px的高
```

4、按比例划分尺寸

```
width: 500;
height: 300px;
grid-template-rows: 1fr 2fr 1fr; // 3份，比例是1:2:1
grid-template-columns: 1fr 2fr 1fr; // 3份，比例是1:2:1
```

5、尺寸波动范围

```
width: 500px;
height: 300px;
grid-template-rows: repeat(2, minmax(50px, 100px)); // 2份，每份在50px~100px之间变动
grid-template-columns: repeat(5, 1fr);
```

6、间距

```
grid-row-gap: 10px;
grid-column-gap: 10px;
简写：
row-gap: 10px; // 每行格子的间距是10px
column-gap: 10px; // 每列格子的间距是10px
再简写：
gap: 20px 10px; // 行间距20px，列间距10px
```

7、根据栅格线编号放置元素

```
1）
grid-row-start: 1; // 从第一行开始
grid-column-start: 1; // 从第一列开始
grid-row-end: 2; // 到第二行结束
grid-column-end: 3; // 到第三列结束
// 结果是出现在 下图编号2的格子里

简写：
grid-row: 1 / 2; // 第一行开始，第二行结束
grid-column: 1 / 3; // 第一列开始，第三列结束

位偏移写法
grid-row: 1 / span 1; // 第一行开始，位偏移1个（占1个）
grid-column: 1 / span 3; // 第一列开始，位偏移3个（占3个）

2）
grid-row-start: 2; // 从第二行开始
grid-column-start: 3; // 从第三列开始
grid-row-end: 4; // 到第四行结束
grid-column-end: 4; // 到第四列结束
// 结果是出现在 下图编号6、9的格子里
```



![image-20200528225540816](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20200528225540816.png)