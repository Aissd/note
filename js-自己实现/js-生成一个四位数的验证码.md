```
function queryCode() {
	// 1、准备验证码获取的范围（索引：0~61）
	var codeArea = 'qwertyuiopasdfghjklzxcvbnm' +
		'QWERTYUIOPASDFGHJKLZXCVBNM' +
		'1234567890';
	// 2、需要准备四个索引，即可在codeArea中通过chartAt方法获取到四个字符，把把四个字符串拼接成一个字符串就是验证码
	for(var i = 0; i < 4; i++) {
		var n = Math.round(Math.random() * 61), // * (61 - 0) + 0
        	char = codeArea.charAt(n);
        result += char;
	}
	return result;
}

// 开始加载页面（和点击link）需要生成一个验证码
codeBox.innerHTML = queryCode();
link.onclick = function() {
	codeBox.innerHTML = queryCode();
}

生成不重复的验证码，用以下循环替换上面的for循环
while(result.length < 4) {
	var n = Math.round(Math.random() * 61),
    	char = codeArea.charAt(n);
    if(result.indexOf(char) === -1) {
        result += char;
    }
}

```

