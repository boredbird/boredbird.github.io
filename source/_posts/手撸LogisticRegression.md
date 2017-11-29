---
title: 手撸LogisticRegression
date: 2017-11-16 20:06:12 
categories: "机器学习" 
tags: 
     - LogisticRegression
description: 手撸LogisticRegression
toc: true
---
## LogisticRegression算法概述：
利用Logistic回归进行分类的主要思想是：根据现有数据对分类边界线建立回归公式，以此进行分类。
* 优点：计算代价不高，易于理解和实现。
* 缺点：容易欠拟合，分类精度可能不高。
* 适用数据类型：数值型和标称型数据。

## 梯度下降法求最佳参数伪代码：
1. 每个回归系数初始化为1
2. 重复R次：
	* a.计算整个数据集的梯度
	* b.使用alpha*gradient更新回归系数的向量
	* c.返回回归系数

<!--more-->

## 梯度下降法求最佳参数代码实现：
``` python

	# 定义sigmoid函数：
	def sigmoid(inX):
	    return 1.0 / (1 + exp(-inX))
	
	# 梯度下降法
	def gradAscent(dataMatIn, classLabels):
	    """
	    利用梯度下降法求解逻辑回归系数
	    :param dataMatIn:2维NumPy数组，每列分别代表每个不同的特征，每行则代表每个训练样本
	    :param classLabels:
	    :return: 返回训练好的回归系数
	    """
	    dataMatrix = mat(dataMatIn)  # convert to NumPy matrix
	    labelMat = mat(classLabels).transpose()  # convert to NumPy matrix
	    m, n = shape(dataMatrix)
	    alpha = 0.001 # 步长
	    maxCycles = 500 # 迭代次数
	    weights = ones((n, 1))
	    for k in range(maxCycles):  # heavy on matrix operations
	        h = sigmoid(dataMatrix * weights)  # matrix mult
	        error = (labelMat - h)  # vector subtraction
	        weights = weights + alpha * dataMatrix.transpose() * error  # matrix mult
	    return weights
```

## 随机梯度下降法求最佳参数伪代码：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/linear_model/QQ截图20171116153650.png" width="60%">
  <div class="figcaption">
  </div>
</div>

## 随机梯度下降法求最佳参数代码实现：
``` python

	def stocGradAscent(dataMatrix, classLabels):
	    m, n = shape(dataMatrix)
	    alpha = 0.01
	    weights = ones(n)  # initialize to all ones
	    for i in range(m):
	        h = sigmoid(sum(dataMatrix[i] * weights))
	        error = classLabels[i] - h
	        weights = weights + alpha * error * dataMatrix[i]
	    return weights
```

## mini-batch梯度下降法求最佳参数代码实现：
``` python

	def batchGradAscent(dataMatrix, classLabels, numIter=150):
	    m, n = shape(dataMatrix)
	    weights = ones(n)  # initialize to all ones
	    for j in range(numIter):
	        dataIndex = range(m)
	        for i in range(m):
	            alpha = 4 / (1.0 + j + i) + 0.0001  # apha decreases with iteration, does not
	            randIndex = int(random.uniform(0, len(dataIndex)))  # go to 0 because of the constant
	            h = sigmoid(sum(dataMatrix[randIndex] * weights))
	            error = classLabels[randIndex] - h
	            weights = weights + alpha * error * dataMatrix[randIndex]
	            del (dataIndex[randIndex])
	    return weights
```

## LogisticRegression小结
Logistic回归的目的是寻找一个非线性函数Sigmoid的最佳拟合参数，求解过程可以由最优化算法来完成。在最优化算法中，最常用的就是梯度下降算法。

via:

* 《机器学习实战》

