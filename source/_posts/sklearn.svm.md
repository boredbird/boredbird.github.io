---
title: sklearn.svm
date: 2017-11-14 22:06:12 
categories: "机器学习" 
tags: 
     - sklearn
     - svm
     - SVC
     - SVR
     - train_test_split
     - GridSearchCV
     - precision_score
     - recall_score
     - f1_score
     - fbeta_score
     - precision_recall_fscore_support
     - classification_report
description: sklearn.svm
toc: true
---

### SVC:ovr
``` python

	import numpy as np
	from sklearn import svm
	from sklearn.model_selection import train_test_split
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	from sklearn.datasets import load_iris
	iris = load_iris()
	X = iris.data[:, :2]
	y = iris.target
	x_train, x_test, y_train, y_test = train_test_split(X, y, train_size=0.7, random_state=1)
	
	# 'sepal length', 'sepal width', 'petal length', 'petal width'
	iris_feature = u'花萼长度', u'花萼宽度', u'花瓣长度', u'花瓣宽度'
	
	def iris_type(s):
	    it = {'Iris-setosa': 0, 'Iris-versicolor': 1, 'Iris-virginica': 2}
	    return it[s]
	
	def show_accuracy(a, b, tip):
	    acc = a.ravel() == b.ravel()
	    print tip + '正确率：', np.mean(acc)
	
	# 分类器
	# clf = svm.SVC(C=0.1, kernel='linear', decision_function_shape='ovr')
	# ‘ovo’ 一对一, ‘ovr’ 多对多  or None 无, default=None
	clf = svm.SVC(C=0.8, kernel='rbf', gamma=20, decision_function_shape='ovr')
	clf.fit(x_train, y_train.ravel())
	
	# 准确率
	# score(X, y, sample_weight=None) ：Returns the mean accuracy on the given test data and labels.
	print clf.score(x_train, y_train)  # 精度
	y_hat = clf.predict(x_train)
	show_accuracy(y_hat, y_train, '训练集')
	print clf.score(x_test, y_test)
	y_hat = clf.predict(x_test)
	show_accuracy(y_hat, y_test, '测试集')
	
	# decision_function
	print 'decision_function:\n', clf.decision_function(x_train)
	print '\npredict:\n', clf.predict(x_train)
	"""
	# decision_function(): Distance of the samples X to the separating hyperplane.
	# 分类归属于距离数值最小的类别，距离有正有负只是平面的两侧而已
	decision_function:
	[[-0.25631211  0.80529378  2.45101833]
	 [ 2.35232967  0.82494155 -0.17727121]
	 [ 2.45418203  0.77495649 -0.22913852]
	 [ 2.45421283  0.77518383 -0.22939666]
	 [-0.24854074  2.39614366  0.85239708]
	 [ 2.46621083  0.76927647 -0.23548729]
	 [ 2.45410944  0.77775367 -0.2318631 ]
	 [-0.24677667  0.84905678  2.39771989]
	 [-0.46050688  1.21154683  2.24896005]
	 [-0.26893412  0.80449581  2.46443831]
	
	predict:
	[2 0 0 0 1 0 0 2 2 2
	"""
	
	# 画图
	x1_min, x1_max = X[:, 0].min(), X[:, 0].max()  # 第0列的范围
	x2_min, x2_max = X[:, 1].min(), X[:, 1].max()  # 第1列的范围
	x1, x2 = np.mgrid[x1_min:x1_max:200j, x2_min:x2_max:200j]  # 生成网格采样点
	# numpy.ndarray.flat : A 1-D iterator over the array.
	# This is a numpy.flatiter instance, which acts similarly to,
	# but is not a subclass of, Python’s built-in iterator object.
	grid_test = np.stack((x1.flat, x2.flat), axis=1)  # 测试点
	# print 'grid_test = \n', grid_test
	# Z = clf.decision_function(grid_test)    # 样本到决策面的距离
	# print Z
	grid_hat = clf.predict(grid_test)       # 预测分类值
	print grid_hat
	grid_hat = grid_hat.reshape(x1.shape)  # 使之与输入的形状相同
	mpl.rcParams['font.sans-serif'] = [u'SimHei']
	mpl.rcParams['axes.unicode_minus'] = False
	
	cm_light = mpl.colors.ListedColormap(['#A0FFA0', '#FFA0A0', '#A0A0FF'])
	cm_dark = mpl.colors.ListedColormap(['g', 'r', 'b'])
	plt.pcolormesh(x1, x2, grid_hat, cmap=cm_light)
	
	plt.scatter(X[:, 0], X[:, 1], c=y, edgecolors='k', s=50, cmap=cm_dark)      # 样本
	plt.scatter(x_test[:, 0], x_test[:, 1], s=120, facecolors='none', zorder=10)     # 圈中测试集样本
	plt.xlabel(iris_feature[0], fontsize=13)
	plt.ylabel(iris_feature[1], fontsize=13)
	plt.xlim(x1_min, x1_max)
	plt.ylim(x2_min, x2_max)
	plt.title(u'鸢尾花SVM二特征分类', fontsize=15)
	plt.grid()
	plt.show()
```
#### 输出：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/Figure_1.png" width="80%">
  <div class="figcaption">
  </div>
</div>

<!--more-->

### SVC:ovo
``` python

	import numpy as np
	from sklearn import svm
	from scipy import stats
	from sklearn.metrics import accuracy_score
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	
	def extend(a, b, r):
	    x = a - b
	    m = (a + b) / 2
	    return m-r*x/2, m+r*x/2
	
	np.random.seed(0)
	N = 20
	x = np.empty((4*N, 2))
	means = [(-1, 1), (1, 1), (1, -1), (-1, -1)]
	sigmas = [np.eye(2), 2*np.eye(2), np.diag((1,2)), np.array(((2,1),(1,2)))]
	for i in range(4):
	    # scipy.stats.multivariate_normal:
	    # A multivariate normal random variable.
	    # The mean keyword specifies the mean. The cov keyword specifies the covariance matrix.
	    mn = stats.multivariate_normal(means[i], sigmas[i]*0.3)
	    # rvs(mean=None, cov=1)	Draw random samples from a multivariate normal distribution.
	    x[i*N:(i+1)*N, :] = mn.rvs(N)
	
	a = np.array((0,1,2,3)).reshape((-1, 1))
	y = np.tile(a, N).flatten()
	clf = svm.SVC(C=1, kernel='rbf', gamma=1, decision_function_shape='ovo')
	# clf = svm.SVC(C=1, kernel='linear', decision_function_shape='ovr')
	clf.fit(x, y)
	y_hat = clf.predict(x)
	acc = accuracy_score(y, y_hat)
	np.set_printoptions(suppress=True)
	print u'预测正确的样本个数：%d，正确率：%.2f%%' % (round(acc*4*N), 100*acc)
	# decision_function
	print clf.decision_function(x)
	# print y_hat
	
	x1_min, x2_min = np.min(x, axis=0)
	x1_max, x2_max = np.max(x, axis=0)
	x1_min, x1_max = extend(x1_min, x1_max, 1.05)
	x2_min, x2_max = extend(x2_min, x2_max, 1.05)
	x1, x2 = np.mgrid[x1_min:x1_max:500j, x2_min:x2_max:500j]
	x_test = np.stack((x1.flat, x2.flat), axis=1)
	y_test = clf.predict(x_test)
	y_test = y_test.reshape(x1.shape)
	cm_light = mpl.colors.ListedColormap(['#FF8080', '#A0FFA0', '#6060FF', '#F080F0'])
	cm_dark = mpl.colors.ListedColormap(['r', 'g', 'b', 'm'])
	mpl.rcParams['font.sans-serif'] = [u'SimHei']
	mpl.rcParams['axes.unicode_minus'] = False
	plt.figure(facecolor='w')
	plt.pcolormesh(x1, x2, y_test, cmap=cm_light)
	plt.scatter(x[:, 0], x[:, 1], s=40, c=y, cmap=cm_dark, alpha=0.7)
	plt.xlim((x1_min, x1_max))
	plt.ylim((x2_min, x2_max))
	plt.grid(b=True)
	plt.tight_layout(pad=2.5)
	plt.title(u'SVM多分类方法：One/One or One/Other', fontsize=18)
	plt.show()
```
#### 输出：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/Figure_2.png" width="80%">
  <div class="figcaption">
  </div>
</div>


### 参数选择:linear/rbf,c,gamma
``` python

	from sklearn.model_selection import train_test_split
	from sklearn.datasets import load_iris
	import numpy as np
	from sklearn import svm
	import matplotlib as mpl
	import matplotlib.colors
	import matplotlib.pyplot as plt
	
	iris = load_iris()
	X = iris.data
	y = iris.target
	
	X = X[y != 0, :2]
	y = y[y != 0]
	x_train, x_test, y_train, y_test = train_test_split(X, y, train_size=0.7, random_state=1)
	
	# 'sepal length', 'sepal width', 'petal length', 'petal width'
	iris_feature = u'花萼长度', u'花萼宽度', u'花瓣长度', u'花瓣宽度'
	
	def iris_type(s):
	    it = {'Iris-setosa': 0, 'Iris-versicolor': 1, 'Iris-virginica': 2}
	    return it[s]
	
	def show_accuracy(a, b):
	    acc = a.ravel() == b.ravel()
	    print '正确率：%.2f%%' % (100*float(acc.sum()) / a.size)
	
	# 分类器
	clf_param = (('linear', 0.1), ('linear', 0.5), ('linear', 1), ('linear', 2),
	            ('rbf', 1, 0.1), ('rbf', 1, 1), ('rbf', 1, 10), ('rbf', 1, 100),
	            ('rbf', 5, 0.1), ('rbf', 5, 1), ('rbf', 5, 10), ('rbf', 5, 100))
	x1_min, x1_max = X[:, 0].min(), X[:, 0].max()  # 第0列的范围
	x2_min, x2_max = X[:, 1].min(), X[:, 1].max()  # 第1列的范围
	x1, x2 = np.mgrid[x1_min:x1_max:200j, x2_min:x2_max:200j]  # 生成网格采样点
	grid_test = np.stack((x1.flat, x2.flat), axis=1)  # 测试点
	
	cm_light = mpl.colors.ListedColormap(['#77E0A0', '#FFA0A0'])
	cm_dark = mpl.colors.ListedColormap(['g', 'r'])
	mpl.rcParams['font.sans-serif'] = [u'SimHei']
	mpl.rcParams['axes.unicode_minus'] = False
	plt.figure(figsize=(14, 10), facecolor='w')
	for i, param in enumerate(clf_param):
	    clf = svm.SVC(C=param[1], kernel=param[0])
	    if param[0] == 'rbf':
	        clf.gamma = param[2]
	        title = u'高斯核，C=%.1f，$\gamma$ =%.1f' % (param[1], param[2])
	    else:
	        title = u'线性核，C=%.1f' % param[1]
	
	    clf.fit(X, y)
	    y_hat = clf.predict(X)
	    show_accuracy(y_hat, y)  # 准确率
	
	    # 画图
	    print title
	    print '支撑向量的数目：', clf.n_support_
	    print '支撑向量的系数：', clf.dual_coef_
	    print '支撑向量：', clf.support_
	    plt.subplot(3, 4, i+1)
	    grid_hat = clf.predict(grid_test)       # 预测分类值
	    grid_hat = grid_hat.reshape(x1.shape)  # 使之与输入的形状相同
	    plt.pcolormesh(x1, x2, grid_hat, cmap=cm_light, alpha=0.8)
	    plt.scatter(X[:, 0], X[:, 1], c=y, edgecolors='k', s=40, cmap=cm_dark)      # 样本的显示
	    plt.scatter(X[clf.support_, 0], X[clf.support_, 1], edgecolors='k', facecolors='none', s=100, marker='o')   # 支撑向量
	    z = clf.decision_function(grid_test)
	    # print 'z = \n', z
	    z = z.reshape(x1.shape)
	    plt.contour(x1, x2, z, colors=list('kmrmk'), linestyles=['--', '-.', '-', '-.', '--'], linewidths=[1, 0.5, 1.5, 0.5, 1], levels=[-1, -0.5, 0, 0.5, 1])
	    plt.xlim(x1_min, x1_max)
	    plt.ylim(x2_min, x2_max)
	    plt.title(title, fontsize=14)
	plt.suptitle(u'SVM不同参数的分类', fontsize=20)
	plt.tight_layout(1.4)
	plt.subplots_adjust(top=0.92)
	plt.savefig('1.png')
	plt.show()
```
#### 输出：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/QQ截图20171114171330.png" width="80%">
  <div class="figcaption">
  </div>
</div>


### sklearn.metrics模型评价指标：
``` python

	import numpy as np
	from sklearn.metrics import accuracy_score
	from sklearn.metrics import precision_score, recall_score, f1_score, fbeta_score
	from sklearn.metrics import precision_recall_fscore_support, classification_report
	
	y_true = np.array([1, 1, 1, 1, 0, 0])
	y_hat = np.array([1, 0, 1, 1, 1, 1])
	print 'Accuracy：\t', accuracy_score(y_true, y_hat)
	
	# The precision is the ratio 'tp / (tp + fp)' where 'tp' is the number of
	# true positives and 'fp' the number of false positives. The precision is
	# intuitively the ability of the classifier not to label as positive a sample
	# that is negative.
	# The best value is 1 and the worst value is 0.
	precision = precision_score(y_true, y_hat)
	print 'Precision:\t', precision
	
	# The recall is the ratio 'tp / (tp + fn)' where 'tp' is the number of
	# true positives and 'fn' the number of false negatives. The recall is
	# intuitively the ability of the classifier to find all the positive samples.
	# The best value is 1 and the worst value is 0.
	recall = recall_score(y_true, y_hat)
	print 'Recall:  \t', recall
	
	# F1 score, also known as balanced F-score or F-measure
	# The F1 score can be interpreted as a weighted average of the precision and
	# recall, where an F1 score reaches its best value at 1 and worst score at 0.
	# The relative contribution of precision and recall to the F1 score are
	# equal. The formula for the F1 score is:
	#     F1 = 2 * (precision * recall) / (precision + recall)
	print 'f1 score: \t', f1_score(y_true, y_hat)
	print 2 * (precision * recall) / (precision + recall)
	
	# The F-beta score is the weighted harmonic mean of precision and recall,
	# reaching its optimal value at 1 and its worst value at 0.
	# The 'beta' parameter determines the weight of precision in the combined
	# score. 'beta < 1' lends more weight to precision, while 'beta > 1'
	# favors recall ('beta -> 0' considers only precision, 'beta -> inf' only recall).
	print 'F-beta：'
	for beta in np.logspace(-3, 3, num=7, base=10):
		fbeta = fbeta_score(y_true, y_hat, beta=beta)
		print '\tbeta=%9.3f\tF-beta=%.5f' % (beta, fbeta)
		#print (1+beta**2)*precision*recall / (beta**2 * precision + recall)
	
	print precision_recall_fscore_support(y_true, y_hat, beta=1)
	print classification_report(y_true, y_hat)
```
#### 输出：
```

	Accuracy：	0.5
	Precision:	0.6
	Recall:  	0.75
	f1 score: 	0.666666666667
	0.666666666667
	F-beta：
		beta=    0.001	F-beta=0.60000
		beta=    0.010	F-beta=0.60001
		beta=    0.100	F-beta=0.60119
		beta=    1.000	F-beta=0.66667
		beta=   10.000	F-beta=0.74815
		beta=  100.000	F-beta=0.74998
		beta= 1000.000	F-beta=0.75000
	(array([ 0. ,  0.6]), array([ 0.  ,  0.75]), array([ 0.        ,  0.66666667]), array([2, 4], dtype=int64))
	             precision    recall  f1-score   support
	
	          0       0.00      0.00      0.00         2
	          1       0.60      0.75      0.67         4
	
	avg / total       0.40      0.50      0.44         6
	
```

### 样本不均衡问题：
``` python

	import numpy as np
	from sklearn import svm
	import matplotlib.colors
	import matplotlib.pyplot as plt
	from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, fbeta_score
	import warnings
	
	def show_accuracy(a, b):
	    acc = a.ravel() == b.ravel()
	    print '正确率：%.2f%%' % (100*float(acc.sum()) / a.size)
	
	def show_recall(y, y_hat):
	    # print y_hat[y == 1]
	    print '召回率：%.2f%%' % (100 * float(np.sum(y_hat[y == 1] == 1)) / np.extract(y == 1, y).size)
	
	warnings.filterwarnings("ignore")   # UndefinedMetricWarning
	np.random.seed(0)   # 保持每次生成的数据相同
	
	c1 = 990
	c2 = 10
	N = c1 + c2
	x_c1 = 3*np.random.randn(c1, 2)
	x_c2 = 0.5*np.random.randn(c2, 2) + (4, 4)
	x = np.vstack((x_c1, x_c2))
	y = np.ones(N)
	y[:c1] = -1
	
	# 显示大小
	s = np.ones(N) * 30
	s[:c1] = 10
	
	# 分类器
	clfs = [svm.SVC(C=1, kernel='linear'),
	       svm.SVC(C=1, kernel='linear', class_weight={-1: 1, 1: 50}),
	       svm.SVC(C=0.8, kernel='rbf', gamma=0.5, class_weight={-1: 1, 1: 2}),
	       svm.SVC(C=0.8, kernel='rbf', gamma=0.5, class_weight={-1: 1, 1: 10})]
	titles = 'Linear', 'Linear, Weight=50', 'RBF, Weight=2', 'RBF, Weight=10'
	
	x1_min, x1_max = x[:, 0].min(), x[:, 0].max()  # 第0列的范围
	x2_min, x2_max = x[:, 1].min(), x[:, 1].max()  # 第1列的范围
	x1, x2 = np.mgrid[x1_min:x1_max:500j, x2_min:x2_max:500j]  # 生成网格采样点
	grid_test = np.stack((x1.flat, x2.flat), axis=1)  # 测试点
	
	cm_light = matplotlib.colors.ListedColormap(['#77E0A0', '#FF8080'])
	cm_dark = matplotlib.colors.ListedColormap(['g', 'r'])
	matplotlib.rcParams['font.sans-serif'] = [u'SimHei']
	matplotlib.rcParams['axes.unicode_minus'] = False
	plt.figure(figsize=(10, 8), facecolor='w')
	for i, clf in enumerate(clfs):
	    clf.fit(x, y)
	    y_hat = clf.predict(x)
	    # show_accuracy(y_hat, y) # 正确率
	    # show_recall(y, y_hat)   # 召回率
	    print i+1, '次：'
	    print '正确率：\t', accuracy_score(y, y_hat)
	    print ' 精度 ：\t', precision_score(y, y_hat, pos_label=1)
	    print '召回率：\t', recall_score(y, y_hat, pos_label=1)
	    print 'F1-score：\t', f1_score(y, y_hat, pos_label=1)
	    print
	
	    # 画图
	    plt.subplot(2, 2, i+1)
	    grid_hat = clf.predict(grid_test)       # 预测分类值
	    grid_hat = grid_hat.reshape(x1.shape)  # 使之与输入的形状相同
	    plt.pcolormesh(x1, x2, grid_hat, cmap=cm_light, alpha=0.8)
	    plt.scatter(x[:, 0], x[:, 1], c=y, edgecolors='k', s=s, cmap=cm_dark)      # 样本的显示
	    plt.xlim(x1_min, x1_max)
	    plt.ylim(x2_min, x2_max)
	    plt.title(titles[i])
	    plt.grid()
	plt.suptitle(u'不平衡数据的处理', fontsize=18)
	plt.tight_layout(1.5)
	plt.subplots_adjust(top=0.92)
	plt.show()
```

#### 输出：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/QQ截图20171114172602.png" width="80%">
  <div class="figcaption">
  </div>
</div>

```

	1 次：
	正确率：	0.99
	 精度 ：	0.0
	召回率：	0.0
	F1-score：	0.0
	2 次：
	正确率：	0.94
	 精度 ：	0.142857142857
	召回率：	1.0
	F1-score：	0.25
	3 次：
	正确率：	0.994
	 精度 ：	0.625
	召回率：	1.0
	F1-score：	0.769230769231
	4 次：
	正确率：	0.994
	 精度 ：	0.625
	召回率：	1.0
	F1-score：	0.769230769231
```

### SVR：
``` python

	import numpy as np
	from sklearn import svm
	import matplotlib.pyplot as plt
	
	N = 50
	np.random.seed(0)
	x = np.sort(np.random.uniform(0, 6, N), axis=0)
	y = 2*np.sin(x) + 0.1*np.random.randn(N)
	x = x.reshape(-1, 1)
	print 'x =\n', x
	print 'y =\n', y
	
	print 'SVR - RBF'
	svr_rbf = svm.SVR(kernel='rbf', gamma=0.2, C=100)
	svr_rbf.fit(x, y)
	print 'SVR - Linear'
	svr_linear = svm.SVR(kernel='linear', C=100)
	svr_linear.fit(x, y)
	print 'SVR - Polynomial'
	svr_poly = svm.SVR(kernel='poly', degree=3, C=100)
	svr_poly.fit(x, y)
	print 'Fit OK.'
	
	x_test = np.linspace(x.min(), 1.1*x.max(), 100).reshape(-1, 1)
	y_rbf = svr_rbf.predict(x_test)
	y_linear = svr_linear.predict(x_test)
	y_poly = svr_poly.predict(x_test)
	
	plt.figure(figsize=(9, 8), facecolor='w')
	plt.plot(x_test, y_rbf, 'r-', linewidth=2, label='RBF Kernel')
	plt.plot(x_test, y_linear, 'g-', linewidth=2, label='Linear Kernel')
	plt.plot(x_test, y_poly, 'b-', linewidth=2, label='Polynomial Kernel')
	plt.plot(x, y, 'mo', markersize=6)
	plt.scatter(x[svr_rbf.support_], y[svr_rbf.support_], s=130, c='r', marker='*', label='RBF Support Vectors')
	plt.legend(loc='lower left')
	plt.title('SVR', fontsize=16)
	plt.xlabel('X')
	plt.ylabel('Y')
	plt.grid(True)
	plt.tight_layout(2)
	plt.show()

```
#### 输出：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/QQ截图20171114173757.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### SVR GridSearchCV example:
``` python

	import numpy as np
	from sklearn import svm
	from sklearn.model_selection import GridSearchCV    # 0.17 grid_search
	import matplotlib.pyplot as plt
	
	N = 50
	np.random.seed(0)
	x = np.sort(np.random.uniform(0, 6, N), axis=0)
	y = 2*np.sin(x) + 0.1*np.random.randn(N)
	x = x.reshape(-1, 1)
	print 'x =\n', x
	print 'y =\n', y
	
	model = svm.SVR(kernel='rbf')
	c_can = np.logspace(-2, 2, 10)
	gamma_can = np.logspace(-2, 2, 10)
	svr = GridSearchCV(model, param_grid={'C': c_can, 'gamma': gamma_can}, cv=5)
	svr.fit(x, y)
	print '验证参数：\n', svr.best_params_
	
	x_test = np.linspace(x.min(), x.max(), 100).reshape(-1, 1)
	y_hat = svr.predict(x_test)
	
	sp = svr.best_estimator_.support_
	plt.figure(facecolor='w')
	plt.scatter(x[sp], y[sp], s=120, c='r', marker='*', label='Support Vectors', zorder=3)
	plt.plot(x_test, y_hat, 'r-', linewidth=2, label='RBF Kernel')
	plt.plot(x, y, 'go', markersize=5)
	plt.legend(loc='upper right')
	plt.title('SVR', fontsize=16)
	plt.xlabel('X')
	plt.ylabel('Y')
	plt.grid(True)
	plt.show()
```
#### 输出：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/Figure_3.png" width="80%">
  <div class="figcaption">
  </div>
</div>


via

* [SVM的两个参数 C 和 gamma](http://blog.csdn.net/lujiandong1/article/details/46386201)