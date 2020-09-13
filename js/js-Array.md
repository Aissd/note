### Array.from() - 转化成数组

```
Array.from();
```

### DOM节点调用数组的map方法

```
const div = document.querySelectorAll('div');
// 1、Array.from
Array.from(div).map(function(item) {
	console.log(item);
});
// 2、原型链
Array.prototype.map.call(div, function(item) {
	console.log(item);
});

// 3、点语法
[...div].map(function(item) {
	console.log(item);
});
```

### Array.slice(); // 不改变原数组

```
let arr = [1,2,3,4,5];
console.log(arr.slice()); // [1,2,3,4,5] 浅拷贝一个数组
console.log(arr.slice(1)); // [2,3,4,5] 从第一个位置开始，截取到最后一个
console.log(arr.slice(1,2)); // [2] 第一个开始，截到第二个
```

### Array.splice(); // 改变原数组

```
1）移除操作
let arr = [1,2,3,4,5];
console.log(arr.splice(0, 2)); // [1,2] 从第0个开始，截取两个
2)替换操作
console.log(arr.splice(0, 2 , 'a', 'b')); // [1,2] 从第0个开始，截取两个，并从0的位置之后插入'a', 'b'
3)追加操作
console.log(arr.splice(1, 0, 'a')); // [1,'a',2,3,4,5] 从第1个位置开始，移除0个，并在1的位置上追加'a'
4)末尾追加，相当于push
console.log(arr.splice(arr.length, 0, 'a')); // [1,2,3,4,5,'a'] 从数组最后一个位置开始，移除0个，并在最后追加'a'
5)头部追加，相当于unshift
console.log(arr.splice(0, 0, 'a')); // ['a',1,2,3,4,5] 从数组第0个位置开始，移除0个，并在0的位置上追加'a'

```

### 移动数组元素的方法

```
let arr = [1,2,3,4,5];
function move(array, from, to) {
	if(from <= 0 || to >= arr.length) {
		console.error('参数错误');
		return;
	}
	let newArr = [...array]; // 创建一个新的数组，不改变原数组
	let item = newArr.splice(from, 1);
	newArr.splice(to, 0, ...item); // item是一个数组，必须展开，否则会追加一个数组
	return newArr;
}
move(arr, 2, 4);
```

### 清空数组

```
let arr = [1,2,3,4];
let newArr = arr;

1)newArr.length = 0; // arr也会被清空，因为是引用同一个内存地址
2)newArr = []; // arr不会受影响，因为用了一个新的空数组赋予了newArr，此时两个数组各有自己的内存地址
3)newArr.splice(0); // newArr.splice(0, newArr.length);
4)while(newArr.pop()) {}

```

### 查找元素：indexOf()是严格匹配

### 查找元素：includes() - 对引用类型的（对象，数组）无效

```
function includes(array, find) {
	for(let value of array) 
	if(value === find) return true
	return false;
}
```

### 查找元素：find() - 就近原则，找到即返回那个要找的元素的值，对引用类型（对象，数组）有效

> 查不到返回undefined

```
let arr = [1,2,3,4,5];
let res = arr.find(function(item) {
	return item === 2;
});
console.log(res); // 2
```

```
let arr = [{name: 'a'}, {name: 'b'}];
let res = arr.find(function(item) {
	return item.name == 'a';
});
console.log(res); // {name: 'a'}
```

### 查找元素索引:findIndex() - 

```
let arr = [{name: 'a'}, {name: 'b'}];
let index = arr.findIndex(function(item) {
	return item.name == 'a';
});
console.log(index); // 0
```

### 排序

```
let arr = [3,7,5,9,1];
arr = arr.sort(function(a, b) {
	// a - b： -1的话，从小到大（升序）
	// b - a： 1的话，从大到小（降序）
	return a - b;
});
```

### 自己实现sort()函数

```
let arr = [3,5,9,1,4];
function sort(arr) {
	for(let n in arr) {
		for(let m in arr) {
			if(arr[n] < arr[m]) {
				let temp = arr[n];
				arr[n] = arr[m];
				arr[m] = temp;
			}
		}
	}
	return arr;
}
```

### 遍历：array.forEach(function(value, index, array) {}); - 可直接操作DOM元素

```
let arr = [{n: 'a'}, {n: 'b'}];
arr.forEach(function(value, index, array){
	console.log(this); // {} 就是下面的那个{}，不定义就是window
}, {});
```

### interator迭代器

```
let arr = [{n: 'a'}, {n: 'b'}];
let keys = arr.keys(); // 索引
let values = arr.values(); // 值
let entries = arr.entries(); // [index, value]
// 方法一：while遍历
while(({ value, done } = values.next()) && done === false) { 
// ({ value, done } = values.next()) // 这里要加括号提高优先级，保证前面先执行，不然done会报错
	console.log(value);
}
// 方法二：for of
for(let value of arr.values()) {
	console.log(value);
}

for(let [key, value] of arr.entries()) {
	console.log(key, value);
}
```

### every() - 当遍历的全部为真时，返回true，当有一个为false时，返回false，后面就不遍历了

### some() - 有一个为真，即返回true，后面就不遍历了

### map() - 映射

```
let arr = [{name: 'a'}, {name: 'b'}];
arr.map(function (item) {
	item.age = 18; 
}); // 若不return item的话，会改变原数组，因为item的引用地址还是arr的

```

### reduce() -  两个参数（匿名函数，pre的初始值）

```
1）只有一个匿名函数参数时：
let arr = [1,2,3,4,5];
arr.reduce(function(pre, value, index, array) {
	console.log(pre, value);
	// 第一次，pre是第一个元素，value是第二个元素，即 1,2
	// 第二次，pre是第一次的返回值，若无则为undefined，value是第三个元素，即 undefined, 3
	// 当前会遍历4次，因为没有定义初始值
});

2）两个参数（匿名函数，初始值）
let arr = [1,2,3,4,5];
arr.reduce(function(pre, value, index, array) {
	console.warn(pre, value);
	return 99;
	// 第一次，pre是初始值，value是第一个元素，即 0,1
	// 第二次，pre是第一次的返回值99，若无则为undefined，value是第二个元素，即 99, 2
	// 当前会遍历5次，因为有初始值
}, 0);

例子1，用来做统计一个数在数组中出现的个数
let arr = [1,2,1,2,3,4,5,1];
function count(array, item) {
	return array.reduce(function(total, cur) {
		total += cur === item ? 1 : 0;
		return total;
	}, 0);
}
console.log(count(arr, 1));
例子2：用来获取数组中最大在值
let arr = [1,2,5,44,3,87,99];
function getMax(array) {
	return array.reduce(function(pre, cur) {
		return pre > cur ? pre : cur;
	});
}
console.log(getMax(arr));

例子3：数组去重
let arr = [1,2,1,3,4,5,3,2,1];
function uniqueArr(array) {
	return array.reduce(function(arr, cur) {
		if(arr.includes(cur) === false) {
			arr.push(cur);
		}
		return arr;
	}, []);
	return 
}
console.table(uniqueArr(arr));

例子4：展平数组
const twoDArr = [ [1,2], [3,4], [5,6], [7,8] , [9,10] ];

const oneDArr = twoDArr.reduce((accumulator, currentValue) => accumulator.concat(currentValue));

console.log(oneDArr);
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
```

