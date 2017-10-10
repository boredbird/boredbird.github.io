---
title: Django[13]从数据库中获取某个对象
date: 2017-10-08 17:08:02 
categories: "django" 
tags: 
     - django
description: Django[13]从数据库中获取某个对象
---
# 获取对象

``` python

	models.Post.objects.get(id=3)
	
	models.Post.objects.get(title="隔壁老王是谁？")  # 获取 标题是隔壁老王是谁？的帖子
	
	models.Post.objects.get(title__icontains="隔壁")  # 获取 标题中包含隔壁两个字 的帖子

```

# 404页面，get_object_or_404

``` python

	from django.shortcuts import get_object_or_404
	
	get_object_or_404(models.Post, id=3)

```

# 新建了一个detail.html页面

用于展示的是帖子详情

```

	<div class="row">
	<h1>{{obj.title}}</h1>>
	<p>{{obj.content}}</p>
	</div><!-- /.row -->
```

# 修改views.py
``` python

	def posts_detail(request):
		# obj = models.Post.objects.get(id=3)
		obj = get_object_or_404(models.Post,id=1)
		data = {
			"obj":obj
		}
	
		return render(request,"detail.html",data)
```
# 效果
![](https://i.imgur.com/F2lHBVY.png)

via [Django1.10教程 -13 -从数据库中获取某个对象](http://v.youku.com/v_show/id_XMjUzMTM1NDM2MA==.html?spm=a2h0j.8191423.playlist_content.5!16~5~5~A&&f=28961906&from=y1.2-3.4.16)
