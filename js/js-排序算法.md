十大经典排序算法：

https://sort.hust.cc/

1、冒泡排序

算法步骤：

​	1）比较相邻的元素。如果第一个比第二个大，就交换他们两个。

​	2）对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。

​	3）针对所有的元素重复以上的步骤，除了最后一个。

​	4）持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

```
function bubbleSort(arr) {
    var len = arr.length;
    for (var i = 0; i < len - 1; i++) {
        for (var j = 0; j < len - 1 - i; j++) {
            if (arr[j] > arr[j+1]) {        // 相邻元素两两对比
                var temp = arr[j+1];        // 元素交换
                arr[j+1] = arr[j];
                arr[j] = temp;
        	}
        }
    }
    return arr;
}
```

2、选择排序

算法步骤

​	1）首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置

​	2）再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。

​	3）重复第二步，直到所有元素均排序完毕。

```
function selectionSort(arr) {
    var len = arr.length;
    var minIndex, temp;
    for (var i = 0; i < len - 1; i++) {
        minIndex = i;
        for (var j = i + 1; j < len; j++) {
            if (arr[j] < arr[minIndex]) {     // 寻找最小的数
                minIndex = j;                 // 将最小数的索引保存
            }
        }
        temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
    return arr;
}
```

