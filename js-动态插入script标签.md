```
var editorJs = document.createElement("script");
editorJs.src = "./test1.js";
editorJs.async = false;
document.body.appendChild(editorJs);

var editorJs2 = document.createElement("script");
editorJs2.src = "./test2.js";
editorJs2.onload = getReadyForEditor;
editorJs2.async = false;
document.body.appendChild(editorJs2);
```

async： 该布尔属性指示浏览器是否在允许的情况下异步执行该脚本。该属性对于内联脚本无作用 (即没有**src**属性的脚本）

defer：这个布尔属性被设定用来通知浏览器该脚本将在文档完成解析后，触发 `DOMContentLoaded` 事件前执行。如果缺少 `src` 属性（即内嵌脚本），该属性不应被使用，因为这种情况下它不起作用。

参考地址：

https://mp.weixin.qq.com/s/WC1cRt_40dgZ59_UkgGF5g

https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/script