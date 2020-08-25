1、获得 body 元素的节点类型：

​	1）如果节点是元素节点，则 nodeType 属性将返回 1。

​	2）如果节点是属性节点，则 nodeType 属性将返回 2。

```
document.body.nodeType;
```

2、获取某元素下所有直接子节点

```
document.body.childNodes;
```

3、获取某元素下所有属性

```
document.getElementById(#id).attributes
```

4、移除子元素

```

```

5、查找元素

```
document.querySelector('#id');
document.querySelector('.className');
document.querySelector("[name='password']");
```

6、创建元素

```
document.createElement('div');
```

7、原生js添加，移除class

```
el.classList.add('active');
el.classList.remove('active');
```

8、切换类toggle

```
el.classList.toggle('active');
```

9、是否存在类

```
el.classList.contains('active');
```

10、item（index） -  返回类名在元素中的索引值，从0开始，范围外则返回null

```
el.classList.item(0); // active
```

11、兼容性：IE10即IE10以上支持

```
if (!("classList" in document.documentElement)) {  
    Object.defineProperty(HTMLElement.prototype, 'classList', {  
        get: function() {  
            var self = this;  
            function update(fn) {  
                return function(value) {  
                    var classes = self.className.split(/\s+/g),  
                        index = classes.indexOf(value);  
                      
                    fn(classes, index, value);  
                    self.className = classes.join(" ");  
                }  
            }  
            return {                      
                add: update(function(classes, index, value) {  
                    if (!~index) classes.push(value);  
                }),  
                remove: update(function(classes, index) {  
                    if (~index) classes.splice(index, 1);  
                }),  
                toggle: update(function(classes, index, value) {  
                    if (~index)  
                        classes.splice(index, 1);  
                    else  
                        classes.push(value);  
                }),  
                contains: function(value) {  
                    return !!~self.className.split(/\s+/g).indexOf(value);  
                },  
                item: function(i) {  
                    return self.className.split(/\s+/g)[i] || null;  
                }  
            };  
        }  
    });  
} 
```

12、获取容器高度

```
1）包括内填充，边框：document.querySelector('#a').offsetHeight
2）仅容器高度：document.querySelector('#a').clientHeight
```

13、设置滚动条位置

```
document.querySelector('#a').scrollTop = 100;
```

14、a标签返回上一页

```
<a href="javascript:history.go(-1)">返回上一步</a>
```



DOM树

```
当浏览器加载HTML页面的时候，首先就是DOM结构的计算，计算出来的DOM结构就是DOM树（把页面中的HTML标签像树状结构一样，分析出之间的层级关系）
```

在js中获取DOM元素的方法

```
- 使用时的document是限定了获取元素的范围，我们把它称之为上下文（context）
document.getElementById
	1）上下文只能是document
	2）如果ID重复了，只能获取第一个
	3）在IE6~7中，会把表单元素（input）的name属性值当做ID来使用（建议：以后使用表单元素的时候，不要让name和id的值有冲突）
document.getElementsByTagName
	1）[context].getElementsByTagName在指定的上下文中，根据标签名获取到一组元素集合
	2）元素集合是类数组，不能直接使用数组的方法
	3）它会把当前上下文中，子子孙孙（后代）层级内的标签都能获取到
document.getElementsByClassName
	1）IE6~8下不兼容
document.getElementsByName
	1）在IE浏览器中（IE9及以下版本），制度表单元素的name属性起作用
document.head
	1）获取head元素对象
document.body
	1）获取body元素对象
document.documentElement
	1）获取html元素对象
querySelector
	1）哪怕选择器匹配多个，只获取第一个
	2）不兼容IE6~IE8
	3）性能消耗较大
querySelectorAll
	1）在querySelector的基础上，获取到选择器匹配的所有元素，结果是一个节点集合
	2）不兼容IE6~IE8
	3）性能消耗较大

```

需求：获取浏览器一屏幕的宽度和高度（兼容所有的浏览器）

```
document.documentElement.clientWidth || document.body.clientWidth
document.documentElement.clientHeight || document.body.clientHeight
```

获取当前页面所有的id为hh的项

```
// 1、首先获取当前文档中所有的HTML标签
// 2、依次遍历这些元素标签对象，谁的id等于hh，就把它存储起来
function queryAllById(id) {
	// 基于通配符*获取到整个文档中所有的HTML标签
	var nodeList = document.getElementsByTagName(*);
	// 遍历集合中的每一项，把元素ID和传递ID相同的这一项存储起来
	var ary = [];
	for(var i = 0; i < nodeList.length; i++) {
		var item = nodeList[i];
		item.id = nodeList[i];
		item.id === id ? ary.push(item) : null;
	}
	return ary;
}
```

节点（node）

```
在一个html文档中出现的所有东西都是节点
1）元素节点（html标签）
	nodeType：1
	nodeName：大写标签名
	nodeValue：null
2）文本节点（文字内容）
	nodeType：3
	nodeName：'#text'
	nodeValue：文本内容
	
	在标准浏览器中会把空格/换行等当做文本节点来处理
3）注释节点（注释内容）
	nodeType：8
	nodeName：'#common'
	nodeValue：注释内容
4）文档节点（document）
	nodeType：9
	nodeName：'#document'
	nodeValue：null
每一种类型的节点都会有一些属性区分自己的特性和特征
1）nodeType 节点类型
2）nodeName 节点名称
3）nodeValue 节点值
```

描述节点之前关系的属性

```
1）parentNode
	获取当前节点唯一的父亲节点
2）childNodes
	获取当前元素的所有子节点
	- 子节点：只获取儿子级别的
	- 所有：包含所有元素节点，文本节点
3）children
	获取当前元素的所有元素子节点
	- IE6~8中会把注释节点也当做元素节点获取到，所以兼容性不好
4）previousSibling
	获取当前节点的上一个兄弟节点（可能是元素也可能是文本）
5）previousElementSibling
	获取上一个兄弟元素节点（不兼容IE6~8）
6）nextSibling
	获取当前节点的下一个兄弟节点
7）nextElementSibling
	获取下一个兄弟元素节点（不兼容IE6~8）
8）firstChild
	获取当前元素的第一个子节点（可能是元素或者文本）
9）firstElementChild
	获取当前元素的第一个子节点
10）lastChild
	获取当前元素的最后一个子节点（可能是元素或者文本）
11）lastElementChild
	获取当前元素的最后一个子节点
```

关于DOM的增删改

```
1）createElement
	创建一个元素标签（元素对象）
	document.createElement([标签名])
2）appendChild
	把一个元素对象插入到指定容器的末尾
	[container].appendChild([newEle])
3）insertBefore
	把一个元素对象插入到指定容器中某一个元素标签之前
	[container].insertBefore([newEle],[oldEle])
4）cloneNode
	拷贝某一个节点
	[curEle].cloneNode(); // 浅拷贝，只拷贝当前标签
	[curEle].cloneNode(true); // 深拷贝，当前标签及其里面的内容
5）removeChild
	在指定容器中删除某一个元素
	[container].removeChild([curEle])
6）set/get/removeAttribute
	设置/获取/删除当前元素的某一个自定义属性
```

