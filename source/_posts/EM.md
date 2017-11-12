---
title: EM
date: 2017-11-12 19:15:12 
categories: "机器学习" 
tags: 
     - EM
     - 主题模型
description: 主题模型
toc: true
---
# 引子
## k-Means算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112192635.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 对K-Means的思考
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112192704.png" width="80%">
  <div class="figcaption">
  </div>
</div>

<!--more-->

## Jensen不等式：若f是凸函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112192840.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 最大似然估计
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112192930.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 二项分布的最大似然估计
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193004.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 进一步考察
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193106.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 按照MLE的过程分析
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193203.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 化简对数似然函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193248.png" width="60%">
  <div class="figcaption">
  </div>
</div>

#### 参数估计的结论
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193330.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 符合直观想象
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193422.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 问题：随机变量无法直接（完全）观察到
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193618.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 从直观理解猜测GMM的参数估计
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193703.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 建立目标函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193756.png" width="80%">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193809.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 第一步：估算数据来自哪个组份
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112193924.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 第二步：估计每个组份的参数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112194011.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# EM算法
## EM算法的提出
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112194109.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 通过最大似然估计建立目标函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112194158.png" width="60%">
  <div class="figcaption">
  </div>
</div>

### 问题的提出
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112194450.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### Jensen不等式
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112194525.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 寻找尽量紧的下界
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112194624.png" width="60%">
  <div class="figcaption">
  </div>
</div>

### 进一步分析
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112194659.png" width="60%">
  <div class="figcaption">
  </div>
</div>

## EM算法整体框架
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112194758.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 坐标上升
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112194913.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 从理论公式推导GMM
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112204148.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### E-step
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112204702.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### M-step
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112204747.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 对均值求偏导
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112204846.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 高斯分布的均值
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112204955.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 高斯分布的方差：求偏导，等于0
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112205041.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 多项分布的参数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112205125.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 拉格朗日乘子法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112205225.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 求偏导，等于0
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112205303.png" width="60%">
  <div class="figcaption">
  </div>
</div>

# 结论
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/EM/TIM截图20171112205423.png" width="60%">
  <div class="figcaption">
  </div>
</div>

