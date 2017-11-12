---
title: AdaBoost
date: 2017-11-12 14:15:12 
categories: "机器学习" 
tags: 
     - 提升
     - AdaBoost
     - 决策树
description: 提升
toc: true
---
# Boosting的思想
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112142536.png" width="60%">
  <div class="figcaption">
  </div>
</div>

# AdaBoost算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112142651.png" width="80%">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112142718.png" width="80%">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112142731.png" width="80%">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112142745.png" width="80%">
  <div class="figcaption">
  </div>
</div>

<!--more-->

# AdaBoost误差上限
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112143143.png" width="80%">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112143240.png" width="80%">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112143351.png" width="80%">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112143418.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# 前向分步算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144030.png" width="60%">
  <div class="figcaption">
  </div>
</div>

## 前向分步算法的含义
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144100.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 前向分步算法的算法框架
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144139.png" width="80%">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144153.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 前向分步算法与AdaBoost
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144255.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 证明
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144322.png" width="80%">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144348.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 基分类器
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144426.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 权值的计算
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144459.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 分类错误率
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144527.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 权值的更新
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144552.png" width="60%">
  <div class="figcaption">
  </div>
</div>

### 权值和错误率的关键解释
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112144626.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# AdaBoost总结
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112143456.png" width="80%">
  <img src="/assets/chinahadoop/AdaBoost/TIM截图20171112143553.png" width="80%">
  <div class="figcaption">
  </div>
</div>