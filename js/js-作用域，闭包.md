1、全局环境变量不会被回收

2、解决闭包内存泄漏的解决方法

```
<div desc="houdunren.com">在线学习</div>
<div desc="hdcms">开源产品</div>

// 点击div，取其desc属性的值
let divs = document.querySelectorAll('div');
divs.forEach(function(item) {
	let desc = item.getAttribute('desc');
	item.addEventListener('click', function() {
		conosle.log(desc); // 目的只想取desc
		console.log(item); // null
	});
	item = null; // 释放内存，因为只需要desc而已
});
```

3、解决this的历史遗留闭包问题

```
// 原：
let hd = {
	name: 'abc',
	get: function parent() {
		return function sub() {
			return this.name;
		}
	}
};

let a = hd.get();
a(); // undefined，a相当于运行sub这个函数

// 解决方法：
1)用常量保存this
let hd = {
	name: 'abc',
	get: function parent() {
		let self = this;
		return function sub() {
			return self.name; // 'abc'
		}
	}
};

2）用箭头函数，取父级上下文的this
let hd = {
	name: 'abc',
	get: function parent() {
		return () => {
			return self.name; // 'abc'
		}
	}
};
```

