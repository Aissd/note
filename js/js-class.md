### 生成实例对象的传统方法，是通过构造函数
```
function Point(x, y) {
	this.x = x;
	this.y = y;
}
Point.prototype.toString = function() {
	return '(' + this.x + ', ' + this.y + ')';
}

var p = new Point(1, 2);
p.toString();
```

### es6改写
```
class Point {
	constructor(x, y) {
		this.x = x;
		this.y = y;
	}
	toString() {
		return '(' + this.x + ', ' + this.y + ')';
	}
}

var p = new Point(1, 2);
p.toString();
```