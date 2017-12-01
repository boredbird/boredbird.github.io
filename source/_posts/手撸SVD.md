---
title: 手撸SVD
date: 2017-12-01 20:26:12 
categories: "机器学习" 
tags: 
     - SVD
     - 推荐系统
description: 手撸SVD
toc: true
---
利用SVD，我们能够用小得多的数据集来表示原始数据集。这样做，实际上是去除了噪声和冗余信息。

![](https://i.imgur.com/rJzpOxt.png)

在PCA中得到的是矩阵的特征值，它们告诉我们数据集中的重要特征。这里的奇异值也是如此。奇异值和特征值是有关系的。这里的奇异值就是矩阵Data*DataT特征值的平方根。

### 相似度计算：
``` python

	from numpy import *
	from numpy import linalg as la
	
	def ecludSim(inA,inB):
	    return 1.0/(1.0 + la.norm(inA - inB))
	
	def pearsSim(inA,inB):
	    if len(inA) < 3 : return 1.0
	    return 0.5+0.5*corrcoef(inA, inB, rowvar = 0)[0][1]
	
	def cosSim(inA,inB):
	    num = float(inA.T*inB)
	    denom = la.norm(inA)*la.norm(inB)
	    return 0.5+0.5*(num/denom)
```

<!--more-->

### 基于物品相似度的推荐引擎：
``` python

	def standEst(dataMat, user, simMeas, item):
	    n = shape(dataMat)[1]
	    simTotal = 0.0; ratSimTotal = 0.0
	    for j in range(n):
	        userRating = dataMat[user,j]
	        if userRating == 0: continue
	        overLap = nonzero(logical_and(dataMat[:,item].A>0, \
	                                      dataMat[:,j].A>0))[0]
	        if len(overLap) == 0: similarity = 0
	        else: similarity = simMeas(dataMat[overLap,item], \
	                                   dataMat[overLap,j])
	        print 'the %d and %d similarity is: %f' % (item, j, similarity)
	        simTotal += similarity
	        ratSimTotal += similarity * userRating
	    if simTotal == 0: return 0
	    else: return ratSimTotal/simTotal
	
	def recommend(dataMat, user, N=3, simMeas=cosSim, estMethod=standEst):
	    unratedItems = nonzero(dataMat[user,:].A==0)[1]#find unrated items 
	    if len(unratedItems) == 0: return 'you rated everything'
	    itemScores = []
	    for item in unratedItems:
	        estimatedScore = estMethod(dataMat, user, simMeas, item)
	        itemScores.append((item, estimatedScore))
	    return sorted(itemScores, key=lambda jj: jj[1], reverse=True)[:N]
```

### 利用SVD提高推荐的效果
基于SVD的评分估计

``` python

	def svdEst(dataMat, user, simMeas, item):
	    n = shape(dataMat)[1]
	    simTotal = 0.0; ratSimTotal = 0.0
	    U,Sigma,VT = la.svd(dataMat)
	    Sig4 = mat(eye(4)*Sigma[:4]) #arrange Sig4 into a diagonal matrix
	    xformedItems = dataMat.T * U[:,:4] * Sig4.I  #create transformed items
	    for j in range(n):
	        userRating = dataMat[user,j]
	        if userRating == 0 or j==item: continue
	        similarity = simMeas(xformedItems[item,:].T,\
	                             xformedItems[j,:].T)
	        print 'the %d and %d similarity is: %f' % (item, j, similarity)
	        simTotal += similarity
	        ratSimTotal += similarity * userRating
	    if simTotal == 0: return 0
	    else: return ratSimTotal/simTotal
```

### 小结
SVD是一种强大的降维工具，我们可以利用SVD来逼近矩阵并从中提取重要特征。通过保留均值80%~90%的能量，就可以得到重要的特征并去掉噪声。协同过滤的核心是相似度计算方法；有很多相似度计算方法都可以用于计算物品或用户之间的相似度。通过在低维空间下计算相似度，SVD提高了推荐引擎的效果。
