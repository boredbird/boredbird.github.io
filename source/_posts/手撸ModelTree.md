---
title: 手撸ModelTree
date: 2017-12-01 20:26:12 
categories: "机器学习" 
tags: 
     - 决策树
     - model tree
description: 手撸ModelTree
toc: true
---
## 模型树
用树来对数据建模，除了把叶节点简单地设定为常数值之外，还有一种方法是把也节点设定为分段线性函数，这里所谓的分段线性(piecewis linear)是指模型由多个线性片段组成。即分段线性模型。

相比CART，叶节点误差的计算需要稍加变化，对于给定的数据集，应该先用线性的模型来对它进行拟合，然后计算真实值与预测值的差值。最后将这些差值的平方求和就得到了所需的误差。

### 叶节点误差的计算：

``` python

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

```

<!--more-->

### 用树回归进行预测的代码：
``` python

	def regTreeEval(model, inDat):
	    return float(model)
	
	def modelTreeEval(model, inDat):
	    n = shape(inDat)[1]
	    X = mat(ones((1,n+1)))
	    X[:,1:n+1]=inDat
	    return float(X*model)
	
	def treeForeCast(tree, inData, modelEval=regTreeEval):
	    if not isTree(tree): return modelEval(tree, inData)
	    if inData[tree['spInd']] > tree['spVal']:
	        if isTree(tree['left']): return treeForeCast(tree['left'], inData, modelEval)
	        else: return modelEval(tree['left'], inData)
	    else:
	        if isTree(tree['right']): return treeForeCast(tree['right'], inData, modelEval)
	        else: return modelEval(tree['right'], inData)
	        
	def createForeCast(tree, testData, modelEval=regTreeEval):
	    m=len(testData)
	    yHat = mat(zeros((m,1)))
	    for i in range(m):
	        yHat[i,0] = treeForeCast(tree, mat(testData[i]), modelEval)
	    return yHat
```
调用函数treeForeCast()时需要指定树的类型，以便在叶节点上能够调用合适的模型。参数modelEval是对叶节点数据进行预测的函数的引用。treeForeCast()自顶向下遍历整棵树，直到命中叶节点为止。一旦到达叶节点，它就会在输入数据上调用modelEval()函数，而该函数的默认值是regTreeEval()。

若叶节点使用的模型是分段常数则称为回归树，若叶节点使用的模型是线性回归方程则成为模型树。
