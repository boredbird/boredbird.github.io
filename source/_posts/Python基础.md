---
title: Python基础
date: 2017-11-08 21:15:12 
categories: "Python" 
tags: 
     - Python
description: Python基础
---
# intro

<!--more-->

``` python

	#!/usr/bin/python
	# -*- coding:utf-8 -*-
	
	# 导入NumPy函数库，一般都是用这样的形式(包括别名np，几乎是约定俗成的)
	import numpy as np
	import matplotlib as mpl
	from mpl_toolkits.mplot3d import Axes3D
	from matplotlib import cm
	import time
	from scipy.optimize import leastsq
	from scipy import stats
	import scipy.optimize as opt
	import scipy
	import matplotlib.pyplot as plt
	from scipy.stats import norm, poisson
	# from scipy.interpolate import BarycentricInterpolator
	# from scipy.interpolate import CubicSpline
	import math
	# import seaborn
	
	
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
	
	
	if __name__ == "__main__":
	    # # 开场白：
	    # numpy是非常好用的数据包，如：可以这样得到这个二维数组
	    # [[ 0  1  2  3  4  5]
	    #  [10 11 12 13 14 15]
	    #  [20 21 22 23 24 25]
	    #  [30 31 32 33 34 35]
	    #  [40 41 42 43 44 45]
	    #  [50 51 52 53 54 55]]
	    # a = np.arange(0, 60, 10).reshape((-1, 1)) + np.arange(6)
	    # print a
	
	    # 正式开始  -:)
	    # 标准Python的列表(list)中，元素本质是对象。
	    # 如：L = [1, 2, 3]，需要3个指针和三个整数对象，对于数值运算比较浪费内存和CPU。
	    # 因此，Numpy提供了ndarray(N-dimensional array object)对象：存储单一数据类型的多维数组。
	
	    # # 1.使用array创建
	    # 通过array函数传递list对象
	    # L = [1, 2, 3, 4, 5, 6]
	    # print "L = ", L
	    # a = np.array(L)
	    # print "a = ", a
	    # print type(a)
	    # # # 若传递的是多层嵌套的list，将创建多维数组
	    # b = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
	    # print b
	    # # #
	    # # # # 数组大小可以通过其shape属性获得
	    # print a.shape
	    # print b.shape
	    # # #
	    # # # 也可以强制修改shape
	    # b.shape = 4, 3
	    # print b
	    # # # # 注：从(3,4)改为(4,3)并不是对数组进行转置，而只是改变每个轴的大小，数组元素在内存中的位置并没有改变
	    # # #
	    # # # 当某个轴为-1时，将根据数组元素的个数自动计算此轴的长度
	    # b.shape = 2, -1
	    # print b
	    # print b.shape
	    # # #
	    # b.shape = 3, 4
	    # # # 使用reshape方法，可以创建改变了尺寸的新数组，原数组的shape保持不变
	    # c = b.reshape((4, -1))
	    # print "b = \n", b
	    # print 'c = \n', c
	    # #
	    # # # 数组b和c共享内存，修改任意一个将影响另外一个
	    # b[0][1] = 20
	    # print "b = \n", b
	    # print "c = \n", c
	    # # #
	    # # # 数组的元素类型可以通过dtype属性获得
	    # print a.dtype
	    # print b.dtype
	    # # #
	    # # # # 可以通过dtype参数在创建时指定元素类型
	    # d = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]], dtype=np.float)
	    # f = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]], dtype=np.complex)
	    # print d
	    # print f
	    # # #
	    # # # 如果更改元素类型，可以使用astype安全的转换
	    # f = d.astype(np.int)
	    # print f
	    # #
	    # # # 但不要强制仅修改元素类型，如下面这句，将会以int来解释单精度float类型
	    # d.dtype = np.int
	    # print d
	    #
	    # 2.使用函数创建
	    # 如果生成一定规则的数据，可以使用NumPy提供的专门函数
	    # arange函数类似于python的range函数：指定起始值、终止值和步长来创建数组
	    # 和Python的range类似，arange同样不包括终值；但arange可以生成浮点类型，而range只能是整数类型
	    # a = np.arange(1, 10, 0.5)
	    # print a
	    # # #
	    # # # linspace函数通过指定起始值、终止值和元素个数来创建数组，缺省包括终止值
	    # b = np.linspace(1, 10, 10)
	    # print 'b = ', b
	    # # #
	    # # 可以通过endpoint关键字指定是否包括终值
	    # c = np.linspace(1, 10, 10, endpoint=False)
	    # print 'c = ', c
	    # # #
	    # # 和linspace类似，logspace可以创建等比数列
	    # # 下面函数创建起始值为10^1，终止值为10^2，有20个数的等比数列
	    # d = np.logspace(1, 2, 10, endpoint=True)
	    # print d
	    # # #
	    # # # 下面创建起始值为2^0，终止值为2^10(包括)，有10个数的等比数列
	    # f = np.logspace(0, 10, 11, endpoint=True, base=2)
	    # print f
	    # # #
	    # # # 使用 frombuffer, fromstring, fromfile等函数可以从字节序列创建数组
	    # s = 'abcd'
	    # g = np.fromstring(s, dtype=np.int8)
	    # print g
	    # #
	    # 3.存取
	    # 3.1常规办法：数组元素的存取方法和Python的标准方法相同
	    # a = np.arange(10)
	    # print a
	    # # # 获取某个元素
	    # print a[3]
	    # # # # 切片[3,6)，左闭右开
	    # print a[3:6]
	    # # # # 省略开始下标，表示从0开始
	    # print a[:5]
	    # # # # 下标为负表示从后向前数
	    # print a[3:]
	    # # # # 步长为2
	    # print a[1:9:2]
	    # # # # 步长为-1，即翻转
	    # print a[::-1]
	    # # # # 切片数据是原数组的一个视图，与原数组共享内容空间，可以直接修改元素值
	    # a[1:4] = 10, 20, 30
	    # print a
	    # # # # 因此，在实践中，切实注意原始数据是否被破坏，如：
	    # b = a[2:5]
	    # b[0] = 200
	    # print a
	    #
	    # # 3.2 整数/布尔数组存取
	    # # 3.2.1
	    # 根据整数数组存取：当使用整数序列对数组元素进行存取时，
	    # 将使用整数序列中的每个元素作为下标，整数序列可以是列表(list)或者数组(ndarray)。
	    # 使用整数序列作为下标获得的数组不和原始数组共享数据空间。
	    # a = np.logspace(0, 9, 10, base=2)
	    # print a
	    # i = np.arange(0, 10, 2)
	    # print i
	    # # # # 利用i取a中的元素
	    # b = a[i]
	    # print b
	    # # # b的元素更改，a中元素不受影响
	    # b[2] = 1.6
	    # print b
	    # print a
	
	    # # 3.2.2
	    # 使用布尔数组i作为下标存取数组a中的元素：返回数组a中所有在数组b中对应下标为True的元素
	    # # 生成10个满足[0,1)中均匀分布的随机数
	    # a = np.random.rand(10)
	    # print a
	    # # # 大于0.5的元素索引
	    # print a > 0.5
	    # # # # 大于0.5的元素
	    # b = a[a > 0.5]
	    # print b
	    # # # # 将原数组中大于0.5的元素截取成0.5
	    # a[a > 0.5] = 0.5
	    # print a
	    # # # # b不受影响
	    # print b
	
	    # 3.3 二维数组的切片
	    # [[ 0  1  2  3  4  5]
	    #  [10 11 12 13 14 15]
	    #  [20 21 22 23 24 25]
	    #  [30 31 32 33 34 35]
	    #  [40 41 42 43 44 45]
	    #  [50 51 52 53 54 55]]
	    # a = np.arange(0, 60, 10)    # 行向量
	    # print 'a = ', a
	    # b = a.reshape((-1, 1))      # 转换成列向量
	    # print b
	    # c = np.arange(6)
	    # print c
	    # f = b + c   # 行 + 列
	    # print f
	    # # 合并上述代码：
	    # a = np.arange(0, 60, 10).reshape((-1, 1)) + np.arange(6)
	    # print a
	    # # 二维数组的切片
	    # print a[[0, 1, 2], [2 ,3, 4]]
	    # print a[4, [2, 3, 4]]
	    # print a[4:, [2, 3, 4]]
	    # i = np.array([True, False, True, False, False, True])
	    # print a[i]
	    # print a[i, 3]
	
	    # # 4.1 numpy与Python数学库的时间比较
	    # for j in np.logspace(0, 7, 10):
	    #     j = int(j)
	    #     x = np.linspace(0, 10, j)
	    #     start = time.clock()
	    #     y = np.sin(x)
	    #     t1 = time.clock() - start
	    #
	    #     x = x.tolist()
	    #     start = time.clock()
	    #     for i, t in enumerate(x):
	    #         x[i] = math.sin(t)
	    #     t2 = time.clock() - start
	    #     print j, ": ", t1, t2, t2/t1
	
	    # 4.2 元素去重
	    # 4.2.1直接使用库函数
	    # a = np.array((1, 2, 3, 4, 5, 5, 7, 3, 2, 2, 8, 8))
	    # print '原始数组：', a
	    # # 使用库函数unique
	    # b = np.unique(a)
	    # print '去重后：', b
	    # # 4.2.2 二维数组的去重，结果会是预期的么？
	    # c = np.array(((1, 2), (3, 4), (5, 6), (1, 3), (3, 4), (7, 6)))
	    # print '二维数组', c
	    # print '去重后：', np.unique(c)
	    # # 4.2.3 方案1：转换为虚数
	    # # r, i = np.split(c, (1, ), axis=1)
	    # # x = r + i * 1j
	    # x = c[:, 0] + c[:, 1] * 1j
	    # print '转换成虚数：', x
	    # print '虚数去重后：', np.unique(x)
	    # print np.unique(x, return_index=True)   # 思考return_index的意义
	    # idx = np.unique(x, return_index=True)[1]
	    # print '二维数组去重：\n', c[idx]
	    # # 4.2.3 方案2：利用set
	    # print '去重方案2：\n', np.array(list(set([tuple(t) for t in c])))
	
	    # # 4.3 stack and axis
	    # a = np.arange(1, 10).reshape((3, 3))
	    # b = np.arange(11, 20).reshape((3, 3))
	    # c = np.arange(101, 110).reshape((3, 3))
	    # print 'a = \n', a
	    # print 'b = \n', b
	    # print 'c = \n', c
	    # print 'axis = 0 \n', np.stack((a, b, c), axis=0)
	    # print 'axis = 1 \n', np.stack((a, b, c), axis=1)
	    # print 'axis = 2 \n', np.stack((a, b, c), axis=2)
	
	    # 5.绘图
	    # 5.1 绘制正态分布概率密度函数
	    # mu = 0
	    # sigma = 1
	    # x = np.linspace(mu - 3 * sigma, mu + 3 * sigma, 50)
	    # y = np.exp(-(x - mu) ** 2 / (2 * sigma ** 2)) / (math.sqrt(2 * math.pi) * sigma)
	    # print x.shape
	    # print 'x = \n', x
	    # print y.shape
	    # print 'y = \n', y
	    # # plt.plot(x, y, 'ro-', linewidth=2)
	    # plt.plot(x, y, 'r-', x, y, 'go', linewidth=2, markersize=8)
	    # plt.grid(True)
	    # plt.show()
	
	    mpl.rcParams['font.sans-serif'] = [u'SimHei']  #FangSong/黑体 FangSong/KaiTi
	    mpl.rcParams['axes.unicode_minus'] = False
	
	    # # 5.2 损失函数：Logistic损失(-1,1)/SVM Hinge损失/ 0/1损失
	    # x = np.array(np.linspace(start=-2, stop=3, num=1001, dtype=np.float))
	    # y_logit = np.log(1 + np.exp(-x)) / math.log(2)
	    # y_boost = np.exp(-x)
	    # y_01 = x < 0
	    # y_hinge = 1.0 - x
	    # y_hinge[y_hinge < 0] = 0
	    # plt.plot(x, y_logit, 'r-', label='Logistic Loss', linewidth=2)
	    # plt.plot(x, y_01, 'g-', label='0/1 Loss', linewidth=2)
	    # plt.plot(x, y_hinge, 'b-', label='Hinge Loss', linewidth=2)
	    # plt.plot(x, y_boost, 'm--', label='Adaboost Loss', linewidth=2)
	    # plt.grid()
	    # plt.legend(loc='upper right')
	    # # plt.savefig('1.png')
	    # plt.show()
	
	    # # 5.3 x^x
	    # x = np.linspace(-1.3, 1.3, 101)
	    # y = f(x)
	    # plt.plot(x, y, 'g-', label='x^x', linewidth=2)
	    # plt.grid()
	    # plt.legend(loc='upper left')
	    # plt.show()
	
	    # # 5.4 胸型线
	    # x = np.arange(1, 0, -0.001)
	    # y = (-3 * x * np.log(x) + np.exp(-(40 * (x - 1 / np.e)) ** 4) / 25) / 2
	    # plt.figure(figsize=(5,7))
	    # plt.plot(y, x, 'r-', linewidth=2)
	    # plt.grid(True)
	    # plt.show()
	
	    # 5.5 心形线
	    # t = np.linspace(0, 7, 100)
	    # x = 16 * np.sin(t) ** 3
	    # y = 13 * np.cos(t) - 5 * np.cos(2*t) - 2 * np.cos(3*t) - np.cos(4*t)
	    # plt.plot(x, y, 'r-', linewidth=2)
	    # plt.grid(True)
	    # plt.show()
	
	    # # 5.6 渐开线
	    # t = np.linspace(0, 50, num=1000)
	    # x = t*np.sin(t) + np.cos(t)
	    # y = np.sin(t) - t*np.cos(t)
	    # plt.plot(x, y, 'r-', linewidth=2)
	    # plt.grid()
	    # plt.show()
	
	    # # Bar
	    # mpl.rcParams['font.sans-serif'] = [u'SimHei']  #黑体 FangSong/KaiTi
	    # mpl.rcParams['axes.unicode_minus'] = False
	    # x = np.arange(0, 10, 0.1)
	    # y = np.sin(x)
	    # plt.bar(x, y, width=0.04, linewidth=0.2)
	    # plt.plot(x, y, 'r--', linewidth=2)
	    # plt.title(u'Sin曲线')
	    # plt.xticks(rotation=-60)
	    # plt.xlabel('X')
	    # plt.ylabel('Y')
	    # plt.grid()
	    # plt.show()
	
	    # # 6. 概率分布
	    # # 6.1 均匀分布
	    # x = np.random.rand(10000)
	    # t = np.arange(len(x))
	    # plt.hist(x, 30, color='m', alpha=0.5, label=u'均匀分布')
	    # # plt.plot(t, x, 'r-', label=u'均匀分布')
	    # plt.legend(loc='upper left')
	    # plt.grid()
	    # plt.show()
	
	    # # 6.2 验证中心极限定理
	    # t = 1000
	    # a = np.zeros(10000)
	    # for i in range(t):
	    #     a += np.random.uniform(-5, 5, 10000)
	    # a /= t
	    # plt.hist(a, bins=30, color='g', alpha=0.5, normed=True, label=u'均匀分布叠加')
	    # plt.legend(loc='upper left')
	    # plt.grid()
	    # plt.show()
	
	    # 6.21 其他分布的中心极限定理
	    # lamda = 10
	    # p = stats.poisson(lamda)
	    # y = p.rvs(size=1000)
	    # mx = 30
	    # r = (0, mx)
	    # bins = r[1] - r[0]
	    # plt.figure(figsize=(10, 8), facecolor='w')
	    # plt.subplot(121)
	    # plt.hist(y, bins=bins, range=r, color='g', alpha=0.8, normed=True)
	    # t = np.arange(0, mx+1)
	    # plt.plot(t, p.pmf(t), 'ro-', lw=2)
	    # plt.grid(True)
	    #
	    # N = 1000
	    # M = 10000
	    # plt.subplot(122)
	    # a = np.zeros(M, dtype=np.float)
	    # p = stats.poisson(lamda)
	    # for i in np.arange(N):
	    #     y = p.rvs(size=M)
	    #     a += y
	    # a /= N
	    # plt.hist(a, bins=20, color='g', alpha=0.8, normed=True)
	    # plt.grid(b=True)
	    # plt.show()
	
	    # # 6.3 Poisson分布
	    # x = np.random.poisson(lam=5, size=10000)
	    # print x
	    # pillar = 15
	    # a = plt.hist(x, bins=pillar, normed=True, range=[0, pillar], color='g', alpha=0.5)
	    # plt.grid()
	    # # plt.show()
	    # print a
	    # print a[0].sum()
	
	    # # 6.4 直方图的使用
	    # mu = 2
	    # sigma = 3
	    # data = mu + sigma * np.random.randn(1000)
	    # h = plt.hist(data, 30, normed=1, color='#a0a0ff')
	    # x = h[1]
	    # y = norm.pdf(x, loc=mu, scale=sigma)
	    # plt.plot(x, y, 'r--', x, y, 'ro', linewidth=2, markersize=4)
	    # plt.grid()
	    # plt.show()
	
	
	    # # 6.5 插值
	    # rv = poisson(5)
	    # x1 = a[1]
	    # y1 = rv.pmf(x1)
	    # itp = BarycentricInterpolator(x1, y1)  # 重心插值
	    # x2 = np.linspace(x.min(), x.max(), 50)
	    # y2 = itp(x2)
	    # cs = scipy.interpolate.CubicSpline(x1, y1)       # 三次样条插值
	    # plt.plot(x2, cs(x2), 'm--', linewidth=5, label='CubicSpine')           # 三次样条插值
	    # plt.plot(x2, y2, 'g-', linewidth=3, label='BarycentricInterpolator')   # 重心插值
	    # plt.plot(x1, y1, 'r-', linewidth=1, label='Actural Value')             # 原始值
	    # plt.legend(loc='upper right')
	    # plt.grid()
	    # plt.show()
	
	    # 7. 绘制三维图像
	    # x, y = np.ogrid[-3:3:100j, -3:3:100j]
	    # # u = np.linspace(-3, 3, 101)
	    # # x, y = np.meshgrid(u, u)
	    # z = x*y*np.exp(-(x**2 + y**2)/2) / math.sqrt(2*math.pi)
	    # # z = x*y*np.exp(-(x**2 + y**2)/2) / math.sqrt(2*math.pi)
	    # fig = plt.figure()
	    # ax = fig.add_subplot(111, projection='3d')
	    # # ax.plot_surface(x, y, z, rstride=5, cstride=5, cmap=cm.coolwarm, linewidth=0.1)  #
	    # ax.plot_surface(x, y, z, rstride=5, cstride=5, cmap=cm.Accent, linewidth=0.5)
	    # plt.show()
	    # # cmaps = [('Perceptually Uniform Sequential',
	    # #           ['viridis', 'inferno', 'plasma', 'magma']),
	    # #          ('Sequential', ['Blues', 'BuGn', 'BuPu',
	    # #                          'GnBu', 'Greens', 'Greys', 'Oranges', 'OrRd',
	    # #                          'PuBu', 'PuBuGn', 'PuRd', 'Purples', 'RdPu',
	    # #                          'Reds', 'YlGn', 'YlGnBu', 'YlOrBr', 'YlOrRd']),
	    # #          ('Sequential (2)', ['afmhot', 'autumn', 'bone', 'cool',
	    # #                              'copper', 'gist_heat', 'gray', 'hot',
	    # #                              'pink', 'spring', 'summer', 'winter']),
	    # #          ('Diverging', ['BrBG', 'bwr', 'coolwarm', 'PiYG', 'PRGn', 'PuOr',
	    # #                         'RdBu', 'RdGy', 'RdYlBu', 'RdYlGn', 'Spectral',
	    # #                         'seismic']),
	    # #          ('Qualitative', ['Accent', 'Dark2', 'Paired', 'Pastel1',
	    # #                           'Pastel2', 'Set1', 'Set2', 'Set3']),
	    # #          ('Miscellaneous', ['gist_earth', 'terrain', 'ocean', 'gist_stern',
	    # #                             'brg', 'CMRmap', 'cubehelix',
	    # #                             'gnuplot', 'gnuplot2', 'gist_ncar',
	    # #                             'nipy_spectral', 'jet', 'rainbow',
	    # #                             'gist_rainbow', 'hsv', 'flag', 'prism'])]
	
	    # 8.1 scipy
	    # 线性回归例1
	    # x = np.linspace(-2, 2, 50)
	    # A, B, C = 2, 3, -1
	    # y = (A * x ** 2 + B * x + C) + np.random.rand(len(x))*0.75
	    #
	    # t = leastsq(residual, [0, 0, 0], args=(x, y))
	    # theta = t[0]
	    # print '真实值：', A, B, C
	    # print '预测值：', theta
	    # y_hat = theta[0] * x ** 2 + theta[1] * x + theta[2]
	    # plt.plot(x, y, 'r-', linewidth=2, label=u'Actual')
	    # plt.plot(x, y_hat, 'g-', linewidth=2, label=u'Predict')
	    # plt.legend(loc='upper left')
	    # plt.grid()
	    # plt.show()
	
	    # # 线性回归例2
	    # x = np.linspace(0, 5, 100)
	    # A = 5
	    # w = 1.5
	    # y = A * np.sin(w*x) + np.random.rand(len(x)) - 0.5
	    #
	    # t = leastsq(residual2, [3, 1], args=(x, y))
	    # theta = t[0]
	    # print '真实值：', A, w
	    # print '预测值：', theta
	    # y_hat = theta[0] * np.sin(theta[1] * x)
	    # plt.plot(x, y, 'r-', linewidth=2, label='Actual')
	    # plt.plot(x, y_hat, 'g-', linewidth=2, label='Predict')
	    # plt.legend(loc='lower left')
	    # plt.grid()
	    # plt.show()
	
	    # # 8.2 使用scipy计算函数极值
	    # a = opt.fmin(f, 1)
	    # b = opt.fmin_cg(f, 1)
	    # c = opt.fmin_bfgs(f, 1)
	    # print a, 1/a, math.e
	    # print b
	    # print c
	
	    # marker	description
	    # ”.”	point
	    # ”,”	pixel
	    # “o”	circle
	    # “v”	triangle_down
	    # “^”	triangle_up
	    # “<”	triangle_left
	    # “>”	triangle_right
	    # “1”	tri_down
	    # “2”	tri_up
	    # “3”	tri_left
	    # “4”	tri_right
	    # “8”	octagon
	    # “s”	square
	    # “p”	pentagon
	    # “*”	star
	    # “h”	hexagon1
	    # “H”	hexagon2
	    # “+”	plus
	    # “x”	x
	    # “D”	diamond
	    # “d”	thin_diamond
	    # “|”	vline
	    # “_”	hline
	    # TICKLEFT	tickleft
	    # TICKRIGHT	tickright
	    # TICKUP	tickup
	    # TICKDOWN	tickdown
	    # CARETLEFT	caretleft
	    # CARETRIGHT	caretright
	    # CARETUP	caretup
	    # CARETDOWN	caretdown
```
# calc_e
``` python

	#!/usr/bin/python
	#  -*- coding:utf-8 -*-
	
	import numpy as np
	import math
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	
	
	def calc_e_small(x):
	    n = 10
	    f = np.arange(1, n+1).cumprod()
	    b = np.array([x]*n).cumprod()
	    return np.sum(b / f) + 1
	
	
	def calc_e(x):
	    reverse = False
	    if x < 0:   # 处理负数
	        x = -x
	        reverse = True
	    ln2 = 0.69314718055994530941723212145818
	    c = x / ln2
	    a = int(c+0.5)
	    b = x - a*ln2
	    y = (2 ** a) * calc_e_small(b)
	    if reverse:
	        return 1/y
	    return y
	
	
	if __name__ == "__main__":
	    t1 = np.linspace(-2, 0, 10, endpoint=False)
	    t2 = np.linspace(0, 3, 20)
	    t = np.concatenate((t1, t2))
	    print t     # 横轴数据
	    y = np.empty_like(t)
	    for i, x in enumerate(t):
	        y[i] = calc_e(x)
	        print 'e^', x, ' = ', y[i], '(近似值)\t', math.exp(x), '(真实值)'
	        # print '误差：', y[i] - math.exp(x)
	    plt.figure(facecolor='w')
	    mpl.rcParams['font.sans-serif'] = [u'SimHei']
	    mpl.rcParams['axes.unicode_minus'] = False
	    plt.plot(t, y, 'r-', t, y, 'go', linewidth=2)
	    plt.title(u'Taylor展式的应用 - 指数函数', fontsize=18)
	    plt.xlabel('X', fontsize=15)
	    plt.ylabel('exp(X)', fontsize=15)
	    plt.grid(True)
	    plt.show()

```
# calc_sin
``` python

	#!/usr/bin/python
	#  -*- coding:utf-8 -*-
	
	import numpy as np
	import math
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	
	
	def calc_sin_small(x):
	    x2 = -x ** 2
	    t = x
	    f = 1
	    sum = 0
	    for i in range(10):
	        sum += t / f
	        t *= x2
	        f *= ((2*i+2)*(2*i+3))
	    return sum
	
	
	def calc_sin(x):
	    a = x / (2*np.pi)
	    k = np.floor(a)
	    a = x - k*2*np.pi
	    return calc_sin_small(a)
	
	
	if __name__ == "__main__":
	    t = np.linspace(-2*np.pi, 2*np.pi, 100, endpoint=False)
	    print t     # 横轴数据
	    y = np.empty_like(t)
	    for i, x in enumerate(t):
	        y[i] = calc_sin(x)
	        print 'sin(', x, ') = ', y[i], '(近似值)\t', math.sin(x), '(真实值)'
	        # print '误差：', y[i] - math.exp(x)
	    mpl.rcParams['font.sans-serif'] = [u'SimHei']
	    mpl.rcParams['axes.unicode_minus'] = False
	    plt.figure(facecolor='w')
	    plt.plot(t, y, 'r-', t, y, 'go', linewidth=2)
	    plt.title(u'Taylor展式的应用 - 正弦函数', fontsize=18)
	    plt.xlabel('X', fontsize=15)
	    plt.ylabel('sin(X)', fontsize=15)
	    plt.xlim((-7, 7))
	    plt.ylim((-1.1, 1.1))
	    plt.grid(True)
	    plt.show()

```
# class_intro
``` python

	#!/usr/bin/python
	#  -*- coding:utf-8 -*-
	
	
	class People:
	    def __init__(self, n, a, s):
	        self.name = n
	        self.age = a
	        self.__score = s
	        self.print_people()
	        # self.__print_people()   # 私有函数的作用
	
	    def print_people(self):
	        str = u'%s的年龄：%d，成绩为：%.2f' % (self.name, self.age, self.__score)
	        print str
	
	    __print_people = print_people
	
	
	class Student(People):
	    def __init__(self, n, a, w):
	        People.__init__(self, n, a, w)
	        self.name = 'Student ' + self.name
	
	    def print_people(self):
	        str = u'%s的年龄：%d' % (self.name, self.age)
	        print str
	
	
	def func(p):
	    p.age = 11
	
	
	if __name__ == '__main__':
	    p = People('Tom', 10, 3.14159)
	    func(p)     # p传入的是引用类型
	    p.print_people()
	    print
	
	    # 注意分析下面语句的打印结果，是否觉得有些“怪异”？
	    j = Student('Jerry', 12, 2.71828)
	    print
	
	    # 成员函数
	    p.print_people()
	    j.print_people()
	    print
	
	    People.print_people(p)
	    People.print_people(j)

```
# stat
``` python

	#!/usr/bin/python
	#  -*- coding:utf-8 -*-
	
	import numpy as np
	from scipy import stats
	import math
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	from mpl_toolkits.mplot3d import Axes3D
	from matplotlib import cm
	
	
	def calc_statistics(x):
	    n = x.shape[0]  # 样本个数
	
	    # 手动计算
	    m = 0
	    m2 = 0
	    m3 = 0
	    m4 = 0
	    for t in x:
	        m += t
	        m2 += t*t
	        m3 += t**3
	        m4 += t**4
	    m /= n
	    m2 /= n
	    m3 /= n
	    m4 /= n
	
	    mu = m
	    sigma = np.sqrt(m2 - mu*mu)
	    skew = (m3 - 3*mu*m2 + 2*mu**3) / sigma**3
	    kurtosis = (m4 - 4*mu*m3 + 6*mu*mu*m2 - 4*mu**3*mu + mu**4) / sigma**4 - 3
	    print '手动计算均值、标准差、偏度、峰度：', mu, sigma, skew, kurtosis
	
	    # 使用系统函数验证
	    mu = np.mean(x, axis=0)
	    sigma = np.std(x, axis=0)
	    skew = stats.skew(x)
	    kurtosis = stats.kurtosis(x)
	    return mu, sigma, skew, kurtosis
	
	
	if __name__ == '__main__':
	    d = np.random.randn(100000)
	    print d
	    mu, sigma, skew, kurtosis = calc_statistics(d)
	    print '函数库计算均值、标准差、偏度、峰度：', mu, sigma, skew, kurtosis
	    # 一维直方图
	    mpl.rcParams[u'font.sans-serif'] = 'SimHei'
	    mpl.rcParams[u'axes.unicode_minus'] = False
	    y1, x1, dummy = plt.hist(d, bins=50, normed=True, color='g', alpha=0.75)
	    t = np.arange(x1.min(), x1.max(), 0.05)
	    y = np.exp(-t**2 / 2) / math.sqrt(2*math.pi)
	    plt.plot(t, y, 'r-', lw=2)
	    plt.title(u'高斯分布，样本个数：%d' % d.shape[0])
	    plt.grid(True)
	    plt.show()
	
	    d = np.random.randn(100000, 2)
	    mu, sigma, skew, kurtosis = calc_statistics(d)
	    print '函数库计算均值、标准差、偏度、峰度：', mu, sigma, skew, kurtosis
	
	    # 二维图像
	    N = 30
	    density, edges = np.histogramdd(d, bins=[N, N])
	    print '样本总数：', np.sum(density)
	    density /= density.max()
	    x = y = np.arange(N)
	    t = np.meshgrid(x, y)
	    fig = plt.figure(facecolor='w')
	    ax = fig.add_subplot(111, projection='3d')
	    ax.scatter(t[0], t[1], density, c='r', s=15*density, marker='o', depthshade=True)
	    ax.plot_surface(t[0], t[1], density, cmap=cm.Accent, rstride=2, cstride=2, alpha=0.9, lw=0.75)
	    ax.set_xlabel(u'X')
	    ax.set_ylabel(u'Y')
	    ax.set_zlabel(u'Z')
	    plt.title(u'二元高斯分布，样本个数：%d' % d.shape[0], fontsize=20)
	    plt.tight_layout(0.1)
	    plt.show()

```
# MultiGuass
``` python

	#!/usr/bin/python
	#  -*- coding:utf-8 -*-
	
	import numpy as np
	from scipy import stats
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	from mpl_toolkits.mplot3d import Axes3D
	from matplotlib import cm
	
	mpl.rcParams['axes.unicode_minus'] = False
	mpl.rcParams['font.sans-serif'] = 'SimHei'
	
	if __name__ == '__main__':
	    x1, x2 = np.mgrid[-5:5:51j, -5:5:51j]
	    x = np.stack((x1, x2), axis=2)
	
	    plt.figure(figsize=(9, 8), facecolor='w')
	    sigma = (np.identity(2), np.diag((3,3)), np.diag((2,5)), np.array(((2,1), (2,5))))
	    for i in np.arange(4):
	        ax = plt.subplot(2, 2, i+1, projection='3d')
	        norm = stats.multivariate_normal((0, 0), sigma[i])
	        y = norm.pdf(x)
	        ax.plot_surface(x1, x2, y, cmap=cm.Accent, rstride=1, cstride=1, alpha=0.9, lw=0.3)
	        ax.set_xlabel(u'X')
	        ax.set_ylabel(u'Y')
	        ax.set_zlabel(u'Z')
	    plt.suptitle(u'二元高斯分布方差比较', fontsize=18)
	    plt.tight_layout(1.5)
	    plt.show()

```
# gamma
``` python

	# -*- coding:utf-8 -*-
	# /usr/bin/python
	
	import numpy as np
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	from scipy.special import gamma
	from scipy.special import factorial
	
	mpl.rcParams['axes.unicode_minus'] = False
	mpl.rcParams['font.sans-serif'] = 'SimHei'
	
	
	if __name__ == '__main__':
	    N = 5
	    x = np.linspace(0, N, 50)
	    y = gamma(x+1)
	    plt.figure(facecolor='w')
	    plt.plot(x, y, 'r-', x, y, 'm*', lw=2)
	    z = np.arange(0, N+1)
	    f = factorial(z, exact=True)    # 阶乘
	    print f
	    plt.plot(z, f, 'go', markersize=8)
	    plt.grid(b=True)
	    plt.xlim(-0.1,N+0.1)
	    plt.ylim(0.5, np.max(y)*1.05)
	    plt.xlabel(u'X', fontsize=15)
	    plt.ylabel(u'Gamma(X) - 阶乘', fontsize=15)
	    plt.title(u'阶乘和Gamma函数', fontsize=16)
	    plt.show()

```
# Benford
``` python

	# -*- coding:utf-8 -*-
	# /usr/bin/python
	
	import numpy as np
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	from time import time
	from scipy.special import factorial
	import math
	
	mpl.rcParams['axes.unicode_minus'] = False
	mpl.rcParams['font.sans-serif'] = 'SimHei'
	
	
	def top1(number, a):
	    number /= a
	    while number >= 10:
	        number /= 10
	        a *= 10
	    return number, a
	
	
	def top2(number, N2):
	    while number >= N2:
	        number /= 10
	    n = number
	    while number >= 10:
	        number /= 10
	    return n, number
	
	
	def top3(number):
	    number -= int(number)
	    return int(10 ** number)
	
	
	def top4(number):
	    number -= int(number)
	    frequency[int(10 ** number) - 1] += 1
	
	
	if __name__ == '__main__':
	    N = 100000
	    x = range(1, N+1)
	    frequency = np.zeros(9, dtype=np.int)
	    f = 1
	    print '开始计算...'
	    t0 = time()
	    # top1
	    # a = 1
	    # for t in x:
	    #     f *= t
	    #     i, a = top1(f, a)
	    #     # print t, i, f, a
	    #     frequency[i-1] += 1
	
	    # top2
	    # N2 = N ** 3
	    # for t in x:
	    #     f *= t
	    #     f, i = top2(f, N2)
	    #     frequency[i-1] += 1
	
	    # Top 3：实现1
	    # f = 0
	    # for t in x:
	    #     f += math.log10(t)
	    #     frequency[top3(f) - 1] += 1
	
	    # Top 3：实现2
	    # y = np.cumsum(np.log10(x))
	    # for t in y:
	    #     frequency[top3(t) - 1] += 1
	
	    # Top 4：本质与Top3相同
	    y = np.cumsum(np.log10(x))
	    map(top4, y)
	
	    t1 = time()
	    print '耗时：', t1 - t0
	    print frequency
	    t = np.arange(1, 10)
	    plt.plot(t, frequency, 'r-', t, frequency, 'go', lw=2, markersize=8)
	    for x,y in enumerate(frequency):
	        plt.text(x+1.1, y, frequency[x], verticalalignment='top', fontsize=15)
	    plt.title(u'%d!首位数字出现频率' % N, fontsize=18)
	    plt.xlim(0.5, 9.5)
	    plt.ylim(0, max(frequency)*1.03)
	    plt.grid(b=True)
	    plt.show()
	
	    # 使用numpy
	    # N = 170
	    # x = np.arange(1, N+1)
	    # f = np.zeros(9, dtype=np.int)
	    # t1 = time()
	    # y = factorial(x, exact=False)
	    # z = map(top, y)
	    # t2 = time()
	    # print '耗时 = \t', t2 - t1
	    # for t in z:
	    #     f[t-1] += 1
	    # print f

```
# Pearson
``` python

	#!/usr/bin/python
	#  -*- coding:utf-8 -*-
	
	import numpy as np
	from scipy import stats
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	import warnings
	
	mpl.rcParams['axes.unicode_minus'] = False
	mpl.rcParams['font.sans-serif'] = 'SimHei'
	
	
	def calc_pearson(x, y):
	    std1 = np.std(x)
	    # np.sqrt(np.mean(x**2) - np.mean(x)**2)
	    std2 = np.std(y)
	    cov = np.cov(x, y, bias=True)[0,1]
	    return cov / (std1 * std2)
	
	
	def intro():
	    N = 10
	    x = np.random.rand(N)
	    y = 2 * x + np.random.randn(N) * 0.1
	    print x
	    print y
	    print '系统计算：', stats.pearsonr(x, y)[0]
	    print '手动计算：', calc_pearson(x, y)
	
	
	def rotate(x, y, theta=45):
	    data = np.vstack((x, y))
	    # print data
	    mu = np.mean(data, axis=1)
	    mu = mu.reshape((-1, 1))
	    # print mu
	    data -= mu
	    # print data
	    theta *= (np.pi / 180)
	    c = np.cos(theta)
	    s = np.sin(theta)
	    m = np.array(((c, -s), (s, c)))
	    return m.dot(data) + mu
	
	
	def pearson(x, y, tip):
	    clrs = list('rgbmycrgbmycrgbmycrgbmyc')
	    plt.figure(figsize=(10, 8), facecolor='w')
	    for i, theta in enumerate(np.linspace(0, 90, 6)):
	        xr, yr = rotate(x, y, theta)
	        p = stats.pearsonr(xr, yr)[0]
	        # print calc_pearson(xr, yr)
	        print '旋转角度：', theta, 'Pearson相关系数：', p
	        str = u'相关系数：%.3f' % p
	        plt.scatter(xr, yr, s=40, alpha=0.9, linewidths=0.5, c=clrs[i], marker='o', label=str)
	    plt.legend(loc='upper left', shadow=True)
	    plt.xlabel(u'X')
	    plt.ylabel(u'Y')
	    plt.title(u'Pearson相关系数与数据分布：%s' % tip, fontsize=18)
	    plt.grid(b=True)
	    plt.show()
	
	
	if __name__ == '__main__':
	    # warnings.filterwarnings(action='ignore', category=RuntimeWarning)
	    np.random.seed(0)
	
	    # intro()
	
	    N = 1000
	    # tip = u'一次函数关系'
	    # x = np.random.rand(N)
	    # y = np.zeros(N) + np.random.randn(N)*0.001
	
	    # tip = u'二次函数关系'
	    # x = np.random.rand(N)
	    # y = x ** 2 #+ np.random.randn(N)*0.002
	
	    # tip = u'正切关系'
	    # x = np.random.rand(N) * 1.4
	    # y = np.tan(x)
	
	    # tip = u'二次函数关系'
	    # x = np.linspace(-1, 1, 101)
	    # y = x ** 2
	
	    tip = u'椭圆'
	    x, y = np.random.rand(2, N) * 60 - 30
	    y /= 5
	    idx = (x**2 / 900 + y**2 / 36 < 1)
	    x = x[idx]
	    y = y[idx]
	
	    pearson(x, y, tip)

```

# candle
``` python

	#!/usr/bin/python
	# -*- coding:utf-8 -*-
	
	import numpy as np
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	from matplotlib.finance import candlestick_ohlc
	
	
	if __name__ == "__main__":
	    mpl.rcParams['font.sans-serif'] = [u'SimHei']
	    mpl.rcParams['axes.unicode_minus'] = False
	
	    np.set_printoptions(suppress=True, linewidth=100, edgeitems=5)
	    data = np.loadtxt('7.SH600000.txt', dtype=np.float, delimiter='\t', skiprows=2, usecols=(1, 2, 3, 4))
	    data = data[:30]
	    N = len(data)
	
	    t = np.arange(1, N+1).reshape((-1, 1))
	    data = np.hstack((t, data))
	
	    fig, ax = plt.subplots(facecolor='w')
	    fig.subplots_adjust(bottom=0.2)
	    candlestick_ohlc(ax, data, width=0.6, colorup='r', colordown='g', alpha=0.9)
	    plt.xlim((0, N+1))
	    plt.grid(b=True)
	    plt.title(u'股票K线图', fontsize=18)
	    plt.tight_layout(2)
	    plt.show()

```