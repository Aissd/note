##### 生命周期

完整支持vue实例的生命周期，同时还新增了应用生命周期和页面生命周期

##### 模板语法

完整支持vue的模板语法

##### data属性

```
//正确用法，使用函数返回对象
data() {
    return {
        title: 'Hello'
    }
}
```


> 由于小程序端不支持更新属性值为 undefined，框架内部将替换 undefined 为 null，此时可能出现预期之外的情况，需要自行判断一下

##### class和style绑定

class支持的语法
```
<view :class="{ active: isActive }">111</view>
<view class="static" v-bind:class="{ active: isActive, 'text-danger': hasError }">222</view>
<view class="static" :class="[activeClass, errorClass]">333</view>
<view class="static" v-bind:class="[isActive ? activeClass : '', errorClass]">444</view>
<view class="static" v-bind:class="[{ active: isActive }, errorClass]">555</view>
```

style支持的语法
```
<view v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">666</view>
<view v-bind:style="[{ color: activeColor, fontSize: fontSize + 'px' }]">777</view>
```

**以:style=""这样方式设置px像素，其值为实际像素，不会被编译器转换**

此外，还支持computed方法生成的class或者style字符串插入到页面中
```
<template>
    <!-- 支持 -->
    <view class="container" :class="computedClassStr"></view>
    <view class="container" :class="{active: isActive}"></view>

    <!-- 不支持 -->
    <view class="container" :class="computedClassObject"></view>
</template>
<script>
    export default {
        data () {
            return {
                isActive: true
            }
        },
        computed: {
            computedClassStr () {
                return this.isActive ? 'active' : ''
            },
            computedClassObject () {
                return { active: this.isActive }
            }
        }
    }
</script>
```