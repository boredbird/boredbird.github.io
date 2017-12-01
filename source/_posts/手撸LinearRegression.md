---
title: 手撸LinearRegression
date: 2017-12-01 20:26:12 
categories: "机器学习" 
tags: 
     - 回归
     - 岭回归
     - 局部加权线性回归
     - 逐步回归
description: 手撸LinearRegression
toc: true
---
## 线性回归
解析式求解：

### 线性回归解析式解Python代码实现
``` python

	from numpy import *
	
	def loadDataSet(fileName):      #general function to parse tab -delimited floats
	    numFeat = len(open(fileName).readline().split('\t')) - 1 #get number of fields 
	    dataMat = []; labelMat = []
	    fr = open(fileName)
	    for line in fr.readlines():
	        lineArr =[]
	        curLine = line.strip().split('\t')
	        for i in range(numFeat):
	            lineArr.append(float(curLine[i]))
	        dataMat.append(lineArr)
	        labelMat.append(float(curLine[-1]))
	    return dataMat,labelMat
	
	def standRegres(xArr,yArr):
	    xMat = mat(xArr); yMat = mat(yArr).T
	    xTx = xMat.T*xMat
	    if linalg.det(xTx) == 0.0:
	        print "This matrix is singular, cannot do inverse"
	        return
	    ws = xTx.I * (xMat.T*yMat)
	    return ws
```

<!--more-->

## 局部加权线性回归
局部加权线性回归(Locally Weighted Linear Regression,LWLR)。在该算法中，我们给待预测点附近的每个点赋予一定的权重；然后在这个子集上基于最小均方差来进行普通的回归。与kNN一样，这种算法每次预测均需要事先选取出对应的数据子集。

该算法解出回归系数w的形式如下：

![](https://i.imgur.com/NLwNawn.png)

其中*w*是一个矩阵，用来给每个数据点赋予权重。

LWLR使用“核”（与支持向量机中的核类似）来对附近的点赋予更高的权重。核的类型可以自由选择，最常用的核就是高斯核，高斯核对应的权重如下：
![](https://i.imgur.com/JJWjlIc.png)

这样就构建了一个只含对角元素的权重矩阵*w*，并且点*x*与*x(i)*越近，*w(i,i)*将会越大。参数*k*决定了对附近的点赋予多大的权重，则也是使用LWLR时唯一需要考虑的参数。

下面是参数*k*与权重的关系：
![](https://i.imgur.com/GFpPMOR.png)

### 局部加权线性回归解析式解Python代码实现
``` python

	def lwlr(testPoint,xArr,yArr,k=1.0):
	    xMat = mat(xArr); yMat = mat(yArr).T
	    m = shape(xMat)[0]
	    weights = mat(eye((m)))
	    for j in range(m):                      #next 2 lines create weights matrix
	        diffMat = testPoint - xMat[j,:]     #
	        weights[j,j] = exp(diffMat*diffMat.T/(-2.0*k**2))
	    xTx = xMat.T * (weights * xMat)
	    if linalg.det(xTx) == 0.0:
	        print "This matrix is singular, cannot do inverse"
	        return
	    ws = xTx.I * (xMat.T * (weights * yMat))
	    return testPoint * ws
	
	def lwlrTest(testArr,xArr,yArr,k=1.0):  #loops over all the data points and applies lwlr to each one
	    m = shape(testArr)[0]
	    yHat = zeros(m)
	    for i in range(m):
	        yHat[i] = lwlr(testArr[i],xArr,yArr,k)
	    return yHat
```

局部加权线性回归的问题在于，每次必须在整个数据集上运行，也就是说为了做出预测，必须保存所有的训练数据。

## 岭回归和逐步线性回归
岭回归最先用来处理特征数多于样本数的情况，现在也用于在估计中加入偏差，从而得到更好的估计。这里通过引入lamda来限制了所有*w*之和，通过引入该惩罚项，能够减少不重要的参数，这个技术在统计学中也叫做缩减（shrinkage）。

![](https://i.imgur.com/oKBvUwq.png)

### 岭回归中的岭是什么？
岭回归使用了单位矩阵乘以常量lamda，最先是用来处理特征数多于样本数的情况，我们观察其中的单位矩阵*I*，可以看到值1贯穿整个对角线，其余元素全是0。形象地，在0构成的平面上有一条1组成的“岭”，这就是岭回归中的“岭”的由来。

### 岭回归解析式解Python代码实现
``` python

	def ridgeRegres(xMat,yMat,lam=0.2):
	    xTx = xMat.T*xMat
	    denom = xTx + eye(shape(xMat)[1])*lam
	    if linalg.det(denom) == 0.0:
	        print "This matrix is singular, cannot do inverse"
	        return
	    ws = denom.I * (xMat.T*yMat)
	    return ws
	    
	def ridgeTest(xArr,yArr):
	    xMat = mat(xArr); yMat=mat(yArr).T
	    yMean = mean(yMat,0)
	    yMat = yMat - yMean     #to eliminate X0 take mean off of Y
	    #regularize X's
	    xMeans = mean(xMat,0)   #calc mean then subtract it off
	    xVar = var(xMat,0)      #calc variance of Xi then divide by it
	    xMat = (xMat - xMeans)/xVar
	    numTestPts = 30
	    wMat = zeros((numTestPts,shape(xMat)[1]))
	    for i in range(numTestPts):
	        ws = ridgeRegres(xMat,yMat,exp(i-10))
	        wMat[i,:]=ws.T
	    return wMat
```

### 岭回归的回归系数变化图
这里的lambda应以指数级变化，这样可以看出lambda在取非常小的值时和取非常大的值时分别对结果造成的影响。

![](https://i.imgur.com/MzRmIS4.png)

还有一些其他缩减方法，如lasso、LAR、PCA回归以及子集选择等。与岭回归一样，这些方法不仅可以提高预测精确率，而且可以解释回归系数。

在增加如下约束时，普通的最小二乘法回归会得到与岭回归的一样的公式：

![](https://i.imgur.com/KurI4yr.png)

上式限定了所有回归系数的平方和不能大于lambda。使用普通的最小二乘法回归在当两个或更多的特征相关时，可能会得出一个很大的正系数和一个很大的负系数。正是因为上述限制条件的存在，使用岭回归可以避免这个问题。

与岭回归类似，另一个缩减方法lasso也对回归系数做了限定，对应的约束条件如下：

![](https://i.imgur.com/SLXZ5AR.png)

唯一的不同点在于，这个约束条件使用绝对值取代了平方和。虽然约束形式只是稍作变化，结果却大相径庭：在lambda足够小的时候，一些系数会因此被迫缩减到0，这个特性可以帮助我们更好地理解数据。这两个约束条件在公式上看起来相差无几，但细微的变化却极大地增加了计算复杂度（为了在这个新的约束条件下解出回归系数，需要使用二次规划算法）。

## 前向逐步回归
前向逐步回归属于一种贪心算法，即每一步都尽可能减少误差。一开始所有的权重都设为0，然后每一步所做的决策是对某个权重增加或减少一个很小的值。

该算法的伪代码如下所示：
```

	数据标准化，使其分布满足0均值和单位方差
	在每轮迭代过程中：
		设置当前最小误差lowestError为正无穷
		对每个特征：
			增大或缩小：
				改变一个系数得到一个新的W
				计算新W下的误差
				如果误差Error小于当前最小误差lowestError：设置Wbest等于当前的W
			将W设置为新的Wbest
```
### 前向逐步回归python代码实现
``` python

	def rssError(yArr,yHatArr): #yArr and yHatArr both need to be arrays
	    return ((yArr-yHatArr)**2).sum()

	def stageWise(xArr,yArr,eps=0.01,numIt=100):
	    xMat = mat(xArr); yMat=mat(yArr).T
	    yMean = mean(yMat,0)
	    yMat = yMat - yMean     #can also regularize ys but will get smaller coef
	    xMat = regularize(xMat)
	    m,n=shape(xMat)
	    returnMat = zeros((numIt,n)) #testing code remove
	    ws = zeros((n,1)); wsTest = ws.copy(); wsMax = ws.copy()
	    for i in range(numIt):#could change this to while loop
	        #print ws.T
	        lowestError = inf; 
	        for j in range(n):
	            for sign in [-1,1]:
	                wsTest = ws.copy()
	                wsTest[j] += eps*sign
	                yTest = xMat*wsTest
	                rssE = rssError(yMat.A,yTest.A)
	                if rssE < lowestError:
	                    lowestError = rssE
	                    wsMax = wsTest
	        ws = wsMax.copy()
	        returnMat[i,:]=ws.T
	    return returnMat
```

![](https://i.imgur.com/7dMvufp.png)

逐步线性回归，主要的优点在于它可以帮助人们理解现有的模型并做出改进。当构建了一个模型后，可以运行该算法找出重要的特征，这样就有可能及时停止对那些不重要特征的收集。

当应用缩减方法（如逐步线性回归或岭回归）时，模型也就增加了偏差（bias),与此同时却减少了模型的方差。


### 权衡偏差与方差
![](https://i.imgur.com/rrkbnxb.png)

误差由三个部分组成：偏差、误差和噪声。
