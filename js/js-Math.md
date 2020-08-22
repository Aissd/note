Math称为数学函数，但是它是属于对象类型的

```
typeof Math; // 'object'
之所以叫做数学函数，是因为Math这个对象中提供了很多操作数学的方法
```

1、abs - 取绝对值

```
Math.abs(10); // 10
Math.abs(-10); // 10
```

2、ceil/floor -向上取整/向下取整

```
Math.ceil(10.01); // 11
Math.ceil(-10.01); // -10

Math.floor(10.999); // 10
Math.floor(-10.999); // -11
```

3、round - 四舍五入

```
Math.round(10.49); // 10
Math.round(10.5); // 11
Math.round(-10.49); // -10.49
Math.round(-10.5); // -10
Math.round(-10.51); // -11

5是临界点，
正数时，5是向上取整
负数时，5是向下取整
```

4、sqrt - 开平方

```
Math.sqrt(100); // 10
Math.sqrt(16); // 4
```

5、pow - 幂（n的m次方）

```
Math.pow(2, 10); // 1024
```

6、max/min - 获取最大值和最小值

```
Math.max(1,2,3,4,5); // 5
Math.min (1,2,3,4,5); // 1
```

7、PI - 获取圆周率（属性）

```
Math.PI; // 3.1415926...
```

8、random - 获取0~1之前的随机小数

```
Math.random(); // 0.151561456416416...

1-10整数
获取n-m之前的随机整数
Math.round(Math.random() * ((m - n) + n));
```

