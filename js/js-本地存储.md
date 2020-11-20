### localstorage

> 特点：
1）最大容量5M
2）受同源访问限制，不允许跨域访问
3）浏览器的隐私模式下无法使用
4）本地保存（硬盘），不会发送数据，网络爬虫无法抓取
5）只能存放字符串

> localStorage.getItem(); // 没有返回null

### sessionstorage
> 不同tab不同享

### cookies
> 特点
> 1）按浏览器不同，有个数和大小的限制，一般大小是4k（同一个域名）
> 2）cookie具有保质期，不设置时间的话，浏览器关闭，立即销毁
> 3）安全性：本地可以更改，不宜放敏感数据
> 4）同域共享数据（谁写的cookie，谁才有权利读取）
> 5）与服务端通信，每次都会携带在HTTP头中【保存过多数据会有性能问题】


### cookie的封装
```
function setCookie(name, value, time) {
	var date = new Date();
	date.setDate(date.getDate() + time);
	document.cookie = name + '=' + value + ';expires=' + date;
}

function getCookie(name) {
	var str = document.cookie;
	var arr = str.split('; ');
	for(var i = 0; i < arr.length; i++) {
		var newArr = arr[i].split('=');
		if(newArr[0] == name) {
			return newArr[1];
		}
	}
}

function removeCookie(name) {
	setCookie(name, 1, -1);
}
```