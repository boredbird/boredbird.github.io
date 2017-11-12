---
title: PLSA
date: 2017-11-12 20:56:12 
categories: "机器学习" 
tags: 
     - PLSA
     - 主题模型
     - EM
description: 主题模型
toc: true
---
# PLSA模型
## PLSA模型概述
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112205947.png" width="80%">
  <div class="figcaption">
  </div>
</div>

## PLSA模型过程

<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210114.png" width="80%">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210128.png" width="80%">
  <div class="figcaption">
  </div>
</div>

<!--more-->

### 最大似然估计
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210238.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 目标函数分析
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210320.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 求隐含变量主题zk的后验概率
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210414.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 分析似然函数期望
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210454.png" width="80%">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210527.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 完成目标函数的建立
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210626.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### 目标函数的求解
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210705.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 分析第一等式
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210752.png" width="80%">
  <div class="figcaption">
  </div>
</div>

#### 同理分析第二等式
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210839.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# PLSA总结
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112210922.png" width="80%">
  <div class="figcaption">
  </div>
</div>

# PLSA进一步思考
<div class="fig figcenter fighighlight">
  <img src="/assets/chinahadoop/PLSA/TIM截图20171112211031.png" width="80%">
  <div class="figcaption">
  </div>
</div>