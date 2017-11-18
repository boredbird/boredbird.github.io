---
title: Django[04]App和Model
date: 2017-10-08 06:52:02 
categories: "django" 
tags: 
     - django
description: Django[04]App和Model
---

# Django中project和app分别是什么？

* Project：python manage.py startproject [你的project名]
* app: python manage.py startapp [你的app名字]
* project是项目，project下面分一个或多个app


# 我们的第一个App

```

	python manage.py startapp [app的名字]
```

# 一定要注意：
把你的app在project的settings.py里面的INSTALLED_APPS加上

# Model
models.py里面创建类（与数据库建立联系的）

```

	python manage.py makemigrations（告诉Django我设计了一些表结构，你去准备一下）

	python manage.py migrate（告诉Django去数据库里操作一下刚才的动作）
```

MVC:Model View Controllers

MTV:Model View Template

# 1、创建一个app
![](https://i.imgur.com/bSC8Op9.png)

# 2、修改app目录下的models.py文件
``` python

	from django.db import models
	class Posts(models.Model):
		title = models.CharField(max_length=256) # 标题，存文字的
		content = models.TextField() # 内容
		update = models.DateTimeField(auto_now=True,auto_now_add=False) # 更新时间
		timestamp = models.DateTimeField(auto_now=False,auto_now_add=True) #创建时间
		
		def __str__(): # python3
			return self.title
		
		def __unicode__(): #python2
			return self.title
```
# 3、修改project目录下的setting.py文件
	INSTALLED_APPS 中添加你刚创建的app名称。
![](https://i.imgur.com/JLFyqiJ.png)

# 4、提交修改至数据库
![](https://i.imgur.com/VgFExeq.png)

via [Django1.10教程[04]之App和Model](http://v.youku.com/v_show/id_XMTkwMzgxNzY1Ng==.html?spm=a2h0j.8191423.playlist_content.5!6~5~5~A&&f=28961906&from=y1.2-3.4.6)

via [Django1.10教程[04]_APPandModel补录](http://v.youku.com/v_show/id_XMTk1MDY2MzA0OA==.html?spm=a2h0j.8191423.playlist_content.5!7~5~5~A&&f=28961906&from=y1.2-3.4.7)