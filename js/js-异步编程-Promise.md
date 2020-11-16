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
		.then(() => console.log('在setTimeout里面的微任务的resolve2微任务'), () => console.log('在setTimeout里面的微任务的reject2微任务'))
	}, 0);
})
.then(() => console.log('在resolve里面的微任务'), () => console.log('在reject里面的微任务'))
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

4、then方法

```
1）then会在promise执行完成后执行；
2）默认返回的promise状态是fulfiled（resolve）；
3）每次的then都是一个全新的promise；
4）若只关心成功则不需要传递then的第二个参数（默认返回fulfield）；
5）若只关心失败则第一个参数传递null；
6）promise传向then的传递值，如果then没有可处理函数，会一直向后传递；

```

5、promise的封装ajax

```
function ajax(url) {
	return new Promise((resolve, reject) => {
		 let xhr = new XMLHttpRequest();
		 xhr.open('GET', url);
		 xhr.send();
		 xhr.onload = function() {
		 	if(this.status == 200) {
		 		sresolve(JSON.parse(this.response));
		 	} else {
		 		reject('加载失败');
		 	}
		 }
		 xhr.onerror = function() {
		 	reject(this);
		 }
	});
}

ajax(`xxx.php?a=${name}`)
.then(value => {
	console.log(value);
}, reason => {
	console.log(reason);
});
```

6、promise多种错误监测

```
new Promise((resolve, reject) => {
	// reject(new Error('promise fail')); // 会被reject里的then接收到
	// throw new Error('fail'); // 会被reject里的then接收到
	// aaa + 1; // 这个表达式会报错，也会被reject里的then接收到
}).then(
	value => console.log('resolve ' + value),
	reason => console.log('reject ' + reason)
);
```

7、finally - 无论成功或失败始终会执行

8、promise异步加载图片

```
function loadImage(src) {
	return new Promise((resolve, reject) => {
		const image = new Image();
		image.src = src;
		image.onload = () => {
			resolve(image);
		};
		image.onerror = reject();
		document.body.appendChild(image);
	})
}

loadImage('xxx.png').then(image => {
	// 图片加载成功之后可以进行二次处理
	image.style.border = '6px solid red';
});
```

9、封装setTimeout定时器

```
function timeout(delay=1000) {
	return new Promise(resolve => setTimeout(resolve, delay));
}

timeout(2000).then(() => {
	console.log('两秒钟之后输出');
	return timeout(2000);
}).then(() => {
	console.log('再两秒钟之后输出');
});
```

10、构建扁平化的setInterval 

```
function interval(delay=1000, callback) {
	return new Promise(resolve => {
		let id = setInterval(() => {
			callback(id, resolve);
		}, delay);
	});
}

interval(1000, (id, resolve) => {
	console.log(1);
	clearInterval(id);
	resolve();
})
.then(() => {
	return interval(1000, (id, resolve) => {
		console.log(2);
		clearInterval(id);
		resolve();
	});
})
.then(() => {
	console.log('结束');
});
```

11、script脚本的promise加载引擎

```
function loadScript(src) {
	return new Promise((resolve, reject) => {
		const script = document.createElement('script');
		script.src = src;
		script.onload = () => resolve(script);
		script.onerror = reject;
		document.body.appendChild(script);
	});
}

loadScript('js/hd.js')
.then(script => {
	return loadScript('js/ad.js');
})
.then(script => {
	console.log('finish');
});
```

12、promise.all - 批量发送promise - 只要有一个失败的，那全部都是失败的

```
promise.all([promise1, promise2]).then(resolve, reject);
```

13、promise.allSettled - 批量发送promise，不论成功与否，都会返回promise的结果

```
promise.allSettled([promise1, promise2]).then(resolve, reject);
```

14、promise.race() - 批量发送promise，只取最快返回的那个结果

```
promise.race([promise1, promise2]).then(resolve, reject);
```

15、promise的队列原理 - 按顺序执行promise，即前面一个promise返回后再接着下一个promise，而不是全部一起返回

​	1）使用map实现promise实现队列

```
function queue(num) {
	let promise = Promise.resolve();
	num.map(v => {
		promise = promise.then(_ => { // 关键点，把下面的then结果返回给promise去做处理
			return v();
		});
	});
}

function p1() {
    return new Promise(resolve => {
        setTimeout(() => {
            console.log('p1');
            resolve();
        }, 1000);
    });
}

function p2() {
    return new Promise(resolve => {
        setTimeout(() => {
            console.log('p2');
            resolve();
        }, 1000);
    });
}

queue([p1, p2]);
```

16、reduce封装promise队列

```
function queue(num) {
	num.reduce((promise, n) => {
		return promise.then(_ => {
			return new Promise(resolve => {
				setTimeout(() => {
					console.log(n);
					resolve();
				}, 1000);
			});
		});
	}, Promise.resolve());
}

queue([1,2,3,4]);
```

17、catch

```
1）catch用于失败状态的处理函数，等同于then(null, reject){}；
```

18、finally

```
1）无论状态是resolve或reject都会执行此动作，finally与状态无关；
```

19、allSettled

```
用于处理多个promise，只关注执行完成，不关注是否全部执行完成，状态只会是fulfilled（即使rejected也是）
```

20、race

```
1）哪个先返回用哪个；
2）若最快返回的状态为rejected，那整个promise为rejected执行catch；
3）若参数不是promise，内部将自动转为promise（？）
```

21、sleep() - 模拟延迟

```
function sleep(delay=2000) {
	return new Promise(resolve => {
		setTimeout(resolve, delay);
	});
}


sleep(1000).then(() => console.log('-----'));
```

