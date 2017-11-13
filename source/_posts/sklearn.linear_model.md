---
title: sklearn.linear_model
date: 2017-11-13 21:06:12 
categories: "机器学习" 
tags: 
     - sklearn
     - scipy
     - linear_model
     - GridSearchCV
     - MSE
     - RMSE
     - cross_val_predict
description: sklearn.linear_model
toc: true
---
# 导入数据集
``` python

	from sklearn import datasets
	from sklearn.model_selection import train_test_split
	boston = datasets.load_boston()
	X = boston.data
	y = boston.target
	"""
	划分数据集
	"""
	x_train, x_test, y_train, y_test = train_test_split(X, y, random_state=1)
```

# GridSearchCV寻参
``` python

	lr = linear_model.LinearRegression()
	model = Lasso()
	# model = Ridge()
	
	alpha_can = np.logspace(-3, 2, 10)
	lasso_model = GridSearchCV(model, param_grid={'alpha': alpha_can}, cv=5)
	lasso_model.fit(x_train, y_train)
	print '超参数：\n', lasso_model.best_params_
```

<!--more-->

# 预测
``` python
	
	y_hat = lasso_model.predict(np.array(x_test))
```

# 模型评价
``` python
	
	mse = np.average((y_hat - np.array(y_test)) ** 2)  # Mean Squared Error
	rmse = np.sqrt(mse)  # Root Mean Squared Error
	print mse, rmse
```
## 或者用scikit-learn计算MSE/RMSE
``` python
	
	from sklearn import metrics
	print "MSE:",metrics.mean_squared_error(y_test, y_hat)
	print "RMSE:",np.sqrt(metrics.mean_squared_error(y_test, y_hat))
```

## `cross_val_predict`
``` python
	
	boston = datasets.load_boston()
	X = boston.data
	y = boston.target
	
	from sklearn.model_selection import cross_val_predict
	predicted = cross_val_predict(model, X, y, cv=10)
	print "MSE:",metrics.mean_squared_error(y, predicted)
	print "RMSE:",np.sqrt(metrics.mean_squared_error(y, predicted))
```

# 输出图形展示
这里画图真实值和预测值的变化关系，离中间的直线y=x直线越近的点代表预测损失越低。

``` python
	
	t = np.arange(len(x_test))
	mpl.rcParams['font.sans-serif'] = [u'simHei']
	mpl.rcParams['axes.unicode_minus'] = False
	plt.plot(t, y_test, 'r-', linewidth=2, label=u'真实数据')
	plt.plot(t, y_hat, 'g-', linewidth=2, label=u'预测数据')
	plt.title(u'线性回归预测销量', fontsize=18)
	plt.legend(loc='upper right')
	plt.grid()
	plt.show()
```

<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/ML/linear_model/Figure_1.png" width="80%">
  <div class="figcaption">
  </div>
</div>

