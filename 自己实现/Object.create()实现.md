Object.create(obj)：创建一个空对象，让空对象____proto____指向obj

```
Object.create = function(obj) {
	function Fn() {};
	Fn.prototype = obj;
	return new Fn();
}
```

