---
title: python读取文件数据的几种方式
date: 2017-11-13 14:53:12 
categories: "Python" 
tags: 
     - Python
description: python读取文件数据的几种方式
---
# 方式一：f = file(path)

``` python

    f = file(path)
    x = []
    y = []
    for i, d in enumerate(f):
        if i == 0:
            continue
        d = d.strip()
        if not d:
            continue
        d = map(float, d.split(','))
        x.append(d[1:-1])
        y.append(d[-1])
    pprint(x)
    pprint(y)
    x = np.array(x)
    y = np.array(y)
```

# 方式二：Python自带库csv

``` python

	import csv
    f = file(path, 'rb')
    print f
    d = csv.reader(f)
    for line in d:
        print line
    f.close()
```

# 方式三：Python自带库numpy

``` python

	import numpy as np
	p = np.loadtxt(path, delimiter=',', skiprows=1)
```


# 方式四：Python自带库pandas

``` python

	import pandas as pd
	data = pd.read_csv(path)
```

