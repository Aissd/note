手写reduce

```
Array.prototype.myReduce = function(fn, prev) {
	// 函数接收两个参数，一个是函数fn，另一个是初始值prev
	for(let i = 0; i < this.length; i++) { // this即当前数组
        if(typeof prev === 'undefined') {
            prev = fn(this[i], this[i + 1], i + 1, this);
            ++i; // 保证下次取值时是正确的结果
        } else {
			prev = fn(prev, this[i], i, this);
        }
	}
	return prev;
}
```

手写forEach

```
Array.prototype.myForEach = function(fn) {
	for(let i = 0; i < this.length; i++) {
		fn(this[i], i);
	}
}
```

手写map

```
Array.prototype.myMap = function(fn) {
	let arr = [];
	for(let i = 0; i < this.length; i++) {
		arr.push(fn(this[i], i));
	}
	return arr;
}
```

手写filter

```
Array.prototype.myFilter = function(fn) {
	let arr = [];
	for(let i = 0; i < this.length; i++) {
		if(fn(this[i], i)) {
			arr.push(fn(this[i], i));
		}
	}
	return arr;
}
```

手写find - 返回查找的那一项，没有返回undefined，找到后就不会继续查找了

```
1）返回符合函数条件的数组的第一个元素，且之后的不再执行；
2）没有符合函数条件的，返回undefined；
3）对于空数组，函数不会执行的；
4）IE11及更早版本不支持find()                            

Array.prototype.myFind = function(fn) {
    if(this.length === 0) return; // 空数组不执行
    let o;
    for(let i = 0; i < this.length; i++) {
        if(fn(this[i])) {
        	o = this[i];
        	break; // 找到符合条件之后，不再执行
        }
    }
    return o; // 返回第一个符合条件的元素，没有则返回undefined
}
```

手写some - 找到后返回true且不会继续查找了（找false可以用every）

手写includes - 

手写Array.from() - 希望将类数组转化成数组

手写Array.of()

