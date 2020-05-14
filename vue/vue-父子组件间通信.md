1、给子组件添加一个ref，就可以在父组件里获取子组件的元素

​	1）子组件：

```
<mapViewG :markers="markers" ref="mapView" :isDraw="true" :isDrawPoint="true" />
```

​	2）父组件调用：

```
mounted() {      
	console.log(this.$refs.mapView.map);
	this.$refs.mapView.$el.style.display = "block"; // 操作dom
	this.$refs.mapView.initFn(); // 直接调用子组件方法
}
```

2、子组件调用父组件的元素

​	1）子组件：

```
this.$parent
```

3、子组件接收组件数据

```
props: {
	markers: [Array, Object], // 指定多个类型
    size: String, // 指定单个类型
    isOpenLeft: { // 数据限制
    	type: Boolean, 
    	required: true,
    	default: false
    },
}
```

