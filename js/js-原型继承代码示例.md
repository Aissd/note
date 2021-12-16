```
// .__proto__ 是实例【对象】来调用的
// .prototype 是构造函数 【类】来调用的
function User() {}

let user = new User(); // 通过构造器创建出来的实例，默认会帮实例的原型指向其父类的原型User.prototype

console.log(User.prototype === user.__proto__); // true
console.log(User.__proto__ === user.__proto__); // false 这个是为何？【】

User.prototype.__proto__ === User.__proto__.__proto__; // true 均指向Object.prototype
即：
User.prototype.__proto__ === 均指向Object.prototype; // true 

Object.prototype.__proto__; // null

let obj = {}; // new Object构造器的实例
obj.__proto__ === Object.prototype;

let array = []; // new Array构造器的实例
array.__proto__ === Array.prototype;

let string = ''; // new String构造器的实例
string.__proto__ === String.prototype;

let reg = /a/i; // new RegExp构造器的实例
reg.__proto__ === RegExp.prototype;

let bool = true; // new Boolean构造器的实例
bool.__proto__ === Boolean.prototype;
```

### 自定义对象的原型设置
```
let man = { name: 'man' };
let person = { name: 'person' };

man.__proto__ === Object.prototype; // true 原来的原型指向

Object.setPrototypeOf(man, person); // 将man的原型指向改为person的原型指向

man.prototype === person.prototype; // true

Object.getPrototypeOf(man); // 获取原型 打印出person对象 { name: 'person' }

```