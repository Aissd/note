可以理解为一个永远不会重复的数字或字符串

### 定义

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

### 添加描述

```
let hd = Symbol('online');
console.log(hd.description); // online
```

### 比较

```
1）存储一个Symbol，然后取出来与自己比较，所以为true
let val = Symbol('00');
console.log(val == val); // true
2）分别创建了两个同名的Symbol，所以为false
console.log(Symbol('AA') == Symbol('AA')); // false
```

### 消除魔术字符串

```

```

### symbol不能被new

### 不参与for in/of遍历

```
for in
for of
Object.keys()
Object.values()
getOwnPropertyNames()
JSON.stringify();
都不能遍历Symbol

单独拿到Symbol
Object.getOwnPropertySymbols()
```

### Symbol()创建出来的，不是Symbol的实例

```
Symbol() instanceof Symbol; // false
```

### Symbol的对象类实例

```
Object(Symbol()); // 
```

### Symbol不能参与计算 - 不能隐式转换

```
let n = Symbol();
n+10; // 报错 - 不能隐式转换成数字
n+''; // 报错 - 不能隐式转换成字符串

支持显式转换
String(Symbol()); // 'Symbol()';
Symbol().toString(); // 'Symbol()';

/* 
/!*  *!/
*/
```

