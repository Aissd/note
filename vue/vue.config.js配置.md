1、配置scss全局变量

```
  module.exports = {
    ...
    css: {
        loaderOptions: {
            sass: {
              // @是src的别名
              data: `
                @import "@/assets/variable.scss";
              `
            }
        }
    }
    ...
  }
```

