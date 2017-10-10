---
title: Django[03]DjangoAdmin
date: 2017-10-07 22:47:02 
categories: "django" 
tags: 
     - django
description: Django[03]DjangoAdmin
---
# WSGI
WSGI(Web  server gateway interface)：Web服务器网关接口是为Python语言定义的Web服务器和Web应用程序或框架之间的一种简单而通用的接口。自从WSGI被开发出来以后，许多其它语言中也出现了类似接口。

web app <-WSGI->web server(nginx/tomcat)

# createsuperuser注意事项

注：至少八个字符，不能是简单的数字

# Django admin使用的介绍
* python manage.py runserver 127.0.0.1:8000
* 浏览器里面输入：http://127.0.0.1:8000/admin/
* 输入用户名、密码登录即可。

# urls.py使用的介绍
django的路由是通过正则表达式来匹配的。

via [Django1.10教程[03]之DjangoAdmin](http://v.youku.com/v_show/id_XMTg4NDk0NzA3Mg==.html?spm=a2h0j.8191423.playlist_content.5!4~5~5~A&&f=28961906&from=y1.2-3.4.4)

via [Django1.10教程[03]之DjangoAdmin](http://v.youku.com/v_show/id_XMTg5Nzk3NTczNg==.html?spm=a2h0j.8191423.playlist_content.5!5~5~5~A&&f=28961906&from=y1.2-3.4.5)