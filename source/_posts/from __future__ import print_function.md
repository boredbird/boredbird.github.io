---
title: from __future__ import print_function
date: 2018-07-16 12:53:12
categories: "Python"
tags:
     - Python
description: from __future__ import print_function
---

Python提供了__future__模块,把下一个新版本的特性导入到当前版本,于是我们就可以在当前版本中测试一些新版本的特性。

下面从__future__引入对于python2来说比较先进的模块print_function接口参数:
```
print(*values, sep=' ', end='/n', file=sys.stdout)
print(value1, value2, value3, sep=' ', end='/n', file=sys.stdout)

这里,输出的变量可以是一个序列或者多个变量,可以像上面一样用逗号分开每个变量。 参数sep,end,file是三个可选参数。
sep:
指每个输出变量之间的分隔符,默认是一个空格
end:
指的是输出结束后的内容,默认是换行
file:
指的是输出流要输出的目的文件,默认sys.stdout(标准输出)
```

<!--more-->

效果如下所示:
```python
Python 2.7.14 |Anaconda, Inc.| (default, Nov  8 2017, 13:40:45) [MSC v.1500 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> value1 = 1
>>> value2 = 2
>>> value3 = 3
>>> print(value1, value2, value3, sep=' ', end='/n', file=sys.stdout)
  File "<stdin>", line 1
    print(value1, value2, value3, sep=' ', end='/n', file=sys.stdout)
                                     ^
SyntaxError: invalid syntax
>>> from __future__ import print_function
>>> print(value1, value2, value3, sep=' ', end='/n', file=sys.stdout)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'sys' is not defined
>>> import sys
>>> print(value1, value2, value3, sep=' ', end='/n', file=sys.stdout)
1 2 3/n
>>>
>>>
```
