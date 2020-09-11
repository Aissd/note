localstorage

```
特点：
1）最大容量5M
2）受同源访问限制，不允许跨域访问
3）浏览器的隐私模式下无法使用
4）本地保存（硬盘），不会发送数据，网络爬虫无法抓取
5）只能存放字符串

localStorage.getItem(); // 没有返回null
```

sessionstorage 不同tab不同享

cookies同域共享数据