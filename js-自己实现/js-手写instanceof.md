### instanceof原理
> 只要原型链上存在，就返回true
```
console.log([] instanceof Array);
console.log([] instanceof Object);

console.log([].__proto__ === Array.prototype); // true
console.log([].__proto__.__proto__ === Object.prototype); // true
```
###  手写instanceof

```
// A instanceof B
function myInstanceof(A, B) {
	B = B.prototype;
	A = A.__proto__;
	while(true) {
		if(A === null) { // Object.prototype.__proto__
			return false;
		}
		if(A === B) {
			return true;
		}
		A = A.__proto__; // 继续在原型链上找
	}
}
```