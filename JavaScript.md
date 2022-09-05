---
title: JavaScrip
tags: JavaScript,ES6,日志
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

## ES6
![enter description here](https://www.runoob.com/wp-content/uploads/2018/12/es6-tutorial.jpg)
ECMAScript 6

> 变量提升：JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行的运行，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）

###  let、const 和 block 作用域
let 允许创建块级作用域，ES6 推荐在函数中使用 let 定义变量，而非 var：

``` javascript
var a = 2;
{
  let a = 3;
  console.log(a); // 3
}
console.log(a); // 2
```

同样在块级作用域有效的另一个变量声明方式是 const，它可以声明一个常量。ES6 中，const 声明的常量类似于指针，它指向某个引用，也就是说这个「常量」并非一成不变的，如：

``` javascript
{
  const ARR = [5,6];
  ARR.push(7);
  console.log(ARR); // [5,6,7]
  ARR = 10; // TypeError
}
```
 - let 关键词声明的变量不具备变量提升（hoisting）特性
 - let 和 const 声明只在最靠近的一个块中（花括号内）有效
 - 当使用常量 const 声明时，请使用大写变量，如：CAPITAL_CASING
 - const 在声明时必须被赋值

### 箭头函数（Arrow Functions）
ES6 中，箭头函数就是函数的一种简写形式，使用括号包裹参数，跟随一个 =>，紧接着是函数体：

``` javascript
var getPrice = function() {
  return 4.55;
};
 
// Implementation with Arrow Function
var getPrice = () => 4.55;
```

需要注意的是，上面例子中的 getPrice 箭头函数采用了简洁函数体，它不需要 return 语句，下面这个例子使用的是正常函数体：

``` javascript
let arr = ['apple', 'banana', 'orange'];
 
let breakfast = arr.map(fruit => {
  return fruit + 's';
});
 
console.log(breakfast); // apples bananas oranges
```
箭头函数不仅仅是让代码变得简洁，函数中 this 总是绑定总是指向对象自身。具体可以看看下面几个例子：

``` javascript
function Person() {
  this.age = 0;
 
  setInterval(function growUp() {
    // 在非严格模式下，growUp() 函数的 this 指向 window 对象
    this.age++;
  }, 1000);
}
var person = new Person();
```
我们经常需要使用一个变量来保存 this，然后在 growUp 函数中引用：

``` javascript
function Person() {
  var self = this;
  self.age = 0;
 
  setInterval(function growUp() {
    self.age++;
  }, 1000);
}
```
使用箭头函数可以省却这个麻烦

``` javascript
function Person(){
  this.age = 0;
 
  setInterval(() => {
    // |this| 指向 person 对象
    this.age++;
  }, 1000);
}
 
var person = new Person();
```
### 函数参数默认值
ES6 中允许你对函数参数设置默认值：

``` javascript
let getFinalPrice = (price, tax=0.7) => price + price * tax;
getFinalPrice(500); // 850
```
### Spread / Rest 操作符
Spread / Rest 操作符指的是 ...，具体是 Spread 还是 Rest 需要看上下文语境。
当被用于迭代器中时，它是一个 Spread 操作符(参数为数组)：

``` javascript
function foo(x,y,z) {
  console.log(x,y,z);
}
let arr = [1,2,3];
foo(...arr); // 1 2 3
```
当被用于函数传参时，是一个 Rest 操作符（参数转化为数组）：

``` javascript
function foo(...args) {
  console.log(args);
}
foo( 1, 2, 3, 4, 5); // [1, 2, 3, 4, 5]
```
### 对象此法扩展
ES6 允许声明在对象字面量时使用简写语法，来初始化属性变量和函数的定义方法，并且允许在对象属性中进行计算操作：

``` javascript
function getCar(make, model, value) {
  return {
    // 简写变量
    make,  // 等同于 make: make
    model, // 等同于 model: model
    value, // 等同于 value: value
 
    // 属性可以使用表达式计算值
    ['make' + make]: true,
 
    // 忽略 `function` 关键词简写对象函数
    depreciate() {
      this.value -= 2500;
    }
  };
}
 
let car = getCar('Barret', 'Lee', 40000);
 
// output: {
//     make: 'Barret',
//     model:'Lee',
//     value: 40000,
//     makeBarret: true,
//     depreciate: [Function: depreciate]
// }
```
### 二进制和八进制字面量
ES6 支持二进制和八进制的字面量，通过在数字前面添加 0o 或者0O 即可将其转换为八进制值：

``` javascript
let oValue = 0o10;
console.log(oValue); // 8
 
let bValue = 0b10; // 二进制使用 `0b` 或者 `0B`
console.log(bValue); // 2
```
###  对象和数组解构
解构可以避免在对象赋值时产生中间变量

``` javascript
function foo() {
  return [1,2,3];
}
let arr = foo(); // [1,2,3]
 
let [a, b, c] = foo();
console.log(a, b, c); // 1 2 3
 
function bar() {
  return {
    x: 4,
    y: 5,
    z: 6
  };
}
let {x: x, y: y, z: z} = bar();
console.log(x, y, z); // 4 5 6
```
### 对象超类
ES6 允许在对象中使用 super 方法

``` javascript
var parent = {
  foo() {
    console.log("Hello from the Parent");
  }
}
 
var child = {
  foo() {
    super.foo();
    console.log("Hello from the Child");
  }
}
 
Object.setPrototypeOf(child, parent);
child.foo(); // Hello from the Parent
             // Hello from the Child
```
### 模板语法和分隔符
 - ${ ... } 用来渲染一个变量】
 - ` 作为分隔符

``` javascript
let user = 'Barret';
console.log(`Hi ${user}!`); // Hi Barret!
```
###  for...of VS for...in
for...of 用于遍历一个迭代器，如数组：

``` js
let nicknames = ['di', 'boo', 'punkeye'];
nicknames.size = 3;
for (let nickname of nicknames) {
  console.log(nickname);
}
// 结果: di, boo, punkeye
```
for...in 用来遍历对象中的属性：

``` js
let nicknames = ['di', 'boo', 'punkeye'];
nicknames.size = 3;
for (let nickname in nicknames) {
  console.log(nickname);
}
Result: 0, 1, 2, size
```
### Map 和 WeakMap
ES6 中两种新的数据结构集：Map 和 WeakMap。事实上每个对象都可以看作是一个 Map。
一个对象由多个 key-val 对构成，在 Map 中，任何类型都可以作为对象的 key，如：

``` js
var myMap = new Map();
 
var keyString = "a string",
    keyObj = {},
    keyFunc = function () {};
 
// 设置值
myMap.set(keyString, "value 与 'a string' 关联");
myMap.set(keyObj, "value 与 keyObj 关联");
myMap.set(keyFunc, "value 与 keyFunc 关联");
 
myMap.size; // 3
 
// 获取值
myMap.get(keyString);    // "value 与 'a string' 关联"
myMap.get(keyObj);       // "value 与 keyObj 关联"
myMap.get(keyFunc);      // "value 与 keyFunc 关联"
```

> **弱引用**
> 在计算机程序中，弱引用与强引用相对，是指不能确保其引用的对象不会被垃圾回收器回收的引用。一个对象若只被弱引用所引用，则被认为是不可访问的（或弱访问的），并因此可能在任何时刻被回收

WeakMap 就是一个 Map，只不过它的所有 key 都是弱引用，意思就是 WeakMap 中的东西垃圾回收时不考虑，使用它不用担心内存泄漏问题。
另一个需要注意的点是，WeakMap 的所有 key 必须是对象。它只有四个方法 delete(key),has(key),get(key) 和set(key, val)：

``` js
let w = new WeakMap();
w.set('a', 'b'); 
// Uncaught TypeError: Invalid value used as weak map key
 
var o1 = {},
    o2 = function(){},
    o3 = window;
 
w.set(o1, 37);
w.set(o2, "azerty");
w.set(o3, undefined);
 
w.get(o3); // undefined, because that is the set value
 
w.has(o1); // true
w.delete(o1);
w.has(o1); // false
```
### Set和WeakSet
Set 对象是一组不重复的值，重复的值将被忽略，类似于python中的集合set，值类型可以是原始类型和引用类型：

``` js
let mySet = new Set([1, 1, 2, 2, 3, 3]);
mySet.size; // 3
mySet.has(1); // true
mySet.add('strings');
mySet.add({ a: 1, b:2 });
```
可以通过 forEach 和 for...of 来遍历 Set 对象：

``` js
mySet.forEach((item) => {
  console.log(item);
    // 1
    // 2
    // 3
    // 'strings'
    // Object { a: 1, b: 2 }
});
 
for (let value of mySet) {
  console.log(value);
    // 1
    // 2
    // 3
    // 'strings'
    // Object { a: 1, b: 2 }
}
```
Set 同样有 delete() 和 clear() 方法。
### WeakSet
类似于 WeakMap，WeakSet 对象可以让你在一个集合中保存对象的弱引用，在 WeakSet 中的对象只允许出现一次：

``` js
var ws = new WeakSet();
var obj = {};
var foo = {};
 
ws.add(window);
ws.add(obj);
 
ws.has(window); // true
ws.has(foo);    // false, foo 没有添加成功
 
ws.delete(window); // 从结合中删除 window 对象
ws.has(window);    // false, window 对象已经被删除
```
### 类class
ES6 中有 class 语法。值得注意是，这里的 class 不是新的对象继承模型，它只是原型链的语法糖表现形式。
函数中使用 static 关键词定义构造函数的的方法和属性：

``` javascript
class Task {
  constructor() {
    console.log("task instantiated!");
  }
 
  showId() {
    console.log(23);
  }
 
  static loadAll() {
    console.log("Loading all tasks..");
  }
}
 
console.log(typeof Task); // function
let task = new Task(); // "task instantiated!"
task.showId(); // 23
Task.loadAll(); // "Loading all tasks.."
```
类中的继承和超集：

``` javascript
class Car {
  constructor() {
    console.log("Creating a new car");
  }
}
 
class Porsche extends Car {
  constructor() {
    super();
    console.log("Creating Porsche");
  }
}
 
let c = new Porsche();
// Creating a new car
// Creating Porsche
```
extends 允许一个子类继承父类，需要注意的是，子类的constructor 函数中需要执行 super() 函数。

当然，你也可以在子类方法中调用父类的方法，如super.parentMethodName()。

### Symbol
Symbol 是一种新的数据类型，它的值是唯一的，不可变的。ES6 中提出 symbol 的目的是为了生成一个唯一的标识符，不过你访问不到这个标识符：

``` js
var sym = Symbol( "some optional description" );
console.log(typeof sym); // symbol
```
如果要获取对象 symbol 属性，需要使用Object.getOwnPropertySymbols(o)。

### 迭代器（Iterators）
迭代器允许每次访问数据集合的一个元素，当指针指向数据集合最后一个元素时，迭代器便会退出。它提供了 next() 函数来遍历一个序列，这个方法返回一个包含 done 和 value 属性的对象。

ES6 中可以通过 Symbol.iterator 给对象设置默认的遍历器，无论什么时候对象需要被遍历，执行它的 @@iterator 方法便可以返回一个用于获取值的迭代器。

``` js
var arr = [11,12,13];
var itr = arr[Symbol.iterator]();
 
itr.next(); // { value: 11, done: false }
itr.next(); // { value: 12, done: false }
itr.next(); // { value: 13, done: false }
 
itr.next(); // { value: undefined, done: true }
```
可以通过 `[Symbol.iterator]()` 自定义一个对象的迭代器。
### Generators
Generator 函数是 ES6 的新特性，它允许一个函数返回的可遍历对象生成多个值。
在使用中你会看到 * 语法和一个新的关键词 yield:

``` js
function *infiniteNumbers() {
  var n = 1;
  while (true){
    yield n++;
  }
}
 
var numbers = infiniteNumbers(); // returns an iterable object
 
numbers.next(); // { value: 1, done: false }
numbers.next(); // { value: 2, done: false }
numbers.next(); // { value: 3, done: false }
```
每次执行 yield 时，返回的值变为迭代器的下一个值。
### Promises
ES6 对 Promise 有了原生的支持，一个 Promise 是一个等待被异步执行的对象，当它执行完成后，其状态会变成 resolved 或者rejected。

``` js
var p = new Promise(function(resolve, reject) {  
  if (/* condition */) {
    // fulfilled successfully
    resolve(/* value */);  
  } else {
    // error, rejected
    reject(/* reason */);  
  }
});
```
每一个 Promise 都有一个 .then 方法，这个方法接受两个参数，第一个是处理 resolved 状态的回调，一个是处理 rejected 状态的回调（详见promises部分）：

``` js
p.then((val) => console.log("Promise Resolved", val),
       (err) => console.log("Promise Rejected", err));
```

## async、await
async：用于申明一个函数是异步的
await：用于等待一个异步方法执行完成
   
> await 等到了它要等的东西，一个 Promise 对象，或者其它值，然后呢？我不得不先说，await 是个运算符，用于组成表达式，await 表达式的运算结果取决于它等的东西。
如果它等到的不是一个 Promise 对象，那 await 表达式的运算结果就是它等到的东西。
如果它等到的是一个 Promise 对象，await 就忙起来了，它会阻塞后面的代码，等着 Promise 对象 resolve，然后得到 resolve 的值，作为 await 表达式的运算结果。
其实这就是 await 必须用在 async 函数中的原因。async 函数调用不会造成阻塞，它内部所有的阻塞都被封装在一个 Promise 对象中异步执行。

