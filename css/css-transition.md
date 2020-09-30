### IE10及以上才支持transition属性
### 全部属性
```
transition-property（设置过渡效果的css属性名）
transition-duration（完成动画的时间）
transition-timing-function（动画速度）
transition-delay（延迟）
```

> transition-duration默认为0，0时不产生过渡效果
```
transition-duration: 2s;
transition-duration: 200ms;
transition-duration: 200ms, 2s; // 第1个200ms，第2个2s，第3个200ms（循环）
```

> transition-property

默认为all
不需要默认值时设置为none
可以写多个属性
```
transition-property: background, width, height, border-radius;
transition-property: none;
transition-property: all;
```

> transition-timing-function默认为ease


可选值有
linear - 匀速
ease - 慢开始，变快，再变慢直至结束
ease-in - 慢速开始
ease-in-out - 慢速开始和结束
cubic-bezier(n,n,n,n) - 贝塞尔曲线（n的值是0~1之前的数值）
steps(3, start) - 步进帧动画过渡效果

```
transition-timing-function: steps(3, start); // 分3步完成，开始的时候执行
step-start === steps(1, end)
transition-timing-function: steps(3, end); // 分3步完成，开始还是初始状态
step-end
```

> transition-delay默认为0
```
transition-delay: 2s;
transition-delay: 200ms;
transition-delay: 200ms, 2s; // 第1个200ms，第2个2s，第3个200ms（循环）
```

### 组合设置
```
// 属性 过渡速度 持续时间 延迟时间
transition: all linear 2s 1s;
// 多个属性时
transition: border-radius linear 2s 0s, background ease 2s 2s; 
```

### transitionend动画的API接口
> transitionedn 事件

捕获到动画结束时的触发事件
```
document.querySelector(selector)
.addEventListener('transitionend', function(e) {}, false)
```