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

