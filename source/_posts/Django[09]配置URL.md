---
title: Django[09]配置URL
date: 2017-10-08 08:57:02 
categories: "django" 
tags: 
     - django
description: Django[09]配置URL
---

# bbs URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/1.11/topics/http/urls/

# Examples:
## Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
## Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  url(r'^$', Home.as_view(), name='home')
## Including another URLconf
    1. Import the include() function: from django.conf.urls import url, include
    2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))

# project(project/urls.py)中的urls.py常见的几种写法
## 1、基于function的view
[详见上回](https://boredbird.github.io/2017/10/08/Django[08]%E7%AC%AC%E4%B8%80%E4%B8%AAview%EF%BC%88%E8%A7%86%E5%9B%BE%EF%BC%89/)
## 2、基于class的view
### 1、修改posts[app]下views.py
``` python 
	from django.views.generic import ListView
	class PostList(ListView):
		"""post的视图类"""
	
		def get(self,request):
			return HttpResponse("<h1>post的视图类</h1>") 
```
### 2、修改bbs[project]下urls.py
``` python 
	from posts import views
	
	urlpatterns = [
	    url(r'^admin/', admin.site.urls),
	    # url(r'^home/', views.posts_home),
	    url(r'^home/', views.PostList.as_view()),
	]
```
### 3、效果
![](https://i.imgur.com/kgAiXW3.png)

## 3、view别名
``` python 
	from app01 import views as app01_views
	from app02 import views as app02_views
	
	urlpatterns = [
	    url(r'^admin/', admin.site.urls),
	    url(r'^home/', app01_views.posts_home),
	    url(r'^home/', app02_views.PostList.as_view()),
	]
```
## 4、在app中的urls.py的使用
### 1、posts[app]下增加urls.py：
``` python

	from django.conf.urls import url
	from . import views
	
	urlpatterns = [
	    url(r'^home/', views.posts_home),
	]

```
### 2、在project下的urls.py 中设置第一级的路由：
``` python
	from django.conf.urls import url,include
	from django.contrib import admin
	from posts import views
	from posts import urls as posts_urls
	urlpatterns = [
	    url(r'^admin/', admin.site.urls),
	    # url(r'^home/', views.posts_home),
	    # url(r'^home/', views.PostList.as_view()),
	    url(r'^post/',include(posts_urls))
	]
```
### 3、在app下的urls.py中设置第二级路由，同第一步：
``` python

	from django.conf.urls import url
	from . import views
	
	urlpatterns = [
	    url(r'^home/', views.posts_home),
	]

```

# 多视图示例
## 1、app下的urls.py
``` python
	from django.conf.urls import url
	from . import views
	
	urlpatterns = [
	    url(r'^$', views.posts_home),
	    url(r'^create/$', views.posts_create),
	    url(r'^update/$', views.posts_update),
	    url(r'^detail/$', views.posts_detail),
	    url(r'^delete/$', views.posts_delete),
	    url(r'^', views.posts_home),
	]
```
## 2、app下的view.py
``` python
	# -*- coding: utf-8 -*-
	from __future__ import unicode_literals
	
	from django.shortcuts import render
	
	# Create your views here.
	from django.http import HttpResponse
	
	def posts_home(request):
		return HttpResponse("Hello World!")
	
	def posts_create(request):
		return HttpResponse("<h1>posts_create</h1>")
	
	def posts_update(request):
		return HttpResponse("<h1>posts_update</h1>")
	
	def posts_detail(request):
		return HttpResponse("<h1>posts_detail</h1>")
	
	def posts_delete(request):
		return HttpResponse("<h1>posts_delete</h1>")
```

注：

1、如果匹配到排在上面的正则表达式那么就不会适配下面的正则表达式了

2、不要忘记加'^'和'$'

via [Class-based views](https://docs.djangoproject.com/en/1.9/topics/class-based-views/)

via [Django1.10教程 -09 -配置URL](http://v.youku.com/v_show/id_XMjQ4Mzc0NjkxNg==.html?spm=a2h0j.8191423.playlist_content.5!12~5~5~A&&f=28961906&from=y1.2-3.4.12)
