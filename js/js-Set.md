1、特性：不能放重复的数据，严格匹配（所以1和"1"可同时存在）

2、声明方式：

```
1）let set = new Set();
set.add(1);
set.add(1); // 因为Set的特性，不能重复，所以无法添加进去
set.add('1');
console.log(set); // Set [ 1, "1" ]

2）let set = new Set([1,2,1,1,2,3,4,5]);
console.log(set); // // Set [1,2,3,4,5]

3）参数是字符串的话，会做展开处理
let set = new Set('google');
console.log(set); // Set ['g', 'o', 'o', 'g', 'l', 'e']
```

3、获取数量 - Set.size()

4、是否含有某元素 - Set.has(''xxx); // true 或 false

5、添加 - Set.add()

6、删除 - Set.delete(); 删除成功，返回true。删除不存在的，会返回false

7、查看元素 - Set.values() // SetIterator {'xxx'}

8、彻底清空 - Set.clear() // 返回undefined

9、转换成数组

```
let set = new Set(['a', 'b']);
console.log(Array.from(set));
console.log([...set]);
```

10、数组转换成Set

```
let arr = [1,2,3,4,5];
arr = new Set(arr);
```

11、使用for of 遍历

```
let set = new Set(['a', 'b']);
for(const value of set) {
	console.log(value); // 'a'   // 'b'
}
```

