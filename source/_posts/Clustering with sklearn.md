---
title: Clustering with sklearn
date: 2017-11-15 19:06:12 
categories: "机器学习" 
tags: 
     - sklearn
     - make_blobs
     - euclidean_distances
     - KMeans
     - KMeans++
     - homogeneity_score
     - completeness_score
     - v_measure_score
     - adjusted_rand_score
     - AffinityPropagation
     - MeanShift
     - spectral_clustering
description: Clustering with sklearn
toc: true
---
# 生成聚类数据集的方法

`生成数据集方法`：sklearn.datasets.make_blobs(n_samples,n_featurs,centers)可以生成数据集,n_samples表示个数，n_features表示特征个数，centers表示y的种类数:

* make_blobs函数是为聚类产生数据集产生一个数据集和相应的标签
* n_samples:表示数据样本点个数,默认值100
* n_features:表示数据的维度，默认值是2
* centers:产生数据的中心点，默认值3
* cluster_std：数据集的标准差，浮点数或者浮点数序列，默认值1.0
* center_box：中心确定之后的数据边界，默认值(-10.0, 10.0)
* shuffle ：洗乱，默认值是True
* random_state:官网解释是随机生成器的种子

y3 = np.array([0]*100 + [1]*50 + [2]*20 + [3]*5)可以这样建立array数组

k-means对于方差不相等和数据与坐标轴不平行时效果不理想；对于数据大小量纲敏感。

<!--more-->

# The Influence of Data Distribution on KMeans Clustering
``` python

	import numpy as np
	import matplotlib.pyplot as plt
	import sklearn.datasets as ds
	import matplotlib.colors
	from sklearn.cluster import KMeans
	
	def expand(a, b):
	    d = (b - a) * 0.1
	    return a-d, b+d
	
	N = 400
	centers = 4
	data, y = ds.make_blobs(N, n_features=2, centers=centers, random_state=2)
	data2, y2 = ds.make_blobs(N, n_features=2, centers=centers, cluster_std=(1,2.5,0.5,2), random_state=2)
	data3 = np.vstack((data[y == 0][:], data[y == 1][:50], data[y == 2][:20], data[y == 3][:5]))
	y3 = np.array([0] * 100 + [1] * 50 + [2] * 20 + [3] * 5)
	
	cls = KMeans(n_clusters=4, init='k-means++')
	y_hat = cls.fit_predict(data)
	y2_hat = cls.fit_predict(data2)
	y3_hat = cls.fit_predict(data3)
	
	m = np.array(((1, 1), (1, 3)))
	data_r = data.dot(m)
	y_r_hat = cls.fit_predict(data_r)
	
	matplotlib.rcParams['font.sans-serif'] = [u'SimHei']
	matplotlib.rcParams['axes.unicode_minus'] = False
	cm = matplotlib.colors.ListedColormap(list('rgbm'))
	
	plt.figure(figsize=(9, 10), facecolor='w')
	plt.subplot(421)
	plt.title(u'Raw data')
	plt.scatter(data[:, 0], data[:, 1], c=y, s=30, cmap=cm, edgecolors='none')
	x1_min, x2_min = np.min(data, axis=0)
	x1_max, x2_max = np.max(data, axis=0)
	x1_min, x1_max = expand(x1_min, x1_max)
	x2_min, x2_max = expand(x2_min, x2_max)
	plt.xlim((x1_min, x1_max))
	plt.ylim((x2_min, x2_max))
	plt.grid(True)
	
	plt.subplot(422)
	plt.title(u'KMeans++ clustering')
	plt.scatter(data[:, 0], data[:, 1], c=y_hat, s=30, cmap=cm, edgecolors='none')
	plt.xlim((x1_min, x1_max))
	plt.ylim((x2_min, x2_max))
	plt.grid(True)
	
	plt.subplot(423)
	plt.title(u'Data after rotation')
	plt.scatter(data_r[:, 0], data_r[:, 1], c=y, s=30, cmap=cm, edgecolors='none')
	x1_min, x2_min = np.min(data_r, axis=0)
	x1_max, x2_max = np.max(data_r, axis=0)
	x1_min, x1_max = expand(x1_min, x1_max)
	x2_min, x2_max = expand(x2_min, x2_max)
	plt.xlim((x1_min, x1_max))
	plt.ylim((x2_min, x2_max))
	plt.grid(True)
	
	plt.subplot(424)
	plt.title(u'Data rotated KMeans++ clustering')
	plt.scatter(data_r[:, 0], data_r[:, 1], c=y_r_hat, s=30, cmap=cm, edgecolors='none')
	plt.xlim((x1_min, x1_max))
	plt.ylim((x2_min, x2_max))
	plt.grid(True)
	
	plt.subplot(425)
	plt.title(u'Unequal variance data')
	plt.scatter(data2[:, 0], data2[:, 1], c=y2, s=30, cmap=cm, edgecolors='none')
	x1_min, x2_min = np.min(data2, axis=0)
	x1_max, x2_max = np.max(data2, axis=0)
	x1_min, x1_max = expand(x1_min, x1_max)
	x2_min, x2_max = expand(x2_min, x2_max)
	plt.xlim((x1_min, x1_max))
	plt.ylim((x2_min, x2_max))
	plt.grid(True)
	
	plt.subplot(426)
	plt.title(u'Data with unequal variance KMeans++ clustering')
	plt.scatter(data2[:, 0], data2[:, 1], c=y2_hat, s=30, cmap=cm, edgecolors='none')
	plt.xlim((x1_min, x1_max))
	plt.ylim((x2_min, x2_max))
	plt.grid(True)
	
	plt.subplot(427)
	plt.title(u'Data with unequal numbers')
	plt.scatter(data3[:, 0], data3[:, 1], s=30, c=y3, cmap=cm, edgecolors='none')
	x1_min, x2_min = np.min(data3, axis=0)
	x1_max, x2_max = np.max(data3, axis=0)
	x1_min, x1_max = expand(x1_min, x1_max)
	x2_min, x2_max = expand(x2_min, x2_max)
	plt.xlim((x1_min, x1_max))
	plt.ylim((x2_min, x2_max))
	plt.grid(True)
	
	plt.subplot(428)
	plt.title(u'Data with unequal numbers KMeans++ clustering')
	plt.scatter(data3[:, 0], data3[:, 1], c=y3_hat, s=30, cmap=cm, edgecolors='none')
	plt.xlim((x1_min, x1_max))
	plt.ylim((x2_min, x2_max))
	plt.grid(True)
	
	plt.tight_layout(2)
	plt.suptitle(u'The Influence of Data Distribution on KMeans Clustering', fontsize=18)
	# https://github.com/matplotlib/matplotlib/issues/829
	plt.subplots_adjust(top=0.92)
	plt.show()
```

## 输出
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/cluster/QQ截图20171115094526.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# 聚类性能的评价指标
* 均一性sklearn.metrics.homogeneity_score
* 完整性sklearn.metrics.completeness_score
* 均一性完整性二者的加权平均v_measure_score
* ARI（Adjusted Rand index(调整兰德指数)：sklearn.metrics.adjusted_rand_score
* AMI: sklearn.metrics.adjusted_mutual_info_score

[关于指标的定义请看这里](http://zhangchunhui.cn/2017/11/12/%E8%81%9A%E7%B1%BB/)


``` python

	from sklearn import metrics
	
	y =     [0, 0, 0, 1, 1, 1]
	y_hat = [0, 0, 1, 1, 2, 2]
	h = metrics.homogeneity_score(y, y_hat)
	c = metrics.completeness_score(y, y_hat)
	print u'同一性(Homogeneity)：', h
	print u'完整性(Completeness)：', c
	v2 = 2 * c * h / (c + h)
	v = metrics.v_measure_score(y, y_hat)
	print u'V-Measure：', v2, v
	
	y = [0, 0, 0, 1, 1, 1]
	y_hat = [0, 0, 1, 2, 3, 3]
	h = metrics.homogeneity_score(y, y_hat)
	c = metrics.completeness_score(y, y_hat)
	v = metrics.v_measure_score(y, y_hat)
	print u'同一性(Homogeneity)：', h
	print u'完整性(Completeness)：', c
	print u'V-Measure：', v
	
	# 允许不同值
	y = [0, 0, 0, 1, 1, 1]
	y_hat = [1, 1, 1, 0, 0, 0]
	h = metrics.homogeneity_score(y, y_hat)
	c = metrics.completeness_score(y, y_hat)
	v = metrics.v_measure_score(y, y_hat)
	print u'同一性(Homogeneity)：', h
	print u'完整性(Completeness)：', c
	print u'V-Measure：', v
	
	y = [0, 0, 1, 1]
	y_hat = [0, 1, 0, 1]
	ari = metrics.adjusted_rand_score(y, y_hat)
	print ari
	
	y = [0, 0, 0, 1, 1, 1]
	y_hat = [0, 0, 1, 1, 2, 2]
	ari = metrics.adjusted_rand_score(y, y_hat)
	print ari
```

## 输出
```

	同一性(Homogeneity)： 0.666666666667
	完整性(Completeness)： 0.420619835714
	V-Measure： 0.515803742979 0.515803742979
	同一性(Homogeneity)： 1.0
	完整性(Completeness)： 0.521296028614
	V-Measure： 0.685331478962
	同一性(Homogeneity)： 1.0
	完整性(Completeness)： 1.0
	V-Measure： 1.0
	-0.5
	0.242424242424
```

# AffinityPropagation

``` python

	import numpy as np
	import matplotlib.pyplot as plt
	import sklearn.datasets as ds
	import matplotlib.colors
	from sklearn.cluster import AffinityPropagation
	from sklearn.metrics import euclidean_distances
	
	N = 400
	centers = [[1, 2], [-1, -1], [1, -1], [-1, 1]]
	data, y = ds.make_blobs(N, n_features=2, centers=centers, cluster_std=[0.5, 0.25, 0.7, 0.5], random_state=0)
	m = euclidean_distances(data, squared=True)
	preference = -np.median(m)
	print 'Preference：', preference
	
	matplotlib.rcParams['font.sans-serif'] = [u'SimHei']
	matplotlib.rcParams['axes.unicode_minus'] = False
	plt.figure(figsize=(12, 9), facecolor='w')
	for i, mul in enumerate(np.linspace(1, 4, 9)):
	    print mul
	    p = mul * preference
	    model = AffinityPropagation(affinity='euclidean', preference=p)
	    af = model.fit(data)
	    center_indices = af.cluster_centers_indices_
	    n_clusters = len(center_indices)
	    print ('p = %.1f' % mul), p, '聚类簇的个数为：', n_clusters
	    y_hat = af.labels_
	
	    plt.subplot(3, 3, i+1)
	    plt.title(u'Preference：%.2f，簇个数：%d' % (p, n_clusters))
	    clrs = []
	    for c in np.linspace(16711680, 255, n_clusters):
	        clrs.append('#%06x' % c)
	    # clrs = plt.cm.Spectral(np.linspace(0, 1, n_clusters))
	    for k, clr in enumerate(clrs):
	        cur = (y_hat == k)
	        plt.scatter(data[cur, 0], data[cur, 1], c=clr, edgecolors='none')
	        center = data[center_indices[k]]
	        for x in data[cur]:
	            plt.plot([x[0], center[0]], [x[1], center[1]], color=clr, zorder=1)
	    plt.scatter(data[center_indices, 0], data[center_indices, 1], s=100, c=clrs, marker='*', edgecolors='k', zorder=2)
	    plt.grid(True)
	plt.tight_layout()
	plt.suptitle(u'AP聚类', fontsize=20)
	plt.subplots_adjust(top=0.92)
	plt.show()
```
## 输出
```

	Preference： -5.29914553034
	1.0
	p = 1.0 -5.29914553034 聚类簇的个数为： 16
	1.375
	p = 1.4 -7.28632510422 聚类簇的个数为： 12
	1.75
	p = 1.8 -9.27350467809 聚类簇的个数为： 11
	2.125
	p = 2.1 -11.260684252 聚类簇的个数为： 10
	2.5
	p = 2.5 -13.2478638258 聚类簇的个数为： 8
	2.875
	p = 2.9 -15.2350433997 聚类簇的个数为： 8
	3.25
	p = 3.2 -17.2222229736 聚类簇的个数为： 75
	3.625
	p = 3.6 -19.2094025475 聚类簇的个数为： 7
	4.0
	p = 4.0 -21.1965821214 聚类簇的个数为： 7

```
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/cluster/QQ截图20171115105338.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# MeanShift Clustering

``` python

	import numpy as np
	import matplotlib.pyplot as plt
	import sklearn.datasets as ds
	import matplotlib.colors
	from sklearn.cluster import MeanShift
	from sklearn.metrics import euclidean_distances
	
	N = 1000
	centers = [[1, 2], [-1, -1], [1, -1], [-1, 1]]
	data, y = ds.make_blobs(N, n_features=2, centers=centers, cluster_std=[0.5, 0.25, 0.7, 0.5], random_state=0)
	
	matplotlib.rcParams['font.sans-serif'] = [u'SimHei']
	matplotlib.rcParams['axes.unicode_minus'] = False
	plt.figure(figsize=(10, 9), facecolor='w')
	m = euclidean_distances(data, squared=True)
	bw = np.median(m)
	print bw
	for i, mul in enumerate(np.linspace(0.1, 0.4, 4)):
	    band_width = mul * bw
	    model = MeanShift(bin_seeding=True, bandwidth=band_width)
	    ms = model.fit(data)
	    centers = ms.cluster_centers_
	    y_hat = ms.labels_
	    n_clusters = np.unique(y_hat).size
	    print '带宽：', mul, band_width, '聚类簇的个数为：', n_clusters
	
	    plt.subplot(2, 2, i+1)
	    plt.title(u'带宽：%.2f，聚类簇的个数为：%d' % (band_width, n_clusters))
	    clrs = []
	    for c in np.linspace(16711680, 255, n_clusters):
	        clrs.append('#%06x' % c)
	    # clrs = plt.cm.Spectral(np.linspace(0, 1, n_clusters))
	    print clrs
	    for k, clr in enumerate(clrs):
	        cur = (y_hat == k)
	        plt.scatter(data[cur, 0], data[cur, 1], c=clr, edgecolors='none')
	    plt.scatter(centers[:, 0], centers[:, 1], s=150, c=clrs, marker='*', edgecolors='k')
	    plt.grid(True)
	plt.tight_layout(2)
	plt.suptitle(u'MeanShift聚类', fontsize=20)
	plt.subplots_adjust(top=0.92)
	plt.show()
```
## 输出
```

	5.31661129692
	带宽： 0.1 0.531661129692 聚类簇的个数为： 7
	['#ff0000', '#d4802a', '#aa0055', '#7f807f', '#5500aa', '#2a80d4', '#0000ff']
	带宽： 0.2 1.06332225938 聚类簇的个数为： 4
	['#ff0000', '#aa0055', '#5500aa', '#0000ff']
	带宽： 0.3 1.59498338907 聚类簇的个数为： 3
	['#ff0000', '#7f807f', '#0000ff']
	带宽： 0.4 2.12664451877 聚类簇的个数为： 1
	['#ff0000']
```
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/cluster/QQ截图20171115105702.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# DBSCAN

``` python

	import numpy as np
	import matplotlib.pyplot as plt
	import sklearn.datasets as ds
	import matplotlib.colors
	from sklearn.cluster import DBSCAN
	from sklearn.preprocessing import StandardScaler
	
	def expand(a, b):
	    d = (b - a) * 0.1
	    return a-d, b+d
	
	N = 1000
	centers = [[1, 2], [-1, -1], [1, -1], [-1, 1]]
	data, y = ds.make_blobs(N, n_features=2, centers=centers, cluster_std=[0.5, 0.25, 0.7, 0.5], random_state=0)
	data = StandardScaler().fit_transform(data)
	params = ((0.2, 5), (0.2, 10), (0.2, 15), (0.3, 5), (0.3, 10), (0.3, 15))
	
	matplotlib.rcParams['font.sans-serif'] = [u'SimHei']
	matplotlib.rcParams['axes.unicode_minus'] = False
	
	plt.figure(figsize=(12, 8), facecolor='w')
	plt.suptitle(u'DBSCAN聚类', fontsize=20)
	
	for i in range(6):
	    eps, min_samples = params[i]
	    model = DBSCAN(eps=eps, min_samples=min_samples)
	    model.fit(data)
	    y_hat = model.labels_
	
	    core_indices = np.zeros_like(y_hat, dtype=bool)
	    core_indices[model.core_sample_indices_] = True
	
	    y_unique = np.unique(y_hat)
	    n_clusters = y_unique.size - (1 if -1 in y_hat else 0)
	    print y_unique, '聚类簇的个数为：', n_clusters
	
	    # clrs = []
	    # for c in np.linspace(16711680, 255, y_unique.size):
	    #     clrs.append('#%06x' % c)
	    plt.subplot(2, 3, i+1)
	    clrs = plt.cm.Spectral(np.linspace(0, 0.8, y_unique.size))
	    for k, clr in zip(y_unique, clrs):
	        cur = (y_hat == k)
	        if k == -1:
	            plt.scatter(data[cur, 0], data[cur, 1], s=20, c='k')
	            continue
	        plt.scatter(data[cur, 0], data[cur, 1], s=30, c=clr, edgecolors='k')
	        plt.scatter(data[cur & core_indices][:, 0], data[cur & core_indices][:, 1], s=60, c=clr, marker='o', edgecolors='k')
	    x1_min, x2_min = np.min(data, axis=0)
	    x1_max, x2_max = np.max(data, axis=0)
	    x1_min, x1_max = expand(x1_min, x1_max)
	    x2_min, x2_max = expand(x2_min, x2_max)
	    plt.xlim((x1_min, x1_max))
	    plt.ylim((x2_min, x2_max))
	    plt.grid(True)
	    plt.title(ur'$\epsilon$ = %.1f  m = %d，聚类数目：%d' % (eps, min_samples, n_clusters), fontsize=16)
	plt.tight_layout()
	plt.subplots_adjust(top=0.9)
	plt.show()
```
## 输出
```

	[-1  0  1  2  3] 聚类簇的个数为： 4
	[-1  0  1  2  3] 聚类簇的个数为： 4
	[-1  0  1  2  3  4] 聚类簇的个数为： 5
	[-1  0] 聚类簇的个数为： 1
	[-1  0  1] 聚类簇的个数为： 2
	[-1  0  1  2  3] 聚类簇的个数为： 4
```
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/cluster/QQ截图20171115110020.png" width="80%">
  <div class="figcaption">
  </div>
</div>


# 谱聚类

``` python

	import numpy as np
	import matplotlib.pyplot as plt
	import sklearn.datasets as ds
	import matplotlib.colors
	from sklearn.cluster import spectral_clustering
	from sklearn.metrics import euclidean_distances
	
	def expand(a, b):
	    d = (b - a) * 0.1
	    return a-d, b+d
	
	matplotlib.rcParams['font.sans-serif'] = [u'SimHei']
	matplotlib.rcParams['axes.unicode_minus'] = False
	
	t = np.arange(0, 2*np.pi, 0.1)
	data1 = np.vstack((np.cos(t), np.sin(t))).T
	data2 = np.vstack((2*np.cos(t), 2*np.sin(t))).T
	data3 = np.vstack((3*np.cos(t), 3*np.sin(t))).T
	data = np.vstack((data1, data2, data3))
	
	n_clusters = 3
	m = euclidean_distances(data, squared=True)
	sigma = np.median(m)
	
	plt.figure(figsize=(12, 8), facecolor='w')
	plt.suptitle(u'谱聚类', fontsize=20)
	clrs = plt.cm.Spectral(np.linspace(0, 0.8, n_clusters))
	for i, s in enumerate(np.logspace(-2, 0, 6)):
	    print s
	    af = np.exp(-m ** 2 / (s ** 2)) + 1e-6
	    y_hat = spectral_clustering(af, n_clusters=n_clusters, assign_labels='kmeans', random_state=1)
	    plt.subplot(2, 3, i+1)
	    for k, clr in enumerate(clrs):
	        cur = (y_hat == k)
	        plt.scatter(data[cur, 0], data[cur, 1], s=40, c=clr, edgecolors='k')
	    x1_min, x2_min = np.min(data, axis=0)
	    x1_max, x2_max = np.max(data, axis=0)
	    x1_min, x1_max = expand(x1_min, x1_max)
	    x2_min, x2_max = expand(x2_min, x2_max)
	    plt.xlim((x1_min, x1_max))
	    plt.ylim((x2_min, x2_max))
	    plt.grid(True)
	    plt.title(ur'$\sigma$ = %.2f' % s, fontsize=16)
	plt.tight_layout()
	plt.subplots_adjust(top=0.9)
	plt.show()
```
## 输出
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/cluster/QQ截图20171115111813.png" width="80%">
  <div class="figcaption">
  </div>
</div>
