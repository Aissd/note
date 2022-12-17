```
// returnValue - 需要返回的值，有初始值则用初始值，否则用数组第一个值
// currentValue - 当前值
// currentIndex - 当前值索引
// array - 当前数组本身
// initialValue - 初始值
// 注意：reduce对于空数组是不会执行回调函数的。
// 注意：如果没有初始值，循环会比有初始值多走一遍循环

array.reduce(function(returnValue, currentValue, currentIndex, array) {}, initialValue);

Array.prototype.myReduce = function(fn, initialValue) {
	var arr = Array.prototype.slice.call(this); // 浅拷贝数组
	if (arr.length === 0) throw new TypeError('Reduce of empty array with no initial value'); // reduce对于空数组是不会执行回调函数的
	var res = initialValue; // 默认初始值
	// 遍历数组的每一个值
	for (let i = 0; i < arr.length; i++) {
		if (res === undefined && i === 0)  {
			res = arr[0];
			continue;
		}
		// 每一个值都会在该方法中被（加工处理）
		res = fn.call(null, res, arr[i], i, this);
	}
	// 最后的返回值
	return res;
}
```