---
title: Django[15]反向解析路由
date: 2017-10-08 18:15:02 
categories: "django" 
tags: 
     - django
description: Django[15]反向解析路由
---

# 给url起一个名字
```
    url(r'^(?P<id>\d+)/$', views.posts_detail, name="detail"),
```


1. Template中
```
<a href="{% url 'detail' id=obj.id %}">{{ obj.title }}</a>
```


2. Python代码中

``` python

	from django.shortcuts import redirect  # 调转请求
	from django.urls import reverse  # 反向解析url的
	
	...
	return redirect(reverse("detail", kwargs={"id": 3}))
```

3. Model中 get_absolute_url()

``` python

    def get_absolute_url(self):
        return reverse("detail", kwargs={"id": self.id})
        # return "/post/{}/".format(self.id)
        # return "/post/%s/" % (self.id)
```

# url的命令空间 namespace

在一级的url设置的，用于区分不用的app，因为不同的app下面可能存在同名的 url
``` python

	url(r'^post/', include(posts_urls, namespace="post")),
	
	<a href="{% url 'post:detail' id=obj.id %}">
	
	def get_absolute_url(self):
	    return reverse("post:detail", kwargs={"id": self.id})
        
```

via [Django1.10教程 -15 -反向解析路由](http://v.youku.com/v_show/id_XMjYxMzI1ODE4MA==.html?spm=a2h0j.8191423.playlist_content.5!18~5~5~A&&f=28961906&from=y1.2-3.4.18)
