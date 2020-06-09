1、string.repeat()  -  复制指定次数

```
'abc'.repeat(2); // abcabc
```

2、string.trim()  - 移除头尾空格字符串

3、标签模板

```
let lessons = [
  { title: "后盾人媒体查询响应式布局", author: "后盾人向军" },
  { title: "FLEX 弹性盒模型", author: "后盾人" },
  { title: "GRID 栅格系统后盾人教程", author: "古老师" }
];

function links(strings, ...vars) {
  return strings
    .map((str, key) => {
      return (
        str +
        (vars[key] ? vars[key].replace("后盾人",`<a href="https://www.houdunren.com">后盾人</a>`): "")
      ); 
    })
    .join("");
}

function template() {
  return `<ul>
        ${lessons
          .map(item => links`<li>${item.author}:${item.title}</li>`)
          .join("")}
	</ul>`;
}
document.body.innerHTML += template();
```

4、截取字符串

​	slice、substring 第二个参数为截取的结束位置

​	substr 第二个参数指定获取字符数量

```
let hd = 'houdunren.com';
console.log(hd.slice(3)); //dunren.com
console.log(hd.substr(3)); //dunren.com
console.log(hd.substring(3)); //dunren.com

console.log(hd.slice(3, 6)); //dun
console.log(hd.substring(3, 6)); //dun
console.log(hd.substring(3, 0)); //hou 较小的做为起始位置
console.log(hd.substr(3, 6)); //dunren

console.log(hd.slice(3, -1)); //dunren.co 第二个为负数表示从后面算的字符
console.log(hd.slice(-2));//om 从末尾取
console.log(hd.substring(3, -9)); //hou 负数转为0
console.log(hd.substr(-3, 2)); //co 从后面第三个开始取两个
```

