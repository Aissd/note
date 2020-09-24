### JSON.stringify()做“深拷贝”的缺陷：

1、不能处理函数
2、不能处理正则，日期
3）不能处理undefined

### JSON.stringify(res, null, 2); // null - 保留所有属性，2 - tab两位

