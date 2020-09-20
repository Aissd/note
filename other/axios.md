axios库，是基于promist的http库，可运行在浏览器和node.js中。

vue整合axios

http://www.axios-js.com/docs/vue-axios.html


实例

https://blog.csdn.net/p445098355/article/details/106300065?utm_source=app

### axios跨域请求发送两次
> 原因：跨域请求时，浏览器会首先使用OPTIONS方法发起一个预请求，判断接口是否能够正常通讯，若通讯异常，则不会发送真正的请求，如果测试通讯正常，则开始真正的请求