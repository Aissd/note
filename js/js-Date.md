1、封装Date

```
function dateFormat(date, format = "YYYY-MM-DD HH:mm:ss") {
  const config = {
    YYYY: date.getFullYear(),
    MM: date.getMonth() + 1,
    DD: date.getDate(),
    HH: date.getHours(),
    mm: date.getMinutes(),
    ss: date.getSeconds()
  };
  for (const key in config) {
    format = format.replace(key, config[key]);
  }
  return format;
}
console.log(dateFormat(new Date(), "YYYY年MM月DD日"));
```

2、获取时间戳 - new Date()

```
let date = new Date();
date.getTime(); // 1590021572058
date * 1; // 1590021572058
```

Date().getTime() 与 Date.now()等价，但建议使用Date.now()，性能相比会更好； 

3、给给定的时间加秒

```
// time - 时间字符串 - '2020-07-23 15:15:15'
// second - 要加的秒 - 10
function addSecondFn(time, second) {
	let res = (new Date(time).getTime() / 1000 + second) * 1000;
	return formatFn(res, 'yyyy-MM-dd HH:mm:ss');
}

// 把时间戳转换为特定格式的函数
function formatFn(time, format) {
	...
}
```
