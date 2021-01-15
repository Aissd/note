https://blog.csdn.net/striveb/article/details/91585050

##### http相关状态码
* 1xx：请求处理中，请求已被接受，正在处理
* 2xx：请求成功，请求被成功处理
	200 OK // 客户端请求成功
* 3xx：重定向，要完成请求必须进行进一步处理
	301 Moved Permanently // 永久重定向，使用域名跳转
	302 Found // 临时重定向，未登录的用户访问用户中心重定向到登录页面
* 4xx：客户端错误，请求不合法
	400 Bad Request // 客户端请求有语法错误，不能被服务器所理解
	401 Unauthorized // 请求未经授权，这个状态代码必须和 WWW-Authenticate 报头域一起使用
	403 Forbidden // 服务器收到请求，但是拒绝提供服务
	404 Not Found // 请求资源不存在，eg：输入了错误的 URL
* 5xx：服务度错误，服务器不能合理处理合法请求
	500 Internal Server Error // 服务器发生不可预期的错误
	502 Bad Gateway //作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到无效的响应。
	503 Server Unavailable // 服务器当前不能处理客户端的请求，一段时间后可能恢复正常
	504 Gateway Time-out //网关超时，这个有时候Nginx会抛出的异常，主要原因是请求超时，比如你想导出下载某个文件，结果文件太大，就可能请求超时了。