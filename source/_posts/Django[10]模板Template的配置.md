---
title: Django[10]模板Template的配置
date: 2017-10-08 09:49:02 
categories: "django" 
tags: 
     - django
description: Django[10]模板Template的配置
---
# BASE_DIR 和 os.path.join(xx, xxx)

``` python

	import os
	
	# Build paths inside the project like this: os.path.join(BASE_DIR, ...)
	BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
```
# 创建一个templates目录

![](https://i.imgur.com/8SnMh2q.png)

# 在settings.py中配置templates路径
``` python
	TEMPLATES = [
	    {
	        'BACKEND': 'django.template.backends.django.DjangoTemplates',
	        'DIRS': [os.path.join(BASE_DIR,"templates")],
	        'APP_DIRS': True,
	        'OPTIONS': {
	            'context_processors': [
	                'django.template.context_processors.debug',
	                'django.template.context_processors.request',
	                'django.contrib.auth.context_processors.auth',
	                'django.contrib.messages.context_processors.messages',
	            ],
	        },
	    },
	]
```
# 在templates文件夹下创建html文件
``` html
<!DOCTYPE html>
<!DOCTYPE html>
<html>
<head>
	<title>try django</title>
</head>
<body>
<h1>Hello World! Django!</h1>>
</body>
</html>
```

# 在views.py中使用templates目录下的html文件
``` python
	# -*- coding: utf-8 -*-
	from __future__ import unicode_literals
	
	from django.shortcuts import render
	
	# Create your views here.
	from django.http import HttpResponse
	
	def posts_home(request):
		return render(request,"index.html")
```

# 查看效果
![](https://i.imgur.com/2o9FySq.png)


via [Django1.10教程 -10 -模板Template的配置](http://v.youku.com/v_show/id_XMjUyMDA3MDQ3Ng==.html?spm=a2h0j.8191423.playlist_content.5!13~5~5~A&&f=28961906&from=y1.2-3.4.13)
