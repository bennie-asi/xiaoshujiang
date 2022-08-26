---
title: Django blog开发
tags: Django,Python,日志
category: /小书匠/日记/2022-08
renderNumberedHeading: true
grammar_cjkRuby: true
---
## 配置连接数据库
在mysql中创建blog数据库，并在项目的setting.py文件中修改配置如下
``` python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': '127.0.0.1',
        'PORT': '3306',
        'USER': 'root',
        'PASSWORD': 'root',
        'NAME': 'blog',
    }
}
```
安装驱动程序`pip install PyMySQL`，并在__init__.py文件中添加如下代码

``` python
import pymysql
pymysql.install_as_MySQLdb()
```
