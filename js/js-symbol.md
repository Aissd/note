可以理解为一个永远不会重复的数字或字符串

1、定义

```
1)
let hd = Symbol();
let edu = Symbol();
console.log(hd == edu); // false，每声明一次就多生成一个内存

hd.name = 'hhhh';
console.log(hd.name); // undefined

2)反复被使用，用这种定义方式（全局声明，重复声明就会引用原有的）
let cmd = Symbol.for('google');
let edu = Symbol.for('google');
console.log(cms == edu); // true
```

2、添加描述

```
let hd = Symbol('online');
console.log(hd.description); // online
```

