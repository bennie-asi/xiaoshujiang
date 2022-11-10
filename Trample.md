---
title: Trample
tags: Trample,踩坑,日志
category: /小书匠/日记/2022-09
renderNumberedHeading: true
grammar_cjkRuby: true
---
`Pillow==5.3` 模块安装失败
解决办法：python版本不匹配，卸载原装3.9版本python，重装3.7版本python

`pycrypto==2.6.1`模块安装报错：`Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/`
解决办法：windows下没有该模块依赖，从网上寻找对应依赖下载安装[visual studio C++ build tools](https://pan.baidu.com/s/1GrzxqB8zdXbN9OhSTQIqFA?pwd=xwuw)

缺少的其他模块无需安装也能运行，猜测后期用到才需要进行安装

需要安装的模块

``` txt
Django==2.1.5
yaml
uniapi
six
lxml
pymysql
kombu
celery
django-redis
bson

```


css flex布局
常用属性
flex-direction
flex-wrap
flew-flow
justify-content
align-items
align-content

使用fixed定位后，标签在循环中会只能获取到最后一个元素，原因是fixed定位脱离文档流

js中for in语法只能作用于 对象用于遍历对象属性，而不能作用于数组