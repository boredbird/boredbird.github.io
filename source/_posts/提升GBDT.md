---
title: 提升GBDT
date: 2017-11-11 16:15:12 
categories: "机器学习" 
tags: 
     - 提升
     - GBDT
     - 决策树
description: 提升
toc: true
---
# 由决策树和随机森林的关系的思考
* 随机森林的决策树分别采样建立，相对独立。
* 思考：
* * 假定当前已经得到了m-1棵决策树，是否可以通过现有样本和决策树的信息，对第m棵决策树的建立产生有益的影响呢？
* * 各个决策树组成随机森林后，最后的投票过程可否在建立决策树时即确定呢？

# 提升的概念
* 提升是一个机器学习技术，可以用于回归和分类问题，它每一步产生一个弱预测模型（如决策树），并加权累加到总模型中；如果每一步的弱预测模型生成都是依据损失函数的梯度方向，则称之为梯度提升（Gradient Boosting）
* 梯度提升算法首先给定一个目标损失函数，它的定义域是所有可行的弱函数集合（基函数）；提升算法通过迭代的选择一个负梯度方向上的基函数来逐渐逼近局部极小值。这种在函数域的梯度提升观点对机器学习的很多领域有深刻影响。
* 提升的理论意义：如果一个问题存在弱分类器，则可以通过提升的办法得到强分类器。

<!--more-->

# 提升算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/提升/TIM截图20171111165558.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 提升算法推导
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/提升/TIM截图20171111165655.png" width="80%">
  <div class="figcaption">
  </div>
</div>

<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/提升/TIM截图20171111165800.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 提升算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/提升/TIM截图20171111165945.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 梯度提升决策树GBDT
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/提升/TIM截图20171111170101.png" width="80%">
  <img src="/assets/chinahadoop/提升/TIM截图20171111170237.png" width="80%">  
<div class="figcaption">
  </div>
</div>

## 参数设置和正则化
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/提升/TIM截图20171111170325.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 衰减因子、降采样
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/提升/TIM截图20171111170413.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## GBDT总结
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/提升/TIM截图20171111170450.png" width="80%">
  <div class="figcaption">
  </div>
</div>
