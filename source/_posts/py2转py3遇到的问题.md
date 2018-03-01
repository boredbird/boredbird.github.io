---
title: py2转py3遇到的问题
date: 2018-03-01 12:53:12
categories: "Python"
tags:
     - Python
description: py2转py3遇到的问题
---

##  python2与python3在处理异常的区别：
* 1.所以异常都从 BaseException继承，并删除了StardardError
* 2.去除了异常类的序列行为和.message属性
* 3.用 raise Exception(args)代替 raise Exception, args语法
* 4.捕获异常的语法改变，引入了as关键字来标识异常实例，
在Py2中：
``` python
    >>> try:
    ...    raise NotImplementedError('Error')
    ... except NotImplementedError, error:

    ...    print error.message
    ...
    Error
```
在Py3中：
``` python
    >>> try:
          raise NotImplementedError('Error')
        except NotImplementedError as error: #注意这个 as
          print(str(error))
    Error
```
* 5.异常链，因为`__context__`在3.0a1版本中没有实现

## tuple parameter unpacking is not supported in Pyhton 3
As tuple parameters are used by lambdas because of the single expression limitation, they must also be supported. This is done by having the expected sequence argument bound to a single parameter and then indexing on that parameter:
``` python
lambda (x, y): x + y
```
will be translated into:
``` python
lambda x_y: x_y[0] + x_y[1]
```

## py2与py3在map返回类型上的区别
py2：
``` python
Python 2.7.13 |Anaconda 4.3.1 (64-bit)| (default, Dec 19 2016, 13:29:36) [MSC v.1500 64 bit (AMD64)] on win32
In[2]: list_a = [2,3,4,5]
In[3]: list_b = [1,2,3,4]
In[4]: map(lambda a: a[0] / (a[1]+0.000000001), zip(list_a, list_b))
Out[4]:
[1.9999999979999998, 1.49999999925, 1.3333333328888888, 1.2499999996875]
In[5]: type(map(lambda a: a[0] / (a[1]+0.000000001), zip(list_a, list_b)))
Out[5]:
list
```

py3:
``` python
Python 3.5.2 |Anaconda custom (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
In[2]: list_a = [2,3,4,5]
In[3]: list_b = [1,2,3,4]
In[4]: map(lambda a: a[0] / (a[1]+0.000000001), zip(list_a, list_b))
Out[4]:
<map at 0x24dc066f160>
In[5]: type(map(lambda a: a[0] / (a[1]+0.000000001), zip(list_a, list_b)))
Out[5]:
map
```
在py3中需要用list()转换一下。


## windows下py2与py3共存切换问题
### 配置环境变量
![](assets/python/20180301155811.png)
### 修改文件名称
![](assets/python/20180301155930.png)
### 效果如下
![](assets/python/20180301155650.png)
