1、建一个Bus的js

```
import Vue from 'vue';
// 使用Event Bus - 解决非父子间的通信问题
const Bus = new Vue();
export default Bus;
```

2、发送方：

```
import Bus from '@/utils/Bus.js';
Bus.$emit('busname', '张三');
```

3、接收方

```
import Bus from '@/utils/Bus.js';
mounted() {
	Bus.$on('busname', val => {
		this.username = val;
	});
}
```

4、先监听（$on），后发送（$emit）