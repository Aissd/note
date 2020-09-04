```
let { length } = [1,2];
console.log(length); // 2
```

如果有关键字，可以采用:的形式做别名

```
let { name, default:d } = { name: 'john', defalut: 'xxx' };
console.log(d); // 'xxx'
```

复杂的解构

如果想设置某个属性的默认值，必须采用=号的形式

```
let [, { address: [, a] }, hobby = 'swimming'] = [
	{ name: 'xxx' },
	{ age: 9, address: [1, 2, 3] }
];
console.log(a); // 2
console.log(hobby); // swimming
```

