### 数据劫持思路
1、new 一个Vue实例，传入Vue的基本配置#el和data方法；
2、Vue原型上挂载一个初始化函数，用于初始化Vue的data，mixin，watch等...并把实例绑定到this；
3、initState初始化data，要判断是否存在data方法，且判断这个data是函数还是对象（vue不建议使用对象形式）；
4、对data的每个属性做数据代理；
5、对data做数据观察，判断是否是对象且不为null；
6、若data是对象，则使用Object.definedProperty劫持data的每一个属性；
7、若data是数组，则遍历data，重写数组的七个能改变原数组的方法（若有新增项，需要再对其做数据观察）；