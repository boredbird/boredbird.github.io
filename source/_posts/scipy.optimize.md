---
title: scipy.optimize使用
date: 2017-11-13 21:06:12 
categories: "机器学习" 
tags: 
     - optimize
     - scipy
description: scipy.optimize使用
toc: true
---
# 定义损失函数
``` python

	#!/usr/bin/python
	# -*- coding:utf-8 -*-
	
	# 导入NumPy函数库，一般都是用这样的形式(包括别名np，几乎是约定俗成的)
	import numpy as np
	from scipy.optimize import leastsq
	import matplotlib.pyplot as plt
	
	def residual(t, x, y):
	    return y - (t[0] * x ** 2 + t[1] * x + t[2])
	
	
	def residual2(t, x, y):
	    print t[0], t[1]
	    return y - t[0]*np.sin(t[1]*x)
	
	
	# x ** x        x > 0
	# (-x) ** (-x)  x < 0
	def f(x):
	    y = np.ones_like(x)
	    i = x > 0
	    y[i] = np.power(x[i], x[i])
	    i = x < 0
	    y[i] = np.power(-x[i], -x[i])
	    return y

```

<!--more-->

# 利用scipy.optimize求解线性回归1

``` python

    x = np.linspace(-2, 2, 50)
    A, B, C = 2, 3, -1
    y = (A * x ** 2 + B * x + C) + np.random.rand(len(x))*0.75

    t = leastsq(residual, [0, 0, 0], args=(x, y))
    theta = t[0]
    print '真实值：', A, B, C
    print '预测值：', theta
    y_hat = theta[0] * x ** 2 + theta[1] * x + theta[2]
    plt.plot(x, y, 'r-', linewidth=2, label=u'Actual')
    plt.plot(x, y_hat, 'g-', linewidth=2, label=u'Predict')
    plt.legend(loc='upper left')
    plt.grid()
    plt.show()
```

## 利用scipy.optimize求解线性回归1输出图例
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/ML/optimize/QQ截图20171113123110.png" width="80%">
  <div class="figcaption">
  </div>
</div>


# 利用scipy.optimize求解非线性回归

``` python

    x = np.linspace(0, 5, 100)
    A = 5
    w = 1.5
    y = A * np.sin(w*x) + np.random.rand(len(x)) - 0.5

    t = leastsq(residual2, [3, 1], args=(x, y))
    theta = t[0]
    print '真实值：', A, w
    print '预测值：', theta
    y_hat = theta[0] * np.sin(theta[1] * x)
    plt.plot(x, y, 'r-', linewidth=2, label='Actual')
    plt.plot(x, y_hat, 'g-', linewidth=2, label='Predict')
    plt.legend(loc='lower left')
    plt.grid()
    plt.show()
```

## 利用scipy.optimize求解非线性回归输出图例
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/ML/optimize/QQ截图20171113123423.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# 使用scipy计算函数极值
``` python

    a = opt.fmin(f, 1)
    b = opt.fmin_cg(f, 1)
    c = opt.fmin_bfgs(f, 1)
    print a, 1/a, math.e
    print b
    print c
```
## 使用scipy计算函数极值输出
``` 

	Optimization terminated successfully.
	         Current function value: 0.692201
	         Iterations: 16
	         Function evaluations: 32
	Optimization terminated successfully.
	         Current function value: 0.692201
	         Iterations: 4
	         Function evaluations: 30
	         Gradient evaluations: 10
	Optimization terminated successfully.
	         Current function value: 0.692201
	         Iterations: 5
	         Function evaluations: 24
	         Gradient evaluations: 8
	[ 0.36787109] [ 2.71834351] 2.71828182846
	[ 0.36787948]
	[ 0.36787942]

```
