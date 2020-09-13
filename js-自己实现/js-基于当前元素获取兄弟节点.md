1、获取当前元素的上一个兄弟元素节点 - pre

```
previousSibling：上一个兄弟元素节点
previousElementSibling：上一个兄弟元素节点，但不兼容

function prev(curEle) {
	// 1、先找到当前元素的兄弟节点，看是否为元素节点，不是则基于向上查找
	// 2、若没有上一个兄弟节点了，说明当前节点即为第一个元素，结束查找
	var pre = curEle.previousSibling;
	while(pre && pre.nodeType !== 1) {
		// 验证pre是否存在，不存在则为null
		// pre.nodeType是验证是否为元素
		pre = pre.previousSibling;
	}
	return pre;
}
```

2、获取当前元素的下一个兄弟元素节点 - next

3、获取当前元素前面的所有兄弟元素节点 - preAll

4、获取当前元素后面的所有兄弟元素节点 - nextAll

5、获取所有兄弟元素节点 - siblings

6、获取当前元素的索引 - index

7、获取当前元素的所有元素子节点

```
基于children不兼容IE低版本浏览器（会把注释当做元素节点）
function children(curEle) {
	// 1、首先获取当前元素下所有子节点
	// 2、然后遍历，筛选并存储出nodeType===1
	var nodeList = curEle.childNodes, result = [];
	for(var i = 0; i < nodeList.length; i++) {
		var item = nodeList[i];
		if(item.nodeType === 1) {
			result.push(item);
		}
	}
	return result;
}
```

