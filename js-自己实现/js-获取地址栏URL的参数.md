1、基于动态创建A标签重写

```
function queryURLParameter(str) {
	// 1、创建一个a标签，把需要解析的地址当做A标签的href赋值
	var link = document.createElement('a');
	link.href = str;
	// 2、a元素对象的hash/search两个属性分别存储了哈希值和参数值
	var hash = link.hash.substr(1), search = link.search.substr(1);
	// 3、分别解析出hash和参数即可
	var obj = {};
	hash ? obj.HASH = hash : null;
	if(search) {
		search = search.split('&');
		for(var i = 0; i < search.length; i++) {
				var itemAry = search[i].split('=');
				obj[itemAry[0]] = itemAry[1];
		}
	}
	return obj;
}
```

