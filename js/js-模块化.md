### 为什么要使用模块化
> 当项目变大时，没有模块化就会变得难以维护，需要用模块化的思想来组织代码

1、命名空间冲突：两个库可能会使用同一个名称，例如zepto，也被放在window.$下；
2、无法合理管理项目的依赖和版本；
3、无法方便地控制依赖的加载顺序


### 模块化历史

> AMD - require.js - 采用了异步的方式去加载依赖的模块。
* 优点：
	1）可在不转换代码的情况下直接在浏览器中运行；
	2）可异步加载依赖
	3）可并行加载多个依赖
	4）代码可运行在浏览器环境和node.js环境
* 缺点：
	1）js运行环境没有原生支持AMD，需要先导入实现AMD的库后才能正常使用。
> CMD - sea.js（淘宝）
> Commonjs  - node.js - 通过require方法来同步加载依赖的其他模块，通过module.exports导出需要暴露的接口；
* 优点：
	1）代码可复用与node.js环境下运行
	2）通过npm发布的第三方模块都采用commonjs规范
* 缺点： 
	无法直接运行在浏览器环境下，必须通过工具转换成标准的ES5
> UMD - 支持AMD和Commonjs

### 模块化特点

1）有独立作用域
2）可暴露出部分函数
3）默认启用严格模式
4）运作机制 - 后解析，无关顺序（是否标签渲染完了）【模块延迟解析】（所有模块先全部加载，解析，再工作）
5）预解析（引入即执行，无论后面重复引入几次，都不再执行）

### 立即执行函数实现模块化

```
let module = (function() {
	const moduleList = {}; // 依赖模块的容器
	// name - 模块的名称
	// modules - 要依赖的模块
	// action - 动作
	function define(name, modules, action) {
		moduleList[name] = action.apply(null, modules); // 往容器里加依赖模块
	}
	return { define };
})();

module.define('hd', [], function() {
	
});
```

### 模块的基本使用

```
// index.html
<script src="hd.js"></script>
<script type="module"> // 需要加上type="module"，定义成模块
	import { title, url, show } from './hd.js'; // 具名导入
	console.log(title); // 后盾人
	console.log(url); // 没有暴露url，所以报错
	show(); // 向军
</script>
```

```
// hd.js
let title = '后盾人';
let utl = 'houdunren.com';
function show() {
	console.log('向军');
}
export { title, show }; // 只暴露了title，show函数，所以url引用不到的
```

### 模块的批量导入

```
// 以4的index.html和hd.js举例
<script type="module">
	import * as api from 'hd.js';
	console.log(api.title); // 后盾人
	api.show(); // 向军
</script>

// 这种方法有一定缺陷，打包工具会把hd.js里面暴露出来的方法全部打包，不管你用了几个，增加了文件的体积
```

### 模块的导入的别名使用

```
// 以4的index.html和hd.js举例
<script type="module">
	import { title as t } from 'hd.js';
	let title = 'hdcms.com'; // 不用别名，会跟这个同名，所以会报错
	console.log(t); // 后盾人
</script>
```

### 模块导出的别名使用

```
// 以4的index.html和hd.js举例

// hd.js
export { title as t, show };

// index.html
<script type="module">
	import { t } from 'hd.js';
	console.log(t); // 后盾人
</script>
```

### default默认导出

```
// a.js
export default Admin {};

// a.html
<script type="module">
	import aaa from 'a.js'; // 默认导出时，aaa变量可以不必跟到导出的名字一致
</script>
```

### 混合导入导出

```
// b.js
export let site = '后盾人';
export default class User {
	static render() {
		return 'user static render';
	}
}

// b.html
<script type="module">
	import { site }, User from 'b.js'; // {}包裹的是具名导出，没有的则是默认导出
</script>

```

### 模块的合并导出

```
// index.js
import Admin from 'a.js';
import { site }, User from 'b.js';
export { site, User, Admin };

// temp.js
import { site, User, Admin } from 'index.js';
```

### 按需动态加载模块

```
1）import { site }, User from 'b.js'; // 这种引入方式必须放到最顶层操作；因此不能包裹到if，或者函数等模块里面，会报错；
2）import('./a.js'); // 返回一个promise对象，通过这种引入方式，就可以放到回调函数或者if里面；

3）import('./a.js').then(module => {
	console.log('---');
});
```

### ES5的模块化
```
// 工具类 - tools.js
var tools = (function() {
	function total() {}
	
	return {
		total: total
	}
})();

// main.js
;(function(doc, tools) {
	function init();
	function fn1() {}
	init();
})(document, tools);

```

### 引入资源文件
```
import Vue from 'vue'; // 默认会从node_modules文件夹中查找依赖
```