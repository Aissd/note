```
// 解析url中的参数
const parseQuery = (url) => {
	q = {};
	url.replace(
		/([^?&=]+)=([^&]+)/g,
		(_, k, v) => (q[k] = v)
	);
	return q;
};
// { a: 1, b: 2 }
```