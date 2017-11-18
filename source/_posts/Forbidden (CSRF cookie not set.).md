---
title: Forbidden (CSRF cookie not set.)
date: 2017-10-11 15:03:02 
categories: "django" 
tags: 
     - django
     - CSRF
     - get
     - post
description: Forbidden (CSRF cookie not set.)
---
# 问题描述
用postman提交post请求时，终端打印错误`Forbidden (CSRF cookie not set.)`：

```

	[11/Oct/2017 14:55:00] "GET /post/post/ HTTP/1.1" 200 47
	Forbidden (CSRF cookie not set.): /post/post/
	[11/Oct/2017 14:55:16] "POST /post/post/ HTTP/1.1" 403 2829
	Forbidden (CSRF cookie not set.): /post/post/
	[11/Oct/2017 15:00:06] "POST /post/post/ HTTP/1.1" 403 2829
	Performing system checks...
```

情况如下图所示：

<div class="fig figcenter fighighlight">
  <img src="/assets/django/django_post_forbiden.png" >
</div>

# 解决方法

**修改settings.py文件，注释掉**

<!--more-->

`django.middleware.csrf.CsrfViewMiddleware',`

# 效果
post请求处理正常。

<div class="fig figcenter fighighlight">
  <img src="/assets/django/django_post_forbiden_settled.png" >
</div>


参考：

* [(django1.10)访问url报错Forbidden (CSRF cookie not set.): xxx](http://www.cnblogs.com/meitian/p/7016336.html)