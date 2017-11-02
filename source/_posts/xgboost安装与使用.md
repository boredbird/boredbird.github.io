---
title: xgboost安装与使用
date: 2017-01-02 15:00:12 
categories: "Python" 
tags: 
     - Python
description: xgboost安装与使用
---
环境:

* win7 64位
* Python 2.7.13 
* MINGW：GNU Make 3.82.90 Built for i686-pc-mingw32

首先，打开Git Shell，依次执行如下命令：

```

	git clone --recursive https://github.com/dmlc/xgboost
	cd xgboost
	git checkout 9a48a40//新版本这一步可以省略
	git submodule init
	git submodule update
	
	cp make/mingw64.mk config.mk
	cp make/mingw64.mk dmlc-core/config.mk
	
	cd rabit
	make lib/librabit_empty.a -j4
	
	cd ../dmlc-core
	make -j4
	
	cd..
	make -j4
```

然后，安装到Python包中

```
	
	cd python-package
	python setup.py install
```
<!--more-->

最后，导入xgboost包，测试demo

```

	cd ..//或者直接进入xgboost目录
	cd demo
	cd guide-python
	python basic_walkthrough.py
```

```

	--1--

	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code
	$ git clone --recursive https://github.com/dmlc/xgboost

	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code
	$ cd xgboost
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost (master)
	$ git submodule init
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost (master)
	$ git submodule update
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost (master)
	$ cp make/mingw64.mk config.mk
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost (master)
	$ cp make/mingw64.mk dmlc-core/config.mk
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost (master)
	$ cd rabit/
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost/rabit ((a764d45...))
	$ make lib/librabit_empty.a -j4
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost/rabit ((a764d45...))
	$ cd ../dmlc-core
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost/dmlc-core ((b5bec54...))
	$ make -j4
	

	--2--
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost (master)
	$ cd python-package
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost/python-package (master)
	$ python setup.py install


	--3--
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost/python-package (master)
	$ cd ..
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost (master)
	$ cd demo
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost/demo (master)
	$ cd guide-python/
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost/demo/guide-python (master)
	$ python basic_walkthrough.py
	[09:58:28] 6513x127 matrix with 143286 entries loaded from ../data/agaricus.txt.train
	[09:58:28] 1611x127 matrix with 35442 entries loaded from ../data/agaricus.txt.test
	[0]     eval-error:0.042831     train-error:0.046522
	[1]     eval-error:0.021726     train-error:0.022263
	[09:58:28] 1611x127 matrix with 35442 entries loaded from dtest.buffer
	error=0.021726
	start running example of build DMatrix from scipy.sparse CSR Matrix
	[0]     eval-error:0.042831     train-error:0.046522
	[1]     eval-error:0.021726     train-error:0.022263
	start running example of build DMatrix from scipy.sparse CSC Matrix
	[0]     eval-error:0.042831     train-error:0.046522
	[1]     eval-error:0.021726     train-error:0.022263
	start running example of build DMatrix from numpy array
	[0]     eval-error:0.042831     train-error:0.046522
	[1]     eval-error:0.021726     train-error:0.022263
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/xgboost/demo/guide-python (master)
	$
```

via

* [64位Windows下安装xgboost详细参考指南（支持Python2.x和3.x）](http://blog.csdn.net/bon_mot/article/details/51742869)
