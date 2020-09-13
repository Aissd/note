1、交集

```
let a1 = [1,2,3,1,3,6];
let a2 = [3,4,5,1,2];
function union() {
	let s1 = new Set(a1);
	let s2 = new Set(a2);
	console.log([...new Set([...s1,...s2])]);
}
```

2、并集

```
let a1 = [1,2,3,1,3,6];
let a2 = [3,4,5,1,2];
function intersetcion() {
	// 返回true的留下
	return [...new Set(a1)].filter(function(item){
		return new Set(a2).has(item);
	});
}
```

3、差集

```
let a1 = [1,2,3,1,3,6];
let a2 = [3,4,5,1,2];
function diff() {
	// 返回false的留下
	return [...new Set(a1)].filter(function(item){
		return !new Set(a2).has(item);
	});
}
```

