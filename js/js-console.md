1、打印数组

```
console.table(['a', 'b']); // 打印出一个表格，第一列是索引，第二列是值
```

2、打印错误信息

```
console.error('打印错误信息);
```

3、打印警告信息

```
console.warn('打印警告信息');
```

4、测试程序执行的时间

```
console.time('A');
for(let i = 0; i < 1000000; i++) {}
console.timeEnd('A'); // A:6.9848484848484ms
```

5、打印原型

```
console.dir()
```

6、console.profile() - 火狐浏览器安装firebug后可用，可更精准的获取到程序每一个步骤所消耗的时间

```

```

