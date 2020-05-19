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

