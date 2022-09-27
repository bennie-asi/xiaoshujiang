---
title: Django
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
## tips
render函数会根据传入的参数来构造HttpResponse
用 {% %} 包裹起来的叫做模板标签。

==为了能在模板中使用 {% static %} 模板标签，别忘了在最顶部 {% load static %} 。static 模板标签位于 static模块中，只有通过 load 模板标签将该模块引入后，才能在模板中使用 {% static %} 标签。 #F44336==

list_display 属性控制 Post 列表页展示的字段

## URL调度器
- 从URL中取值可以使用尖括号<>
- 捕获的值可以选择性地包含转换器类型。比如，使用 <int:name> 来捕获整型参数。如果不包含转换器，则会匹配除了 / 外的任何字符
 
 
 {% url %} 解析视图函数 blog:archive 对应的 URL 模式
 
 迁移数据库
 

``` python
python manage.py makemigrations
 python manage.py migrate
```


## Django 返回JSON数据方法
 1. 手动组装字典返回
  

``` python
def get_book(request):
    all_book = Book.objects.all()
    d = []
    for i in all_book:
        d.append({'name': i.name})
    return JsonResponse(d, safe=False)
```

 2. JsonResponse返回
   

``` python
def get_book2(request):
    from django.forms.models import model_to_dict
    all_book = Book.objects.all()
    d = []
    for i in all_book:
        d.append(model_to_dict(i))           # <-------针对一个对象()
    return JsonResponse(d, safe=False) # 非字典要设置成false
```

``` python
def booapi(request):
    from django.core.serializers import serialize
    book_list = [
        {'id': 1, 'name': 'ptyhon'},
        {'id': 2, 'name': 'go'},
    ]
    import json
    return HttpResponse(json.dumps(book_list), content_type='application/json')
```

 3. Django自带的serializers返回
 只能针对queryset操作,即本地db里的数据,不能操作从其他系统api获取到的list ,dict等
 

``` python
def get_book3(request):
    from django.core.serializers import serialize
    d = serialize('json', Book.objects.all()) # <-------针对一个queryset,[{}, {}]

    # return HttpResponse(d)
    return HttpResponse(d)

return render(request, 'myapp/index.html', {'foo': 'bar',}, content_type='application/xhtml+xml')

return HttpResponse(t.render(c, request), content_type='application/xhtml+xml')

return HttpResponse(json.dumps(data), content_type='application/json', status=400)

JsonResponse = HttpResponse+content-type
```

多条件多字段过滤筛选数据

``` python
conditions ={
    'server_ip': ip,
    "bk_biz_id": bk_biz_id,
    'cron_min': c["cron_min"],
    'cron_hour': c["cron_hour"],
    'cron_day': c["cron_day"],
    'cron_month': c["cron_month"],
    'cron_week': c["cron_week"],
    'cron_task': c["cron_task"],
    "creator": c["user"],
    "deleted": 0
}
query_set = CrontabInfo.objects.filter(**conditions)
```

> @classmethod 多态，使得继承体系中的多个类都能以各自所独有的方式来实现某个方法。
> 通过@classmethod，可以用一种与构造器类似的方式来构造类的对象。

> @property 我们可以使用@property装饰器来创建只读属性，@property装饰器会将方法转换为相同名称的只读属性,可以与所定义的属性配合使用，这样可以防止属性被修改。
> 
> @property其实就是实现了getter功能； @xxx.setter实现的是setter功能；还有一个 @xxx.deleter实现删除功能
定义方法的时候 @property必须在 @xxx.setter之前，且二者修饰的方法名相同（age()）
如果只实现了 @property（而没有实现@xxx.setter），那么该属性为 只读属性


@csrf_exempt类的视图跨域
方法一：在类的 dispatch 方法上使用 @csrf_exempt

``` python
from django.views.decorators.csrf import csrf_exempt

class MyView(View):

    def get(self, request):
        return HttpResponse("hi")

    def post(self, request):
        return HttpResponse("hi")

    @csrf_exempt
    def dispatch(self, *args, **kwargs):
        return super(MyView, self).dispatch(*args, **kwargs)
```

方法二：在urls.py中配置

``` python
from django.conf.urls import url
from django.views.decorators.csrf import csrf_exempt
import views

urlpatterns = [
    url(r'^myview/$', csrf_exempt(views.MyView.as_view()), name='myview'),
]

```

template_name是类视图中的一个变量，默认值是'registration/login.html'，通过向as_view传入参数template_name='account/login.html'可以修改这个变量值

