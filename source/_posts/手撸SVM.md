---
title: 手撸SVM
date: 2017-11-16 20:26:12 
categories: "机器学习" 
tags: 
     - SVM
     - SMO
description: 手撸SVM
toc: true
---
## 基于最大间隔分隔数据
* 优点：泛化错误率低，计算开销不大，结果易解释。
* 缺点：对参数调节和核函数的选择敏感，原始分类器不加修改仅适用于处理二类问题。
* 适用数据类型：数值型和标称型数据。

## SMO伪代码

```

	创建一个alpha向量并将其初始化为0向量
	当迭代次数小于最大迭代次数时（外循环）
		对数据集中的每个数据向量（内循环）：
			如果该数据向量可以被优化：
				随机选择另外一个数据向量
				同时优化这两个向量
				如果两个向量都不能被优化，退出内循环
		如果所有向量都没被优化，增加迭代数目，继续下一次循环
```
## SMO代码实现
首先定义一些SMO算法中的辅助函数
``` python

	def loadDataSet(fileName):
	    dataMat = []
	    labelMat = []
	    fr = open(fileName)
	    for line in fr.readlines():
	        lineArr = line.strip().split('\t')
	        dataMat.append([float(lineArr[0]), float(lineArr[1])])
	        labelMat.append(float(lineArr[2]))
	    return dataMat, labelMat
	
	
	def selectJrand(i, m):
	    j = i  # we want to select any J not equal to i
	    while (j == i):
	        j = int(random.uniform(0, m))
	    return j
	
	
	def clipAlpha(aj, H, L):
	    if aj > H:
	        aj = H
	    if L > aj:
	        aj = L
	    return aj
```

### 简化版SMO算法

``` python

	def smoSimple(dataMatIn, classLabels, C, toler, maxIter):
	    dataMatrix = mat(dataMatIn)
	    labelMat = mat(classLabels).transpose()
	    b = 0
	    m, n = shape(dataMatrix)
	    alphas = mat(zeros((m, 1)))
	    iter = 0
	    while (iter < maxIter):
	        alphaPairsChanged = 0
	        for i in range(m):
	            fXi = float(multiply(alphas, labelMat).T * (dataMatrix * dataMatrix[i, :].T)) + b
	            Ei = fXi - float(labelMat[i])  # if checks if an example violates KKT conditions
	            if ((labelMat[i] * Ei < -toler) and (alphas[i] < C)) or ((labelMat[i] * Ei > toler) and (alphas[i] > 0)):
	                j = selectJrand(i, m)
	                fXj = float(multiply(alphas, labelMat).T * (dataMatrix * dataMatrix[j, :].T)) + b
	                Ej = fXj - float(labelMat[j])
	                alphaIold = alphas[i].copy()
	                alphaJold = alphas[j].copy()
	                if (labelMat[i] != labelMat[j]):
	                    L = max(0, alphas[j] - alphas[i])
	                    H = min(C, C + alphas[j] - alphas[i])
	                else:
	                    L = max(0, alphas[j] + alphas[i] - C)
	                    H = min(C, alphas[j] + alphas[i])
	                if L == H:
	                    print "L==H"
	                    continue
	                eta = 2.0 * dataMatrix[i, :] * dataMatrix[j, :].T - dataMatrix[i, :] * dataMatrix[i, :].T - dataMatrix[j,:] * dataMatrix[j, :].T
	                if eta >= 0:
	                    print "eta>=0"
	                    continue
	                alphas[j] -= labelMat[j] * (Ei - Ej) / eta
	                alphas[j] = clipAlpha(alphas[j], H, L)
	                if (abs(alphas[j] - alphaJold) < 0.00001):
	                    print "j not moving enough"
	                    continue
	                alphas[i] += labelMat[j] * labelMat[i] * (alphaJold - alphas[j])  # update i by the same amount as j
	                # the update is in the oppostie direction
	                b1 = b - Ei - labelMat[i] * (alphas[i] - alphaIold) * dataMatrix[i, :] * dataMatrix[i, :].T - labelMat[j] * (alphas[j] - alphaJold) * dataMatrix[i,:] * dataMatrix[j,:].T
	                b2 = b - Ej - labelMat[i] * (alphas[i] - alphaIold) * dataMatrix[i, :] * dataMatrix[j, :].T - labelMat[j] * (alphas[j] - alphaJold) * dataMatrix[j,:] * dataMatrix[j,:].T
	                if (0 < alphas[i]) and (C > alphas[i]):
	                    b = b1
	                elif (0 < alphas[j]) and (C > alphas[j]):
	                    b = b2
	                else:
	                    b = (b1 + b2) / 2.0
	                alphaPairsChanged += 1
	                print "iter: %d i:%d, pairs changed %d" % (iter, i, alphaPairsChanged)
	        if (alphaPairsChanged == 0):
	            iter += 1
	        else:
	            iter = 0
	        print "iteration number: %d" % iter
	    return b, alphas
```

上面函数有5个输入参数，分别是：数据集、类别标签、常数C、容错率和取消前最大的循环次数。函数将多个列表和输入参数转换成NumPy矩阵，这样就可以简化很多数学处理操作。由于转置了类别标签，因此我们得到的就是一个列向量而不是列表。于是类别标签向量的每行元素都和数据矩阵中的行一一对应。构建一个alpha列矩阵，矩阵中元素都初始化为0，并建立一个iter变量。该变量存储的则是没有任何alpha改变的情况下遍历数据集的次数。当该变量达到输入值maxIter时，函数结束运行并退出。

每次循环当中，将alphaParirsChanged先设为0，然后再对整个集合顺序遍历。变量alphaPairsChanged用于记录alpha是否已经进行优化。

首先，fxi能够计算出来，这就是我们预测的类别。然后，基于这个实例的预测结果和真是结果的比对，就可以计算误差Ei。如果误差很大，那么可以对该数据实例所对应的alpha值进行优化。在if语句中，不管是正间隔还是负间隔都会被测试。并且在该if语句中，也要同时检查alpha值，以保证其不能等于0或C。由于后面alpha小于0或大于C时将调整为0或C，所以一旦在该if语句中它们等于这两个值得话，那么它们就已经在“边界”上了，因而不再能够减少或增大，因此也就不值得再对它们进行优化了。

接下来，利用辅助函数来随机选择第二个alpha值，即alpha[j]。同样，可以采用第一个alpha值（alpha[i]）的误差计算方法，来计算这个alpha值得误差。这个过程可以通过copy（）的方法来实现，因此稍后可以将新的alpha值与老的alpha值进行比较。之后开始计算L和H，它们用于将alpha[j]调整到0到C之间。如果L和H相等，就不做任何改变，直接执行continue语句。

Eta是alpha[j]的最优修改量，如果eta为0，那就是说需要退出for循环的当前迭代过程。该过程对真实SMO算法进行了简化处理。于是，可以计算出一个新的alpha[j]，然后利用辅助函数以及L和H值对其进行调整。

然后，就是检查alpha[j]是否轻微改变。如果是的话，就退出for循环。然后alpha[i]和alpha[j]同样进行改变，虽然改变的大小一样，但是改变的方向正好相反（即如果一个增加，那么另外一个减少）。在对alpha[i]和alpha[j]进行优化之后，给这两个alpha值设置一个常数项b。

最后，在优化过程结束的同时，必须确保在合适的时机结束循环。如果程序执行到for循环的最后一行都不执行continue语句，那么就已经成功地改变了一对alpha，同时可以增加alphaPairsChanged的值。在for循环之外，需要检查alpha值是否做了更新，如果有更新则将iter设为0后继续运行程序。只有在所有数据集上遍历maxIter次，且不再发生任何alpha修规之后，程序才会停止并退出while循环。

### 利用完整Platt SMO算法加速优化
在这两个版本中，实现alpha的更改和代数运算的优化环节一模一样。在优化过程中，唯一的不同就是选择alpha的方式。完整版的Platt SMO算法应用了一些能够提速的启发方法。

