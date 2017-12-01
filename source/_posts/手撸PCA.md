---
title: 手撸PCA
date: 2017-12-01 20:26:12 
categories: "机器学习" 
tags: 
     - PCA
     - 因子分析
     - 独立成分分析
description: 手撸PCA
toc: true
---

## 降维技术
### PCA(Principal Component Analysis,主成分分析)
在PCA中，数据从原来的坐标系转换到了新的坐标系，新坐标系的选择是由数据本身决定的。第一个新坐标轴选择的是原始数据中方差最大的方向，第二个新坐标轴的选择和第一个坐标轴正交且具有最大方差的方向。该过程一直重复，重复次数为原始数据中特征的数目。然后会发现，大部分方差都包含在最前面的几个新坐标轴中。因此，我们可以忽略余下的坐标轴，即对数据进行了降维处理。

### FA(Factor Analysis,因子分析)
在因子分析中，假设在观察数据的生成中有一些观察不到的隐变量(latent variable)。假设观察数据是这些隐变量和某些噪声的线性组合。那么隐变量的数据可能比观察数据的数目少，也就是说通过找到隐变量就可以实现数据的降维。

### ICA(Independent Component Analysis,独立成分分析)
ICA假设数据是从N个数据源生成的，这额鹅鹅鹅一点和因子分析有些类似。假设数据为多个数据源的混合观察结果，这些数据源之间在统计上是相互独立的，而在PCA中只假设数据是不相关的。同因子分析一样，如果数据源的数目少于观察数据的数目，则可以实现降维过程。

<!--more-->

## PCA
用一组正交基对坐标轴进行旋转，坐标轴的旋转并没有减少数据的维度。特征值分析是线性代数中的一个领域，它能够通过数据的一般格式来揭示数据的“真实”结构，即我们常说的特征向量和特征值。NumPy中有寻找特征向量和特征值得模块linalg,它有eig()方法，该方法用于求解特征向量和特征值。

### 在NumPy中实现PCA的伪代码

```

	去除平均值
	计算协方差矩阵
	计算协方差矩阵的特征值和特征向量
	将特征值从大到小排序
	保留最上面的N个特征向量
	将数据转换到上述N个特征向量构建的新空间中
```

### PCA的代码实现
``` python

	from numpy import *
	
	def loadDataSet(fileName, delim='\t'):
	    fr = open(fileName)
	    stringArr = [line.strip().split(delim) for line in fr.readlines()]
	    datArr = [map(float,line) for line in stringArr]
	    return mat(datArr)
	
	def pca(dataMat, topNfeat=9999999):
	    meanVals = mean(dataMat, axis=0)
	    meanRemoved = dataMat - meanVals #remove mean
	    covMat = cov(meanRemoved, rowvar=0)
	    eigVals,eigVects = linalg.eig(mat(covMat))
	    eigValInd = argsort(eigVals)            #sort, sort goes smallest to largest
	    eigValInd = eigValInd[:-(topNfeat+1):-1]  #cut off unwanted dimensions
	    redEigVects = eigVects[:,eigValInd]       #reorganize eig vects largest to smallest
	    lowDDataMat = meanRemoved * redEigVects#transform data into new dimensions
	    reconMat = (lowDDataMat * redEigVects.T) + meanVals
	    return lowDDataMat, reconMat
	
	def replaceNanWithMean():
	    datMat = loadDataSet('secom.data', ' ')
	    numFeat = shape(datMat)[1]
	    for i in range(numFeat):
	        meanVal = mean(datMat[nonzero(~isnan(datMat[:,i].A))[0],i]) #values that are not NaN (a number)
	        datMat[nonzero(isnan(datMat[:,i].A))[0],i] = meanVal  #set NaN values to mean
	    return datMat
```

在上面的代码中，首先计算并减去原始数据集的平均值。

然后，计算协方差矩阵及其特征值，接着利用argsort()函数对特征值进行从小到大的排序。

根据特征值排序结果的逆序就可以得到topNfeat个最大的特征向量。这些特征向量构成后面对数据进行转换的矩阵，该矩阵则利用N个特征将原始数据转换到新空间中。

最后，原始数据乘上特征向量矩阵，数据被重构返回。

### PCA小结
降维技术使得数据变得更易使用，并且它们往往能够去除数据中的噪声，使得其他机器学习任务更加精确。降维往往作为预处理步骤，在数据应用到其他算法之前清洗数据。
