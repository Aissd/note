##### http中GET和POST的区别
* GET在浏览器回退时是无害的【无害是指多个请求返回相同的结果】，而POST会再次提交请求；
* GET产生的URL地址可以被Bookmark【书签】，而POST不可以
* GET请求会被浏览器主动cache【缓存】，而POST不会，除非手动设置
* GET请求只能进行url编码，而POST支持多种编码方式
* GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留
* GET请求在URL中传送的参数是有长度限制的，而POST没有
* 对参数的数据类型，GET只接受ASCII字符，而POST没有限制
* GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息
* GET参数通过URL传递，POST放在Request body中

* 对于GET请求，浏览器会把HTTP header和data一并发送出去，服务器响应200（返回数据）
* 对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）
* 本质上说，GET和POST都是基于TCP/IP的HTTP协议的请求方式（TCP连接）。此外，要注意：GET产生一个TCP数据包，POST产生两个TCP数据包。