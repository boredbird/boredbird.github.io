---
title: 手撸kNN
date: 2017-11-16 19:06:12 
categories: "机器学习" 
tags: 
     - NumPy
     - kNN
description: 手撸kNN
toc: true
---
## k近邻算法概述：
k-近邻算法采用测量不同特征值之间的距离方法进行分类。
* 优点：精度高、对异常值不敏感、无数据输入假定
* 缺点：计算复杂度高、空间复杂度高
* 适用数据范围：数值型和标称型

## kNN伪代码：
对未知类别属性的数据集中的每个点依次执行以下操作：
1. 计算已知类别数据集中的点与当前点之间的距离；
2. 按照距离递增次序排序；
3. 选取与当前点距离最小的k个点；
4. 确定前k个点所在类别的出现频率；
5. 返回前k个点出现频率最高的类别作为当前点的预测分类。

## kNN代码实现：

<!--more-->

``` python

	from numpy import *
	import operator
	from os import listdir
	
	def createDataSet():
	    """
	    创建数据集
	    :return:特征数据 array，标注数据 list
	    """
	    group = array([[1.0, 1.1], [1.0, 1.0], [0, 0], [0, 0.1]])
	    labels = ['A', 'A', 'B', 'B']
	    return group, labels
	
	def autoNorm(dataSet):
	    # 参数0使得函数可以从列中选取最小值，而不是选取当前行的最小值
	    minVals = dataSet.min(0)
	    maxVals = dataSet.max(0)
	    ranges = maxVals - minVals
	    normDataSet = zeros(shape(dataSet))
	    m = dataSet.shape[0]
	    normDataSet = dataSet - tile(minVals, (m, 1))
	    # element wise divide 矩阵数值相除
	    normDataSet = normDataSet / tile(ranges, (m, 1))
	    return normDataSet, ranges, minVals
	
	def knn_classifier(inX, dataSet, labels, k):
	    """
	    k-近邻算法
	    :param inX:待分类的输入向量
	    :param dataSet:训练样本集
	    :param labels:标签向量
	    :param k:用于选择最近邻居的数目
	    :return:k个近邻投票的最终类别
	    """
	    dataSetSize = dataSet.shape[0]
	    # 计算两个向量点的距离
	    # tile: 复制输出，将变量内容复制成输入矩阵同样大小的矩阵
	    diffMat = tile(inX, (dataSetSize, 1)) - dataSet
	    sqDiffMat = diffMat ** 2
	    sqDistances = sqDiffMat.sum(axis=1)
	    distances = sqDistances ** 0.5
	    sortedDistIndicies = distances.argsort()
	    # 选择距离最小的k个点
	    classCount = {}
	    for i in range(k):
	        voteIlabel = labels[sortedDistIndicies[i]]
	        classCount[voteIlabel] = classCount.get(voteIlabel, 0) + 1
	    # 排序
	    sortedClassCount = sorted(classCount.iteritems(), key=operator.itemgetter(1), reverse=True)
	    return sortedClassCount[0][0]
```


## kNN小结:
1. k-近邻算法是基于实例的学习，使用算法时必须有接近实际数据的训练样本数据。
2. k-近邻算法必须保存全部数据集，如果训练数据集的很大，必须使用大量的存储空间。
3. 此外，由于必须对数据集中的每个数据计算距离值，实际使用时可能非常耗时。
4. k-近邻算法的另一缺陷是他无法给出任何数据的基础结构信息，因此我们无法知晓平均实例样本和典型实例样本具有什么特征。

via:

* 《机器学习实战》



