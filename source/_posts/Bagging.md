---
title: Bagging
date: 2017-11-14 21:06:12 
categories: "机器学习" 
tags: 
     - sklearn
     - tree
     - Bagging
     - BaggingRegressor
     - reduce
     - DecisionTreeRegressor
     - RidgeCV
     - PolynomialFeatures
description: Bagging
toc: true
---
# 引子
假设一个分类器分类正确的概率为0.6，如果有n个独立的分类器，选择其中的k个采用投票的方式，作为预测结果，则预测正确的概率为：

``` python

	import operator
	# operator.__mul__(a, b)
	# Return a * b, for a and b numbers.
	
	def c(n, k):
	    # 求组合数
	    return reduce(operator.mul, range(n-k+1, n+1)) / reduce(operator.mul, range(1, k+1))
	
	def bagging(n, p):
	    s = 0
	    for i in range(n / 2 + 1, n + 1):
	        s += c(n, i) * p ** i * (1 - p) ** (n - i)
	    return s
	
	for t in range(9, 100, 10):
	    # 假设事件发生的概率为0.6
	    print t, '次采样正确率：', bagging(t, 0.6)
```

### 输出

```

	9 次采样正确率： 0.73343232
	19 次采样正确率： 0.813907978585
	29 次采样正确率： 0.863787051336
	39 次采样正确率： 0.897941368711
	49 次采样正确率： 0.922424437652
	59 次采样正确率： 0.940447995732
	69 次采样正确率： 0.953949756505
	79 次采样正确率： 0.964189692839
	89 次采样正确率： 0.972027516007
	99 次采样正确率： 0.97806955787

```

<!--more-->

# BaggingRegressor

``` python

	import numpy as np
	import matplotlib.pyplot as plt
	import matplotlib as mpl
	from sklearn.linear_model import RidgeCV
	from sklearn.ensemble import BaggingRegressor
	from sklearn.tree import DecisionTreeRegressor
	from sklearn.pipeline import Pipeline
	from sklearn.preprocessing import PolynomialFeatures
	
	def f(x):
	    return 0.5*np.exp(-(x+3) **2) + np.exp(-x**2) + + 0.5*np.exp(-(x-3) ** 2)
	
	np.random.seed(0)
	N = 200
	x = np.random.rand(N) * 10 - 5  # [-5,5)
	x = np.sort(x)
	y = f(x) + 0.05*np.random.randn(N)
	x.shape = -1, 1
	
	ridge = RidgeCV(alphas=np.logspace(-3, 2, 10), fit_intercept=False)
	ridged = Pipeline([('poly', PolynomialFeatures(degree=10)), ('Ridge', ridge)])
	bagging_ridged = BaggingRegressor(ridged, n_estimators=100, max_samples=0.3)
	dtr = DecisionTreeRegressor(max_depth=5)
	regs = [
	    ('DecisionTree Regressor', dtr),
	    ('Ridge Regressor(6 Degree)', ridged),
	    ('Bagging Ridge(6 Degree)', bagging_ridged),
	    ('Bagging DecisionTree Regressor', BaggingRegressor(dtr, n_estimators=100, max_samples=0.3))]
	x_test = np.linspace(1.1*x.min(), 1.1*x.max(), 1000)
	mpl.rcParams['font.sans-serif'] = [u'SimHei']
	mpl.rcParams['axes.unicode_minus'] = False
	plt.figure(figsize=(12, 8), facecolor='w')
	plt.plot(x, y, 'ro', label=u'训练数据')
	plt.plot(x_test, f(x_test), color='k', lw=3.5, label=u'真实值')
	
	clrs = 'bmyg'
	for i, (name, reg) in enumerate(regs):
	    reg.fit(x, y)
	    y_test = reg.predict(x_test.reshape(-1, 1))
	    plt.plot(x_test, y_test.ravel(), color=clrs[i], lw=i+1, label=name, zorder=6-i)
	plt.legend(loc='upper left')
	plt.xlabel('X', fontsize=15)
	plt.ylabel('Y', fontsize=15)
	plt.title(u'回归曲线拟合', fontsize=21)
	plt.ylim((-0.2, 1.2))
	plt.tight_layout(2)
	plt.grid(True)
	plt.show()
```

<div class="fig figcenter fighighlight">
  <img src="/assets/ML/tree/QQ截图20171114151258.png" width="80%">
  <div class="figcaption">
  </div>
</div>
