---
title: JavaScript
tags: Django,Python,日志
category: /小书匠/日记/2022-09
renderNumberedHeading: true
grammar_cjkRuby: true
---
## Promise
构造函数，本身有all、reject、resolve方法，原型有then、catch等方法

Promise主要是用于链式回调、解决回调地狱问题

> 回调地狱：回调函数里面嵌套回调函数。

Promise的all方法提供了并行执行异步操作的能力，并且在所有异步操作执行完后才执行回调。

### resolve
异步操作执行成功后的回调函数

### reject
一般u操作执行失败后的回调函数

### catch
在执行resolve的回调（也就是上面then中的第一个参数）时，如果抛出异常了（代码出错了），那么并不会报错卡死js，而是会进到这个catch方法中

### all
谁跑的慢，以谁为准执行回调。all接收一个数组参数，里面的值最终都算返回Promise对象

### race
谁跑的快，以谁为准执行回调

### then
用于链式调用