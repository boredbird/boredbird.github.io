---
title: POST和GET区别
date: 2017-10-10 16:04:02 
categories: "django" 
tags: 
     - django
description: POST和GET区别
---
HTTP协议定义了很多与服务器交互的方法，最基本的有4种，分别是GET,POST,PUT,DELETE. 一个URL地址用于描述一个网络上的资源，而HTTP中的GET, POST, PUT, DELETE就对应着对这个资源的查，改，增，删4个操作，其中最常见请求方式是GET和POST，并且现在浏览器一般只支持GET和POST方法。

**GET一般用于获取/查询资源信息，而POST一般用于更新资源信息，他们之间主要区别如下：**

1）根据HTTP规范，GET用于信息获取，而且应该是安全的和幂等的，这里安全是指该操作用于获取信息而非修改信息，幂等是指对同一URL的多个请求应该返回同样的结果（这一点在实质实现时，可能并不满足）；POST表示可能修改变服务器上的资源的请求。

2）GET请求的数据会附在URL之后（就是把数据放置在HTTP协议头中），以?分割URL和传输数据，参数之间以&相连，如果数据是英文字母/数字，原样发送，如果是空格，转换为+，如果是中文/其他字符，
则直接把字符串用BASE64编码；POST把提交的数据则放置在是HTTP包的包体中。

3）因为GET是通过URL提交数据，那么GET可提交的数据量就跟URL的长度有直接关系，理论上URL长度是没有限制的，即HTTP协议没有规定URL的长度，但在实质中，特定的浏览器可能对这个长度做了限制；理论上POST也是没有大小限制的，HTTP协议规范也没有进行大小限制，但在服务端通常会对这个大小做一个限制，当然这个限制比GET宽松的多，即使用POST可以提交的数据量比GET大得多。

最后，网上有人说，POST的安全性要比GET的安全性高，实质上POST跟GET都是明文传输，这可以通过类似WireShark工具看到。总之，Get是向服务器发索取数据的一种请求，而Post是向服务器提交数据的一种请求。


via 

* [浅析HTTP中POST和GET区别并用Python模拟其响应和请求](http://blog.csdn.net/kevin_darkelf/article/details/40979333)
* [浅谈HTTP中Get与Post的区别](http://www.cnblogs.com/hyddd/archive/2009/03/31/1426026.html)
* [GET和POST的区别](http://www.cnblogs.com/wswang/p/6054619.html)