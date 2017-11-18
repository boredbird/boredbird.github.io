---
title: Django[12]Queryset介绍以及Template context补充
date: 2017-10-08 16:12:02 
categories: "django" 
tags: 
     - django
description: Django[12]Queryset介绍以及Template context补充
---

# Django shell

```
python manage.py shell
```

进入django shell,可以在命令行做一些操作。

``` python

	#查询出所有的post对象，for循环遍历
	queryset = models.Post.objects.all()
	for obj in queryset:
	    print(obj.title)
	    print(obj.content)
	    print(obj.update)
	    print(obj.timestamp)
	    print(obj.id)
	    print(obj.pk)
	
	#创建一条新的post记录
	models.Post.objects.create(title="abc", content="abc abc abc")
	
	#获取所有的记录条数
	models.Post.objects.all().count()
```

![](https://i.imgur.com/Jk5HHJB.png)

# queryset介绍
queryset 是一个可以遍历取值的结果集

queryset 里面都是 对象，可以通过对象.字段名的形式取值

一个对象就对应了数据库里面的一条记录

**数据库里面的一条记录  <- ORM -> Python中的对象**


# 如何在前端使用queryset

## 1. 从数据库里取出数据   
``` python      
	queryset = models.Post.objects.all()
```
## 2. 把渠道的数据塞进 data    
``` python     
	data = {"queryset": queryset}
```

即，修改views.py

``` python    

from . import models
def posts_home(request):
	queryset = models.Post.objects.all()
	data = {
		"queryset": queryset,
		"name": "home",
		"age": "18",
	}
	return render(request,"base.html",data)
```

## 3. 用data去填充前端的页面   
``` python     
	render(request, "xxx.html", data)
```

```
	{% for obj in queryset %}
	  <div class="blog-post">
	    <h2 class="blog-post-title">{{ obj.title }}</h2>
	    <p class="blog-post-meta">{{ obj.timestamp }}<a href="#">Mark</a></p>
	
	    <p>{{ obj.content }}</p>
	
	  </div><!-- /.blog-post -->
	{% endfor %} 
```
# 效果
![](https://i.imgur.com/5E6Nuje.png)

# 补充 Django的模板语言语法
```

	{% for x in xx %}
	{% endfor %}
	
	{{ val }}
```

via [Django1.10教程 -12 -Queryset介绍以及Template context补充](http://v.youku.com/v_show/id_XMjUzMTM0MjQwOA==.html?spm=a2h0j.8191423.playlist_content.5!15~5~5~A&&f=28961906&from=y1.2-3.4.15)
