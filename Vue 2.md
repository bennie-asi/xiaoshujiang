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

v-model：用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。(调用的是set和get函数)

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
watch在监听的时候，可以有两次参数，第一次参数为更新的数据，第二个参数为之前的旧数据
``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>
<script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>
</head>
<body>
<div id = "app">
    <p style = "font-size:25px;">计数器: {{ counter }}</p>
    <button @click = "counter++" style = "font-size:25px;">点我</button>
</div>
<script type = "text/javascript">
var vm = new Vue({
    el: '#app',
    data: {
        counter: 1
    }
});
vm.$watch('counter', function(nval, oval) {
    alert('计数器值的变化 :' + oval + ' 变为 ' + nval + '!');
});
setTimeout(
    function(){
        vm.counter += 20;
    },10000
);
</script>
</body>
</html>
```
Tips:如果监听的数据为一个对象（类似于引用/指针）的时候，需要开启深度监控`deep:true`
，因为在我们没有开启深度监控的时候，watch只会监听第一层，而对象的数据修改了，但对象它的首地址没有修改，所以watch判定它没有发生数据的变化，从而监听不到

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
emit:用于子组件向父组件传递数据的方法。

### 事件修饰符
**prevent：阻止默认事件（常用）**

``` html
   <!-- 阻止默认事件（常用） -->
    <a href="http://www.atguigu.com" @click.prevent="showInfo">点我提示信息</a>
```
a标签的默认有跳转到href的行为，我们把默认行为禁用后，就不会跳转页面
**stop：阻止事件冒泡（常用）**

``` html
      <!-- 阻止事件冒泡（常用） -->
        <div class="demo1" @click="showInfo">
            <button @click.stop="showInfo">点我提示信息</button>
            <!-- 修饰符可以连续写 -->
             <a href="http://www.atguigu.com" @click.prevent.stop="showInfo">点我提示信息</a> 
        </div>
```
**once：事件只触发一次（常用）**

``` html
      <!-- 事件只触发一次（常用） -->
        <button @click.once="showInfo">点我提示信息</button>
```
**capture：使用事件的捕获模式**

``` html
  <!-- 使用事件的捕获模式 -->
        <div class="box1" @click.capture="showMsg(1)">
            div1
            <div class="box2" @click="showMsg(2)">
                div2
            </div>
        </div>
```
**self：只有event.target是当前操作的元素时才触发事件**

``` html
  <!-- 只有event.target是当前操作的元素时才触发事件； -->
        <div class="demo1" @click.self="showInfo">
            <button @click="showInfo">点我提示信息</button>
        </div>
```

v-model:一般用在表达输入，很轻松的实现表单控件和数据的双向绑定
v-html：更新元素的innerHTML
v-show与v-if：条件渲染，注意二者区别
v-on:click:可以简写为@click,@绑定一个事件。如果事件触发了，就可以指定事件的处理函数
v-for：基于源数据多次渲染元素或模板
v-bind:当表达式的值改变时，将其产生的连带影响，响应式地作用于DOM语法，dom属性节点与data数据绑定响应
v-bind:title=”msg”简写：title="msg"

--------------------------------------------------------
绑定class的数组用法
1.对象方法v-bind:class="{'orange':isRipe, 'green':isNotRipe}”
2.数组方法v-bind:class="【class1,class2】"
3.行内v-bind:style="{color:color,fontSize:fontSize+'px'}”

--------------------------------------------------------
路由跳转方式
1.router-link标签会渲染为标签，咋填template中的跳转都是这种；
2.另一种是编辑是导航，也就是通过js跳转比如router.push('/home')

**在Vue2中新增属性进行拦截**
==Vue.set(Object,property,value) #F44336==


## Vue.js Ajax(axios)
创建请求时可用的配置选项，注意只有 url 是必需的。如果没有指定 method，请求将默认使用 get 方法。

``` js
{
  // `url` 是用于请求的服务器 URL
  url: "/user",

  // `method` 是创建请求时使用的方法
  method: "get", // 默认是 get

  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: "https://some-domain.com/api/",

  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 只能用在 "PUT", "POST" 和 "PATCH" 这几个请求方法
  // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
  transformRequest: [function (data) {
    // 对 data 进行任意转换处理

    return data;
  }],

  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对 data 进行任意转换处理

    return data;
  }],

  // `headers` 是即将被发送的自定义请求头
  headers: {"X-Requested-With": "XMLHttpRequest"},

  // `params` 是即将与请求一起发送的 URL 参数
  // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
  params: {
    ID: 12345
  },

  // `paramsSerializer` 是一个负责 `params` 序列化的函数
  // (e.g. https://www.npmjs.com/package/qs, https://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: "brackets"})
  },

  // `data` 是作为请求主体被发送的数据
  // 只适用于这些请求方法 "PUT", "POST", 和 "PATCH"
  // 在没有设置 `transformRequest` 时，必须是以下类型之一：
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属：FormData, File, Blob
  // - Node 专属： Stream
  data: {
    firstName: "Fred"
  },

  // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
  // 如果请求花费了超过 `timeout` 的时间，请求将被中断
  timeout: 1000,

  // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // 默认的

  // `adapter` 允许自定义处理请求，以使测试更轻松
  // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
  adapter: function (config) {
    /* ... */
  },

  // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
  // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
  auth: {
    username: "janedoe",
    password: "s00pers3cret"
  },

  // `responseType` 表示服务器响应的数据类型，可以是 "arraybuffer", "blob", "document", "json", "text", "stream"
  responseType: "json", // 默认的

  // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: "XSRF-TOKEN", // default

  // `xsrfHeaderName` 是承载 xsrf token 的值的 HTTP 头的名称
  xsrfHeaderName: "X-XSRF-TOKEN", // 默认的

  // `onUploadProgress` 允许为上传处理进度事件
  onUploadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  onDownloadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

  // `maxContentLength` 定义允许的响应内容的最大尺寸
  maxContentLength: 2000,

  // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
  validateStatus: function (status) {
    return status &gt;= 200 &amp;&amp; status &lt; 300; // 默认的
  },

  // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
  // 如果设置为0，将不会 follow 任何重定向
  maxRedirects: 5, // 默认的

  // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
  // `keepAlive` 默认没有启用
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // "proxy" 定义代理服务器的主机名称和端口
  // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
  // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
  proxy: {
    host: "127.0.0.1",
    port: 9000,
    auth: : {
      username: "mikeymike",
      password: "rapunz3l"
    }
  },

  // `cancelToken` 指定用于取消请求的 cancel token
  // （查看后面的 Cancellation 这节了解更多）
  cancelToken: new CancelToken(function (cancel) {
  })
}
```
响应结构

``` js
{
  // `data` 由服务器提供的响应
  data: {},

  // `status`  HTTP 状态码
  status: 200,

  // `statusText` 来自服务器响应的 HTTP 状态信息
  statusText: "OK",

  // `headers` 服务器响应的头
  headers: {},

  // `config` 是为请求提供的配置信息
  config: {}
}
```
全局axios默认值

``` js
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```
自定义实例默认值：

``` js
// 创建实例时设置配置的默认值
var instance = axios.create({
  baseURL: 'https://api.example.com'
});

// 在实例已创建后修改默认值
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
```
拦截器
在请求或响应被 then 或 catch 处理前拦截它们。

``` js
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```
如果你想在稍后移除拦截器，可以这样：

``` js
var myInterceptor = axios.interceptors.request.use(function () {/*...*/});
axios.interceptors.request.eject(myInterceptor);
```
可以为自定义 axios 实例添加拦截器。

``` js
var instance = axios.create();
instance.interceptors.request.use(function () {/*...*/});
```
错误处理

``` js
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // 请求已发出，但服务器响应的状态码不在 2xx 范围内
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else {
      // Something happened in setting up the request that triggered an Error
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
```
可以使用 validateStatus 配置选项定义一个自定义 HTTP 状态码的错误范围。

``` js
axios.get('/user/12345', {
  validateStatus: function (status) {
    return status < 500; // 状态码在大于或等于500时才会 reject
  }
})
```

## Vue.js Ajax(vue-resource)
用于异步加载


Vue中install方法
vue提供install可供我们开发新的插件及全局注册组件等
install方法第一个参数是vue的构造器，第二个参数是可选的选项对象

``` js
export default {
	install(Vue,option){
		组件
		指令
		混入
		挂载vue原型
	}
}
```
全局注册组件

``` javascript
import PageTools from '@/components/PageTools/pageTools.vue'
import update from './update/index.vue'
import ImageUpload from './ImageUpload/ImageUpload.vue'
import ScreenFull from './ScreenFull'
import ThemePicker from './ThemePicker'
import TagsView from './TagsView'
export default {
  install(Vue) {
    Vue.component('PageTools', PageTools)
    Vue.component('update', update)
    Vue.component('ImageUpload', ImageUpload)
    Vue.component('ScreenFull', ScreenFull)
    Vue.component('ThemePicker', ThemePicker)
    Vue.component('TagsView', TagsView)
  }
}
```
在main.js中直接用引用并Vue.use进行注册

``` javascript
import Component from '@/components'
Vue.use(Component)
```
全局自定义指令

``` js
export default{
	install(Vue){
		Vue.directive('pre',{
			inserted(button,bind){
				button.addEventListener('click',()=>{
					if(!button.disabled){
						button.disabled = true;
						setTimeout(()=>{
							button.disabled = false
						},1000)
					}
				})
			}
		})
	}
}
```
在main.js跟注册组件一样

``` js
import pre from '@/aiqi'

Vue.use(pre)

```

process.env 是VUE用于配置开发环境变量

## 自定义组件

``` html
1.第一步：在页面中引入子组件,(假设在components文件下有一个myHeader.vue组件)
import myHeader from '@/components/myHeader.vue'
2.第二步：注册子组件
components:{
	myHeader
}
3.第三步：作为标签使用
<myHeader />
或者
<myHeader></myHeader>

```

对于CSS可以添加scope来避免样式污染全局样式

`<view></view>`标签相当于h5中的`<span></span>`标签，无法直接设置宽高，需要设置属性`display=inline-block`后可设置宽高属性

v-show 在使用自定义组件时可能存在不生效问题，初判是由于组件内部已经使用了display属性，优先级比v-show更高，导致的不生效