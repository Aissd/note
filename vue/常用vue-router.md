1、修改地址栏参数

```
this.$router.replace({ path: '/situationMap/' + params.currentPageType + '?areaId=440303' });
```

2、默认路由

route.js的第一个即为默认路由

可设置成/默认跳转过去

```
{
   path: "/",
   name: 'indexMap',
   redirect: "/indexMap",
   meta: { title: "" }
}
```

