### 柯里化，又称部分求值。
- 一个柯里化的函数首先先接收一些参数，但不会立即求值，而是返回另外一个函数。
- 刚才传的参数在函数形成闭包中被保存起来
- 待到函数被真正需要求值的时候，之前传入的所有参数都会被一次性用于求值

* 假设编写一个计算每月开销的函数，在每天结束前都记录今天花掉了多少钱。直到当月最后一天时才进行求值计算。
```
var currying = function(fn) { // 传入要转为柯里化的函数
	var args = []; // 通过闭包缓存之前传入的数据
	return function() { // 返回一个函数，产生闭包
        if (arguments.length === 0) { // 若没有传值进来，则进行求值计算
            return fn.apply(this, args); // 执行计算函数并返回结果
        } else {
            [].push.apply(args, arguments); // 把数据缓存到args数组
            return arguments.callee; // 返回当前执行的函数fn
        }
	}
}

var cost = (function() {
	var money = 0;
	return function() {
		for (var i = 0, l = arguments.length; i < l; i++) {
			money += arguments[i];
		}
		return money;
	}
})();

var cost = currying(cost); // 转化成currying函数

cost(100); // 未真正求值
cost(200); // 未真正求值
cost(300); // 未真正求值

console.log(cost()); // 求值并输出：600
```