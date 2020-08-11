1、饼状图

```
饼状图是不能通过grid调整边距的；
调整series中的center:['50%', '40%']，即圆心位置
比如将40%调整为20%，饼状图就会往上移动容器高度的20%
```



```

```



2、折线图

```
option = {
	// 图例组件
    legend: {
        data:  ['耗水', '耗电', '耗煤'],
        /* data:  [
        	{name:'耗水', icon: 'circle'}, 
        	{name: '耗电', icon: 'circle'}, 
        	{name: '耗煤', icon: 'circle'}
        ], */
        textStyle: {
            color: '#333',
            fontSize: 12,
            
        }
    },
    grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
    },
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            type: 'cross',
            label: {
                backgroundColor: '#6a7985'
            }
        }
    },
    xAxis: {
    	show: true,
        type: 'category', // 离散类目数据，自动从series.data或dataset.source中取
        data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
    },
    yAxis: {
        type: 'value'
    },
    axisLabel: {
        color: '#333'
    },
    color: ['#7DC852','#1EC9EC', '#F19149'],
    series: [
        {   
            name: '耗水',
            data: [345, 820, 555, 934, 499, 609, 865],
            type: 'line'
        },
        {
            name: '耗电',
            data: [674, 849, 233, 555, 934, 499, 865],
            type: 'line'
        },
        {
            name: '耗煤',
            data: [456, 674, 849, 254, 750, 690, 934],
            type: 'line'
        }
    ]
};
```

