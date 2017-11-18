---
title: sklearn.tree.DecisionTreeRegressor
date: 2017-11-14 20:06:12 
categories: "机器学习" 
tags: 
     - sklearn
     - tree
     - DecisionTreeRegressor
description: sklearn.tree.DecisionTreeRegressor
toc: true
---
### 导入包：
``` python

	import numpy as np
	import matplotlib.pyplot as plt
	from sklearn.tree import DecisionTreeRegressor
```

### 生成数据集：
``` python

	N = 100
	x = np.random.rand(N) * 6 - 3     # [-3,3)
	x.sort()
	y = np.sin(x) + np.random.randn(N) * 0.05
	print y
	x = x.reshape(-1, 1)  # 转置后，得到N个样本，每个样本都是1维的
	print x
```

<!--more-->

### DecisionTreeRegressor：
``` python

	reg = DecisionTreeRegressor(criterion='mse', max_depth=9)
	dt = reg.fit(x, y)
	x_test = np.linspace(-3, 3, 50).reshape(-1, 1)
	y_hat = dt.predict(x_test)
	plt.plot(x, y, 'ro', ms=6, label='Actual')
	plt.plot(x_test, y_hat, 'g-', linewidth=2, label='Predict')
	plt.legend(loc='upper left')
	plt.grid()
	plt.show()
```

<div class="fig figcenter fighighlight">
  <img src="/assets/ML/tree/Figure_1a.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 比较决策树的深度影响：
``` python

	depth = [2, 4, 6, 8, 10]
	clr = 'rgbmy'
	reg = [DecisionTreeRegressor(criterion='mse', max_depth=depth[0]),
	       DecisionTreeRegressor(criterion='mse', max_depth=depth[1]),
	       DecisionTreeRegressor(criterion='mse', max_depth=depth[2]),
	       DecisionTreeRegressor(criterion='mse', max_depth=depth[3]),
	       DecisionTreeRegressor(criterion='mse', max_depth=depth[4])]
	
	plt.plot(x, y, 'k^', linewidth=2, label='Actual')
	x_test = np.linspace(-3, 3, 50).reshape(-1, 1)
	for i, r in enumerate(reg):
	    dt = r.fit(x, y)
	    y_hat = dt.predict(x_test)
	    plt.plot(x_test, y_hat, '-', color=clr[i], linewidth=2, label='Depth=%d' % depth[i])
	plt.legend(loc='upper left')
	plt.grid()
	plt.show()
```

<div class="fig figcenter fighighlight">
  <img src="/assets/ML/tree/Figure_1b.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 多变量决策树回归：
``` python

	import numpy as np
	import matplotlib.pyplot as plt
	from sklearn.tree import DecisionTreeRegressor
	
	N = 400
	x = np.random.rand(N) * 8 - 4     # [-4,4)
	x.sort()
	y1 = np.sin(x) + 3 + np.random.randn(N) * 0.1
	y2 = np.cos(0.3*x) + np.random.randn(N) * 0.01
	y = np.vstack((y1, y2)).T
	x = x.reshape(-1, 1)  # 转置后，得到N个样本，每个样本都是1维的
	
	deep = 5 # 树的深度
	reg = DecisionTreeRegressor(criterion='mse', max_depth=deep)
	dt = reg.fit(x, y)
	
	x_test = np.linspace(-4, 4, num=1000).reshape(-1, 1)
	print x_test
	y_hat = dt.predict(x_test)
	print y_hat
	plt.scatter(y[:, 0], y[:, 1], c='r', s=40, label='Actual')
	plt.scatter(y_hat[:, 0], y_hat[:, 1], c='g', marker='s', s=100, label='Depth=%d' % deep, alpha=1)
	plt.legend(loc='upper left')
	plt.xlabel('y1')
	plt.ylabel('y2')
	plt.grid()
	plt.show()
```

<div class="fig figcenter fighighlight">
  <img src="/assets/ML/tree/Figure_1c.png" width="49%">
  <img src="/assets/ML/tree/Figure_1d.png" width="49%">
  <div class="figcaption">
  </div>
</div>
