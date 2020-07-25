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

