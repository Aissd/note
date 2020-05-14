```
let fragment = document.createDocumentFragment();
let firstChild;
while(firstChild = el.firstChild) {
	fragment.appendChild(firstChild);
}
return fragment;
```

```
while(firstChild = el.firstChild)
```


这个语句进行了2个操作：

1. 执行赋值操作`firstChild = el.firstChild`
2. 执行`while(firstChild)`，`while`是条件为真的情况下才执行，也就是必须`el.firstChild`有值的情况下才执行

使用 appendChild() 方法移除元素到另外一个元素

http://js.jirengu.com/xuxokituve/1/edit?html,js,output

