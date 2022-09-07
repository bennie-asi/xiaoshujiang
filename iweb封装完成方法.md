---
title: iweb封装完成方法
tags: Django,Python,日志
category: /小书匠/日记/2022-09
renderNumberedHeading: true
grammar_cjkRuby: true
---

``` python
def Lock(lockkey, timeout=60 * 10):
     '''锁'''
```

 

``` python
def get_queryfilters(param, trans=None):
    """
    :param param: 参数字典，包括排序信息，更新时间，页码，页码大小，平台（phone or pc），版本，token等等
    :param trans: 转义信息
    :return: 参数param字典中以q__开头的键的键值对字典，并去除键中的q__。
    """
```
	
``` python
def get_pageinfo(param, size=10, page=1):
    """
    :param param: 参数字典，包括排序信息，更新时间，页码，，平台（phone or pc），版本，token等等
    :param size: 页码大小
    :param page: 页码，
    :return: 页码大小，页码，开始页的元组
    """
```

``` python
def get_subquery_filter(query, subkey, v):
    """
    :param query:
    :param subkey:
    :param v:
    :return: 注：通过外键子查询的实现，有更好的处理办法---双下划线，如：user__name
    """
```

``` python
def wrap_query(query, trans=None, param=None):
    """
    :param query: 指定模型的所有查询结果集（queryset）
    :param trans: 转义信息，对应模型里边的x_field_trans = {'user_id': lambda o: o.user.showname if o.user else "",}
                        上一句的意思为user_id的字段信息将不显示原来的信息，而显示为user.shownamez，user_id的原本内容不发生改变。
    :param param: 参数字典，包括排序信息，更新时间，页码，页码大小，平台（phone or pc），版本，token等等
    :return: 指定页码，页码大小等信息的数据库查询结果
    """
```

``` python
def gen_pager(query, trans=None, size=10, page=1, param=None):
    """
    :param query: 指定模型的所有查询结果集（queryset）
    :param trans: 转义字典
    :param size: 页码大小，每个页面最多可以存放多少数据
    :param page: 参数字典，包括排序信息，更新时间，平台（phone or pc），版本，token等等
    :param param: 某函数名，默认不传。
    :return: 指定传入的参数信息的结果集
    """
```

``` python
def gen_pager_array(query, trans=None, size=10, page=1, param=None, func=None):
    """
    :param query: 指定模型的所有查询结果集（queryset）
    :param trans: 转义字典
    :param size: 页码大小，每个页面最多可以存放多少数据
    :param page: 当前页码
    :param param: 参数字典，包括排序信息，更新时间，平台（phone or pc），版本，token等等
    :param func: 某函数名，默认不传。
    :return: 返回指定参数信息的数据库信息集，且集合被转为自定义的Array类型
    """
```

``` python
def obj2dic(o, ks, d=None):
    """
    :param o: 某一个对象，一般为模型对象，如已经初始化之后的user
    :param ks: 字段列表，如：['id', 'name', 'sex', 'date']
    :param d: 参数字典，不传则会创建一个空字典
    :return: 作用：将对象o中的对应键ks，放入字典d中，并相应传值，得到字典d
    """
```

``` python 
def dic2obj(o, ks, d):
    """
    :param o: 某一个对象，一般为模型对象，如已经初始化之后的user
    :param ks: 字段列表，如：['id', 'name', 'sex', 'date']
    :param d: 参数字典
    :return: 作用：把字典d中的键ks放到对象o的属性ks，即o.ks = d['ks']；得到一个对象o；
                dic2obj(user, ['id', 'name', 'sex', 'date'], param)====>user['id'] = param.id；
                一般用在数据库更新上。
    """
```

``` python
def dic2objRefs(o, fs, d):
```

``` python
def obj2obj(dst, ks, src):
    """
    :param dst: 目标对象
    :param ks: 字段列表，如：['id', 'name', 'sex', 'date']
    :param src: 源对象
    :return: 作用：对象src中的属性列表ks赋值给dst的属性列表ks，即dst.ks = src.ks。
    """
```

``` python
def dic2objDecimals(o, fs, d):
    """
    :param o: 某一个对象，一般为模型对象，如已经初始化之后的user
    :param fs: 字段列表，如：['id', 'name', 'sex', 'date']
    :param d: 参数字典
    :return: 作用：把字典d中的键fs放到对象o的属性fs，即o.fs = d['fs']；但注意d['fs']被转换为了decimal数。
                若d['fs']为空，则o的属性fs设置为0；
    """
```

