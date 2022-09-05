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

## callback
机制：js是异步执行的，也就是说js代码不是一行一行按部就班的去执行的，例如：我们在请求一个网络接口时，我们不知道它什么时候请求完成，这个时候，我们要保证我们能及时获取到服务器返回的数据，我们就要用回调函数来解决。

作用：回调函数可以使请求不阻塞后面的代码，但又能保证我们及时获取到返回的数据。

触发调用：回调函数不是由函数的实现方直接调用，而是在特定的事件或条件发生时由另外的一方调用的，用于对该事件或条件进行响应

## AJAX
AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）
AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。

## Websocket

> WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。

创建WebSocket对象

``` javascript
var Socket = new WebSocket(url, [protocol] );
```
第一个参数 url, 指定连接的 URL。第二个参数 protocol 是可选的，指定了可接受的子协议


| 属性                  |                                                                                                                                                                                              |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Socket.readyState     | 只读属性 readyState 表示连接状态，可以是以下值：<br/>0 - 表示连接尚未建立。<br/>1 - 表示连接已建立，可以进行通信。<br/>2 - 表示连接正在进行关闭。<br/>3 - 表示连接已经关闭或者连接不能打开。 |
| Socket.bufferedAmount | 只读属性 bufferedAmount 已被 send() 放入正在队列中等待传输，但是还没有发出的 UTF-8 文本字节数。                                                                                              |

| 事件    | 事件处理程序     | 描述                       |
| ------- | ---------------- | -------------------------- |
| open    | Socket.onopen    | 连接建立时触发             |
| message | Socket.onmessage | 客户端接收服务端数据时触发 |
| error   | Socket.onerror   | 通信发生错误时触发         |
| close   | Socket.onclose   | 连接关闭时触发             |

| 方法          | 描述             |
| ------------- | ---------------- |
| Socket.send() | 使用连接发送数据 |
| Socket        | 关闭连接         |
