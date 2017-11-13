---
title: sklearn.linear_model中的Ridge、Lasso、ElasticNet回归
date: 2017-11-13 21:06:12 
categories: "机器学习" 
tags: 
     - sklearn
     - linear_model
     - Ridge
     - Lasso
     - ElasticNet
     - Pipeline
description: sklearn.linear_model中的Ridge、Lasso、ElasticNet回归
toc: true
---
# 导入包：
``` python

	import numpy as np
	from sklearn.linear_model import LinearRegression, RidgeCV, LassoCV, ElasticNetCV
	from sklearn.preprocessing import PolynomialFeatures
	import matplotlib.pyplot as plt
	from sklearn.pipeline import Pipeline
	import matplotlib as mpl
	import warnings
```

# 定义模型评价函数：
``` python

	def xss(y, y_hat):
	    y = y.ravel()
	    y_hat = y_hat.ravel()
	    tss = np.var(y)
	    rss = np.average((y_hat - y) ** 2)
	    r2 = 1 - rss / tss
	    corr_coef = np.corrcoef(y, y_hat)[0, 1]
	    return r2, corr_coef
```

<!--more-->

# 生成训练数据
``` python

	warnings.filterwarnings("ignore")   # ConvergenceWarning
	np.random.seed(0)
	np.set_printoptions(linewidth=1000)
	N = 9
	x = np.linspace(0, 6, N) + np.random.randn(N)
	x = np.sort(x)
	y = x**2 - 4*x - 3 + np.random.randn(N)
	x.shape = -1, 1
	y.shape = -1, 1
```
# 模型设置

``` python

	models = [Pipeline([('poly', PolynomialFeatures()),
	                    ('linear', LinearRegression(fit_intercept=False))]),
	        Pipeline([('poly', PolynomialFeatures()),
	                ('linear', RidgeCV(alphas=np.logspace(-3, 2, 50), fit_intercept=False))]),
	        Pipeline([('poly', PolynomialFeatures()),
	                ('linear', LassoCV(alphas=np.logspace(-3, 2, 50), fit_intercept=False))]),
	        Pipeline([('poly', PolynomialFeatures()),
	                ('linear', ElasticNetCV(alphas=np.logspace(-3, 2, 50), l1_ratio=[.1, .5, .7, .9, .95, .99, 1],
	                                fit_intercept=False))])]
	
	mpl.rcParams['font.sans-serif'] = [u'simHei']
	mpl.rcParams['axes.unicode_minus'] = False
	np.set_printoptions(suppress=True)
```

# 模型训练与图形展示

``` python

	plt.figure(figsize=(16, 10), facecolor='w')
	d_pool = np.arange(1, N, 1)  # 阶
	m = d_pool.size
	clrs = []  # 颜色
	for c in np.linspace(16711680, 255, m):
	    clrs.append('#%06x' % c)
	
	line_width = np.linspace(5, 2, m)
	titles = u'LinearRegression', u'Ridge', u'LASSO', u'ElasticNet'
	tss_list = []
	rss_list = []
	ess_list = []
	ess_rss_list = []
	for t in range(4):
	    model = models[t]
	    plt.subplot(2, 2, t+1)
	    plt.plot(x, y, 'ro', ms=10, zorder=N)
	    for i, d in enumerate(d_pool):
	        model.set_params(poly__degree=d)
	        model.fit(x, y.ravel())
	        lin = model.get_params('linear')['linear']
	        output = u'%s：%d阶，系数为：' % (titles[t], d)
	        if hasattr(lin, 'alpha_'):
	            idx = output.find(u'系数')
	            output = output[:idx] + (u'alpha=%.6f，' % lin.alpha_) + output[idx:]
	        if hasattr(lin, 'l1_ratio_'):   # 根据交叉验证结果，从输入l1_ratio(list)中选择的最优l1_ratio_(float)
	            idx = output.find(u'系数')
	            output = output[:idx] + (u'l1_ratio=%.6f，' % lin.l1_ratio_) + output[idx:]
	        print output, lin.coef_.ravel()
	        x_hat = np.linspace(x.min(), x.max(), num=100)
	        x_hat.shape = -1, 1
	        y_hat = model.predict(x_hat)
	        s = model.score(x, y)
	        r2, corr_coef = xss(y, model.predict(x))
	        # print 'R2和相关系数：', r2, corr_coef
	        # print 'R2：', s, '\n'
	        z = N - 1 if (d == 2) else 0
	        label = u'%d阶，$R^2$=%.3f' % (d, s)
	        if hasattr(lin, 'l1_ratio_'):
	            label += u'，L1 ratio=%.2f' % lin.l1_ratio_
	        plt.plot(x_hat, y_hat, color=clrs[i], lw=line_width[i], alpha=0.75, label=label, zorder=z)
	    plt.legend(loc='upper left')
	    plt.grid(True)
	    plt.title(titles[t], fontsize=18)
	    plt.xlabel('X', fontsize=16)
	    plt.ylabel('Y', fontsize=16)
	plt.tight_layout(1, rect=(0, 0, 1, 0.95))
	plt.suptitle(u'多项式曲线拟合比较', fontsize=22)
	plt.show()
	
	y_max = max(max(tss_list), max(ess_rss_list)) * 1.05
	plt.figure(figsize=(9, 7), facecolor='w')
	t = np.arange(len(tss_list))
	plt.plot(t, tss_list, 'ro-', lw=2, label=u'TSS(Total Sum of Squares)')
	plt.plot(t, ess_list, 'mo-', lw=1, label=u'ESS(Explained Sum of Squares)')
	plt.plot(t, rss_list, 'bo-', lw=1, label=u'RSS(Residual Sum of Squares)')
	plt.plot(t, ess_rss_list, 'go-', lw=2, label=u'ESS+RSS')
	plt.ylim((0, y_max))
	plt.legend(loc='center right')
	plt.xlabel(u'LinearRegression/Ridge/LASSO/Elastic Net', fontsize=15)
	plt.ylabel(u'XSS值', fontsize=15)
	plt.title(u'总平方和TSS=？', fontsize=18)
	plt.grid(True)
	plt.show()
```

##### 输出如下：

<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/ML/linear_model/QQ截图20171113165729.png" width="80%">
  <div class="figcaption">
  </div>
</div>

<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/ML/linear_model/QQ截图20171113165824.png" width="80%">
  <div class="figcaption">
  </div>
</div>

```

	线性回归：1阶，系数为： [-12.12113792   3.05477422]
	线性回归：2阶，系数为： [-3.23812184 -3.36390661  0.90493645]
	线性回归：3阶，系数为： [-3.90207326 -2.61163034  0.66422328  0.02290431]
	线性回归：4阶，系数为： [-8.20599769  4.20778207 -2.85304163  0.73902338 -0.05008557]
	线性回归：5阶，系数为： [ 21.59733285 -54.12232017  38.43116219 -12.68651476   1.98134176  -0.11572371]
	线性回归：6阶，系数为： [ 14.73304785 -37.87317494  23.67462342  -6.07037979   0.42536833   0.06803132  -0.00859246]
	线性回归：7阶，系数为： [ 314.30344622 -827.89446924  857.33293186 -465.46543638  144.21883851  -25.67294678    2.44658612   -0.09675941]
	线性回归：8阶，系数为： [-1189.50149198  3643.69109456 -4647.92941149  3217.22814712 -1325.87384337   334.32869072   -50.57119119     4.21251817    -0.148521  ]
	Ridge回归：1阶，alpha=0.109854，系数为： [-11.21592213   2.85121516]
	Ridge回归：2阶，alpha=0.138950，系数为： [-2.90423989 -3.49931368  0.91803171]
	Ridge回归：3阶，alpha=0.068665，系数为： [-3.47165245 -2.85078293  0.69245987  0.02314415]
	Ridge回归：4阶，alpha=0.222300，系数为： [-2.84560266 -1.99887417 -0.40628792  0.33863868 -0.02674442]
	Ridge回归：5阶，alpha=1.151395，系数为： [-1.68160373 -1.52726943 -0.8382036   0.2329258   0.03934251 -0.00663323]
	Ridge回归：6阶，alpha=0.001000，系数为： [ 0.53724068 -6.00552086 -3.75961826  5.64559118 -2.21569695  0.36872911 -0.02221343]
	Ridge回归：7阶，alpha=0.033932，系数为： [-2.38021238 -2.26383055 -1.47715232  0.00763115  1.12242917 -0.52769633  0.09199201 -0.00560199]
	Ridge回归：8阶，alpha=0.138950，系数为： [-2.19299093 -1.91896884 -1.21608489 -0.19314178  0.49300277  0.05452898 -0.09690455  0.02114435 -0.00140196]
	LASSO：1阶，alpha=0.222300，系数为： [-10.41556797   2.66199326]
	LASSO：2阶，alpha=0.001000，系数为： [-3.29932625 -3.31989869  0.89878903]
	LASSO：3阶，alpha=0.013257，系数为： [-4.83524033 -1.48721929  0.29726322  0.05804667]
	LASSO：4阶，alpha=0.002560，系数为： [-5.08513199 -1.41147772  0.3380565   0.0440427   0.00099807]
	LASSO：5阶，alpha=0.042919，系数为： [-4.11853758 -1.8643949   0.2618319   0.07954732  0.00257481 -0.00069093]
	LASSO：6阶，alpha=0.001000，系数为： [-4.53546398 -1.70335188  0.29896515  0.05237738  0.00489432  0.00007551 -0.00010944]
	LASSO：7阶，alpha=0.001000，系数为： [-4.51456835 -1.58477275  0.23483228  0.04900369  0.00593868  0.00044879 -0.00002625 -0.00002132]
	LASSO：8阶，alpha=0.001000，系数为： [-4.62623251 -1.37717809  0.17183854  0.04307765  0.00629505  0.00069171  0.0000355  -0.00000875 -0.00000386]
	ElasticNet：1阶，alpha=0.021210，l1_ratio=0.100000，系数为： [-10.74762959   2.74580662]
	ElasticNet：2阶，alpha=0.013257，l1_ratio=0.100000，系数为： [-2.95099269 -3.48472703  0.91705013]
	ElasticNet：3阶，alpha=0.013257，l1_ratio=1.000000，系数为： [-4.83524033 -1.48721929  0.29726322  0.05804667]
	ElasticNet：4阶，alpha=0.010481，l1_ratio=0.950000，系数为： [-4.8799192  -1.5317438   0.3452403   0.04825571  0.00049763]
	ElasticNet：5阶，alpha=0.004095，l1_ratio=0.100000，系数为： [-4.07916291 -2.18606287  0.44650232  0.05102669  0.00239164 -0.00048279]
	ElasticNet：6阶，alpha=0.001000，l1_ratio=1.000000，系数为： [-4.53546398 -1.70335188  0.29896515  0.05237738  0.00489432  0.00007551 -0.00010944]
	ElasticNet：7阶，alpha=0.001000，l1_ratio=1.000000，系数为： [-4.51456835 -1.58477275  0.23483228  0.04900369  0.00593868  0.00044879 -0.00002625 -0.00002132]
	ElasticNet：8阶，alpha=0.001000，l1_ratio=0.500000，系数为： [-4.53761647 -1.45230301  0.18829714  0.0427561   0.00619739  0.00068209  0.00003506 -0.00000869 -0.00000384]
```
