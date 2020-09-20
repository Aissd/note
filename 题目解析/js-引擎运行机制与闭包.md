1、

```
let a = {
	n: 1
};
let b = a;
a.x = a = {
	n: 2
};
console.log(a.x);
console.log(b);
```

2、

```
let x = 1;
function A(y) {
	let x = 2;
	function B(z) {
		console.log(x + y + z);
	}
	return B;
}
let C = A(2);
C(3);
```

3、

```
let a = 12, b = 12;
function fn() {
	let a = b = 13;
	console.log(a, b);
}
fn();
console.log(a, b);
```

4、

```
let i = 1;
let fn = (i) => (n) => console.log(n + (++i));
let f = fn(1);
f(2);
fn(3)(4);
f(5);
console.log(i);

// let fn = (i) => (n) => console.log(n + (++i)); 拆开如下：
let fn = function(i) {
	return function(n) {
		return console.log(n + (++i));
	}
}
```

5、

```
var a = 12;
var b = a;
b = 13;
console.log(a);
```

6、

```
var a = { n: 12 };
var b = a;
b['n'] = 13;
console.log(a.n);
```

7、

```
var a = { n: 12 };
var b = a;
b = { n: 13 };
console.log(a.n);
```

8、

```
var a = {}, b = '0', c = 0;
a[b] =  'zf';
a[c] = 'px';
console.log(a[b]);
```

9、

```
var a = {}, b = Symbol('1'), c = Symbol('1');
a[b] = 'zf';
a[c] = 'px';
console.log(a[b]);
```

10、

```
var a = {}, b = { n: '1' }, c = { m: '2' };
a[b] = 'zf';
a[c] = 'px';
console.log(a[b]);
```

11、

```
var a = { n: 1};
var b = a;
a.x = a = { n: 2};
console.log(a.x);
console.log(b);
```

12、

```
var x = [12, 23];
function fn(y) {
	y[0] = 100;
	y = [100];
	y[1] = 200;
	console.log(y);
}
fn(x);
console.log(x);
```

