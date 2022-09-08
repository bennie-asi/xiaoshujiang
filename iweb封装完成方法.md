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

``` python
def dic2objInts(o, fs, d):
    """
    :param o: 某一个对象，一般为模型对象，如已经初始化之后的user
    :param fs: 字段列表，如：['id', 'name', 'sex', 'date']
    :param d: 参数字典
    :return: 作用：把字典d中的键fs放到对象o的属性fs，即o.fs = d['fs']；但注意d['fs']被转换为了int数。
                若d['fs']为空，则o的属性fs设置为0；
    """
```

``` python
def dic2objFloats(o, fs, d):
    """
        :param o: 某一个对象，一般为模型对象，如已经初始化之后的user
        :param fs: 字段列表，如：['id', 'name', 'sex', 'date']
        :param d: 参数字典
        :return: 作用：把字典d中的键fs放到对象o的属性fs，即o.fs = d['fs']；但注意d['fs']被转换为了float数。
                    若d['fs']为空，则o的属性fs设置为0；
        """
```

``` python
def dic2objNums(o, fs, d):
    """
        :param o: 某一个对象，一般为模型对象，如已经初始化之后的user
        :param fs: 字段列表，如：['id', 'name', 'sex', 'date']
        :param d: 参数字典
        :return: 作用：把字典d中的键fs放到对象o的属性fs，即o.fs = d['fs']；
                    若d['fs']为空，则o的属性fs设置为0；
        """
```

``` python
def dic2objDateTimes(o, fs, d):
```

``` python
def dic2objTimes(o, fs, d):
```

``` python
def dic2dic(dst, ks, src):
```

``` python
def json_filed_default(obj):
```

``` python
def get_one_by_sql(sql, params=None, db=None):
    """
    :param sql: sql语句，算编程语言  sql="insert into cdinfo values(%s,%s,%s,%s,%s)"
    :param params: 参数  params=(title,singer,imgurl,url,alpha)
    :param db: 数据库  db=main
    :return: 返回数据库查询结果集
    """
```

``` python
def objstrip(obj):
    """
    :param obj: 传入一个字典，元组或列表，或一个值.
    :return: 返回原对象。原来是什么就返回什么。作用：删除值为空的键
    """
```

``` python
def splitstrip(strs, seg=' '):
    """
    :param strs: 字符串
    :param seg: 指定通过什么拆分字符串
    :return: 作用：将传入的字符串，通过指定字符拆分为列表，多个连续的该字符会被处理为一个，seg可以指定通过什么拆分；
                默认去除首尾空格；默认通过空格拆分为列表。
    """
```

``` python
def orderinggen():
    """
    :return: 返回当前时间戳
    """
```

``` python
def md5(s):
    """
    :param s: 待加密字符串
    :return: 返回已加密后的字符串
    """
```

``` python
def pwdhash(pwd, salt):
    '''计算加密后的密码,禁止修该函数!!!'''
```

``` python
def get_querykey(query):
```

``` python
def parsedate(s):
    """格式化时间列表，如：parsedate('19960508')====>1996-05-08"""
```

``` python 
def isphone(phone):
    '''是否是手机格式'''
```

``` python
def isidcardno(v):
    """检查18位身份证号"""
```

``` python
def set_cache(key, newval, timeout=30, autolang=True):
    """设置某键缓存为newval"""
```

``` python
def del_cache(key, autolang=True):
    """删除缓存"""
```

``` python
def get_cache(key, default=None, autolang=True):
    """获取某键的缓存"""
```

``` python
def get_or_set_cache(key, newval, timeout=30, autolang=True, lock=False):
    """有就获取键缓存，没有就设置键缓存为newcal"""
```

``` python
def site_get_or_set_cache(key, newval, timeout=30):
    """设置网站配置某键的缓存"""
```

``` python
def site_del_cache(key):
    """删除网站配置某键的缓存"""
```

``` python
def get_model_obj_cache_key(model, objid):
    '''获取对象缓存的键名子'''
```

``` python
def get_obj_cache_key_with_fields(fields):
```

``` python
def get_cached_obj(model, objid, timeout=60 * 60 * 24):
```

``` python
def get_cached_obj_with_fields(model, fields, timeout=60 * 60 * 24):
```

``` python
def del_cached_obj(obj):
```

``` python
def del_obj_all_cache(obj):
    '''删除该对象关联的全部缓存'''
```

``` python
def get_table_cache(key, default=None):
```

``` python
def set_table_cache(key, newval, timeout=30):
```

``` python
def del_table_cache(key):
```

``` python
def get_safe_cache(key, default=None):
```

``` python
def set_safe_cache(key, newval, timeout=30):
```

``` python
def del_safe_cache(key):
```

``` python
def parse_time(s):
```

``` python
def parse_datetime(s):
```

``` python
def get_qrcode_url(text, logourl=None, corner='lt-rb'):
# 二维码生成
```

``` python
def get_barcode_url(text):
# 条形码生成
```

``` python
def wrap_url(path):
```

``` python
def get_urlqrcode_url(path, logo=None):
```

``` python
def month_first_day(y, m):
```

``` python
def month_last_day(y, m):
```

``` python
def last_month_first_day(today=None):
```

``` python
def get_models_text(modelname, ids, attr='name', split=','):
    '''获取模型文本'''
```

``` python
def get_or_set_file(filekey, content, subpath=None, force=False, partition=False, timeout=60 * 60, root=None):
    '''将文件保存到上传临时目录'''
```

``` python
def register_models(models):
    """如果模型被设置为abstract，则不注册，反之则注册"""
```

``` python
def mergedic(rawd, *othd):
    """多个字典合并，就地合并，即合并之后的结果放入rawd中"""
```

``` python
def get_uuid():
    """获取通用唯一识别码"""
```




