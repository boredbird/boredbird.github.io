---
title: 手撸k-Means
date: 2017-12-01 20:26:12 
categories: "机器学习" 
tags: 
     - KMeans
     - 二分K-Means
description: 手撸k-Means
toc: true
---
## K-Means聚类算法
### K-Means聚类算法伪代码

```

	创建k个点作为起始质心
	当任意一个点的簇分配结果发生改变时
		对数据集中的每个数据点
			对每个质心
				计算质心与数据点之间的距离
			将数据点分配到距其最近的簇
		对每一个簇，计算簇中所有点的均值并将均值作为质心
```

<!--more-->

### K-Means聚类辅助函数
``` python

	from numpy import *
	
	def loadDataSet(fileName):      #general function to parse tab -delimited floats
	    dataMat = []                #assume last column is target value
	    fr = open(fileName)
	    for line in fr.readlines():
	        curLine = line.strip().split('\t')
	        fltLine = map(float,curLine) #map all elements to float()
	        dataMat.append(fltLine)
	    return dataMat
	
	def distEclud(vecA, vecB):
	    return sqrt(sum(power(vecA - vecB, 2))) #la.norm(vecA-vecB)
	
	def randCent(dataSet, k):
	    n = shape(dataSet)[1]
	    centroids = mat(zeros((k,n)))#create centroid mat
	    for j in range(n):#create random cluster centers, within bounds of each dimension
	        minJ = min(dataSet[:,j]) 
	        rangeJ = float(max(dataSet[:,j]) - minJ)
	        centroids[:,j] = mat(minJ + rangeJ * random.rand(k,1))
	    return centroids
```

### K-Means聚类主函数
``` python

	def kMeans(dataSet, k, distMeas=distEclud, createCent=randCent):
	    m = shape(dataSet)[0]
	    clusterAssment = mat(zeros((m,2)))#create mat to assign data points 
	                                      #to a centroid, also holds SE of each point
	    centroids = createCent(dataSet, k)
	    clusterChanged = True
	    while clusterChanged:
	        clusterChanged = False
	        for i in range(m):#for each data point assign it to the closest centroid
	            minDist = inf; minIndex = -1
	            for j in range(k):
	                distJI = distMeas(centroids[j,:],dataSet[i,:])
	                if distJI < minDist:
	                    minDist = distJI; minIndex = j
	            if clusterAssment[i,0] != minIndex: clusterChanged = True
	            clusterAssment[i,:] = minIndex,minDist**2
	        print centroids
	        for cent in range(k):#recalculate centroids
	            ptsInClust = dataSet[nonzero(clusterAssment[:,0].A==cent)[0]]#get all the point in this cluster
	            centroids[cent,:] = mean(ptsInClust, axis=0) #assign centroid to mean 
	    return centroids, clusterAssment
```

K-Means算法只能收敛到局部最小值，而非全局最小值。

## 对聚类得到的簇进行后处理
上面在包含簇分配结果额矩阵中保存着每个点的误差，即该点到簇质心的距离平方值。下面会利用该误差来评价聚类质量的方法。

一种用于度量聚类效果的指标是SSE(Sum of Squared Error,误差平方和)。SSE值越小表示数据点越接近于它们的质心，聚类效果也越好。因为对误差取了平方，因此更加重视那些远离中心的点。一种肯定可以降低SSE值得方法是增加簇的个数，但是这违背了聚类的目标。聚类的目标是在保持簇数目不变的情况下提高簇的质量。

那么如何进行改进？

一种方法是将具有最大SSE值得簇划分成两个簇。具体实现时可以将最大簇包含的点过滤出来并在这些点上运行K-Means算法，其中的*k*设为2.

为了保持簇总数不变，可以将某两个簇进行合并。如何合并？

有两种可以量化的办法：合并最近的质心，或者合并两个使得SSE增幅最小的质心。第一种思路通过计算所有质心之间的距离，然后合并距离最近的两个点来实现。第二种方法需要合并两个簇然后计算总SSE值。必须在所有可能的两个簇上重复上述处理过程，直到找到合并最佳的两个簇为止。

## 二分K-Means聚类算法
为克服K-Means算法收敛于局部最小值得问题，有人提出了另一个称为二分K-Means（bisecting K-Means）的算法。该算法首先将所有点作为一个簇，然后将该簇一分为二。之后选择其中一个簇继续进行划分，选择哪一个簇进行划分取决于对其划分是否可以最大程度降低SSE的值。

### 二分K-Means算法的伪代码：

```

	将所有点看成一个簇
	当簇数目小于k时
	对于每一个簇
		计算总误差
		在给定的簇上面进行K-Means聚类（k=2）
		计算将该簇一分为二之后的总误差
	选择使得误差最小的那个簇进行划分操作
```

### 二分K-Means的代码实现：

``` python

	def biKmeans(dataSet, k, distMeas=distEclud):
	    m = shape(dataSet)[0]
	    clusterAssment = mat(zeros((m, 2)))
	    centroid0 = mean(dataSet, axis=0).tolist()[0]
	    centList = [centroid0]  # create a list with one centroid
	    for j in range(m):  # calc initial Error
	        clusterAssment[j, 1] = distMeas(mat(centroid0), dataSet[j, :]) ** 2
	    while (len(centList) < k):
	        lowestSSE = inf
	        for i in range(len(centList)):
	            ptsInCurrCluster = dataSet[nonzero(clusterAssment[:, 0].A == i)[0],
	                               :]  # get the data points currently in cluster i
	            centroidMat, splitClustAss = kMeans(ptsInCurrCluster, 2, distMeas)
	            sseSplit = sum(splitClustAss[:, 1])  # compare the SSE to the currrent minimum
	            sseNotSplit = sum(clusterAssment[nonzero(clusterAssment[:, 0].A != i)[0], 1])
	            print "sseSplit, and notSplit: ", sseSplit, sseNotSplit
	            if (sseSplit + sseNotSplit) < lowestSSE:
	                bestCentToSplit = i
	                bestNewCents = centroidMat
	                bestClustAss = splitClustAss.copy()
	                lowestSSE = sseSplit + sseNotSplit
	        bestClustAss[nonzero(bestClustAss[:, 0].A == 1)[0], 0] = len(centList)  # change 1 to 3,4, or whatever
	        bestClustAss[nonzero(bestClustAss[:, 0].A == 0)[0], 0] = bestCentToSplit
	        print 'the bestCentToSplit is: ', bestCentToSplit
	        print 'the len of bestClustAss is: ', len(bestClustAss)
	        centList[bestCentToSplit] = bestNewCents[0, :].tolist()[0]  # replace a centroid with two best centroids
	        centList.append(bestNewCents[1, :].tolist()[0])
	        clusterAssment[nonzero(clusterAssment[:, 0].A == bestCentToSplit)[0],
	        :] = bestClustAss  # reassign new clusters, and SSE
	    return mat(centList), clusterAssment
```
