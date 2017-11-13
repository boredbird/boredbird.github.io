---
title: ElasticNetCV
date: 2017-11-13 22:06:12 
categories: "机器学习" 
tags: 
     - sklearn
     - linear_model
     - ElasticNetCV
     - ElasticNet
     - PolynomialFeatures
     - StandardScaler
     - train_test_split
     - Pipeline
description: ElasticNetCV
toc: true
---
# 导入包：
``` python

	import numpy as np
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	from sklearn.model_selection import train_test_split
	from sklearn.linear_model import ElasticNetCV
	import sklearn.datasets
	from sklearn.preprocessing import PolynomialFeatures, StandardScaler
	from sklearn.pipeline import Pipeline
	from sklearn.metrics import mean_squared_error
```

# 导入数据集：
``` python

	def not_empty(s):
	    return s != ''
	
	data = sklearn.datasets.load_boston()
	x = np.array(data.data)
	y = np.array(data.target)
	print x.shape
	print y.shape
	
	x_train, x_test, y_train, y_test = train_test_split(x, y, train_size=0.7, random_state=0)
```

<!--more-->

# 初始化模型Pipeline：

``` python

	model = Pipeline([
	    ('ss', StandardScaler()),
	    ('poly', PolynomialFeatures(degree=3, include_bias=True)),
	    ('linear', ElasticNetCV(l1_ratio=[0.1, 0.3, 0.5, 0.7, 0.99, 1], alphas=np.logspace(-3, 2, 5),
	                            fit_intercept=False, max_iter=1e3, cv=3))
	])
```

# 模型训练：
``` python

	model.fit(x_train, y_train.ravel())
	linear = model.get_params('linear')['linear']
	print u'超参数：', linear.alpha_
	print u'L1 ratio：', linear.l1_ratio_
	print u'系数：', linear.coef_.ravel()
```

# 模型预测：
``` python

	y_pred = model.predict(x_test)
	r2 = model.score(x_test, y_test)
	mse = mean_squared_error(y_test, y_pred)
	print 'R2:', r2
	print u'均方误差：', mse
```

# 模型效果图形化展示：
``` python

	t = np.arange(len(y_pred))
	mpl.rcParams['font.sans-serif'] = [u'simHei']
	mpl.rcParams['axes.unicode_minus'] = False
	plt.figure(facecolor='w')
	plt.plot(t, y_test.ravel(), 'r-', lw=2, label=u'真实值')
	plt.plot(t, y_pred, 'g-', lw=2, label=u'估计值')
	plt.legend(loc='best')
	plt.title(u'波士顿房价预测', fontsize=18)
	plt.xlabel(u'样本编号', fontsize=15)
	plt.ylabel(u'房屋价格', fontsize=15)
	plt.grid()
	plt.show()
```
## 输出
```

	(506L, 13L)
	(506L,)
	超参数： 0.316227766017
	L1 ratio： 0.99
	R2: 0.772203419261
	均方误差： 18.9675965682
```

<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/ML/linear_model/QQ截图20171113171456.png" width="80%">
  <div class="figcaption">
  </div>
</div>



