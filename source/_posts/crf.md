---
title: crf
date: 2018-07-16 11:38:12
categories: "机器学习"
tags:
     - crf
description: crf
toc: true
---

[CRF++ 0.58 在Windows中 运行与安装](https://blog.csdn.net/u013736042/article/details/41440045)
4. 命令行格式

4.1 训练程序

    命令行：
    % crf_learn template_file train_file model_file
    这个训练过程的时间、迭代次数等信息会输出到控制台上（感觉上是crf_learn程序的输出信息到标准输出流上了），如果想保存这些信息，我们可以将这些标准输出流到文件上，命令格式如下：
    % crf_learn template_file train_file model_file >> train_info_file

    有四个主要的参数可以调整：
    -a CRF-L2 or CRF-L1     
    规范化算法选择。默认是CRF-L2。一般来说L2算法效果要比L1算法稍微好一点，虽然L1算法中非零特征的数值要比L2中大幅度的小。
    -c float
    这个参数设置CRF的hyper-parameter。c的数值越大，CRF拟合训练数据的程度越高。这个参数可以调整过度拟合和不拟合之间的平衡度。这个参数可以通过交叉验证等方法寻找较优的参数。
    -f NUM
    这个参数设置特征的cut-off threshold。CRF++使用训练数据中至少NUM次出现的特征。默认值为1。当使用CRF++到大规模数据时，只出现一次的特征可能会有几百万，这个选项就会在这样的情况下起到作用。
    -p NUM
    如果电脑有多个CPU，那么那么可以通过多线程提升训练速度。NUM是线程数量。

    带两个参数的命令行例子：
    % crf_learn -f  3 -c 1.5 template_file train_file model_file


<!--more-->

4.2 测试程序

     命令行：
     % crf_test -m model_file test_files
     有两个参数-v和-n都是显示一些信息的，-v可以显示预测标签的概率值，-n可以显示不同可能序列的概率值，对于准确率，召回率，运行效率，没有影响，这里不说明了。
      与crf_learn类似，输出的结果放到了标准输出流上，而这个输出结果是最重要的预测结果信息（测试文件的内容+预测标注），同样可以使用重定向，将结果保存下来，命令行如下。
      % crf_test -m model_file test_files >> result_file
