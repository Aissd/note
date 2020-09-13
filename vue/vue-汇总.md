### watch

* 1）watch不能使用箭头函数，这样使用

```
watch: {
	isOpenLeft(newVal, oldVal) {
		...
	}
}
// 监听路由
"$route"(newVal, oldVal) {
	console.log(newVal, oldVal);
}
```

* 2）初始化时，并不会触发watch

### props

* 传入多种类型，可以

```
xxx: [String, Number]
```

### x-template（字符串模板）

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

### computed

### 深度作用选择器

```
/deep/.el-card__header {}
::v-deep .el-card__header {}
>>> .el-card__header {}
```

### ref
* 1）ref放在标签上，拿到的是原生节点
* 2）ref放在组件上，拿到的是组件对象

### v-bind="$attrs"

* $attrs接收的是除class和style之外父组件传来的属性
* 作用等同于展开了传进来的所有属性（除class和style之外）

![image-20200709235459935](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20200709235459935.png)

以下是添加了inheritAttrs: false之后的结果（div没有继承type和自定义的a属性）

kInput.vue：

![image-20200709235514985](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20200709235514985.png)

### inheritAttrs: false

```
// 避免顶层容器继承属性，但class和style还是不会被$attrs所引用
export default {
	inheritAttrs: false,
	...
}
```

> 路由懒加载 - 给对应的js添加别名

```
const routes = [
	{
		...,
		component: () => import(/* webpackChunkName: "about" */'../views/About.vue')
	}
];
```

###  v-model上的三个修饰符
> .lazy
* 修饰符.lazy的作用相当于把input标签的input事件换成了change事件
* 在光标离开之后才会同步
```
<input v-model.lazy="msg" />
{{msg}}
```
> .number
* 修饰符会把input里输入的变成真正的数字类型（如果不加，即使type="number"时也是string）
```
<input type="number" v-model.number="msg" />
{{ typeof msg }} // "number"
```
> .trim
* 移除左右的空格
```
<input  v-model.trim="msg" />
{{ msg }} 
```