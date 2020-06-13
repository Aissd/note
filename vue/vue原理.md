1、响应式

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

