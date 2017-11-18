---
title: Django[14]动态路由
date: 2017-10-08 17:35:02 
categories: "django" 
tags: 
     - django
description: Django[14]动态路由
---

# Django中的URL介绍
**/bbs/urls.py**

```

	from posts import urls as posts_urls
	
	urlpatterns = [
	    url(r'^admin/', admin.site.urls),
	    url(r'^post/', include(posts_urls)),
	]
```

**/posts/urls.py**

```

	from . import views
	
	urlpatterns = [
	    url(r'^$', views.posts_home),
	    url(r'^detail/$', views.posts_detail),
	    ...
```

http://127.0.0.1:8000/post/detail/

# 动态路由和参数传递

## 页面点击是通过设置a标签来调转的 <a href="/post/detail/id.../"></a>

## 后端view中通过id来查询不同的帖子对象
```
	url(r'^detail/(?P<id>\d+)/$', views.posts_detail,),
```

## 在模板中组合起来

```
	<h2 class="blog-post-title"><a href="/post/detail/{{obj.id}}/">{{ obj.title }}</a></h2>
```

via [Django1.10教程 -14 -动态路由](http://v.youku.com/v_show/id_XMjYwNDA0MzIzNg==.html?spm=a2h0j.8191423.playlist_content.5!17~5~5~A&&f=28961906&from=y1.2-3.4.17)
