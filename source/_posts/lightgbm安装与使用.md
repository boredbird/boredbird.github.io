---
title: lightgbm安装与使用
date: 2017-01-02 15:00:12 
categories: "Python" 
tags: 
     - Python
description: lightgbm安装与使用
---
环境:

* win7 64位
* Python 2.7.13 
* MINGW：GNU Make 3.82.90 Built for i686-pc-mingw32
* Visual Studio 2017

## 1、下载源代码

git clone --recursive https://github.com/Microsoft/LightGBM

## 2、用VS编译

进入LightGBM目录，用VS打开windows/LightGBM.sln，选择DLL和x64，按Ctrl+Shift+B进行编译，dll文件就会在windows/x64/DLL/目录里 

![](assets/Python/light-gbm.png)

编译成功后对应目录`E:\Code\LightGBM\windows\x64\DLL`下会生成一些文件，如果存在DLL这个文件夹就说明安装成功了。

## 3、安装Python包

```

	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/LightGBM (master)
	$ cd python-package/
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/LightGBM/python-package (master)
	$  python setup.py install

```

## 4、测试

```

	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/LightGBM/python-package (master)
	$ cd ../examples/python-guide/
	
	chunhui.zhang@SZXH3FFK041 MINGW64 /e/Code/LightGBM/examples/python-guide (master                                      )
	$ python ./simple_example.py
	Load data...
	Start training...
	[1]     valid_0's auc: 0.764496 valid_0's l2: 0.24288
	Training until validation scores don't improve for 5 rounds.
	[2]     valid_0's auc: 0.766173 valid_0's l2: 0.239307
	[3]     valid_0's auc: 0.785547 valid_0's l2: 0.235559
	[4]     valid_0's auc: 0.797786 valid_0's l2: 0.230771
	[5]     valid_0's auc: 0.805155 valid_0's l2: 0.226297
	[6]     valid_0's auc: 0.800979 valid_0's l2: 0.223692
	[7]     valid_0's auc: 0.806566 valid_0's l2: 0.220941
	[8]     valid_0's auc: 0.808566 valid_0's l2: 0.217982
	[9]     valid_0's auc: 0.809041 valid_0's l2: 0.215351
	[10]    valid_0's auc: 0.805953 valid_0's l2: 0.213064
	[11]    valid_0's auc: 0.804631 valid_0's l2: 0.211053
	[12]    valid_0's auc: 0.802922 valid_0's l2: 0.209336
	[13]    valid_0's auc: 0.802011 valid_0's l2: 0.207492
	[14]    valid_0's auc: 0.80193  valid_0's l2: 0.206016
	Early stopping, best iteration is:
	[9]     valid_0's auc: 0.809041 valid_0's l2: 0.215351
	Save model...
	Start predicting...
	('The rmse of prediction is:', 0.4640593794679212)

```

或者直接通过pip安装。。。

via

* [在Windows下安装LightGBM的Python包](http://blog.csdn.net/jiaqiangbandongg/article/details/53814663)

* [微软开源分布式高性能GB框架LightGBM安装使用](http://blog.csdn.net/testcs_dn/article/details/54176824)

