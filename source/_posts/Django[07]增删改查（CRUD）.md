---
title: Django[07]增删改查（CRUD）
date: 2017-10-08 08:27:02 
categories: "django" 
tags: 
     - django
description: Django[07]增删改查（CRUD）
---

# CRUD

| 缩写|动作名称|  SQL  |     HTTP     |实际动作|
|-----|:------:|:-----:|:------------:|-------:|
|  C  | Create | INSERT|   PUT/POST   |  增加  |
|  R  |Retrieve| SELECT|      GET     |  查询  |
|  U  | Update | UPDATE|POST/PUT/PATCH|  更新  |
|  D  | Delete | DELETE|    DELETE    |  删除  |


# HTTP请求方法

|序号	|方法	|描述|
|---|:------:|-------:|
|1	|GET	|请求指定的页面信息，并返回实体主体。|
|2	|HEAD	|类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头|
|3	|POST	|向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改。|
|4	|PUT	|从客户端向服务器传送的数据取代指定的文档的内容。|
|5	|DELETE	|请求服务器删除指定的页面。|
|6	|CONNECT	|HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。|
|7	|OPTIONS	|允许客户端查看服务器的性能。|
|8	|TRACE	|回显服务器收到的请求，主要用于测试或诊断。|


via [Django1.10教程 -07 -增删改查（CRUD）](http://v.youku.com/v_show/id_XMjQ3MzA0NDY5Mg==.html?spm=a2h0j.8191423.playlist_content.5!10~5~5~A&&f=28961906&from=y1.2-3.4.10)

via [HTTP请求方法](http://www.runoob.com/http/http-methods.html)