---
title: GBDT算法原理与系统设计简介-来自wepon的分享
date: 2017-10-02 17:27:04 
categories: "机器学习" 
tags: 
     - GBDT 
description: GBDT算法原理与系统设计简介-来自wepon的分享
---

# 一、泰勒公式
* 定义：泰勒公式是一个用函数在某点的信息描述其附近取值的公式。局部有效性
![](https://i.imgur.com/nIrdPkM.png)
# 二、最优化方法
## 2.1 梯度下降法（Gradient descend method）
![](https://i.imgur.com/OtJtsoy.png)
## 2.2 牛顿法（Newton's method）
![](https://i.imgur.com/8zoVsFG.png)
# 三、从参数空间到函数空间
## 3.1 从Gradient descend 到 Gradient Boosting
![](https://i.imgur.com/4TRkwMS.png)
![](https://i.imgur.com/Jj8rUYo.png)
## 3.2 从Newton's method 到 Newton Boosting
![](https://i.imgur.com/hJRvJer.png)
![](https://i.imgur.com/lO7KTEr.png)
# 四、Gradient Boosting Tree算法原理
![](https://i.imgur.com/KclXmop.png)
![](https://i.imgur.com/SISeq7n.png)
# 五、Newton Boosting Tree算法原理：详解XGBoost
## 5.1 模型函数形式
![](https://i.imgur.com/SGENIVu.png)
![](https://i.imgur.com/bEdk0hq.png)
## 5.2 目标函数
![](https://i.imgur.com/TlInpcp.png)
### 5.2.1 正则项
![](https://i.imgur.com/fMlDTe1.png)
![](https://i.imgur.com/uArASZT.png)
### 5.2.2 误差函数的二阶泰勒展开
![](https://i.imgur.com/zpVimRg.png)
![](https://i.imgur.com/dMkJkKI.png)
![](https://i.imgur.com/9AQxjbh.png)
![](https://i.imgur.com/omqUwQk.png)
## 5.3 回归树的学习策略
![](https://i.imgur.com/RHJtO8t.png)
### 5.3.1 打分函数
![](https://i.imgur.com/kFwfgpE.png)
### 5.3.2 树节点分裂方法
![](https://i.imgur.com/nQDZs8n.png)
![](https://i.imgur.com/vbKq7gi.png)
![](https://i.imgur.com/zRVBwsj.png)
![](https://i.imgur.com/WPdpamn.png)
### 5.3.3 缺失值的处理
![](https://i.imgur.com/TzC0Jgx.png)
## 5.4 其它特性
![](https://i.imgur.com/6y8fXhr.png)
