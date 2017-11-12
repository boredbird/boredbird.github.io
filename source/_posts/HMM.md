---
title: 主题模型
date: 2017-11-12 22:06:12 
categories: "机器学习" 
tags: 
     - HMM
     - 贝叶斯网络
     - Baum-Welch
     - EM
     - Viterbi
description: 隐马尔科夫模型
toc: true
---
## HMM定义
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112225447.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 隐马尔科夫模型的贝叶斯网络
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112225714.png" width="80%">
  <div class="figcaption">
  </div>
</div>

<!--more-->

## HMM的参数
### HMM的确定
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112225814.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### HMM的参数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112225941.png" width="60%">
  <div class="figcaption">
  </div>
</div>

<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230035.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230044.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### HMM的参数总结
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230124.png" width="60%">
  <div class="figcaption">
  </div>
</div>

## HMM的两个基本性质
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230315.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## HMM举例
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230351.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 示例的各个参数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230439.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 示例的思考
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230513.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## HMM的3个基本问题
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230610.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 概率计算问题
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230657.png" width="60%">
  <div class="figcaption">
  </div>
</div>

#### 直接计算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230811.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230821.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230834.png" width="80%">
  <div class="figcaption">
  </div>
</div>

##### 直接计算法分析
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112230930.png" width="80%">
  <div class="figcaption">
  </div>
</div>

##### 借鉴算法的优化思想
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112231049.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 前向算法
##### 定义：前向概率-后向概率
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112231346.png" width="80%">
  <div class="figcaption">
  </div>
</div>

##### 前向算法定义
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112233757.png" width="80%">
  <div class="figcaption">
  </div>
</div>

##### 前向算法过程
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112233910.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112233920.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 后向算法
##### 后向算法定义
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234032.png" width="80%">
  <div class="figcaption">
  </div>
</div>

##### 后向算法过程
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234110.png" width="60%">
  <div class="figcaption">
  </div>
</div>

##### 后向算法的说明
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234154.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 前后向关系
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234317.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 单个状态的概率
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234446.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234458.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### r的意义
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234549.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 两个状态的联合概率
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234638.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234649.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 期望
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234808.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 学习算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234908.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 大数定理
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112234946.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 监督学习方法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235033.png" width="60%">
  <div class="figcaption">
  </div>
</div>

### Baum-Welch算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235131.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235143.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### EM过程
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235243.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 极大化
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235344.png" width="80%">
  <div class="figcaption">
  </div>
</div>


#### 初始状态概率
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235412.png" width="80%">
  <div class="figcaption">
  </div>
</div>


#### 转移概率和观测概率
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235505.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 预测算法
### 近似算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235643.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 算法：走棋盘/格子取数
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235817.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235829.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### Viterbi算法
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235914.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171112235928.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### Viterbi算法举例
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171113000033.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171113000045.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171113000100.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171113000110.png" width="80%">
  <img src="/assets/chinahadoop/HMM/TIM截图20171113000126.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## 总结
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/HMM/TIM截图20171113000304.png" width="80%">
  <div class="figcaption">
  </div>
</div>