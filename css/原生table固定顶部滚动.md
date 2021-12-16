地址：
https://www.cnblogs.com/jamsbwo/p/5829550.html

```
<style>
    table tbody {
        display:block;
        height:195px;
        overflow-y:scroll;
    }
    table thead, tbody tr {
        display:table;
        width:100%;
        table-layout:fixed;
    }
    table thead { width: calc( 100% - 1em ) }
    table thead th{ background:#ccc;}
</style>
<body>
    <table width="80%" border="1">
    <thead>
      <tr>
        <th>姓名</th>
        <th>年龄</th>
        <th>出生年月</th>
        <th>手机号码</th>
        <th>单位</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>张三</td>
        <td>18</td>
        <td>1990-9-9</td>
        <td>13682299090</td>
        <td>阿里巴巴</td>
      </tr>
    </tbody>
</body>
```