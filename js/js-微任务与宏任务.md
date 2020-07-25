

一、同步代码：promise的同步代码，顶层代码

二、微任务：promise的resolve，promise的reject

三、宏任务：setTimeout

优先级：同步代码 > 微任务 > 宏任务

1、其中微任务队列的优先级比宏任务队列的优先级要高

```
<script>
    setTimeout(() => {
       console.log('来自宏任务队列');
    });
    console.log('同步代码的任务队列');
    Promise.resolve().then(value => {
        console.log('来自微任务队列');
    });
    
    // 同步代码的任务队列
    // 来自微任务队列
    // 来自宏任务队列
</script>
```

2、定时器模块，时间到了会把任务放到同步代码的队列的后面。当同步代码的队列没有任务可执行时，执行定时器的模块（即使定时器时间到了也必须等到同步代码执行完了再走）

当开始执行script时，定时器模块已经把下面的setTimeout的任务放到定时器模块，并开始计时，等执行完同步代码的任务队列后再执行。



多个定时器时也是同样道理。

```
<script>
    setTimeout(() => {
       console.log('定时器，来自宏任务队列');
    }, 4);
    console.log('同步代码的任务队列');
    for(let i = 0; i < 10000; i++) {
		console.log("");
	}
    
    // 同步代码的任务队列
    // "" * 10000 // 输出1w个空格
    // 定时器，来自宏任务队列
</script>
```

3、微任务 

```
<script>
    setTimeout(() => {
       console.log('定时器，来自宏任务队列');
    }, 0);
  	new Promise(resolve => {
  		console.log('Promise, 同步代码的任务队列'); // 这里是promise的同步代码，输入同步任务
  		resolve();
  	}).then(() => {
  		console.log('then，微观任务'); // promise的resolve，属于微任务
    });
	console.log('普通，同步代码的任务队列');
    
    // Promise, 同步代码的任务队列
    // 普通，同步代码的任务队列
    // then，微观任务
    // 定时器，来自宏任务队列
</script>
```

