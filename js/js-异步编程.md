1、promise - 微任务，宏任务与同步任务

```
console.log('普通的同步任务1');
new Promise((resolve, reject) => {
	console.log('在promise里面的同步任务');
	resolve();
	setTimeout(() => {
		console.log('在setTimeout里面的宏任务');
		new Promise((resolve2, reject2) => {
			resolve2();
			console.log('在setTimeout里面的微任务的宏任务');
		})
		.then(() => console.log('在setTimeout里面的微任务的resolve2微任务'))
		.then(() => console.log('在setTimeout里面的微任务的reject2微任务'));
	}, 0);
})
.then(() => console.log('在resolve里面的微任务'))
.then(() => console.log('在reject里面的微任务'));
console.log('普通的同步任务2');

// 普通的同步任务1
// 在promise里面的同步任务
// 普通的同步任务2
// 在resolve里面的微任务
// 在setTimeout里面的宏任务
// 在setTimeout里面的微任务的宏任务
// 在setTimeout里面的微任务的resolve2微任务
```

2、状态中转

```
let p1 = new Promise((resolve, reject) => {
	// resolve('成功');
	setTimeout(() => { reject() }, 2000); // 这里做了延迟，下面的中转promise也会跟着延迟
});
new Promise((resolve, reject) => {
	// 这里接收p1这个promise的返回结果（结果也是一个promise），这里作为中转，走到对应的resolve或reject		resolve(p1);
})
.then(msg => console.log('resolve' + msg))
.then(reason => console.log('reject ' + reason));
```

3、若只想处理其中一种promise状态，传null

```
new Promise((null, reject) => {
	reject('失败');
}).then(reason => console.log(reason));
```

