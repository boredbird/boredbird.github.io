---
title: SVM
date: 2017-11-12 14:15:12 
categories: "机器学习" 
tags: 
     - SVM
description: SVM
toc: true
---
# 支持向量机SVM的原理和目标
## 线性可分支持向量机
硬间隔最大化hard margin maximization;硬间隔支持向量机

### 分割超平面
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112145917.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 分割超平面的思考
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112145956.png" width="80%">
  <div class="figcaption">
  </div>
</div>

<!--more-->

## 线性支持向量机
软间隔最大化soft margin maximization;软间隔支持向量机
### 线性分类问题
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150039.png" width="80%">
  <div class="figcaption">
  </div>
</div>
### 输入数据
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150123.png" width="80%">
  <div class="figcaption">
  </div>
</div>
### 线性可分支持向量机
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150230.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150244.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150259.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 非线性支持向量机
核函数kernel function

# 支持向量机的计算过程和算法步骤
## 推导目标函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150547.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 最大间隔分离超平面
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150650.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 函数间隔和几何间隔
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150729.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 建立目标函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150818.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150914.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150935.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112150950.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112151005.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112151021.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112151031.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 线性可分支持向量机学习算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112151656.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112151705.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 线性SVM的目标函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152020.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 带松弛因子的SVM拉格朗日函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152127.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 代入目标函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152149.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 最终的目标函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152220.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 线性支持向量机
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112151850.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112151903.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 线性支持向量机学习算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152348.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152359.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 损失函数分析
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152453.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 核函数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152616.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152637.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 高斯核
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152822.png" width="80%">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112152835.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## SVM中系数的求解：SMO
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112153001.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## SMO:序列最小最优化
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112153043.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 二变量优化问题
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112153152.png" width="60%">
  <div class="figcaption">
  </div>
</div>

## SMO的迭代公式
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112153238.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 退出条件
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112153313.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# SVM总结
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/SVM/TIM截图20171112153419.png" width="80%">
  <div class="figcaption">
  </div>
</div>

