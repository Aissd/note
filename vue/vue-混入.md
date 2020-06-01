1、局部混入 - 个人理解的是可以通用的配置项，可跟被混入的vue模块合并，加载速度快于被混入的vue模块

```
混入的created > 被混入的vue模块created > 混入的mounted > 被混入的vue模块mounted
```

2、