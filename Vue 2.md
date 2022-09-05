---
title: Vue 2
tags: Vue,Python,日志
category: /小书匠/日记/2022-09
renderNumberedHeading: true
grammar_cjkRuby: true
---
## 模板语法
{{ ... }}

v-html：输出HTML代码

v-bind：HTML属性值使用v-bind指令

指令：是带有v-前缀的特殊属性

修饰符：修饰符是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。

v-model：用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。

过滤器：Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。由"管道符"指示

v-bind 缩写

``` html
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```
v-on 缩写

``` html
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```

## 条件语句
 1. v-if
 2. v-else
 3. v-else-if
 4. v-show
 tips：**v-if与v-show的区别**，v-if是直接操作DOM元素来控制元素的展示，v-show通过控制元素属性display来控制元素是否显示
 
 ## 计算属性
 computed
 **computed与methods的区别**：computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数总会重新调用执行。
 
 computed 属性默认只有 getter ，不过在需要时你也可以提供一个 setter ：
 

``` js
var vm = new Vue({
  el: '#app',
  data: {
    name: 'Google',
    url: 'http://www.google.com'
  },
  computed: {
    site: {
      // getter
      get: function () {
        return this.name + ' ' + this.url
      },
      // setter
      set: function (newValue) {
        var names = newValue.split(' ')
        this.name = names[0]
        this.url = names[names.length - 1]
      }
    }
  }
})
// 调用 setter， vm.name 和 vm.url 也会被对应更新
vm.site = '菜鸟教程 http://www.runoob.com';
document.write('name: ' + vm.name);
document.write('<br>');
document.write('url: ' + vm.url);
```
## 监听属性
watch

## 组件
prop ：子组件用来接受父组件传递过来的数据的一个自定义属性。
父组件的数据需要通过 props 把数据传给子组件，子组件需要显式地用 props 选项声明 "prop"：

``` html
<div id="app">
    <child message="hello!"></child>
</div>
 
<script>
// 注册
Vue.component('child', {
  // 声明 props
  props: ['message'],
  // 同样也可以在 vm 实例中像 "this.message" 这样使用
  template: '<span>{{ message }}</span>'
})
// 创建根实例
new Vue({
  el: '#app'
})
</script>
```
