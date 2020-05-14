1、calc计算

```
$-margin-side: 66px;
transform: translate(calc(100% + #{$-margin-side}), 0);
```

calc不能包含变量，必须使用sass插值的方式#{$variable}

![image-20200419191206782](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20200419191206782.png)

2、继承

```
%test-color{
	color: #f00;
}
.font-test {
	@extend %test-color;
}
```

3、混合宏

```
/* 声明 */
@mixin button-style {
	$btn-bg-color: lightblue;
	color: $btn-bg-color;
}
/* 调用 */
button {
	@include button-style;
}
/* 编译出来的css */
button {
	color: lightblue;
}
```

4、@if指令（配合@else if 和 @else）

```
@mixin blockOrHidden($boolean: true) {
	@if $boolean {
		@debug "$boolean is #{$boolean}"; /* @debug 是在命令管理器里有结果显示的 */
		display: block;
	}
	@else {
		@debug "$boolean is #{$boolean}";
		display: none;
	}
}

.block {
	@include blockOrHidden;
}
.hidden {
	#include blockOrHidden(false);
}
```

5、@for循环

```
@for $i from <start> through <end>
@for $i from <start> to <end>
$i表示变量，start表示起始值，end表示结束值
through表示包括<end>这个数
to则不包括<end>这个数

@for $i from 1 through 3 {
	.item-#{$i} { width: 2em * $i };
}

.item-1 { width: 2em; }
.item-2 { width: 4em; }
.item-3 { width: 6em; }
```

6、@while 循环

```
$types 4;
$type-width: 20px;
@while $types > 0 {
	.while-#{$types} {
		width: $type-width + $types;
	}
}
$types: $types - 1;

/* 编译 */
.while-4 { width: 24px; }
.while-3 { width: 23px; }
.while-2 { width: 22px; }
.while-1 { width: 21px; }
```

7、@each循环

```
@each $var in <list>

$list: adam john wynn mason kurior; // $list是一个列表
@mixin author-images {
	@each $author in $list {
		.photo-#{$author} {
			background: url("/images/avatars/#{$author}.png") no-repeat;
		}
	}
}

.author-bio {
	@include author-images;
}

/* 编译结果 */
.author-bio .photo-adam { background: url("/images/avatars/adam.png") no-repeat; }
.author-bio .photo-john {  background: url("/images/avatars/john.png") no-repeat; }
.author-bio .photo-wynn { background: url("/images/avatars/wynn.png") no-repeat; }
.author-bio .photo-mason { background: url("/images/avatars/mason.png") no-repeat; }
.author-bio .photo-kuroir { background: url("/images/avatars/kuroir.png") no-repeat; }
```

8、字符串函数 - （双引号操作）

```
unquote($string) /* 删除字符中的引号 */
quote($string) /* 给字符添加引号 */
```

9、字符串函数 - 大小写转换

```
to-upper-case()
to-lower-case()
```

10、数字函数 - percentage() - 将数字转换成百分比形式

```
percentage(.2) // 20%
percentage(2px / 10px) // 20%
percentage(2em / 10em) // 20%
```

11、数字函数 - round() - 四舍五入

```
round(12.3) // 12
round(20%) // 20%
```

12、数字函数 - ceil() - 向上取整

```
ceil(2.0) // 2
ceil(2.3%) // 3%
ceil(2px / 3px) // 1
```

13、数字函数 - floor() - 向下取整

```
floor(2.1) // 2
floor(3.5%) // 3%
floor(2px / 10px) // 0
```

14、数字函数 - abs() - 绝对值

```
abs(-10) // 10
abs(-10px) // 10px
abs(-.5%) // 0.5%
```

15、数字函数 - min()  - 在多个数之中找到最小的

```
min(1, 2, 1%, 3, 300%) // 1%
min(1px, 2, 3px) // 1px
```

16、数字函数 - max() - 在多个数之中找到最大的

```
max(1, 5) // 5
max(1px, 5px) // 5px
```

17、数字函数 - random() - 获取一个随机数

```
random() // 0.02551
```

18、列表函数 - length() - 返回列表清单中有多少个值（使用空格隔开）

```
length(10px) // 1
length(10px 20px (border 1px solid) 2em) // 4
```

19、列表函数 - nth($list, $n) - 指定列表中某个位置的值（下标从1开始）

```
nth(10px 20px 30px, 1) // 10px
```

20、列表函数 - join() - 将两个列表连接合并成一个列表

```
join(10px 20px, 30px 40px) // 10px 20px 30px 40px
```

21、列表函数 - append($list, $n) - 将某个值插入到列表最末位

```
append(10px 20px, 30px) // 10px, 20px, 30px
```

22、列表函数 - zip() - 将多个列表值转成一个多维的列表

23、列表函数 - index() - 返回指定值在列表中的位置（找不到返回false）

```
index(1px solid red, 1px) // 1
```



未完...

https://www.imooc.com/code/8432