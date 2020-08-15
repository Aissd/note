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

深入V8底层：GO/VO/AO/EC及作用域和执行上下文

```
1）GO：全局对象（Global Object）
    var globalObject = {
        Math: { ... },
        String: { ... },
        document: { ... },
        ...
        window: this
    }
2）ECStack：Execution Context Stack执行环境栈
3）EC：Execution Context 执行环境（执行上下文）
	VO：Varibale Object 变量对象
	AO：Activation Object 活动对象（函数的叫AO，理解为VO的一个分支）
4）Scope：作用域，创建的函数的时候赋予的
5）Scope Chain：作用域链
```

