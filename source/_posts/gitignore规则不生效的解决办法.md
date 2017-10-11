---
title: gitignore规则不生效的解决办法
date: 2017-10-11 11:50:02 
categories: "python" 
tags: 
     - python
     - git
description: gitignore规则不生效的解决办法
---
# 问题描述

发现添加`.gitignore`文件后，本地做的修改仍被push到GitHub。`.gitignore`规则并没有生效。

# 解决方法
原因是如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。

那么解决方法就是先把本地缓存删除（改变成未被追踪状态），然后再提交：

`git rm -r --cached .`

`git add .`

`git commit -m 'update .gitignore'`


# 如何避免

<!--more-->

## 忽略规则
* 忽略操作系统自动生成的文件，比如缩略图等；
* 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
* 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

##
最后需要强调的一点是，如果你不慎在创建.gitignore文件之前就push了项目，那么即使你在.gitignore文件中写入新的过滤规则，这些规则也不会起作用，Git仍然会对所有文件进行版本管理。
简单来说，出现这种问题的原因就是Git已经开始管理这些文件了，所以你无法再通过过滤规则过滤它们。因此**一定要养成在项目开始就创建.gitignore文件的习惯**，否则一旦push，处理起来会非常麻烦。



参考：

* [Git忽略规则.gitignore梳理](http://www.cnblogs.com/kevingrace/p/5690241.html)
* [Git忽略文件.gitignore的使用](http://blog.csdn.net/Two_Water/article/details/54260931)
* [Git忽略规则和.gitignore规则不生效的解决办法](http://www.cnblogs.com/zhangxiaoliu/p/6008038.html)
* [github官方给的Python项目.gitignore文件模板](https://github.com/github/gitignore/blob/master/Python.gitignore)