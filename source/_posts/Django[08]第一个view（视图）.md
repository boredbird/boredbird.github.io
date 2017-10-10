---
title: Django[08]第一个view（视图）
date: 2017-10-08 08:43:02 
categories: "django" 
tags: 
     - django
description: Django[08]第一个view（视图）
---


# 定义我们第一个视图
修改posts[app]下views.py
``` python
	# Create your views here.
	from django.http import HttpResponse
	
	def posts_home(request):
		return HttpResponse("Hello World!")
```

# url建立映射到view
修改bbs[project]下urls.py
``` python
	from posts import views
	
	urlpatterns = [
	    url(r'^admin/', admin.site.urls),
	    url(r'^home/', views.posts_home),
	]

```
# 效果
![](https://i.imgur.com/9QePi8q.png)

via [Django1.10教程 -08 -第一个view（视图）](http://v.youku.com/v_show/id_XMjQ3MzA0NzAxNg==.html?spm=a2h0j.8191423.playlist_content.5!11~5~5~A&&f=28961906&from=y1.2-3.4.11)
