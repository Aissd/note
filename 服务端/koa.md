### 初始化
> 初始化
```
yarn init -y
```
> 安装依赖
```
yarn add koa koa-static bootstrap jquery
```

### 搭建一个简易服务
```
let Koa = require('koa');
let path = require('path');
let Serve = require('koa-static');
let app = new Koa();
// 中间件，引用资源文件
app.use(Serve(path.join(__dirname, 'client')));
app.use(Serve(path.join(__dirname, 'node_modules')));
app.listen(3000, function() {
	console.log('serve start 3000');
});
```
> 运行后，访问
```
http://localhost:3000
```

### 搭建一个koa2服务
```
npm i koa-generator -g

koa2 project-name

cd project-name

npm install 

npm i koa2-cors -S // 解决跨域问题

npm run dev
```