---
title: django自带的server局域网访问
date: 2017-10-11 16:03:02 
categories: "django" 
tags: 
     - django
     - get
     - post
description: django自带的server局域网访问
---
# 问题描述
用`(myenvs) E:\Code\virtualenvs\myenvs\src>python .\manage.py runserver`启动服务，对应的访问地址为：

```

	Starting development server at http://127.0.0.1:8000/
```

![](/assets/django/django_get.png)

然后，我把`127.0.0.1`改为本机的地址发现居然不能访问。


# 解决方法

使用`python .\manage.py runserver 0.0.0.0:8000`启动服务：

## **又出现新的错误：**

<!--more-->

```
DisallowedHost at /post/act/
Invalid HTTP_HOST header: '10.83.2.132:8000'. You may need to add u'10.83.2.132' to ALLOWED_HOSTS.
Request Method:	GET
Request URL:	http://10.83.2.132:8000/post/act/?eid=1&status=%27F%27
Django Version:	1.11.6
Exception Type:	DisallowedHost
Exception Value:	
Invalid HTTP_HOST header: '10.83.2.132:8000'. You may need to add u'10.83.2.132' to ALLOWED_HOSTS.
Exception Location:	E:\Code\virtualenvs\myenvs\lib\site-packages\django\http\request.py in get_host, line 113
Python Executable:	E:\Code\virtualenvs\myenvs\Scripts\python.exe
Python Version:	2.7.13
Python Path:	
['E:\\Code\\virtualenvs\\myenvs\\src',
 'E:\\Code\\virtualenvs\\myenvs\\Scripts\\python27.zip',
 'E:\\Code\\virtualenvs\\myenvs\\DLLs',
 'E:\\Code\\virtualenvs\\myenvs\\lib',
 'E:\\Code\\virtualenvs\\myenvs\\lib\\plat-win',
 'E:\\Code\\virtualenvs\\myenvs\\lib\\lib-tk',
 'E:\\Code\\virtualenvs\\myenvs\\Scripts',
 'D:\\ProgramData\\Anaconda2\\Lib',
 'D:\\ProgramData\\Anaconda2\\DLLs',
 'D:\\ProgramData\\Anaconda2\\Lib\\lib-tk',
 'E:\\Code\\virtualenvs\\myenvs',
 'E:\\Code\\virtualenvs\\myenvs\\lib\\site-packages']
Server time:	星期三, 11 十月 2017 15:59:19 +0800
```

![](/assets/django/django_get_error1.png)

## 解决方法
去`django-admin.py startproject project-name`创建的项目中去修改 `setting.py` 文件：

``` python
 
ALLOWED_HOSTS = [‘*’] ＃在这里请求的host添加了＊ 
```

## **又又出现新的错误：**
报错`SyntaxError: invalid syntax`:

![](/assets/django/django_get_error2.png)

这尼玛，这是什么鬼，我的引号呢？？？终端上为什么没有引号，于是我有尝试了`"*"`双引号，依然不行。然后无穷的百度（动词），居然没一个类似我的问题。老天干嘛要为难我这个小白啊。

![](/assets/xinsaisaide.png)

## 解决方法
一不做，二不休：

``` python

	# ALLOWED_HOSTS = ['*']
	ALLOWED_HOSTS = list('*')
```

居然works！

加逗号也是可以的：

``` python

	ALLOWED_HOSTS = ['*',]
```

# 效果

![](/assets/django/django_get_settled.png)

参考：

* [django自带的server 让外网主机访问](http://blog.csdn.net/qq_25560423/article/details/56290505)
