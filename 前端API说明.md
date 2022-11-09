---
title: 前端框架说明
tags: Uni-app,Vue,日志
category: /小书匠/日记/2022-11
renderNumberedHeading: true
grammar_cjkRuby: true
---
# 前端框架说明
## 介绍
公司所使用的前端技术框架为uni-app，个人理解为uni-app是集成了vue与微信小程序的一些优势，包含一些uni-app特有的api，以及条件编译；所以会Vue就能很快上手uni-app；建议再了解一下SCSS[（预处理CSS）](https://blog.csdn.net/weixin_67745264/article/details/125141904)。
开发工具建议使用[HbuilderX](https://www.dcloud.io/)，并配置好所需开发者工具的路径
![enter description here](./images/1667961087545.png)
## 环境部署
使用uni-app需要你电脑上安装过Vue框架，以及根据项目需要安装对应的开发者工具（如需求开发微信小程序则安装微信开发者工具），这里给出部分开发者工具与工具的官网链接。
[微信开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)，[支付宝开发者工具](https://render.alipay.com/p/f/fd-jwq8nu2a/pages/home/index.html)，安装vue通常使用[nodejs](http://nodejs.cn/download/)来进行安装，具体安装教程可以参考[nodejs安装教程](https://blog.csdn.net/momohhhhh/article/details/126319350)，如链接失效可自行百度。
## 编码规范
编码前建议先了解已有项目编码风格、以便于不同人员之间的协同开发
变量、属性命名：
> 一般采用小驼峰命名法，复数末尾加S（根据英语复数语法），或者加list，：如name、users、commentList。
> 不得使用Vue、js或者uni-app的内置关键字或者内置变量来命名，如if、which等

class命名：

> 一般采用短横线连接命名法，命名与业务功能相关或者与样式相关，如menu-content、flex-between等
> template最外层类名一般命名为content或者wrapper，如图所示![enter description here](./images/1667959724747.png)
 
 文件命名：
> 一般根据具体业务需求来进行命名，单个单词小写，多个单词之间采用短横线连接如：choose-location.vue、login、setting等

方法命名与风格：

> 单个单词小写，多个单词采用小驼峰命名法。
> 一般将需要有输入（需要传参）的方法或者是需要改变已有数据的方法放在methods中；而将仅仅进行计算的方法放入computed中，此时要注意这个方法已经成为一个属性了，要按照使用属性的方式去使用。如图所示：
> ![enter description here](./images/1667960743553.png)

## 项目结构
![enter description here](./images/1667961230849.png)
#### **colorui**
引入的一个外部CSS库，目前官网`https://www.color-ui.com/` 已经打不开了，其中的main.css可以根据项目需要来对标签进行一些全局修改，如去掉一些默认样式。
#### **common**
![enter description here](./images/1667961888133.png)
放置一些项目通用的js、css、scss文件，其中base64.js用来对文件进行base64转码，ble.js用来对蓝牙设备进行操作。
**common.js** 是需要重点注意的文件，主要是一些uni-app的相关封装方法，一些常用方法需要注意:如$query()、$back()、$toast()、$goto()、$doing()等，具体的介绍与使用参照`前端封装方法使用`文件。
**datamonitor.js**主要用来监测用户操作数的文件，如无需求，不必过多关注。
**geo.js**提供了百度坐标（BD09）、国测局坐标（火星坐标，GCJ02）、和WGS84坐标系之间的转换。后端保存的经纬度可能需要经过转换才能在地图组件中使用。
**hardware.js**中封装了一些跟硬件操作相关的方法。
**index.js**是所有common文件夹中js的入口文件，通过index.js挂载到vue实例中。
**irIcon.css**用来放置项目中使用到的ICON图标的class，需与[阿里巴巴矢量图标库](https://www.iconfont.cn/)配合使用，具体使用参照`前端封装方法使用`文件
**lazy.js**封装了一些懒加载相关方法
**main.scss**存放着一些项目的可复用的样式，项目中重复使用的样式可抽取到该文件中。
**request.js**封装着一些向后端发起网络请求的方法，主要是$callapi、$Pager，具体使用参照`前端封装方法使用`文件
**site.js**封装着一些与站点相关的全局方法，如获取标题，获取url，获取用户信息，复制到剪贴板等方法。
**unimp.js**对uni小程序uni-mp相关功能封装
**utils.js**一些常用工具方法的封装，如格式化浮点数、格式化时间、检查银行卡号、检查手机号、检查身份证号、深拷贝等方法
**websocket.js**主要是建立websocket连接所需方法
**wxh5.js**与微信H5功能相关的方法

