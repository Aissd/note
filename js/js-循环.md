```
1、forEach
_array.forEach((item, index, array) => {});
```



```
const colorMap = {
  '#20a0ff': 'primary',
  '#0190fe': 'secondary',
  '#fbfdff': 'darkWhite',
  '#1f2d3d': 'baseBlack',
  '#324157': 'lightBlack',
  '#48576a': 'extraLightBlack',
  '#8391a5': 'baseSilver',
  '#97a8be': 'lightSilver',
  '#bfcbd9': 'extraLightSilver',
  '#d1dbe5': 'baseGray',
  '#e4e8f1': 'lightGray',
  '#eef1f6': 'extraLightGray',
  '#1d90e6': 'buttonActive',
  '#4db3ff': 'buttonHover',
  '#dfe6ec': 'tableBorder',
  '#d2ecff': 'datepickerInRange',
  '#afddff': 'datepickerInRangeHover',
  '#1c8de0': 'selectOptionSelected',
  '#edf7ff': 'lightBackground'
};

Object.keys(colorMap).forEach((item, index, array) => {
  console.log(item, index, array); 
});
```



2、杨辉三角形

```
function star(row = 5) {
    for(let i = 0; i < row; i++) {
        for(let j = 0; j < i; j++) {
            document.write('*');
        }
        document.write('<br />');
    }
}
star(10);
```



3、标签 - 例子里的parent 和 son

双重循环，可以用标签来设置break或者continue跳到哪去

```
parent: for(let i = 1; 1<= 10; i++) {
	son: for(let n = 1; n <= 10; n++) {
		if(n % 2 == 0) {
			console.log(i, n);
		}
		if(n + i > 10) {
			break parent;
		}
	}
}
```



4、while

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