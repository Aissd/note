vue提供四个事件api
- $on
- $once
- $emit
- $off

初始化事件
```
export function initEvents(vm: Component) {
	vm._events = Object.create(null); // 创建一个空对象存放事件
	vm._hasHookEvent = false; // 是否存在事件的钩子，在lifecycle.ts的声明周期判断存在则发送事件
	const listeners = vm.$options._parentListeners;
	if (listeners) {
		updateComponentListeners(vm, listeners);
	}
}
```
```
Vue.prototype.$on = function(event: string | Array<string>, fn: Function):Component {
    const vm: Component = this;
    if (isArray(event)) {
      for (let i = 0, l = event.length; i < l; i++) {
        vm.$on(event[i], fn); // 数组时，则递归$on，为每一个event成员绑定fn方法
      }
    } else {
      ;(vm._events[event] || (vm._events[event] = [])).push(fn);
      // optimize hook:event cost by using a boolean flag marked at registration
      // instead of a hash lookup
      if (hookRE.test(event)) {
        vm._hasHookEvent = true; 
        /**
        * 是否使用这种方式绑定钩子 
        * <child  @hook:created="hookFromParent" >
        * 【表示的是父组件有没有直接绑定钩子函数在当前组件上】
        */ 
      }
    }
    return vm;
}
```

```
Vue.prototype.$once = function (event: string, fn: Function): Component {
  const vm: Component = this;
  function on () {
  	/*在第一次执行的时候将该事件销毁*/
  	vm.$off(event, on);
  	/*执行注册的方法*/
  	fn.apply(vm, arguments);
  }
  on.fn = fn;
  vm.$on(event, on);
  return vm;
}
```

```
  Vue.prototype.$off = function (event?: string | Array<string>, fn?: Function): Component {
    const vm: Component = this
    // all
    /* 如果不传参数则注销所有事件 */
    if (!arguments.length) {
      vm._events = Object.create(null)
      return vm
    }
    // array of events
    /* 如果event是数组则递归注销事件 */
    if (isArray(event)) {
      for (let i = 0, l = event.length; i < l; i++) {
        vm.$off(event[i], fn)
      }
      return vm
    }
    // specific event
    const cbs = vm._events[event!]
    if (!cbs) {
	    /* 本身不存在该事件则直接返回 */
      return vm
    }
    if (!fn) {
      vm._events[event!] = null
      return vm
    }
    // specific handler
    /* 遍历寻找对应方法并删除 */
    let cb
    let i = cbs.length
    while (i--) {
      cb = cbs[i]
      if (cb === fn || cb.fn === fn) {
        cbs.splice(i, 1)
        break
      }
    }
    return vm
  }
```
```
Vue.prototype.$emit = function (event: string): Component {
	const vm: Component = this;
	if (__DEV__) {
	  const lowerCaseEvent = event.toLowerCase();
	  if (lowerCaseEvent !== event && vm._events[lowerCaseEvent]) {
		tip(
		  `Event "${lowerCaseEvent}" is emitted in component ` +
			`${formatComponentName(
			  vm
			)} but the handler is registered for "${event}". ` +
			`Note that HTML attributes are case-insensitive and you cannot use ` +
			`v-on to listen to camelCase events when using in-DOM templates. ` +
			`You should probably use "${hyphenate(
			  event
			)}" instead of "${event}".`
		)
	  }
	}
	let cbs = vm._events[event];
	if (cbs) {
	  /* 将类数组的对象转换成数组 */
	  cbs = cbs.length > 1 ? toArray(cbs) : cbs;
	  const args = toArray(arguments, 1);
	  const info = `event handler for "${event}"`;
	  for (let i = 0, l = cbs.length; i < l; i++) {
		invokeWithErrorHandling(cbs[i], vm, args, vm, info);
	  }
	}
	return vm
}
```