---
title: Vue事件修饰符
date: 2017-10-15 18:25
tags: Vue
categories: 框架
summary_img: http://p4z3kz4fz.bkt.clouddn.com/u=667735043,3872756134&fm=27&gp=0.jpg
---
## 事件修饰符：

​	在事件处理程序中调用 `event.preventDefault()` 或 `event.stopPropagation()`是非常常见的需求。尽管我们可以在methods 中轻松实现这点，但更好的方式是：methods 只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。为了解决这个问题， Vue.js 为 `v-on` 提供了 事件修饰符。通过由点(.)表示的指令后缀来调用修饰符。

<!--more-->

- `.stop`
- `.prevent`
- `.capture`
- `.self`
- `.once`

```vue
<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>
 
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>
 
<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>
 
<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
 
<!-- 添加事件侦听器时使用事件捕获模式 -->
<div v-on:click.capture="doThis">...</div>
 
<!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
<div v-on:click.self="doThat">...</div>
```

## 按键修饰符：

​	在监听键盘事件时，我们经常需要监测常见的键值。 Vue 允许为 `v-on` 在监听键盘事件时添加按键修饰符：

```vue
<!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
<input v-on:keyup.13="submit">
```

```vue
<!-- 同上 -->
<input v-on:keyup.enter="submit">
 
<!-- 缩写语法 -->
<input @keyup.enter="submit">
```

全部的按键别名：记住所有的 keyCode 比较困难，所以 Vue 为最常用的按键提供了别名：

- `.enter`
- `.tab`
- `.delete` (捕获 “删除” 和 “退格” 键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

可以通过全局 `config.keyCodes` 对象[自定义按键修饰符别名](https://cn.vuejs.org/v2/api/#keyCodes)：

```javascript
// 可以使用 v-on:keyup.f1
Vue.config.keyCodes.f1 = 112
```

同样的在v-model里面修饰符也有很多应用。