---
title: ImportError: No module named functools
date: 2017-10-11 09:59:02 
categories: "django" 
tags: 
     - django
     - virtualenv
description: ImportError: No module named functools
---
# 问题描述
今天早上从git pull代码后，启动本地的virtualenv,发现报错：

```

	(myenvs) E:\Code\virtualenvs\myenvs\src>python .\manage.py runserver
	Traceback (most recent call last):
	  File "E:\Code\virtualenvs\myenvs\lib\site.py", line 703, in <module>
	    main()
	  File "E:\Code\virtualenvs\myenvs\lib\site.py", line 692, in main
	    aliasmbcs()
	  File "E:\Code\virtualenvs\myenvs\lib\site.py", line 515, in aliasmbcs
	    import locale, codecs
	  File "E:\Code\virtualenvs\myenvs\lib\locale.py", line 17, in <module>
	    import functools
	
	ImportError: No module named functools
```
# 解决方法
**检查`ENV_FOLDER\Lib\orig-prefix.txt`文件发现：**

```
	d:\program files\anaconda2
```

<!--more-->

**这个路径应该是我宿舍电脑上的Python环境路径，现在改为我这台电脑的Python路径：**

```
	D:\ProgramData\Anaconda2
```

**再次启动，works!问题解决了**

```

	(myenvs) E:\Code\virtualenvs\myenvs\src>python .\manage.py runserver
	Performing system checks...
	
	System check identified no issues (0 silenced).
	October 11, 2017 - 10:05:10
	Django version 1.11.6, using settings 'bbs.settings'
	Starting development server at http://127.0.0.1:8000/
	Quit the server with CTRL-BREAK.
```

# 如何避免
在`E:\Code\virtualenvs\`下添加`.gitignore`文件，把环境配置文件给过滤掉，两边环境不一样省得冲突。

```

	*.pyc

	myenvs/Lib/orig-prefix.txt
```

参考：

* [changing virtualenv folder on windows](https://stackoverflow.com/questions/16786287/changing-virtualenv-folder-on-windows)