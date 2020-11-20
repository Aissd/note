### 饼状图

```
饼状图是不能通过grid调整边距的；
调整series中的center:['50%', '40%']，即圆心位置
比如将40%调整为20%，饼状图就会往上移动容器高度的20%
```

```
tooltip: {
	confine: true // 解决显示不全的问题
}

饼图中间放数据
title:{
    text: sum + '万',
    left: "center",
    top: "50%",
    textStyle:{
        color: "#fff",
        fontSize: 18,
        align: "center"
    }
},
graphic:{
    type: "text",
    left: "center",
    top: "40%",
    style: {
        text: "账单总收入",
        textAlign: "center",
        fill: "#fff",
        fontSize: 14
    }
}
```

### 折线图

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
    	top: '10px',
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
    	show: true,
        type: 'value',
        data: [11,22,33,44]
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

```
series: [
	{
		type: 'bar',
		barWidth: 18,
		itemStyle: {
			color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
				offset: 0,
				color: '#01E3FE'
			}, {
				offset: 1,
				color: '#1999F9'
			}])
		},
		data: seriesData
	},
	{
		type: 'line',
		lineStyle: {
			color: '#FF0000'
		},
		itemStyle: {
			color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
				offset: 0,
				color: '#01E3FE'
			}, {
				offset: 1,
				color: '#1999F9'
			}])
		},
		yAxisIndex: 1,
		data: seriesData
	}
]
```



### 柱状图

```
yAxis: {
	// 坐标轴
	axisLabel: {
        color: '#fff',
        fontSize: 12
	},
	// 纵坐标阴影
    splitArea: {
    	show: false,
    }
},
xAxis: {
	// 坐标轴
	axisLabel: {
        color: '#fff',
        fontSize: 12
    },
    // 坐标线
    axisLine: {
         lineStyle: {
         	type: 'solid',
         	color: '#f00', // 左边线的颜色
         	width:'2' // 坐标线的宽度
         }
    },
	// 坐标值
    axisLabel: {
         textStyle: {
         	color: '#f00'
		}
	}
}
series: [
	{
		data: [1,2,3,4,5,6],
		type: 'bar',
		// 柱状图上的数据
        label: {
            color: '#fff',
            show: true,
            position: 'top'
        },
        // 柱状图宽度
        barWidth: 30,
        // 显示柱状图的背景
		showBackground: true,
		// 柱状图的背景色
        backgroundStyle: {
           color: 'rgba(220, 220, 220, 0.8)'
        },
        // 柱状图样颜色
        itemStyle: {
            normal: {
                // 随机显示
                // color:function(d){
                return "#"+Math.floor(Math.random()*(256*256*256-1)).toString(16);}
                // 定制显示（按顺序）
                color: params => { 
                    return this.colorList[params.dataIndex] 
                }
            }
        }
	}
]
```

### echart 柱状图 每根柱子显示不同颜色
https://www.cnblogs.com/rexyan/p/7267199.html
