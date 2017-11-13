---
title: 可视化—matploblib 解决中文显示的问题
date: 2017-10-07 10:43:12 
categories: "Python" 
tags: 
     - Python
     - matplotlib
description: 可视化—matploblib 解决中文显示的问题
---

### 导入相关包
``` python

	from matplotlib import mpl
	import matplotlib.pyplot as plt
```

### 指定字体
``` python

	mpl.rcParams['font.sans-serif'] = ['SimHei']
	mpl.rcParams['axes.unicode_minus'] = False
```

<!--more-->

### 测试：使用中文
``` python

	plt.title(u'我是中文')
```

