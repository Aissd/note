1、watch

​	1）watch不能使用箭头函数，这样使用

```
watch: {
	isOpenLeft(newVal, oldVal) {
		...
	}
}
```

​	2）初始化时，并不会触发watch

2、props

传入多种类型，可以

```
xxx: [String, Number]
```

3、x-template（字符串模板）

Vue 提供了另外一种定义模板的方式，在 <script> 标签里使用 text/x-template 类型，并且指定一个 id，将这个 id 赋给 template

```javascript
    <my-component></my-component>
    <script type="text/x-template" id="my-component">
        <div>你可以在这个 script 标签中书写模板的HTML</div>
    </script>
```

```javascript
    Vue.component('my-component'.{
        template:'#my-component'
    })
```

4、computed

5、深度作用选择器

```
/deep/.el-card__header {}
::v-deep .el-card__header {}
>>> .el-card__header {}
```

6、ref

```
1）ref放在标签上，拿到的是原生节点
2）ref放在组件上，拿到的是组件对象
```

