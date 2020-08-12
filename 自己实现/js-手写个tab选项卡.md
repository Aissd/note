1、html

```
<ul id="box">
	<li>中国</li>
	<li>日本</li>
	<li>俄罗斯</li>
</ul>
<div class="active">china</div>
<div>japan</div>
<div>russia</div>
```

2、css

```
ul, li {
	display: inline-block;
}
div {
	display: none;
}
.active {
	display: block;
}
```

3、错误的方式：js

```
let $box = document.getElementById('box');
let $tabList = $box.getElementsByTagName('li');
let $div = document.getElementsByTagName('div');
for(var i = 0; i < $tabList.length; i++) {
	$tabList[i].onclick = function() {
		// 运行失败的原因在于，这个匿名函数只有在点击的时候才运行，目前这个匿名函数还只是一个字符串的函数体
		// 由于var声明的i，当循环结束后，i为最后一项不符合条件的，即为3
		changeTabFn(i);
	}
}

function changeTabFn(index) {
	for(var i = 0; i < $tabList.length; i++) {
		$tabList[i].className = '';
		$div[i].className = '';
	}
	$tabList[index].className = 'active';
	$div[index].className = 'active';
}
```

4、正确的解决方法一：- 使用let声明

```
for(let i = 0; i < $tabList.length; i++) {
	$tabList[i].onclick = function() {
		changeTabFn(i);
	}
}
```

