---
title: sklearn.linear_model.LogisticRegression
date: 2017-11-13 21:06:12 
categories: "机器学习" 
tags: 
     - sklearn
     - linear_model
     - LogisticRegression
     - Pipeline
     - 分割面
description: sklearn.linear_model.LogisticRegression
toc: true
---
# 导入数据集
``` python

	from sklearn import datasets
	iris = datasets.load_iris()
	X = iris.data[:, :2]
	y = iris.target
```

# 数据处理与模型拟合Pipeline
``` python

	import numpy as np
	from sklearn.pipeline import Pipeline
	from sklearn.preprocessing import StandardScaler
	from sklearn.linear_model import LogisticRegression
	lr = Pipeline([('sc', StandardScaler()),
	               ('clf', LogisticRegression()) ])
	lr.fit(X, y.ravel())
	y_hat = lr.predict(X)
	y_hat_prob = lr.predict_proba(X)
	np.set_printoptions(suppress=True)
	print 'y_hat = \n', y_hat
	print 'y_hat_prob = \n', y_hat_prob
	print u'准确度：%.2f%%' % (100*np.mean(y_hat == y.ravel()))
```

<!--more-->

# 绘图：分割面
``` python

	import matplotlib.pyplot as plt
	import matplotlib as mpl
	N, M = 500, 500     # 横纵各采样多少个值
	x1_min, x1_max = X[:, 0].min(), X[:, 0].max()   # 第0列的范围
	x2_min, x2_max = X[:, 1].min(), X[:, 1].max()   # 第1列的范围
	t1 = np.linspace(x1_min, x1_max, N)
	t2 = np.linspace(x2_min, x2_max, M)
	x1, x2 = np.meshgrid(t1, t2)                    # 生成网格采样点
	x_test = np.stack((x1.flat, x2.flat), axis=1)   # 测试点
	
	mpl.rcParams['font.sans-serif'] = [u'simHei']
	mpl.rcParams['axes.unicode_minus'] = False
	cm_light = mpl.colors.ListedColormap(['#77E0A0', '#FF8080', '#A0A0FF'])
	cm_dark = mpl.colors.ListedColormap(['g', 'r', 'b'])
	y_hat = lr.predict(x_test)                  # 预测值
	y_hat = y_hat.reshape(x1.shape)                 # 使之与输入的形状相同
	plt.figure(facecolor='w')
	plt.pcolormesh(x1, x2, y_hat, cmap=cm_light)     # 预测值的显示
	plt.scatter(X[:, 0], X[:, 1], c=y, edgecolors='k', s=50, cmap=cm_dark)    # 样本的显示
	plt.xlabel(u'花萼长度', fontsize=14)
	plt.ylabel(u'花萼宽度', fontsize=14)
	plt.xlim(x1_min, x1_max)
	plt.ylim(x2_min, x2_max)
	plt.grid()
	plt.title(u'鸢尾花Logistic回归分类效果 - 标准化', fontsize=17)
	plt.show()
```

<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/ML/linear_model/Figure_2.png" width="80%">
  <div class="figcaption">
  </div>
</div>