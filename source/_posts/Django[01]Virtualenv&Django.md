---
title: Django[01]Virtualenv&Django
date: 2017-10-07 22:47:02 
categories: "django" 
tags: 
     - django
     - virtualenv
description: Django[01]Virtualenv&Django
---
# 配置虚拟环境
## 安装virtualenv: 
``` python

	pip install virtualenv
```
## 使用virtualenv
### 创建虚拟环境：
**virtualenv [环境（文件夹）名]**

![](https://i.imgur.com/91qxDdD.png)

### 启用虚拟环境：
**.\Scripts\activate**

![](https://i.imgur.com/vAZWmfe.png)
### 退出虚拟环境：
**deactivate**

![](https://i.imgur.com/crvhBNX.png)

# 安装Django
``` python

	pip install django
```

![](https://i.imgur.com/7aXfWWO.png)
# 第一个Django项目
**1、python manage.py startproject my_first(我们的项目名)**
![](https://i.imgur.com/OAE9fFY.png)

**2、python manage.py runserver 127.0.0.1:8000**

![](https://i.imgur.com/rf21gwg.png)

![](https://i.imgur.com/eNM2lYU.png)

补充：

1、PowerShell里面执行activate失败？

输入：

	set-executionpolicy RemoteSigned

2、pip freeze命令使用

* 1、pip freeze > requirements.txt (保存依赖包到requirements.txt)
* 2、pip install -r requirements.txt (批量安装项目需要的所有依赖包)

via [Django1.10教程[01]之virtualenv使用](http://v.youku.com/v_show/id_XMTg3MTU2NDU0NA==.html?spm=a2h0j.8191423.playlist_content.5!2~5~5~A&&f=28961906&from=y1.2-3.4.2)