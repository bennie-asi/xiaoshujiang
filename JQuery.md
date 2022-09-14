---
title: JQuery
tags: JQuery,Python,日志
category: /小书匠/日记/2022-09
renderNumberedHeading: true
grammar_cjkRuby: true
---
## 语法
基础语法： $(selector).action()

- 美元符号定义 jQuery
- 选择符（selector）"查询"和"查找" HTML 元素
- jQuery 的 action() 执行对元素的操作
- 实例:
- $(this).hide() - 隐藏当前元素
- $("p").hide() - 隐藏所有 `<p>` 元素
- $("p.test").hide() - 隐藏所有 class="test" 的 `<p>` 元素
- $("#test").hide() - 隐藏 id="test" 的元素

## 选择器
**元素选择器**
在页面中选取所有 `<p>` 元素:
``` javascript
$("p")
```
**#id 选择器**
通过 id 选取元素语法如下：

``` js
$("#test")
```
**.class 选择器**
jQuery 类选择器可以通过指定的 class 查找元素。

语法如下：

``` js
$(".test")
```
**更多实例**

| 语法                     | 描述                                                       |
| ------------------------ | ---------------------------------------------------------- |
| $("*")                   | 选取所有元素                                               |
| $(this)                  | 选取当前 HTML 元素                                         |
| $("p.intro")             | 选取 class 为 intro 的`<p>` 元素                           |
| $("p:first")             | 选取第一个 `<p>` 元素                                      |
| $("ul li:first")         | 选取第一个 `<ul>` 元素的第一个 `<li>` 元素                 |
| $("ul li:first-child")   | 选取每个 `<ul> `元素的第一个 `<li> `元素                   |
| $("[href]")              | 选取带有 href 属性的元素                                   |
| $("a[target='_blank']")  | 选取所有 target 属性值等于 "_blank" 的` <a>` 元素          |
| $("a[target!='_blank']") | 选取所有 target 属性值不等于 "_blank" 的` <a> `元素        |
| $(":button")             | 选取所有 type="button" 的` <input>`元素 和` <button>` 元素 |
| $("tr:even")             | 选取偶数位置的 <tr> 元素                                   |
| $("tr:odd")              | 选取奇数位置的 <tr> 元素                                   |
