---
title: 基于Django REST Framework创建API服务
date: 2017-10-15 10:06:02 
categories: "django" 
tags: 
     - django
     - REST
     - API
description: 基于Django REST Framework创建API服务
---
Django REST Framework 安装

```
	pip install djangorestframework
	pip install markdown       # Markdown support for the browsable API.
	pip install django-filter  # Filtering support
```

看下我的环境：
```
	(myenvs) E:\Code\virtualenvs\myenvs\django_rest>pip freeze
	Django==1.11.6
	django-bootstrap3==9.0.0
	django-filter==1.0.4
	djangorestframework==3.7.0
	Markdown==2.6.9
	pytz==2017.2
```


创建一个新的项目django_rest，在项目下创建名为api的应用。
> cmd.exe

```

	E:\Code\virtualenvs\myenvs>.\Scripts\activate.bat
	
	(myenvs) E:\Code\virtualenvs\myenvs>python .\Scripts\django-admin.py startproject django_rest
	
	(myenvs) E:\Code\virtualenvs\myenvs>cd django_rest\
	
	(myenvs) E:\Code\virtualenvs\myenvs\django_rest>python .\manage.py startapp api
	
	(myenvs) E:\Code\virtualenvs\myenvs\django_rest>
```

打开settings.py文件，添加应用。
> settings.py

``` python

	# Application definition

	INSTALLED_APPS = [
	    'django.contrib.admin',
	    'django.contrib.auth',
	    'django.contrib.contenttypes',
	    'django.contrib.sessions',
	    'django.contrib.messages',
	    'django.contrib.staticfiles',
	    'rest_framework',
	    'api',
	]

	......

	# 在文件末尾添加
	REST_FRAMEWORK = {
	    'DEFAULT_PERMISSION_CLASSES':(
	        'rest_framework.permissions.IsAuthenticated',
	        )
	}

```

"rest_framework"为Django REST Framework应用，"api"为我们自己创建的应用。默认的权限策略可以设置在全局范围内，通过DEFAULT_PERMISSION_CLASSES设置。

通过`migrate`命令执行数据库迁移。
> cmd.exe

```

	(myenvs) E:\Code\virtualenvs\myenvs\django_rest>python .\manage.py makemigrations

	(myenvs) E:\Code\virtualenvs\myenvs\django_rest>python .\manage.py migrate
```

通过`createsuperuser`命令创建超级管理员账户admin/admin123456。
> cmd.exe

```
	(myenvs) E:\Code\virtualenvs\myenvs\django_rest>python manage.py createsuperuser
	Username (leave blank to use 'maomaochong'): admin
	Email address: admin@email.com
	Password:
	Password (again):
	Superuser created successfully.
```

创建数据序列化，在api应用下创建serializers.py文件。
> serializers.py

``` python

	from django.contrib.auth.models import User,Group
	from rest_framework import serializers
	
	class UserSerializer(serializers.HyperlinkedModelSerializer):
		class Meta:
			model = User
			fields = ('url','username','email','groups')
	
	
	class GroupSerializer(serializers.HyperlinkedModelSerializer):
		class Meta:
			model = Group
			fields = ('url','name')
```

Serializers用于定义API的表现形式，如返回哪些字段、返回怎样的格式等。这里序列化Django自带的User和Group。

编写视图文件，打开api应用下的views.py文件，编写如下代码。
> views.py

``` python
	# -*- coding: utf-8 -*-
	from __future__ import unicode_literals
	
	from django.shortcuts import render
	
	# Create your views here.
	from django.contrib.auth.models import User,Group
	from rest_framework import viewsets
	from api.serializers import UserSerializer,GroupSerializer
	
	# ViewSets 定义视图的展现形式
	class UserViewSet(viewsets.ModelViewSet):
		"""
		API endpoint that allows users to be viewed or edited.
		"""
		queryset = User.objects.all().order_by('-date_joined')
		serializer_class = UserSerializer
	
	class GroupViewSet(viewsets.ModelViewSet):
		"""
		API endpoint that allows users to be viewed or edited.
		"""
		queryset = Group.objects.all().order_by('-date_joined')
		serializer_class = GroupSerializer

```

在Django REST framework 中，ViewSets用于定义视图的展现形式，例如返回哪些内容，需要做哪些权限处理。

在URL中会定义相应的规则到ViewSet。ViewSet则通过serializer_class 找到对应的Serializers。这里讲User和Group的所有对象赋予queryset，并返回这些值。在UserSerializer和GroupSerializer中定义要返回的字段。

打开.../django_rest/urls.py文件，添加api的路由配置。
> urls.py

``` python

	from django.conf.urls import url, include
	from django.contrib import admin
	from rest_framework import routers
	from api import views
	
	# Routers provide an easy way of automatically determining the URL conf.
	router = routers.DefaultRouter()
	router.register(r'users',views.UserViewSet)
	router.register(r'groups',views.GroupViewSet)
	
	# Wire up out API using automatic URL routing.
	# Additionally,we include login URLs for the browsable API.
	urlpatterns = [
	    url(r'^admin/', admin.site.urls),
	    url(r'^',include(router.urls)),
	    url(r'^api-auth/',include('rest_framework.urls',
	    							namespace='rest_framework'))
	]

```

因为使用的是ViewSets,所以可以使用routers类自动生成URL conf。

通过`runserver`命令启动服务。
> cmd.exe

```
	(myenvs) E:\Code\virtualenvs\myenvs\django_rest>python manage.py runserver
	Performing system checks...
	
	System check identified no issues (0 silenced).
	October 15, 2017 - 12:32:14
	Django version 1.11.6, using settings 'django_rest.settings'
	Starting development server at http://127.0.0.1:8000/
	Quit the server with CTRL-BREAK.

```
![](/assets/django/django_rest_api_root.png)

用超级管理员admin/admin123456登录。

![](/assets/django/django_rest_api_root_login.png)


接下来在django_rest项目的基础上，创建模型，打开api应用下的models.py文件。
> models.py

``` python

	# -*- coding: utf-8 -*-
	from __future__ import unicode_literals
	
	from django.db import models
	
	# Create your models here.
	# 发布会
	class Event(models.Model):
	    name = models.CharField(max_length=100)            # 发布会标题
	    limit = models.IntegerField()                      # 限制人数
	    status = models.BooleanField()                     # 状态
	    address = models.CharField(max_length=200)         # 地址
	    start_time = models.DateTimeField('events time')   # 发布会时间
	    create_time = models.DateTimeField(auto_now=True)  # 创建时间（自动获取当前时间）
	
	    def __str__(self):
	        return self.name
	
	
	# 嘉宾
	class Guest(models.Model):
	    event = models.ForeignKey(Event)            # 关联发布会id
	    realname = models.CharField(max_length=64)  # 姓名
	    phone = models.CharField(max_length=16)     # 手机号
	    email = models.EmailField()                 # 邮箱
	    sign = models.BooleanField()                # 签到状态
	    create_time = models.DateTimeField(auto_now=True)  # 创建时间（自动获取当前时间）
	
	    class Meta:
	        unique_together = ('phone', 'event')
	
	    def __str__(self):
	        return self.realname
	
```
然后执行数据库迁移。
> cmd.exe

```

	(myenvs) E:\Code\virtualenvs\myenvs\django_rest>python manage.py makemigrations api
	Migrations for 'api':
	  api\migrations\0001_initial.py
	    - Create model Event
	    - Create model Guest
	    - Alter unique_together for guest (1 constraint(s))
	
	(myenvs) E:\Code\virtualenvs\myenvs\django_rest>python manage.py migrate

```
添加发布会数据序列化，打开api应用下的serializers.py文件（上面创建的）。
> serializers.py
``` python
	
	from django.contrib.auth.models import User,Group
	from rest_framework import serializers
	from api.models import Event,Guest
	
	class UserSerializer(serializers.HyperlinkedModelSerializer):
		class Meta:
			model = User
			fields = ('url','username','email','groups')
	
	
	class GroupSerializer(serializers.HyperlinkedModelSerializer):
		class Meta:
			model = Group
			fields = ('url','name')
	
	class EventSerializer(serializers.HyperlinkedModelSerializer):
		class Meta:
			model = Event
			fields = ('url','name','address','start_time','limit','status')
	
	class GuestSerializer(serializers.HyperlinkedModelSerializer):
		class Meta:
			model = Guest
			fields = ('url','realname','phone','email','sign','event')
```	

打开api应用下的views.py文件，定义发布会和嘉宾视图类。
> views.py

``` python
	
	# -*- coding: utf-8 -*-
	from __future__ import unicode_literals
	
	from django.shortcuts import render
	
	# Create your views here.
	from django.contrib.auth.models import User,Group
	from rest_framework import viewsets
	from api.serializers import UserSerializer,GroupSerializer, EventSerializer, GuestSerializer
	from api.models import Event, Guest 
	
	# ViewSets 定义视图的展现形式
	class UserViewSet(viewsets.ModelViewSet):
		"""
		API endpoint that allows users to be viewed or edited.
		"""
		queryset = User.objects.all().order_by('-date_joined')
		serializer_class = UserSerializer
	
	class GroupViewSet(viewsets.ModelViewSet):
		"""
		API endpoint that allows users to be viewed or edited.
		"""
		queryset = Group.objects.all()
		serializer_class = GroupSerializer
	
	class EventViewSet(viewsets.ModelViewSet):
		"""
		API endpoint that allows users to be viewed or edited.
		"""
		queryset = Event.objects.all()
		serializer_class = EventSerializer
	
	class GuestViewSet(viewsets.ModelViewSet):
		"""
		API endpoint that allows users to be viewed or edited.
		"""
		queryset = Guest.objects.all()
		serializer_class = GuestSerializer

```	

打开.../django_rest/urls.py文件，添加URL配置。
> urls.py

``` python

	from django.conf.urls import url, include
	from django.contrib import admin
	from rest_framework import routers
	from api import views
	
	# Routers provide an easy way of automatically determining the URL conf.
	router = routers.DefaultRouter()
	router.register(r'users',views.UserViewSet)
	router.register(r'groups',views.GroupViewSet)
	router.register(r'events',views.EventViewSet)
	router.register(r'guests',views.GuestViewSet)
	
	# Wire up out API using automatic URL routing.
	# Additionally,we include login URLs for the browsable API.
	urlpatterns = [
	    url(r'^admin/', admin.site.urls),
	    url(r'^',include(router.urls)),
	    url(r'^api-auth/',include('rest_framework.urls',
	    							namespace='rest_framework'))
	]

```


