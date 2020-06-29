相关链接

```
vue模板编译过程：
https://774848686.github.io/blog/technology/2020-0614.html
```

0、响应式原理

```
https://juejin.im/post/5ef010d6f265da0299791fa0
Observer：响应式原理入口，根据数据类型（对象，数组）处理观测逻辑
Watcher：用于执行更新渲染，组件会拥有一个Watcher，常说的收集依赖，就是收集Watcher
Dep：依赖收集器，属性都会有一个Dep，方便发生变化时能够找到对应的依赖触发更新
```

1、

```
1）vue会给每个声明在data的对象，用defineproperty封装set和get方法，其中如果有嵌套的对象，则会使用递归逐层遍历封装；（会判断是否是object类型并且不是null）
```

```
2）vue不会给每个声明在data的数组的每个元素用defineproperty封装set和get方法，因为给每个数组索引封装太消耗性能；

所以：
	2.1）arr[0]这个get过程无法监控；
	2.2）arr[0] = { a: 2 }; 这个set过程无法监控；
因为没有对索引进行defineProperty进行劫持

数组使用的方式是重写数组的方法（仅含会改变数组的7个方法）做函数劫持；
// shift，pop，unshift，push，reserve，sort，splice
以上方法的数组操作的数据才会被监控到；
```

```
检测变化的注意事项：
https://cn.vuejs.org/v2/guide/reactivity.html
1）对于对象：
vue无法检测property的添加或移除；
解决办法：
	1.1）在data对象上声明，可转换为响应式
	1.2）对于已经创建的实例，vue不允许动态添加根级别的响应式属性，但是可以用Vue.set(object, propertyName, value)方法向嵌套对象添加响应式属性；或this.$set(object, propertyName, value);
	1.3）对已有对象赋值多个属性，可使用Object.assign()或_extend()
this.someObject = Object.assign({}, this.someObject, {a:1,b:2});

2）对于数组：
vue不能检测以下数组的变动：
	2.1）利用索引直接设置一个数组项（arr[0]=1）
	2.2）修改数组的长度（arr.length=10)
解决办法：
	2.1.1）2.1的解决办法是：使用Vue.set(vm.items, indexOfItem, newValue);或vm.$set(vm.items, indexOfItem, newValue);
	2.2.1）2.2的解决办法是：使用splice
	vm.items.splice(newLength);
	
3）声明响应式property
Vue不允许动态添加根级响应式property，因此必须在初始化实例前声明所有根级响应式property，哪怕是一个空值。
```

2、vue - 为什么vue文件模板根级目录必须只有一个html标签

```
构建ast树的时候，是通过栈的数据结构遍历生成的。
1）首先往栈上添加第一个html标签，即为root；
2）遍历模板结构，遇到标签，就把记录nodeType为1，父级为root，往栈里推送当前标签；当遇到闭合标签时，从栈中移除当前标签；

如果没有唯一的root级，则会报错
```

3、为什么，data() {return { a: 1}}，用的是this.a即可取到，而不是用this.data.a来取？

```
因为vue对实例进行了一层代理，使用defineProperty来说实现，伪代码如下：
function proxy(target, property, key) { // 这个proxy不是es6的那个
	Object.defineProperty(target, key {
		get() {
			return target[property][key];
		}
		set(newValue) {
			target[property][key] = newValue;
		}
	})
}

for(let key in data) {
	proxy(vm, '_data', key);
}

// 原来是vm._data.a = xxx;
```

4、v-if和v-show的区别

5、v-show的原理是什么

```
v-show是true的话，display是block吗；其实不是
```

6、opacity:0和visibility:hidden的区别

7、MVVM

```
1、Dep
1）什么时候创建
	初始化给data属性进行数据劫持时创建
2）个数
	与data中的属性一一对应
3）结构
	id：标识
	subs：n个相关的watcher的容器
2、Watcher
1）什么时候创建
	初始化解析模板（大括号表达式或一般指令）时创建
2）个数
	与模板中表达式（不包含事件指令）一一对应
3）结构
	cb：// 回调函数 - 用于更新界面的回调
	vm：// 实例
	exp：// 对应的表达式
	depIds：{} // 相关的n个dep的容器对象
	value：// 当前表达式所对应的value
3、Dep与Watcher之间的关系
1）什么关系
	多对多的关系
	举例：
	1.1）data属性->1个Dep->n个Watcher（模板中右多个表达式使用了此属性：{{a}}，v-text="a"）
	1.2）表达式->Watcher->n个Dep（多层表达式：a.b.c）
2）如何建立
	data中属性的get()中建立
3）什么时候建立
	初始化的解析模板中的表达式创建Watcher对象时
```

8、Vue.use

```
执行Vue.use的时候，实际执行的是模块的install方法，会把Vue的实例传递进去
```

