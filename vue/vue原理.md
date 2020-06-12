1、响应式

```
1）vue会给每个声明在data的对象，用defineproperty封装set和get方法，其中如果有嵌套的对象，则会使用递归逐层遍历封装；（会判断是否是object类型并且不是null）
```



```
2）vue不会给每个声明在data的数组的每个元素用defineproperty封装set和get方法，因为给每个数组索引封装太消耗性能；
```

