http://houdunren.gitee.io/note/css/12%20%E5%8F%98%E5%BD%A2%E5%8A%A8%E7%94%BB.html#%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86



1、行内元素不产生变形效果，将其转为inline-block和block以及弹性元素时都可以产生变化效果；

```
<style>
    span {
        display: inline-block; /* 去掉就无效了 */
        transition: 2s;
        transform: translateX(100px) translateX(50px);
        width: 100px;
        height: 100px;
        background: #9b59b6;
    }

    span:hover {
        transition: 2s;
        transform: translateX(100px);
    }
</style>

<span>hdcms</span>
```

