1、JSONP

```
script
img
link
iframe
不存在跨域请求的限制

问题：
JSONP只能处理GET请求

需要后端支持
```

2、CORS跨域资源共享

```
客户端（发送ajax/fetch请求）

问题：
服务端设置允许源，只能选一个：
1）写具体地址（单源）：只能一个
2）写*（多源）：所有都能访问，但不能再允许携带cookie（浏览器的安全策略）
```

3、http proxy => webpack webpack-dev-server

4、ngnix反向代理 => 不需要前端干啥

5、postMessage

6、socket.io

7、document.domain + iframe

```
只能实现：同一个主域，不同子域之前的操作：
v.qq.com // qq.com是主域
sports.qq.com

例子：
父页面A：http://www.zhufengpeixun.cn/A.html
<iframe src="http://school.zhufengpeixun.cn/B.html" style="display: none;"></iframe>
<script>
	document.domain = 'zhufengpeixun.cn';
	var user = 'admin';
</script>
子页面B：http://school.zhufengpeixun.cn/B.html
<script>
	document.domain = 'zhufengpeixun.cn';
	console.log(window.parent.user);
</script>
```

8、window.name + iframe

```
页面A：
let proxy = function(url, callback) {
	let count = 0; // 加载次数
	let iframe = document.createElement('iframe');
	iframe.src = url;
	iframe.onload = function() {
		if(count === 0) {
            iframe.contentWindow.location = 'http://www.zhufengpeixun.cn/proxy.html';
            count++;
            return;
		}
		callback(iframe.contentWidth.name);
	}
	document.body.appendChild(iframe);
}
```

9、location.hash + iframe

```

```

