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