---
title: 记录一次诡异的Python中文乱码
date: 2017-10-17 11:32:12 
categories: "Python" 
tags: 
     - Python
description: 记录一次诡异的Python中文乱码
---

有一天突然出现了这样的中文乱码：

![](assets/Python/luanma1.png)

我的第一反应就是检查：
`# -*- coding:utf-8 -*-`

然后检查：

``` python

	import sys
	sys.getdefaultencoding()
	Out[5]: 
	'utf-8'
```

这，，是中文编码的啊，再检查：

<!--more-->


``` python

	from chardet import detect
	cfg.dataset_train['white_list_type'][0]
	Out[8]: 
	'\xb7\xc7\xb0\xd7\xc3\xfb\xb5\xa5'
	detect(cfg.dataset_train['white_list_type'][0])
	Out[9]: 
	{'confidence': 0.0, 'encoding': None}
```

终于发现问题了，` 'encoding': None `

然后，那就在`read_csv`的时候指定编码：

```

	dataset = pd.read_csv('E:\\ScoreCard\\fpd30_analy_tmp02.csv',encoding='utf-8')
	Traceback (most recent call last):
	  File "D:\ProgramData\Anaconda2\lib\site-packages\IPython\core\interactiveshell.py", line 2881, in run_code
	    exec(code_obj, self.user_global_ns, self.user_ns)
	  File "<ipython-input-13-a9c949155761>", line 1, in <module>
	    dataset = pd.read_csv('E:\\ScoreCard\\fpd30_analy_tmp02.csv',encoding='utf-8')
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pandas\io\parsers.py", line 646, in parser_f
	    return _read(filepath_or_buffer, kwds)
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pandas\io\parsers.py", line 401, in _read
	    data = parser.read()
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pandas\io\parsers.py", line 939, in read
	    ret = self._engine.read(nrows)
	  File "D:\ProgramData\Anaconda2\lib\site-packages\pandas\io\parsers.py", line 1508, in read
	    data = self._reader.read(nrows)
	  File "pandas\parser.pyx", line 848, in pandas.parser.TextReader.read (pandas\parser.c:10415)
	  File "pandas\parser.pyx", line 870, in pandas.parser.TextReader._read_low_memory (pandas\parser.c:10691)
	  File "pandas\parser.pyx", line 947, in pandas.parser.TextReader._read_rows (pandas\parser.c:11728)
	  File "pandas\parser.pyx", line 1049, in pandas.parser.TextReader._convert_column_data (pandas\parser.c:13162)
	  File "pandas\parser.pyx", line 1108, in pandas.parser.TextReader._convert_tokens (pandas\parser.c:14116)
	  File "pandas\parser.pyx", line 1206, in pandas.parser.TextReader._convert_with_dtype (pandas\parser.c:16172)
	  File "pandas\parser.pyx", line 1222, in pandas.parser.TextReader._string_convert (pandas\parser.c:16400)
	  File "pandas\parser.pyx", line 1458, in pandas.parser._string_box_utf8 (pandas\parser.c:22072)
	UnicodeDecodeError: 'utf8' codec can't decode byte 0xb7 in position 0: invalid start byte
```

什么情况，一阵百度，无解。

然后用`notepad++`打开看下我的csv文件编码：

居然没有一种格式是选中的。。。
怎么会出现这种情况，我从数据库导出的时候明明已经指定了编码格式为`utf-8`，而且后面又打开指定了编码格式为`utf-8`，怎么现在会是未指定的状态。。

好吧，重新指定csv文件编码为`utf-8`，再重新试下：

``` python

	dataset = pd.read_csv('E:\\ScoreCard\\fpd30_analy_tmp02.csv')
	detect(dataset['white_list_type'][0])
	Out[17]: 
	{'confidence': 0.938125, 'encoding': 'utf-8'}
	dataset['white_list_type'][0]
	Out[18]: 
	'\xe9\x9d\x9e\xe7\x99\xbd\xe5\x90\x8d\xe5\x8d\x95'
	dataset['white_list_type']
	Out[19]: 
	0        非白名单
	1       普通白名单
	2       普通白名单
```
一切又正常了。诡异。