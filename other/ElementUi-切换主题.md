demo地址：

https://elementui.github.io/theme-preview/#/zh-CN

仓库地址：

https://github.com/ElementUI/theme-preview

实现其实很暴力：

1）先把默认主题文件中涉及到颜色的 CSS 值替换成关键词：https://github.com/ElementUI/theme-preview/blob/master/src/app.vue#L250-L274

2）根据用户选择的主题色生成一系列对应的颜色值：https://github.com/ElementUI/theme-preview/blob/master/src/utils/formula.json

3）把关键词再换回刚刚生成的相应的颜色值：https://github.com/ElementUI/theme-preview/blob/master/src/utils/color.js

4）直接在页面上加 `style` 标签，把生成的样式填进去：https://github.com/ElementUI/theme-preview/blob/master/src/app.vue#L198-L211





编译主题

```
et // 默认编译的主题目录是放到./theme下

et -o public/theme // 改到public/theme目录下
```

