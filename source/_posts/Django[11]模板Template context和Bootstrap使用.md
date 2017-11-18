---
title: Django[11]模板Template context和Bootstrap使用
date: 2017-10-08 15:01:02 
categories: "django" 
tags: 
     - django
description: Django[11]模板Template context和Bootstrap使用
---

# Template context


## **视图views.py中**：

``` python

	# -*- coding: utf-8 -*-
	from __future__ import unicode_literals
	
	from django.shortcuts import render
	
	# Create your views here.
	from django.http import HttpResponse
	
	def posts_home(request):
		context = {
			"title"： "home"
		}
		return render(request,"index.html",context)
	
	def posts_create(request):
		context = {
			"title"： "create"
		}
		return render(request,"index.html",context)
	
	def posts_detail(request):
		context = {
			"title"： "detail"
		}
		return render(request,"index.html",context)
```
## **index.html中**

用 **context**去填充模板 index.html，然后再返回

index.html中添加如下代码：
```
	<h1>Hello {{ title }}}</h1>
```

**context**是一个字典,存放要渲染到页面的数据


# Bootstrap模板使用

## 1. 下载模板文件
[模板文件链接](http://v3.bootcss.com/examples/blog/)

## 2. 把html文件拷贝到了templates文件夹下面

## 3. 新建一个statics文件夹，用于存放css文件和js文件

## 4. 把css和js文件拷贝到statics文件夹下

## 5. 在settings.py中配置statics文件夹

```

	STATICFILES_DIRS = [
	    os.path.join(BASE_DIR, "statics")
	]
```

## 6. 将html文件中指定位置的css和js文件的路径修改为/static/...

**文档结构如下：**

![](https://i.imgur.com/AGdigpr.png)

**效果如图：**
![](https://i.imgur.com/d85xmJA.png)



via [Django1.10教程 -11 -模板Template context和Bootstrap使用](http://v.youku.com/v_show/id_XMjUyMDA4Mzk4NA==.html?spm=a2h0j.8191423.playlist_content.5!14~5~5~A&&f=28961906&from=y1.2-3.4.14)
