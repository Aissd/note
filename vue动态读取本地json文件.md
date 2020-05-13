通过axios加载本地json文件：

1、在vue-cli3中，json文件应放在public文件夹下；

2、执行 npm run build  ，把json文件打包到dist文件里；

3、页面请求即可

```
this.$http.get('http://localhost:18081/static/guangdong.json').then(response => {
	...
}, error => {
	...
});
```

