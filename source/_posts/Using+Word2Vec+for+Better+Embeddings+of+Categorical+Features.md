---
title: Using+Word2Vec+for+Better+Embeddings+of+Categorical+Features
date: 2018-07-16 16:38:12
categories: "深度学习"
tags:
     - Word2Vec
     - Embedding
description: Using+Word2Vec+for+Better+Embeddings+of+Categorical+Features
toc: true
---

### titile & author & year & source
key|info
----|----
titile|Using Word2Vec for Better Embeddings of Categorical Features
author|
year|2014 Apr 25
source|
keyword|category2vec
links|

### problems encountered
how do I represent my categorical features as vectors that my network can work with?

### main arguments
The most popular approach is embedding layers—you add an extra
layer to your network, which assigns a vector to each value of the
categorical feature. During training the network learns the weights for
the diierent layers, including those embeddings.

In this post I will show examples of `when this approach will fail`,
introduce `category2vec`, an alternative method for learning embeddingusing a second network and will present diierent ways of using those
embeddings in your primary network.

在任务中训练embedding主要会带来几个问题：
1. 这种训练出来的embedding是在拟合一个具体的任务或者训练集的过程中产出的，很难适用于其他问题。
2. 即使是在相同或者相似的训练集中产出的embedding，由于任务不同，可解释变量的也会不同。但独立于任务的预训练词向量可以复用。
3. embedding训练作为神经网络训练任务的一部分相当于引入了更多的参数会增加模型的复杂度，意味着需要更多的标记数据。


<!--more-->

```
Embedding layers are trained to bt a specibc task—the one the network
was trained on. Sometimes that’s exactly what you want. But in other
cases you might want your embeddings to capture some intuition about
the domain of the problem, thus reducing the risk of overbtting. You
can think of it as adding prior knowledge to your model, which helps it
to generalize.

Moreover, if you have diierent tasks on similar data, you can use the
embeddings from one task in order to improve your results on another.
This is one of the major tricks in the Deep Learning toolbox. It’s called
transfer learning, pretraining or multi-task learning, depending on the
context. The underlying assumption is that many of the unobserved
random variables explaining the data are shared across tasks. Since the
embeddings try to isolate these variables, they can be reused.

Most importantly, learning the embeddings as part of the network
increases the model’s complexity by adding many weights to the model,
which means you’ll need much more labeled data in order to learn.
```
### methods used
作者举了个例子：广告点击，训练广告商的词向量。把用户点击广告商的序列看成一个sentence，不同的是这些广告商是没有顺序的，可以直接忽略这些顺序（用户量数据比较大的情况下，这些顺序可以忽略）或者随机打乱广告商的点击前后顺序。

`category2vec`中的`category`应该指的是广告商，用户点击的是广告sku，广告商属于类别特征，而且类别数量很大。

```
From Word2Vec to Category2Vec
The idea is simple: we train word2vec on users’ click history. Each
“sentence” is now a set of advertisers that a user clicked on, and we try
to predict a specibc advertiser (“word”) based on other advertisers the
user liked (“context”). The only diierence is that, unlike sentences, the
order is not necessarily important. We can ignore this fact, or enhance
the data set with permutations of each history. You can apply thismethod
to any kinds of categorical features with high modality, e.g,
countries, cities, user ids, etc..
```

### critical challenges

### useful ideas for later use
`category2vec`在实际工作中的应用有很大的想象空间，比如作者举例可以根据用户的点击历史，训练出广告商的embedding，然后将这些embedding平均，用于表征用户的兴趣。

eg.
* 比如类目embedding的训练可以借鉴这个思路：用户点击sku的历史记录（sentence），sku的类目（words)；可以训练出类目embedding，然后类目embedding求平均可以表征用户的偏好。


```
There are three diierent ways to use the new embeddings in our
model:
1. Use the new embeddings as features for the new network. For
example, we can average the embeddings of all the advertisers the
user clicked on, to represent the user history and use it to learn the
user’s tastes. The focus of this post is Neural Networks but you can
actually do it with any ML algorithm.

2. Initialized the weights of the embedding layer in your network,
with the embeddings we just learned. It’s like telling the network
—this is what I know from other tasks, now adjust it for the
current task.

3. Multitask Learning—take two networks and train them together
with parameter sharing. You can either force them to share the
embeddings (hard sharing), or allow them to have slightly
diierent weights by “punishing” the networks when their weights
are too diierent (soft sharing). This is usually done by
regularizing the distance between the weights.

You may think about it as passing knowledge from one task to
another, but also as a regularization technique: the word2vec
network acts as a regularizer to the other network, and forces it to
learn embeddings with characteristics that we are interested in.
```
