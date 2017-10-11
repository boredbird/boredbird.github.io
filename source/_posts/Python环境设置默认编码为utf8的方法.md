---
title: Python环境设置默认编码为utf8的方法
date: 2017-10-11 10:43:12 
categories: "Python" 
tags: 
     - Python
description: Python环境设置默认编码为utf8的方法
---

从网上fork了虫师的代码，发现每个文件都没有加头注释指定文件编码，我这一个一个改得什么时候。想着虫师也是老司机了，不可能连IDE自动添加头注释都不知道，应该是哪边统一设置的。果然他是直接修改的Python环境配置。

**设置之前：**

```

	D:\ProgramData\Anaconda2\python.exe "D:\Program Files (x86)\JetBrains\PyCharm 2016.3.3\helpers\pydev\pydevconsole.py" 52853 52854
	Python 2.7.13 |Anaconda 4.3.1 (64-bit)| (default, Dec 19 2016, 13:29:36) [MSC v.1500 64 bit (AMD64)]
	Type "copyright", "credits" or "license" for more information.
	IPython 5.1.0 -- An enhanced Interactive Python.
	?         -> Introduction and overview of IPython's features.
	%quickref -> Quick reference.
	help      -> Python's own help system.
	object?   -> Details about 'object', use 'object??' for extra details.
	PyDev console: using IPython 5.1.0
	import sys; print('Python %s on %s' % (sys.version, sys.platform))
	sys.path.extend(['E:\\Code\\Python_Crawler', 'E:\\Code\\Python_Exercise_Code', 'E:\\Code\\Python_ML_Code', 'E:/Code/Python_Crawler'])
	Python 2.7.13 |Anaconda 4.3.1 (64-bit)| (default, Dec 19 2016, 13:29:36) [MSC v.1500 64 bit (AMD64)] on win32
	import sys
	sys.getdefaultencoding()
	Out[3]: 
	'ascii'

```

**设置之后：**

<!--more-->

```

	D:\ProgramData\Anaconda2\python.exe "D:\Program Files (x86)\JetBrains\PyCharm 2016.3.3\helpers\pydev\pydevconsole.py" 55595 55596
	Python 2.7.13 |Anaconda 4.3.1 (64-bit)| (default, Dec 19 2016, 13:29:36) [MSC v.1500 64 bit (AMD64)]
	Type "copyright", "credits" or "license" for more information.
	IPython 5.1.0 -- An enhanced Interactive Python.
	?         -> Introduction and overview of IPython's features.
	%quickref -> Quick reference.
	help      -> Python's own help system.
	object?   -> Details about 'object', use 'object??' for extra details.
	PyDev console: using IPython 5.1.0
	import sys; print('Python %s on %s' % (sys.version, sys.platform))
	sys.path.extend(['E:\\Code\\Python_Crawler', 'E:\\Code\\Python_Exercise_Code', 'E:\\Code\\Python_ML_Code', 'E:/Code/Python_Crawler'])
	Python 2.7.13 |Anaconda 4.3.1 (64-bit)| (default, Dec 19 2016, 13:29:36) [MSC v.1500 64 bit (AMD64)] on win32
	import sys
	sys.getdefaultencoding()
	Out[3]: 
	'utf-8'

```

**如何设置：**

可以在Python安装目录下的Lib/site-packages目录中，新建一个sitecustomize.py文件（也可以建在其它地方，然后手工导入，建在这里，每次启动Python的时候设置将自动生效），内容如下：

``` python

	import sys
	sys.setdefaultencoding('utf-8') #set default encoding to utf-8
	 
```

参考：

* [Python设置默认编码为utf8的方法](http://www.jb51.net/article/87785.htm)