---
title: windows下使用crf++
date: 2018-07-16 11:38:12
categories: "机器学习"
tags:
     - crf++
description: windows下使用crf++
toc: true
---

### crf++工具包下载：

[crf++ 0.58 下载](https://drive.google.com/drive/folders/0B4y35FiV1wh7fngteFhHQUN2Y1B5eUJBNHZUemJYQV9VWlBUb3JlX0xBdWVZTWtSbVBneU0)

(后缀为.tar.gz的适合Linux和MacOS用户使用，后缀为.zip的适合Windows用户使用。)
选择编译好的zip包，解压之后目录结构如下：


<!--more-->


```
D:\CRF++-0.58>dir
 驱动器 D 中的卷没有标签。
 卷的序列号是 000A-6B8F

 D:\CRF++-0.58 的目录

2018/03/30  11:30    <DIR>          .
2018/03/30  11:30    <DIR>          ..
2013/02/13  00:40                28 AUTHORS
2013/02/13  00:40             1,494 BSD
2013/02/13  00:40               164 COPYING
2013/02/13  00:40            50,688 crf_learn.exe
2013/02/13  00:40            50,688 crf_test.exe
2018/03/30  11:30    <DIR>          doc
2018/03/30  11:30    <DIR>          example
2013/02/13  00:40            26,428 LGPL
2013/02/13  00:40           337,408 libcrfpp.dll
2013/02/13  00:40                20 README
2018/03/30  11:30    <DIR>          sdk
               8 个文件        466,918 字节
               5 个目录 384,789,987,328 可用字节

```

doc文件夹：
> 就是官方主页的内容。

example文件夹：
> 有四个任务的训练数据、测试数据和模板文件。    

sdk文件夹：
> CRF++的头文件和静态链接库。   
 crf_learn.exe：CRF++的训练程序。    
 crf_test.exe：CRF++的预测程序    

libcrfpp.dll：
> 训练程序和预测程序需要使用的静态链接库。

实际上，需要使用的就是crf_learn.exe，crf_test.exe和libcrfpp.dll，这三个文件。

### 主要参数：
```
D:\CRF++-0.58>crf_learn.exe
CRF++: Yet Another CRF Tool Kit
Copyright (C) 2005-2013 Taku Kudo, All rights reserved.

Usage: crf_learn.exe [options] files
 -f, --freq=INT              use features that occuer no less than INT(default 1)
 -m, --maxiter=INT           set INT for max iterations in LBFGS routine(default 10k)
 -c, --cost=FLOAT            set FLOAT for cost parameter(default 1.0)
 -e, --eta=FLOAT             set FLOAT for termination criterion(default 0.0001)
 -C, --convert               convert text model to binary model
 -t, --textmodel             build also text model file for debugging
 -a, --algorithm=(CRF|MIRA)  select training algorithm
 -p, --thread=INT            number of threads (default auto-detect)
 -H, --shrinking-size=INT    set INT for number of iterations variable needs to  be optimal before considered for shrinking. (default 20)
 -v, --version               show the version and exit
 -h, --help                  show this help and exit
```


### 运行测试:
先拿example中的某个例子，做一下测试。例如：example中chunking文件夹，其中原有4个文件：

  * exec.sh
  * template：特征模版
  * test.data：测试数据
  * train.data：训练数据
在cmd中进入CRF++-0.58所在的文件夹，使用`crf_learn template train.data model`训练数据，
`crf_test -m model test.data >output.txt`测试数据,具体效果如下：


### 效果如下：
目录结构如下：
```

D:\CRF++-0.58\example\chunking 的目录

2018/03/30  11:37    <DIR>          .
2018/03/30  11:37    <DIR>          ..
2013/02/13  00:40               280 exec.sh
2018/03/30  11:36         1,102,576 model
2018/03/30  11:37           367,759 output.txt
2013/02/13  00:40               359 template
2013/02/13  00:40           258,104 test.data
2013/02/13  00:40            25,682 train.data
               6 个文件      1,754,760 字节
               2 个目录 384,789,987,328 可用字节

```

output.txt如下：
```
Rockwell	NNP	B-NP	B-NP
International	NNP	I-NP	I-NP
Corp.	NNP	I-NP	I-NP
's	POS	B-NP	B-NP
Tulsa	NNP	I-NP	I-NP
unit	NN	I-NP	I-NP
said	VBD	B-VP	B-VP
it	PRP	B-NP	B-NP
signed	VBD	B-VP	B-VP
a	DT	B-NP	B-NP
tentative	JJ	I-NP	I-NP
agreement	NN	I-NP	I-NP
extending	VBG	B-VP	B-VP
its	PRP$	B-NP	B-NP
contract	NN	I-NP	I-NP
with	IN	B-PP	B-PP
Boeing	NNP	B-NP	B-NP
Co.	NNP	I-NP	I-NP
to	TO	B-VP	B-VP
provide	VB	I-VP	I-VP
structural	JJ	B-NP	B-NP
parts	NNS	I-NP	I-NP
for	IN	B-PP	B-PP
Boeing	NNP	B-NP	B-NP
's	POS	B-NP	I-NP
747	CD	I-NP	I-NP
jetliners	NNS	I-NP	I-NP
.	.	O	O

Rockwell	NNP	B-NP	B-NP
said	VBD	B-VP	B-VP
the	DT	B-NP	B-NP
agreement	NN	I-NP	I-NP
calls	VBZ	B-VP	B-VP
for	IN	B-SBAR	B-PP
it	PRP	B-NP	B-NP
to	TO	B-VP	B-VP
supply	VB	I-VP	I-VP
200	CD	B-NP	B-NP
additional	JJ	I-NP	I-NP
so-called	JJ	I-NP	I-NP
shipsets	NNS	I-NP	I-NP
for	IN	B-PP	B-PP
the	DT	B-NP	B-NP
planes	NNS	I-NP	I-NP
.	.	O	O
```
