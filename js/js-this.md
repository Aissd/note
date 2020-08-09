1、函数与方法中this的的不同

​	1）如果函数为对象的方法（类方法），this就是当前对象

​	2）如果函数只是普通函数，this就是window

2、改变this指针

```
 // 方法一，通过常量保留this指针
let obj = {
	site: 'abc',
	list: [1,2,3],
	show: function() {
		let self = this;
		return this.list.map(function(value) {
			return `{self.site}-${value}`;
		});
	}
};

 // 方法二，传递函数第二个参数
 let obj = {
	site: 'abc',
	list: [1,2,3],
	show: function() {
		let self = this;
		return this.list.map(function(value) {
			return `{this.site}-${value}`; // 2）这里的this就是map函数第二个参数传进来的this
		}, this); // 1）这里，把show方法的this传进去
	}
};
```





js中this的五种情况

```
1）元素事件的绑定，事件触发，方法执行，方法中的this一般都是当前元素
2）函数执行，看前面是否有"."，有"."前面是谁this就是谁，没有，this就是window（严格模式下是undefined）
3）匿名函数或者回调函数中的this，window居多
4）箭头函数中没有自己的this，this都是上下文中的
5）基于call/apply/bind 暴力改变this
```

