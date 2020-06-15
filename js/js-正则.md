1、

```
// 若配了全局，正则没匹配一次后，lastIndex会改变
let reg = /aa/g;
reg.test('aabb'); // true
console.log(reg.lastIndex); // 2 => 跑去第二个位置了
reg.test('aabb'); // false
console.log(reg.lastIndex); // 0

解决方法是，每使用完一次正则reg，就把reg.lastIndex重置为0
```

