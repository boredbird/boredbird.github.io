---
title: 记一次python数据处理性能调优
date: 2017-10-21 11:24:12 
categories: "Python" 
tags: 
     - Python
description: 记一次python数据处理性能调优
---

Python垃圾回收机制
根据官方的描叙，Python中，有2中方式将会触发垃圾回收：
1、用户显示调用gc.collect()
2、每次Python为新对象分配内存时，检查threshold阀值，当对象数量超过threshold设置的阀值就开始进行垃圾回收。

因为数据量太大，处理过程中留下太多暂时不能清除的变量，而python的垃圾回收却在一遍一遍地扫这些不断在增长的列表，导致程序受到的影响越来越大。赶紧证实一下，import gc，然后在数据载入模块前gc.disable（）,结束后再gc.enable()。结果原来要跑将近两个小时的程序，这下不用5分钟就跑完了。cool~！用gc.get_count()也证明了之前的猜想，在第一次运行之后临时变量数目就从几百上升到百万，并一直在涨。

如果你的python程序在处理大数据量的问题，并且出现某个子程序在做同样量的工作，却越跑越慢的情况。

程序代码：

``` python

	def series_trans(dataset):
	    # 一行转多行
	    dataset_trans = pd.DataFrame({'user_id':dataset['user_id'],
	                                   'shop_id':dataset['shop_id'],
	                                   'time_stamp':dataset['time_stamp'],
	                                   'longitude':dataset['longitude'],
	                                   'latitude':dataset['latitude'],
	                                   'wifi_infos':dataset['wifi_splits']})
	
	    return  dataset_trans
	
	
	print time.asctime( time.localtime(time.time()) )
	dataset_trans = series_trans(dataset.loc[0,:])
	
	for i in xrange(1,dataset.shape[0]):
	    if i % 10000 == 0:
	        print i
	        print time.asctime( time.localtime(time.time()) )
	
	    dataset_trans = dataset_trans.append(series_trans(dataset.loc[i,:]))

```

程序的性能表现如下：

```

	Sat Oct 21 11:01:30 2017
	10000
	Sat Oct 21 11:02:07 2017
	20000
	Sat Oct 21 11:03:41 2017
	30000
	Sat Oct 21 11:06:12 2017
	40000
	Sat Oct 21 11:09:37 2017
	50000
	Sat Oct 21 11:13:55 2017
	60000
	Sat Oct 21 11:19:10 2017
	70000
	Sat Oct 21 11:25:26 2017
	80000
	Sat Oct 21 11:33:03 2017
	90000
	Sat Oct 21 11:41:21 2017
	100000
	Sat Oct 21 11:50:33 2017
	110000
	Sat Oct 21 12:00:41 2017
	120000
	Sat Oct 21 12:11:45 2017
	130000
	Sat Oct 21 12:23:43 2017
	140000
	Sat Oct 21 12:36:37 2017
	150000
	Sat Oct 21 12:50:25 2017
	160000
	Sat Oct 21 13:05:10 2017
	170000
	Sat Oct 21 13:20:46 2017
	180000
	Sat Oct 21 13:37:18 2017
```

采用：dataset_trans.loc[10:19,] = dataset_trans
会提示错误：    
info_idx = indexer[info_axis]
IndexError: tuple index out of range


DataFrame is a 2-dimensional labeled data structure with columns of potentially different types.所以一般说来dataframe就是a set of columns, each column is an array of values. In pandas, the array is one way or another a (maybe variant of) numpy ndarray. 而ndarray本身不存在一种in place append的操作。。。因为它实际上是一段连续内存。。。任何需要改变ndarray长度的操作都涉及分配一段长度合适的新的内存，然后copy。。。这是这类操作慢的原因。。。如果pandas dataframe没有用其他设计减少copy的话，我相信Bren说的"That's probably as efficient as any"是很对的。。。所以in general, 正如Bren说的。。。Pandas/numpy structures are fundamentally not suited for efficiently growing.Matti 和 arynaq说的是两种常见的对付这个问题的方法。。。我想Matti实际的意思是把要加的rows收集成起来然后concatenate, 这样只copy一次。arynaq的方法就是预先分配内存比较好理解。。。如果你真的需要incrementally build a dataframe的话，估计你需要实际测试一下两种方法。。。我的建议是，如有可能，尽力避免incrementally build a dataframe, 比如用其他data structure 收集齐所有data然后转变成dataframe做分析。。。


via

* [Python垃圾回收(gc)拖累了程序执行性能？](http://blog.csdn.net/overstack/article/details/11603893)

* [python pandas 怎样高效地添加一行数据？](https://www.zhihu.com/question/36170252?sort=created)