---
title: Django[06]定制admin
date: 2017-10-08 07:44:02 
categories: "django" 
tags: 
     - django
description: Django[06]定制admin
---
# 在post/admin.py文件中添加如下代码：

```

	class PostAdmin(admin.ModelAdmin):
	
	    list_display = [,]  # 控制页面展示哪些字段
	    list_display_links = [,]  # 控制哪些字段是超链接
	    list_filter = [,]  # 支持在右侧过滤的字段
	    search_fields = [,]  # 支持搜索的字段
	    list_editable = [,]  # 支持直接编辑的字段，注意！不能与list_display_links重复！
	
	    class Meta:
	        model = model.Post

```

# 补充
如何修改admin中显示的app名字？

## 1. 在posts/apps.py中

```

	PostsConfig类中添加
	verbose_name = "帖子"
```

## 2. posts/__init__.py

```

default_app_config = "posts.apps.PostsConfig"
```

# 示例
## 1、修改posts[app]下admin.py
``` python

	# Register your models here.
	from posts import models
	
	class PostAdmin(admin.ModelAdmin):
		"""docstring for PostAdmin"""
		list_display = ["title","content"]
		list_display_links = ["title"]
		list_filter = ["timestamp","content"]
		search_fields = ["title","content"]
		list_editable = ["content"]
		# def __init__(self, arg):
		# 	super(PostAdmin, self).__init__()
		# 	self.arg = arg
	
		class Meta:
			model = models.Post
			
	
	admin.site.register(models.Post,PostAdmin)

```
## 2、修改posts[app]下apps.py
``` python

	class PostsConfig(AppConfig):
	    name = 'posts'
	    verbose_name = "帖子"
```
## 3、修改posts[app]下__init__.py
``` python

	default_app_config = "posts.apps.PostsConfig"
```
## 4、查看效果
![](https://i.imgur.com/Z5dk0nf.png)

via [Django1.10教程[06]_定制admin](http://v.youku.com/v_show/id_XMTk5MzkwMTI5Mg==.html?spm=a2h0j.8191423.playlist_content.5!9~5~5~A&&f=28961906&from=y1.2-3.4.9)