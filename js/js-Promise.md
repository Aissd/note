> 题1：以下三种有什么不同
```
var promise = new Promise(function(resolve, reject){
  setTimeout(function() {
    resolve(1);
  }, 3000);
});

// 1
promise.then(() => {
  return Promise.resolve(2);
}).then((n) => {
  console.log(n);
});

// 2
promise.then(() => {
  return 2
}).then((n) => {
  console.log(n);
});

// 3
promise.then(2).then((n) => {
  console.log(n);
});
```
1）输出2。Promise.resolve就是返回了一个新的Promise对象，然后在下一个事件循环里才会去执行then
2）输出2。和1不一样的是，它不用等下一个事件循环。
3）输出1。then和catch期望接收函数做参数，如果非函数就会发生Promise穿透，打印的是上一个Promise的返回

> 