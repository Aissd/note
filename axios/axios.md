axios库，是基于promist的http库，可运行在浏览器和node.js中。

vue整合axios

http://www.axios-js.com/docs/vue-axios.html


实例

https://blog.csdn.net/p445098355/article/details/106300065?utm_source=app

### axios跨域请求发送两次
> 原因：跨域请求时，浏览器会首先使用OPTIONS方法发起一个预请求，判断接口是否能够正常通讯，若通讯异常，则不会发送真正的请求，如果测试通讯正常，则开始真正的请求


### axios特性
1、根据当前环境自动判断，
	在浏览器中创建XMLHttpRequests
	在node.js中创建http请求
2、支持Promise的API
3、拦截请求和响应
4、转换请求数据和响应数据
5、取消请求
6、自动转换JSON数据
7、客户端支持防御XSRF

### 基本使用方式
1、axios(config)
2、axios.method(url, data, config) // method可以是get，post...

### axios实现原理过程

https://github.com/Sunny-lucking/howToBuildMyAxios

### method
以下方法只接收两个参数：
request，get，delete，head，options
以下方法可接收三个参数：
post，put，patch
