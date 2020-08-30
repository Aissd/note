```
~function(pro) {
	pro.formatTime = function(template) {
		template = template || '{0}年{1}月{2}日 {3}时{4}分{5}秒';
		var ary = this.match(/\d+/g);
		template = template.replace(/\{(\d+)\}/g, function() {
			var n = arguments[1],
				val = ary[n] || '0';
			Number(val) < 10 ? val = '0' + val : null;
			return val;
		});
		return template;
	}
}(String.prototype);

var str = '2020-8-21 07:9:1';
str.formatTime();  // "2020年08月21日 007时09分01秒"
str.formatTime('{1}月{2}日 {3}时{4}分'); // "08月21日 07时09分"
str.formatTime('{0}-{1}-{2}'); // "2020-08-21"
```

