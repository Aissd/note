![img](https://www.html.cn/newimg88/2018/07/syntax-1.png)

![CSS3 box-shadow å±æ§](https://www.html.cn/newimg88/2018/07/syntax-2.png)

![CSS3 box-shadow å±æ§](https://www.html.cn/newimg88/2018/07/syntax-3.png)

![CSS3 box-shadow å±æ§å¾è§£](https://www.html.cn/newimg88/2018/07/box-shadow-diagram.png)

```
/* offset-x | offset-y | color */
box-shadow: 60px -16px teal;
 
/* offset-x | offset-y | blur-radius | color */
box-shadow: 10px 5px 5px black;
 
/* offset-x | offset-y | blur-radius | spread-radius | color */
box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);
 
/* inset | offset-x | offset-y | color */
box-shadow: inset 5em 1em gold;
 
/* Any number of shadows, separated by commas */
box-shadow: 3px 3px red, -1em 0 0.4em olive;
 
/* Global keywords */
box-shadow: inherit;
box-shadow: initial;
box-shadow: unset;
```

取值说明：

- `inset`: 默认阴影在边框外。使用 inset 后，阴影在边框内（即使是透明边框），背景之上内容之下。也有些人喜欢把这个值放在最后，浏览器也支持。
- ` <offset-x> <offset-y> `: 这是头两个 ``值，用来设置阴影偏移量。`` 设置水平偏移量，如果是负值则阴影位于元素左边。 `` 设置垂直偏移量，如果是负值则阴影位于元素上面。可用单位请查看 ``。如果两者都是0，那么阴影位于元素后面。这时如果设置了 `` 或 `` 则有模糊效果。
- ``<blur-radius>: 这是第三个 `` 值。值越大，模糊面积越大，阴影就越大越淡。 不能为负值。默认为0，此时阴影边缘锐利。
- `` <spread-radius>: 这是第四个 `` 值。取正值时，阴影扩大；取负值时，阴影收缩。默认为0，此时阴影与元素同样大。
- `` <color>: 相关事项查看 `` 。如果没有指定，则由浏览器决定——通常是color的值，不过目前Safari取透明。