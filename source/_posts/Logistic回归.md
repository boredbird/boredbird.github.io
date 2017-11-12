---
title: Logistic回归
date: 2017-11-11 11:25:12 
categories: "机器学习" 
tags: 
     - 回归
     - Logistic
description: Logistic回归
toc: true
---

# Logistic回归
分类问题的首选算法;

线性回归：最大似然估计+高斯分布；

Logistic回归：最大似然估计+伯努利分布；

Logistic回归是事件发生几率取对数下的线性回归。高斯分布和伯努利分布都是属于指数族分布，所以说逻辑回归是广义线性模型GLM回归。

## Logistic/Sigmoid函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111113157.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## Logistic回归参数估计
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111114625.png" width="80%">
  <div class="figcaption">
  </div>
</div>

<!--more-->

### 对数似然函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111114737.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 参数的迭代
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111114828.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### Logistic回归的损失函数A：
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111115107.png" width="80%">
  <div class="figcaption">
  </div>
</div>
### Logistic回归的损失函数B：
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111115122.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 广义线性模型GLM
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111120722.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# 多分类：Softmax回归
## Softmax名字由来
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111121449.png" width="80%">
  <div class="figcaption">
  </div>
</div>
## Softmax回归
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111120827.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# 信息熵
## 定义信息量
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111121645.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 熵
熵是随机变量不确定性的度量，不确定性越大，熵值越大。
若随机变量退化成定值，熵最小，为0；若随机分布为均匀分布，熵最大。
## 熵的定义
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111121724.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 熵的公式推导
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111121859.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 均匀分布的信息熵
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111121951.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 联合熵、条件熵、相对熵
### 联合熵、条件熵
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111122343.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 推导条件熵的定义公式
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111122430.png" width="60%">
  <div class="figcaption">
  </div>
</div>

### 相对熵、KL散度
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111122559.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 互信息
### 互信息的定义
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111123042.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 互信息与条件熵的关系
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111123141.png" width="60%">
  <div class="figcaption">
  </div>
</div>

## 公式
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111123335.png" width="80%">
  <div class="figcaption">
  </div>
</div>
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/Logistic回归/TIM截图20171111123431.png" width="80%">
  <div class="figcaption">
  </div>
</div>