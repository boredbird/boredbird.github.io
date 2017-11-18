---
title: django处理HTTP请求流程
date: 2017-10-10 16:29:02 
categories: "django" 
tags: 
     - django
description: django处理HTTP请求流程
---

<div class="fig figcenter fighighlight">
  <img src="/assets/django/django_flow_en.png" width="60%">
  <img src="/assets/django/django_flow_cn.png" width="60%" style="border-left: 1px solid black;">
  <div class="figcaption">Based on @FULLSTACKCTO's understanding of Django, this is how a user request is responded to.</div>
</div>


* **1:** User requests a page
* **2:** Request reaches Request Middlewares, which could manipulate or answer the request
* **3:** The URLConffinds the related View using urls.py
* **4:** View Middlewares are called, which could manipulate or answer the request
* **5:** The view function is invoked
* **6:** The view could optionally access data through models
* **7:** All model-to-DB interactions are done via a manager
* **8:** Views could use a special context if needed
* **9:** The context is passed to the Template for rendering
* **a:** Template uses Filters and Tags to render the output
* **b:** Output is returned to the view
* **c:** HTTPResponse is sent to the Response Middlerwares
* **d:** Any of the response middlewares can enrich the response or return a completely new response
* **e:** The response is sent to the user’s browser.

via 
* [here](http://www.jianshu.com/p/a2bf34b89d01)
* [Django Flowchart](http://hitesh.in/2009/django-flow/)