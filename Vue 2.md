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