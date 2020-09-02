原型（prototype）、原型链（____proto____）

```
1）所有的函数数据类型都天生自带一个属性：prototype（原型），这个属性的值是一个对象，浏览器会默认给它开辟一个堆内存；（函数 -> 自带prototype对象）
2）在浏览器给prorotype开辟的堆内存中有一个天生自带属性：constructor，这个属性存储的值是当前函数本身（原型 -> 自带constructor属性，值是函数本身）
3）每一个对象都有一个__proto__的属性，这个属性指向当前实例所属类的prototype（如果不能确定它是谁的实例，都是Object的实例）（每个实例对象 -> 自带__proto__对象）
```

原型链：

```
它是一种基于__proto__向上查找的机制。当我们操作实例的某个属性或者方法时，首先找自己空间中私有的属性或者方法：
1）找到了，则结束查找，使用自己私有的即可
2）没有找到，则基于__proto__找所属类的prototype，如果找到就用这个公有的，如果没找到，基于原型上的__proto__继续向上查找，一直找到Object.prototype的原型为止。如果再没有操作的属性或方法不存在
```

原型继承：

```
让父类中的属性和方法在子类实例的原型链上
	Child.prototype = new Parent();
	Child.prototype.constructor = Child;
特点：
	1）不像其他语言中的继承一样（其他语言的继承一般都是拷贝继承，也就是子类继承父类，会把父类中的属性和方法拷贝一份到子类中，供子类的实例调取使用），它是把父类的原型放到子类实例的原型上，实例想调取这些方法，是基于__proto__原型链查找机制完成的。
	2）子类可以重写父类上的方法（这样会导致父类其它的实例也受到影响）
	3）父类中私有或者公有的属性方法，最后都会变为子类中公有的属性和方法
```

call继承

```
特点：
	Child方法中把Parent当做普通函数执行，让Parent中的this指向Child的实例，相当于给Child的实例设置了很多私有的属性和方法
	1）只能继承父类私有属性或者方法（因为是把Parent当做普通函数执行，和其原型上的属性和方法没关系）
	2）父类私有的变为子类私有的
```

寄生组合继承：call继承+类似于原型继承

```
特点：父类私有和公有的分别是子类实例的私有和公有属性方法（推荐）
```

es6中的继承

```
es6中基于class创造出来的类不能当做普通函数执行
class Child extends Parent {} => 这样就可以实现：父类公有的，变成子类公有的。等同于寄生组合
等同于 Child.prototype.__proto__ = Parent.prototype 
class A {
	constructor(x) {
		this.x = x;
	}
	getX() {
		console.log(this.x);
	}
}
class B extends A {
	constructor(y) {
		// 子类只要继承父类，可以不写constructor，一旦写了，则必须在constructor中的第一行写super()
		// 不写constructor，浏览器默认创建constructor(...args) { super(...args); }
		super(200); // A.call(this, 200); => 等同于把父类当普通方法执行，给方法传递参数，让方法中的this是子类的实例
		this.y = y;
	}
	getY() {
		console.log(this.y);
	}
}

let b1 = new B(100);
console.log(b1);
```

