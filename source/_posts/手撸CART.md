---
title: 手撸CART
date: 2017-12-01 20:26:12 
categories: "机器学习" 
tags: 
     - 决策树
     - CART
     - regression tree
description: 手撸CART
toc: true
---
CART(Classification And Regression Trees)既可以用于分类还可以用于回归。

CART算法只做二元切分，所以这里可以固定树的数据结构。树包含左键和右键，可以存储另一棵子树或者单个值。字典还包含特征和特征值这两个键，它们给出切分算法所有的特征和特征值。

### 建立树节点：
``` python

	classtreeNode()：
		def __init__(self,feat,val,right,left)：
			featureToSplitOn = feat
			valueOfSplit = val
			rightBranch = right
			leftBranch = left
```

### 函数createTree()的伪代码大致如下：

```

	找到最佳的待切分特征：
		如果该节点不能再分，将该节点存为叶节点
		执行二元切分
		在右子树调用createTree()方法
		在左子树调用createTree()方法
```

<!--more-->

### CART算法的实现：

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
	
	def binSplitDataSet(dataSet, feature, value):
	    mat0 = dataSet[nonzero(dataSet[:,feature] > value)[0],:][0]
	    mat1 = dataSet[nonzero(dataSet[:,feature] <= value)[0],:][0]
	    return mat0,mat1

	def regLeaf(dataSet):#returns the value used for each leaf
	    return mean(dataSet[:,-1])
	
	def regErr(dataSet):
	    return var(dataSet[:,-1]) * shape(dataSet)[0]
	
	def linearSolve(dataSet):   #helper function used in two places
	    m,n = shape(dataSet)
	    X = mat(ones((m,n))); Y = mat(ones((m,1)))#create a copy of data with 1 in 0th postion
	    X[:,1:n] = dataSet[:,0:n-1]; Y = dataSet[:,-1]#and strip out Y
	    xTx = X.T*X
	    if linalg.det(xTx) == 0.0:
	        raise NameError('This matrix is singular, cannot do inverse,\n\
	        try increasing the second value of ops')
	    ws = xTx.I * (X.T * Y)
	    return ws,X,Y
	
	def modelLeaf(dataSet):#create linear model and return coeficients
	    ws,X,Y = linearSolve(dataSet)
	    return ws
	
	def modelErr(dataSet):
	    ws,X,Y = linearSolve(dataSet)
	    yHat = X * ws
	    return sum(power(Y - yHat,2))
	
	def chooseBestSplit(dataSet, leafType=regLeaf, errType=regErr, ops=(1,4)):
	    tolS = ops[0]; tolN = ops[1]
	    #if all the target variables are the same value: quit and return value
	    if len(set(dataSet[:,-1].T.tolist()[0])) == 1: #exit cond 1
	        return None, leafType(dataSet)
	    m,n = shape(dataSet)
	    #the choice of the best feature is driven by Reduction in RSS error from mean
	    S = errType(dataSet)
	    bestS = inf; bestIndex = 0; bestValue = 0
	    for featIndex in range(n-1):
	        for splitVal in set(dataSet[:,featIndex]):
	            mat0, mat1 = binSplitDataSet(dataSet, featIndex, splitVal)
	            if (shape(mat0)[0] < tolN) or (shape(mat1)[0] < tolN): continue
	            newS = errType(mat0) + errType(mat1)
	            if newS < bestS: 
	                bestIndex = featIndex
	                bestValue = splitVal
	                bestS = newS
	    #if the decrease (S-bestS) is less than a threshold don't do the split
	    if (S - bestS) < tolS: 
	        return None, leafType(dataSet) #exit cond 2
	    mat0, mat1 = binSplitDataSet(dataSet, bestIndex, bestValue)
	    if (shape(mat0)[0] < tolN) or (shape(mat1)[0] < tolN):  #exit cond 3
	        return None, leafType(dataSet)
	    return bestIndex,bestValue#returns the best feature to split on
	                              #and the value used for that split

	def createTree(dataSet, leafType=regLeaf, errType=regErr, ops=(1,4)):#assume dataSet is NumPy Mat so we can array filtering
	    feat, val = chooseBestSplit(dataSet, leafType, errType, ops)#choose the best split
	    if feat == None: return val #if the splitting hit a stop condition return val
	    retTree = {}
	    retTree['spInd'] = feat
	    retTree['spVal'] = val
	    lSet, rSet = binSplitDataSet(dataSet, feat, val)
	    retTree['left'] = createTree(lSet, leafType, errType, ops)
	    retTree['right'] = createTree(rSet, leafType, errType, ops)
	    return retTree  

```

### 树剪枝
通过降低决策树的复杂度来避免过拟合的过程称为剪枝。在chooseBestSplit()中的提前终止条件，实际上是在进行一种所谓的预剪枝操作。另一种形式的剪枝需要使用测试集和训练集，称为后剪枝。

停止条件对误差的数量级十分敏感，通过不断修改停止条件来得到合理结果并不是很好的办法。后剪枝，利用测试集来对树进行剪枝。由于不需要用户指定参数，后剪枝是一个更理想化的剪枝方法。

#### 后剪枝
函数prune()的伪代码如下：

```

	基于已有的树切分测试数据：
		如果存在任一子集是一棵树，则在该子集递归剪枝过程
		计算将当前两个叶节点合并后的误差
		计算不合并的误差
		如果合并会降低误差的话，就将叶节点合并
```

回归树剪枝函数Python代码：

``` python

	def isTree(obj):
	    return (type(obj).__name__=='dict')
	
	def getMean(tree):
	    if isTree(tree['right']): tree['right'] = getMean(tree['right'])
	    if isTree(tree['left']): tree['left'] = getMean(tree['left'])
	    return (tree['left']+tree['right'])/2.0
	    
	def prune(tree, testData):
	    if shape(testData)[0] == 0: return getMean(tree) #if we have no test data collapse the tree
	    if (isTree(tree['right']) or isTree(tree['left'])):#if the branches are not trees try to prune them
	        lSet, rSet = binSplitDataSet(testData, tree['spInd'], tree['spVal'])
	    if isTree(tree['left']): tree['left'] = prune(tree['left'], lSet)
	    if isTree(tree['right']): tree['right'] =  prune(tree['right'], rSet)
	    #if they are now both leafs, see if we can merge them
	    if not isTree(tree['left']) and not isTree(tree['right']):
	        lSet, rSet = binSplitDataSet(testData, tree['spInd'], tree['spVal'])
	        errorNoMerge = sum(power(lSet[:,-1] - tree['left'],2)) +\
	            sum(power(rSet[:,-1] - tree['right'],2))
	        treeMean = (tree['left']+tree['right'])/2.0
	        errorMerge = sum(power(testData[:,-1] - treeMean,2))
	        if errorMerge < errorNoMerge: 
	            print "merging"
	            return treeMean
	        else: return tree
	    else: return tree
```




