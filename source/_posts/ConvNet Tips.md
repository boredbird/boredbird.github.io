---
title: convnet-tips
date: 2017-10-08 21:06:12 
categories: "深度学习" 
tags: 
     - convnet
description: convnet-tips
toc: true
---

<a name='overfitting'></a>
### Addressing Overfitting

#### Data Augmentation

- Flip the training images over x-axis
- Sample random crops / scales in the original image
- Jitter the colors

#### Dropout 

- Dropout is just as effective for Conv layers. Usually people apply less dropout right before early conv layers since there are not that many parameters there compared to later stages of the network (e.g. the fully connected layers).
