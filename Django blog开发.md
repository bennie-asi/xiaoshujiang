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
配置Redis数据库，在setting.py中

``` python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/0",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    },
    "session": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    },

}
SESSION_ENGINE = "django.contrib.sessions.backends.cache"
SESSION_CACHE_ALIAS = "session"
```

## 日志配置
配置日志，在setting.py文件中添加如下代码

``` python
LOGGING = {
    "version": 1,
    "disable_existing_loggers": False,  # 是否禁用以及存在的日志器
    'formatters': {  # 日志信息显示的格式
        'verbose': {
            'format': '%(levelname)s %(asctime)s %(module)s %(lineno)d %(message)s'
        },
        'simple': {
            'format': '%(levename)s %(module)s %(lineno)d %(message)s'
        },
    },
    'filters': {  # 对日志进行过滤
        'require_debug_true': {
            '()': 'django.utils.log.RequireDebugTrue',
        },

    },
    'handlers': {  # 日志处理方法
        'console': {  # 向终端输出日志
            'level': 'INFO',
            'filters': ['require_debug_true'],
            'class': 'logging.StreamHandler',
            'formatter': 'simple'
        },
        'file': {  # 向文件中输出日志
            'level': 'INFO',
            'class': 'logging.handlers.RotatingFileHandler',
            'filename': os.path.join(BASE_DIR, 'logs/blog.log'),
            'maxBytes': 300 * 1024 * 1024,
            'backupCount': 10,
            'formatter': 'verbose'
        },
    },
    'loggers': {
        # 日志器
        'django': {
            # 定义了一个名为Django的日志器
            'handlers': ['console', 'file'],  # 可以同时向终端和文件中输出日志
            'propagate': True,  # 是否继续传递日志信息
            'level': 'INFO',  # 日志器接收的最低日志级别
        },
    }
}

```
## 日志记录器的使用
在settings.py文件中添加如下代码
``` python
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,  # 是否禁用已经存在的日志器
    'formatters': {  # 输出日志的格式
        'verbose': {
            'format': '%(levelname)s %(asctime)s %(module)s %(lineno)d %(message)s'
        },
        'simple': {
            'format': '%(levelname)s %(module)s %(lineno)d %(message)s'
        },
    },
    'filters': {  # 对日志进行过滤
        'require_debug_true': {
            '()': 'django.utils.log.RequireDebugTrue',
        },
    },
    'handlers': {  # 日志的处理方式
        'console': {  # 终端输出日志
            'level': 'INFO',  # 大于INFO级别，才输出
            'filters': ['require_debug_true'],
            'class': 'logging.StreamHandler',
            'formatter': 'simple'  # 输出简单的样式
        },
        'file': {
            'level': 'INFO',
            'class': 'logging.handlers.RotatingFileHandler',
            'filename': os.path.join(BASE_DIR, "logs/blog.log"),  # 日志文件的位置
            'maxBytes': 300 * 1024 * 1024,  # 文件最多存储 300M 的内存   日志文件满了，他会自动新建meiduo1 meiduo2
            'backupCount': 10,  # 最多十个文件
            'formatter': 'verbose'
        },
    },
    'loggers': {
        'django': {  # 定义了一个名为django的日志器
            'handlers': ['console', 'file'],  # 可以同时在终端跟文件中输出
            'propagate': True,
            'level;': 'INFO'  # 日至输出的最低级别
        },
    }
}

```
render函数会根据传入的参数来构造HttpResponse
用 {% %} 包裹起来的叫做模板标签。