---
title: pip源设置
date: 2018-07-16 15:55:12
categories: "Python"
tags:
     - Python
     - pip
description: pip源设置
---

### 国内pypi镜像
* V2EX：pypi.v2ex.com/simple
* 豆瓣：http://pypi.douban.com/simple
* 中国科学技术大学：http://pypi.mirrors.ustc.edu.cn/simple/

### 指定单次安装源
pip install <包名> -i http://pypi.v2ex.com/simple

举例：
pip install gensim -i http://pypi.v2ex.com/simple


<!--more-->

```
D:\Program Files (x86)\PowerCmd>pip install gensim -i http://pypi.v2ex.com/simple
Collecting gensim
  The repository located at pypi.v2ex.com is not a trusted or secure host and is being ignored. If this repository is available via HTTPS it is recommended to use HTTPS instead, otherwise you may silence this warning and allow it anyways with '--trusted-host pypi.v2ex.com'.
  Could not find a version that satisfies the requirement gensim (from versions: )
No matching distribution found for gensim
You are using pip version 9.0.1, however version 9.0.3 is available.
You should consider upgrading via the 'python -m pip install --upgrade pip' command.
```


pip  install gensim --isolated http://pypi.douban.com/simple  -- trusted-host pypi.douban.com

pip  install gensim --isolated http://mirrors.aliyun.com/pypi/simple/  -- trusted-host mirrors.aliyun.com

尝试了换源仍然没能解决，最后还是乖乖的使用了默认源，还好速度也不是很慢。



### 指定全局安装源
* 在unix和macos，配置文件为：$HOME/.pip/pip.conf
* 在windows上，配置文件为：%HOME%\pip\pip.ini
```
[global]
timeout = 6000
  index-url = http://pypi.douban.com/simple
```
