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