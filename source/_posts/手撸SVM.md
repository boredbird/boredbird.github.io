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

<!--more-->

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

Platt SMO 算法是通过一个外循环来选择第一个alpha值的，并且其选择过程会在两种方式之间进行交替：一种方式是在所有数据集上进行单遍扫描，另一种方式则是在非边界alpha中实现单遍扫描。而所谓非边界alpha指的就是那些不等于边界0或C的alpha值。对整个数据集的扫描相当容易，而实现非边界alpha值的扫描时，首先需要建立这些alpha值的列表，然后再对这个表进行遍历。同时，该步骤会跳过那些已知的不会改变的alpha值。

在选择第一个alpha值后，算法会通过一个内循环来选择第二个alpha值 。在优化过程中，会通过最大化步长的方式来获得第二个alpha值。在简化版SMO算法中，我们会在选择*j*之后计算错误率*E_j*。但在这里，我们会建立一个全局的缓存用于保存误差值，并从中选择使得步长或者说*E_i-E_j*最大的alpha值。

#### 完整Platt SMO的辅助函数
``` python

	class optStruct:
	    def __init__(self, dataMatIn, classLabels, C, toler, kTup):  # Initialize the structure with the parameters
	        self.X = dataMatIn
	        self.labelMat = classLabels
	        self.C = C
	        self.tol = toler
	        self.m = shape(dataMatIn)[0]
	        self.alphas = mat(zeros((self.m, 1)))
	        self.b = 0
	        self.eCache = mat(zeros((self.m, 2)))  # first column is valid flag
	        self.K = mat(zeros((self.m, self.m)))
	        for i in range(self.m):
	            self.K[:, i] = kernelTrans(self.X, self.X[i, :], kTup)
	
	
	def calcEk(oS, k):
	    fXk = float(multiply(oS.alphas, oS.labelMat).T * oS.K[:, k] + oS.b)
	    Ek = fXk - float(oS.labelMat[k])
	    return Ek
	
	
	def selectJ(i, oS, Ei):  # this is the second choice -heurstic, and calcs Ej
	    maxK = -1
	    maxDeltaE = 0
	    Ej = 0
	    oS.eCache[i] = [1, Ei]  # set valid #choose the alpha that gives the maximum delta E
	    validEcacheList = nonzero(oS.eCache[:, 0].A)[0]
	    if (len(validEcacheList)) > 1:
	        for k in validEcacheList:  # loop through valid Ecache values and find the one that maximizes delta E
	            if k == i: continue  # don't calc for i, waste of time
	            Ek = calcEk(oS, k)
	            deltaE = abs(Ei - Ek)
	            if (deltaE > maxDeltaE):
	                maxK = k
	                maxDeltaE = deltaE
	                Ej = Ek
	        return maxK, Ej
	    else:  # in this case (first time around) we don't have any valid eCache values
	        j = selectJrand(i, oS.m)
	        Ej = calcEk(oS, j)
	    return j, Ej
	
	
	def updateEk(oS, k):  # after any alpha has changed update the new value in the cache
	    Ek = calcEk(oS, k)
	    oS.eCache[k] = [1, Ek]

```

首要的事情就是建立一个数据结构来保存所有的重要值，而这个过程可以通过一个对象来完成。这里使用对象的目的并不是为了面向对象的编程，而只是作为一个数据结构来使用对象。在将值传给函数时，我们可以通过将所有数据移到一个结构中来实现，这样就可以省掉手工输入的麻烦了。而此时，数据就可以通过一个对象来进行传递。实际上，当完成其实现时，可以很容易通过Python的字典来完成。但是在访问对象成员变量时，这样做会有更多的手工输入操作，对比一下myObject.X和myObject['X']就可以知道这一点。为达到这个目的，需要构建一个仅包含init方法的optStruct类。该方法可以实现其成员变量的填充。除了增加一个m*2的矩阵成员变量eCache之外，这些做法和简化SMO一模一样。eCache的第一列给出的是eCache是否有效的标志位，而第二列给出的是实际的E值。

对于给定的alpha值，第一个辅助函数calcEk()能够计算*E*值并返回。以前，该过程是采用内嵌的方式来完成的，这里作为单独的函数。

下一个函数selectJ()用于选择第二个alpha或者说内循环的alpha值。目标是选择合适的第二个alpha值以保证在每次优化中采用最大步长。该函数的误差值与第一个alpha值*E_i*和下标*i*有关。首先将输入值*E_i*在缓存中设置成为有效的。这里的有效意味着它已经计算好了。在eCaohe中，代码nonzero(oS.eCache[:,0].A)[0]构建出了一个非零表。NumPy函数nonzero()返回了一个列表，而这个列表中包含以输入列表为目录的列表值。nonzero()语句返回的是非零E值所对应的alpha值，而不是E值本身。程序会在所有的值上进行循环并选择其中使得改变最大的那个值。如果这是第一次循环的话，那么就随机选择一个alpha值。

最后一个辅助函数updateEk(),它会计算误差值并存入缓存当中。在对alpha值进行优化之后会用到这个值。

#### 完整Platt SMO算法中的优化部分
``` python

	def innerL(i, oS):
	    Ei = calcEk(oS, i)
	    if ((oS.labelMat[i] * Ei < -oS.tol) and (oS.alphas[i] < oS.C)) or (
	        (oS.labelMat[i] * Ei > oS.tol) and (oS.alphas[i] > 0)):
	        j, Ej = selectJ(i, oS, Ei)  # this has been changed from selectJrand
	        alphaIold = oS.alphas[i].copy()
	        alphaJold = oS.alphas[j].copy()
	        if (oS.labelMat[i] != oS.labelMat[j]):
	            L = max(0, oS.alphas[j] - oS.alphas[i])
	            H = min(oS.C, oS.C + oS.alphas[j] - oS.alphas[i])
	        else:
	            L = max(0, oS.alphas[j] + oS.alphas[i] - oS.C)
	            H = min(oS.C, oS.alphas[j] + oS.alphas[i])
	        if L == H:
	            print "L==H"
	            return 0
	        eta = 2.0 * oS.K[i, j] - oS.K[i, i] - oS.K[j, j]  # changed for kernel
	        if eta >= 0:
	            print "eta>=0"
	            return 0
	        oS.alphas[j] -= oS.labelMat[j] * (Ei - Ej) / eta
	        oS.alphas[j] = clipAlpha(oS.alphas[j], H, L)
	        updateEk(oS, j)  # added this for the Ecache
	        if (abs(oS.alphas[j] - alphaJold) < 0.00001):
	            print "j not moving enough"
	            return 0
	        oS.alphas[i] += oS.labelMat[j] * oS.labelMat[i] * (alphaJold - oS.alphas[j])  # update i by the same amount as j
	        updateEk(oS, i)  # added this for the Ecache                    #the update is in the oppostie direction
	        b1 = oS.b - Ei - oS.labelMat[i] * (oS.alphas[i] - alphaIold) * oS.K[i, i] - oS.labelMat[j] * (
	        oS.alphas[j] - alphaJold) * oS.K[i, j]
	        b2 = oS.b - Ej - oS.labelMat[i] * (oS.alphas[i] - alphaIold) * oS.K[i, j] - oS.labelMat[j] * (
	        oS.alphas[j] - alphaJold) * oS.K[j, j]
	        if (0 < oS.alphas[i]) and (oS.C > oS.alphas[i]):
	            oS.b = b1
	        elif (0 < oS.alphas[j]) and (oS.C > oS.alphas[j]):
	            oS.b = b2
	        else:
	            oS.b = (b1 + b2) / 2.0
	        return 1
	    else:
	        return 0

```
使用SelectJ()而不是selectJrand()来选择第二个alpha值。最后，在alpha值改变时更新Ecache.

#### 完整版Platt SMO的外循环代码
``` python

	def smoP(dataMatIn, classLabels, C, toler, maxIter, kTup=('lin', 0)):  # full Platt SMO
	    oS = optStruct(mat(dataMatIn), mat(classLabels).transpose(), C, toler, kTup)
	    iter = 0
	    entireSet = True
	    alphaPairsChanged = 0
	    while (iter < maxIter) and ((alphaPairsChanged > 0) or (entireSet)):
	        alphaPairsChanged = 0
	        if entireSet:  # go over all
	            for i in range(oS.m):
	                alphaPairsChanged += innerL(i, oS)
	                print "fullSet, iter: %d i:%d, pairs changed %d" % (iter, i, alphaPairsChanged)
	            iter += 1
	        else:  # go over non-bound (railed) alphas
	            nonBoundIs = nonzero((oS.alphas.A > 0) * (oS.alphas.A < C))[0]
	            for i in nonBoundIs:
	                alphaPairsChanged += innerL(i, oS)
	                print "non-bound, iter: %d i:%d, pairs changed %d" % (iter, i, alphaPairsChanged)
	            iter += 1
	        if entireSet:
	            entireSet = False  # toggle entire set loop
	        elif (alphaPairsChanged == 0):
	            entireSet = True
	        print "iteration number: %d" % iter
	    return oS.b, oS.alphas
```
完整版的Platt SMO算法，其输入和函数smoSimple()完全一样。函数一开始构建一个数据结构来容纳所有的数据，然后需要对控制函数退出的一些变量进行初始化。整个代码的主体是while循环，这与smosimple（）有些类似，但是这里的循环退出条件更多一些。当迭代次数超过指定的最大值，或者遍历整个集合都未对任意alpha对进行修改时，就退出循环。这里的maxIter变量和函数smoSimple()中的作用有一点不同，后者当没有任何alpha发生改变时会将整个集合的一次遍历过程记成一次迭代，而这里的一次迭代定义为一次循环过程，而不管该循环具体做了什么事。此时，如果在优化过程中存在波动就会停止，因此这里的做法优于SMOSimple()函数中的计数方法。

while循环的内部与smoSimple()中有所不同，一开始的for循环在数据集上遍历任意可能的alpha。我们通过调用innerL()来选择第二个alpha，并在可能时对其进行优化处理。如果有任意一对alpha值发生改变，那么会返回1.第二个for循环遍历所有的非边界alpha值，也就是不在边界0或C上的值。

## 核函数
SVM优化中一个特别好的地方就是，所有的运算都可以写成内积的形式。可以把内积运算替换成核函数，而不必做简化处理。将内积替换成核函数的方式被称为核技巧(kernel trick)。

### 径向基核函数
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig16.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 核转换函数

``` python

	def kernelTrans(X, A, kTup):  # calc the kernel or transform data to a higher dimensional space
	    m, n = shape(X)
	    K = mat(zeros((m, 1)))
	    if kTup[0] == 'lin':
	        K = X * A.T  # linear kernel
	    elif kTup[0] == 'rbf':
	        for j in range(m):
	            deltaRow = X[j, :] - A
	            K[j] = deltaRow * deltaRow.T
	        K = exp(K / (-1 * kTup[1] ** 2))  # divide in NumPy is element-wise not matrix like Matlab
	    else:
	        raise NameError('Houston We Have a Problem -- \
	    That Kernel is not recognized')
	    return K
	
	
	class optStruct:
	    def __init__(self, dataMatIn, classLabels, C, toler, kTup):  # Initialize the structure with the parameters
	        self.X = dataMatIn
	        self.labelMat = classLabels
	        self.C = C
	        self.tol = toler
	        self.m = shape(dataMatIn)[0]
	        self.alphas = mat(zeros((self.m, 1)))
	        self.b = 0
	        self.eCache = mat(zeros((self.m, 2)))  # first column is valid flag
	        self.K = mat(zeros((self.m, self.m)))
	        for i in range(self.m):
	            self.K[:, i] = kernelTrans(self.X, self.X[i, :], kTup)
	
```

其中kTup是一个包含核函数信息的元组。元组的第一个参数是描述所用核函数类型的一个字符串，其他2个参数则都是核函数可能需要的可选参数。在初始化方法结束时，矩阵k先被构建，然后再通过调用函数kernelTrans()进行填充。全局的k值只需计算一次。然后，当想要使用核函数时，就可以对它进行调用。

via

* 《机器学习实战》