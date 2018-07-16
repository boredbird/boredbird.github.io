---
title: word embedding materials
date: 2018-07-16 14:28:12
categories: "深度学习"
tags:
     - Word2vec
description: word embedding materials
toc: true
---

https://mp.weixin.qq.com/s/BLGlefsHTy44hZyXj06pbQ

Hinton 1986 《Learning distributed representations of concepts》
《Linguistic Regularities in Continuous Space Word Representations》
网易有道最初出品的一篇干货《Deep Learning实战之word2vec》
（1）第一篇必须是由 gensim 作者 Radim Řehůřek 本人写的 word2vec 使用教程：《Word2vec Tutorial》，在其本人的博客上。博文最后还给出了他是如何将原始 Google 的C版本代码优化到3倍速的视频讲解噢。真是一手资料呢！
（2）第二篇是数据挖掘竞赛平台 Kaggle 在其比赛“When bag of words meets bags of popcorn”中配套给出的教程，step by step。结合比赛的实际数据，从清洗数据到调参数。实战味道更浓，排版还更清楚！
（3）第三篇是最新的，由微博@52nlp 发表的最新文章《中英文维基百科语料上的Word2Vec实验》，中文语料，代码和结果都贴在了博文里面，完全没有废话。


<!--more-->


通过可视化的方法来研究 word embeddings。
一篇是 Chris Moody 的博文《A Word is Worth a Thousand Vectors》。如果你也对之前的 vector('king') - vector('man') + vector('woman') ≈ vector('queen') 的结果记忆深刻，还想了解更多，不妨去看这篇博文。在文中作者将这些结果进行了动态展示，分析了其背后的“语义”都究竟是什么，更加脑洞大开地把这种加减法运算运用在服装类商品数据上，结果直观地找出了相似的服饰！
第二篇类似的文章是 Hendrik Heuer 的 《word2vec: From theory to practice》的 Slides。他把 word2vec 的语义表示与矩阵分解联系在一起，这类等价矩阵分解的想法可以有很多应用。
第三篇也是和矩阵分解有关，发表在 NIPS'14 的论文，《Neural Word Embedding as Implicit Matrix Factorization》，文中认为 word2vec 中的 word embedding 其实就是 PMI 矩阵的分解，很有启发性。

《word analogy task详解及python版本的测试脚本》

word2vec 中考虑的是 linear 的 bag-of-words contexts。这里面，我们分三点来看：linear、bag-of-words、contexts。linear 强调的就是 plain，没有额外 word-level 以外的信息的，比如 syntax，比如 relation，比如 anything you can imagine；bag-of-words 强调的是 non-ordered，也就是说，词袋模型，这个 word2vec 是没有考虑语序的——丢失了很多信息对不对？第三个是 contexts，一方面是说，word2vec 只能考虑上下文信息（没有考虑词汇内部或者更高的 global/document-level 信息），另一方面是说，这个 contexts 也是被 window size 框住大小的，导致太大的 size computational cost 太大；太小的 size 又不能 handle 足够的信息，同时也会容易出现很多不想出现的词和想出现但没出现的词。

#### linear
打破 linear 的方法，对于 NLPer 来说，首先就会想到加入 dependency relation，使用已经比较成熟的 dependency parsing（比如 Stanford 的工具），就可以很快引入各种语法树结构，既多了non-linear 的 relation 关系，又有了更多的 tag 作为额外信息，而且还有很顺手的工具包。这方面的工作主要有：

Omer Levy and Yoav Goldberg. 2014. Dependency based word embeddings. In Proceedings of ACL.
Wang Ling, Chris Dyer, Alan Black, and Isabel Trancoso. 2015. Two/too simple adaptations of word2vec for syntax problems. In Proc. of NAACL.
Mohit Bansal, Kevin Gimpel, Karen Livescu. 2014. Tailoring Continuous Word Representations for Dependency Parsing. ACL.

总结他们的思想，主要是将抽取好的 dependency relation 或者其他 relation 和 信息，表达成 modifier-relation/tag 的 pair，这个 pair 作为新的 context，替代原先 word2vec 中的 context 信息。

#### bag-of-words
bag-of-words 可以说不仅有 non-order 的问题，还有 words 的问题。也就是说，现在的工作是基于 word/token level 去做的，但实际上已经有不少人质疑这点，认为 character-level 的信息足够可以当做 input 输入。对于 non-order 方面，有人提出了用多个 embedding matrix 来增强 word2vec 中的 同一个 embedding matrix，从而使得原始的 context 位置信息可以保留；而其实刚才上面 linear 增强部分提到的 dependency pair 的方法也可以看做是保留了 order。而，关于 word-level 的问题，很多人虽然考虑了 morpheme 层面的信息，但不能算是直接替代 word-level input；相反，MSR 的 Deep Learning 组，由 Jianfeng Gao 等人 lead 的 DSSM （Deep Structured Semantic Model or Deep Semantic Similarity Model）则提倡从 Sub-Word Unit （SWU）的层面进行输入。相关工作可见：

Mikolov Tomáš, Sutskever Ilya, Deoras Anoop, Le Hai-Son, Kombrink Stefan, Černocký Jan: Subword Language Modeling with Neural Networks. Not published (rejected from ICASSP 2012).
Omer Levy and Yoav Goldberg. 2014. Dependencybased word embeddings. In Proceedings of ACL.
MSR DSSM 系列：
[Huang, He, Gao, Deng, Acero, Heck, CIKM2013]
[Shen, He, Gao, Deng, Mesnil, WWW2014]
[Gao, He, Yih, Deng, ACL2014]
[Yih, He, Meek, ACL2014]
[Song, He, Gao, Deng, Shen, MSR-TR 2014]
[Gao, Pantel, Gamon, He, Deng, Shen, EMNLP2014]
[Shen, He, Gao, Deng, Mesnil, CIKM2014]
[He, Gao, Deng, ICASSP2014 Tutorial]
[Liu, Gao, He, NAACL2015] [Gao, He, Deng, MSR-TR-2015]

Siyu Qiu, Qing Cui, Jiang Bian, Bin Gao, and Tie-Yan Liu, Co-learning of Word Representations and Morpheme Representations, COLING 2014.

#### contexts
既然单纯的 context 可以认为是有用的，也可以被认为是不足的。除了固定 window size 内的上下文 contexts words 信息，还有什么可以用的信息呢？这样的考虑下，又带来了两种不同的改进。一种是直接替换掉 contexts words，用其他 enriched information words，比如 modifier-dependency-label pairs，比如 related word pairs（比如 WordNet 里那些 synonymy words）。另一种就是直接在 local contexts（即 window size 内的 context）的基础上，结合进 global contexts 或者其他 additional information。这种结合多数是线性 combine 进另一个神经网络，首创的就是 Huang et al., 2012 年的非常重要的论文。其他相关改变 contexts 的文章有：

Eric H. Huang, Richard Socher, Christopher D. Manning, Andrew Y. Ng. 2012. Improving Word Representations via Global Context and Multiple Word Prototypes. ACL.
Asli Celikyilmaz, Dilek Hakkani-Tur, Panupong Pasupat, and Ruhi Sarikaya. 2015. Enriching Word Embeddings Using Knowledge Graph for Semantic Tagging in Conversational Dialog Systems. AAAI
Mo Yu and Dredze. 2014. Improving Lexical Embeddings with Semantic Knowledge. ACL


 CSE 599 - Advanced in NLP

 Survey
Bengio et al’s survey on representation learning
Yoshua Bengio, Aaron Courville and Pascal Vincent. “Representation Learning: A Review and New Perspectives.” pdf TPAMI 35:8(1798-1828) 这篇没得说，开山之作，比较长，小S 打印下来读过许多遍，可以让你对这个领域找到一些感觉。

Bengio, LeCun Yann, Yoshua Bengio and Geoffrey Hinton’s survey on Nature
Yann LeCun, Yoshua Bengio and Geoffrey Hinton. “Deep Learning” pdf Nature 521, 436–444 三位深度学习的鼻祖和大佬联合出品的最新 Nature 文章，简要介绍了几种模型及其分别的优势和适用领域。小S 推荐其中的 CNN 部分，卷积神经网络，写得尤其清楚。另外，现在 CSDN 上有中文翻译的版本。

Embeddings & Language Models
Skip-gram embeddings
Tomas Mikolov, Kai Chen, Greg Corrado, and Jeffrey Dean. “Efficient Estimation of Word Representations in Vector Space.” pdf ICLR, 2013. 这篇没啥好介绍的啦，Mikolov 发力的首篇，word2vec 的前身。

Tomas Mikolov, Ilya Sutskever, Kai Chen, Greg Corrado, and Jeffrey Dean. “Distributed Representations of Words and Phrases and their Compositionality.” [pdf] NIPS, 2013.

[king-man+woman=queen] Tomas Mikolov, Wen-tau Yih, and Geoffrey Zweig. “Linguistic Regularities in Continuous Space Word Representations.” pdf NAACL, 2013. 这篇就是第一次出现 word2vec 的神话的论文，里面指出，我们经过词向量的表示，可以使用加减乘除这种简单的线性计算，得出 king-man = queen-woman 这样的度量！是不是很神奇很炫酷！可以说，word2vec 的火爆，有一定程度来自于这个 magic 公式。而且后来，也演变成了 word analogy 的 evaluation task。

[technical note] Yoav Goldberg and Omer Levy “word2vec explained: deriving Mikolov et al.’s negative-sampling word-embedding method” pdf Tech-report 2013 这是后来 Levy 等人对于 word2vec 的一些推导解释，因为 Mikolov 的论文及其最初放出的 Google 版本的 word2vec 代码，都比较简洁（混乱）。

[buzz-busting] Omer Levy and Yoav Goldberg “Linguistic Regularities in Sparse and Explicit Word Representations” pdf CoNLL-2014 Best Paper Award 如果说 word embedding 这边，除了 Mikolov，就应该是 Levy 了。

[lessons learned] Omer Levy, Yoav Goldberg, Ido Dagan “Improving Distributional Similarity with Lessons Learned from Word Embeddings” pdf, TACL 2015 这篇也是我认为的 DL in NLP 中带来的新风潮，就是说，因为这东西充满了 magic，不可解释性，所以相关的讨论类，分析类的论文就变得多起来（不是简单的应用）。这篇论文很值得一看，里面的评测还是很多的。

[syntax-word order] Wang Liang, Chris Dyer, Alan Black, Isabel Trancoso. “Two/Too Simple Adaptations of Word2Vec for Syntax Problems” pdf NAACL 2015 (Short) 这篇是刚刚结束的 NAACL-HIT 2015 大会的论文，虽然只是 Short。但提出了基于 word2vec 的原始 CBOW 和 SkipGram 的两种改进模型，都用来提升模型对于 syntax-based word order 的建模能力。简单有效有代码。

Embedding enhancement: Syntax, Retrofitting, etc
[dependency embeddings] Omer Levy and Yoav Goldberg “Dependency Based Word Embeddings” pdf ACL 2014 (Short) 这篇应该也是很有代表的改进 word2vec 的一篇，改进的主要是 SkipGram 模型，融入 NLP 人最容易考虑到的 dependency relation 信息。

[dependency embeddings] Mohit Bansal, Kevin Gimpel and Karen Livescu. “Tailoring Continuous Word Representations for Dependency Parsing” pdf ACL 2014 (Short) 这篇和楼上（汗，楼上）那篇一样，也是加入 dependency relation 信息，但是对于信息的 representation 不太一样。细微不同。

[retrofitting with lexical knowledge] Manaal Faruqui, Jesse Dodge, Sujay Kumar Jauhar, Chris Dyer, Eduard Hovy and Noah A. Smith. “Retrofitting Word Vectors to Semantic Lexicons” pdf, NAACL 2015

[contrastive estimation] Mnih and Kavukcuoglu, “Learning Word Embeddings Efficiently with Noise-Contrastive Estimation.” pdf NIPS 2013

[embedding documents] Quoc V Le, Tomas Mikolov. “Distributed representations of sentences and documents” pdf ICML 2014 Quoc 的经典文章，必看。不过比较有争议……尽管如此，后来还是被作为一个 baseline。

[synonymy relations] Mo Yu, Mark Dredze. “Improving Lexical Embeddings with Semantic Knowledge” pdf ACL 2014 (Short) 这篇使用了 knowledge base 中的一些思想，把一些同义词的关系作为 additional information 考虑进去，但是模型比较复杂。看看就好。

[embedding relations] Asli Celikyilmaz, Dilek Hakkani-Tur, Panupong Pasupat, Ruhi Sarikaya. “Enriching Word Embeddings Using Knowledge Graph for Semantic Tagging in Conversational Dialog Systems” pdf AAAI 2015 (Short)

[multimodal] Angeliki Lazaridou, Nghia The Pham and Marco Baroni. “Combining Language and Vision with a Multimodal Skip-gram Model” pdf NAACL 2015 multimodal 的代表作。很多童鞋包括小S 可能对 multimodal 不太熟悉，可以了解一下，这个方向现在也被一些大佬看好。

[syntax-word order] Wang Liang, Chris Dyer, Alan Black, Isabel Trancoso. “Two/Too Simple Adaptations of Word2Vec for Syntax Problems” pdf NAACL 2015 (Short) 刚才上面已经点评过了。这篇是刚刚结束的 NAACL-HIT 2015 大会的论文，虽然只是 Short。但提出了基于 word2vec 的原始 CBOW 和 SkipGram 的两种改进模型，都用来提升模型对于 syntax-based word order 的建模能力。简单有效有代码。

Embedding enhancement: Word order, Morphological, etc
[syntax-word order] Wang Liang, Chris Dyer, Alan Black, Isabel Trancoso. “Two/Too Simple Adaptations of Word2Vec for Syntax Problems” pdf NAACL 2015 (Short) 刚才上面已经点评过了。这篇是刚刚结束的 NAACL-HIT 2015 大会的论文，虽然只是 Short。但提出了基于 word2vec 的原始 CBOW 和 SkipGram 的两种改进模型，都用来提升模型对于 syntax-based word order 的建模能力。简单有效有代码。

[word order] Rie Johnson and Tong Zhang. Effective use of word order for text categorization with convolutional neural networks. pdf NAACL 2015 这篇文章……被小S 一度乌龙的记成了 best paper，到处找人请教其精华所在。现在十分汗颜。Tong Zhang 二作的文章。应该是比较 generic 的把 CNN 运用到 text 上的成功作。有代码，有很多实验结果。分别用在了两个任务上，一个 sentiment classification，一个 text categorisation，分别讨论了不同参数对于这两个任务结果的影响。

[word order] Radu Soricut and Franz Och. “Unsupervised Morphology Induction Using Word Embeddings” pdf NAACL 2015 Best Paper Awards 这才是真正的 best paper。是很直观的 Google 出品。个人感觉是 Google 真的遇到了这种需求，很好的做了出来。简单说就是可以把 beautiful → beautifully 这种类似的 relation 都很好的抽出来，并且不会误判 on → only 这种。他们的算法也很直观，改造了一下 word analogy 的公式，全篇基于 rank 的思想来做 morphological relation 的 extraction 和 apply。具有一定通用性。

[morphology] Minh-Thang Luong Richard Socher Christopher D. Manning. “Better Word Representations with Recursive Neural Networks for Morphology” pdf CoNLL 2013

[morpheme] Siyu Qiu, Qing Cui, Jiang Bian, Bin Gao, Tie-Yan Liu. “Co-learning of Word Representations and Morpheme Representations” pdf COLING 2014 MSRA 出品的，可以把 word embedding 和 morpheme embedding 一起学出，个人感觉只是 concatenate 这种思想比较有用，其他内容比较一般。

[morphological] Ryan Cotterell and Hinrich Schütze. “Morphological Word-Embeddings” pdf NAACL 2015 (Short)

[regularization] Dani Yogatama, Manaal Faruqui, Chris Dyer, Noah Smith. “Learning Word Representations with Hierarchical Sparse Coding” pdf ICML 2015 小S 重点关注的一篇论文，几度和作者交涉暂时还没要到代码（据说会发布），用 group LASSO 的方法去 regularise 以前的 word embedding。学出来的结果很 promising。另外这个组的人主要就是做 Bayesian Structured Regularization。

Embeddings as matrix factorization
[approximate interpretation] Levy and Goldberg, “Neural Word Embedding as Implicit Matrix Factorization.” pdf NIPS 2014

Omer Levy, Steffen Remus, Chris Biemann, and Ido Dagan. “Do Supervised Distributional Methods Really Learn Lexical Inference Relations?” pdf NAACL 2015 (Short)

Tim Rocktaschel, Sameer Singh and Sebastian Riedel. “Injecting Logical Background Knowledge into Embeddings for Relation Extraction” pdf NAACL 2015

[exact interpretation] Yitan Li, Linli Xu, Fei Tian, Liang Jiang, Xiaowei Zhong and Enhong Chen. “Word Embedding Revisited: A New Representation Learning and Explicit Matrix Factorization Perspective” pdf IJCAI 2015 相比 Levy 2014 NIPS 上的那篇解释性文章，这篇论文【直接】【显式】地【证明】了 word embedding 就是矩阵分解。

个人认为未来可能有四个小方向，分别是：interpretable relations, lexical resources, beyond words, beyond English。在分别展开这四个小方向之前，大家可能会问，那 word embedding models 的改进已经画上句号了么？



对于这个问题，小S 的答案几乎是肯定的。就好像曾经的 topic model 小浪潮，几乎可以认为是印度美女 S. Moghaddam 发表了两篇“集大成”的 topic model 变形大汇总（1. On the design of LDA models for aspect-based opinion mining; 2. The FLDA model for aspect-based opinion mining: addressing the cold start problem ），把圈圈框框画到了极致，抵达了“艺术之巅峰”——从此 topic model variants 鲜有新作。那么最近 pre-print 了一篇 word embedding 的论文，小S 认为也初有这样的风范。这篇论文就是《How to generate a good word embedding》，来自中科院自动化所，Siwei Lai, Kang Liu, Liheng Xu, Jun Zhao，pre-print 在 arXiv 上，有源码，还有博客自动导读。一作就是因一篇《Deep Learning in NLP(一)》博文备受瞩目的@licstar。篇幅有限，建议大家直接搜索作者本人的论文导读。他的这篇论文：先把从 NNLM，到 GloVe 的各种常见 word embedding model / NN 按两大方面分了类：aspect (i) 是如何 model relation between target word and contexts words 的；aspect (ii) 是如何 represent contexts 的。具体可以见 Table 1 和 Table 2. 同时作者指出，aspect (ii) 严重关系到了是否保留了 word order 这一重要信息。保留与否几乎损失 20% information （ref [12]）。为了更公平的比较各大 model，他除了比较了 2.1 中的常见的几大模型，还自创了一个“Virtual Order”模型，去完成单一变量下的比较。同时有一个问题，既然是在不同的任务下比较，那么performance的 metric 最好统一。他们就搞了个 Performance Gain Ratio,PGR 的东西。意思有点像 negative sampling。把你的 embedding 随机替换一个 random embedding，分别测试，然后看你比人家好出多少。Conclusion 其实粗看没什么意义，但是细看 Section 4的 每一部分还是有点东西的。比如 C&W 虽然原始论文中展现的结果是可以刻画 Paradigmatic relation between words，但其实是因为他们 fine-tune for extrinsic NLP tasks 的结果。具体几个 conclusions 可以见 Introduction 最后。



也就是说，曾经小S 总结过的 word embedding 的一些变形，几乎都能归为他论文中讨论到的两类。具体可以回复代码：GH006。那么回到最初的问题，如果 word embedding model 的变形已经鲜有新意，未来的 word embedding 研究热点在哪里？上文所说的 interpretable relations, lexical resources, beyond words, beyond English，都分别是什么意思？




interpretable relations



众所周知，word embedding / distributed embeddings 虽然效果显著，甚至被人称为“magic”，但其随之而来的就是“不可解释性”，或者说太笼统。把语料扔进去，跑出来的 dense vectors，虽然是基于 statistics，也就是 distributional hypothesis 的，但离 lexical/linguistic 的解释还差得很远。还记得之前我写过的 ACL 主席 Christopher Manning 在 ACL 2015 开幕式上的致辞么（回复代码：GH011），我们 NLPer 不能抛弃 linguistics！于是乎，许多研究者已经开始了这一方向的研究。



最熟悉的可能还是 morphology 的研究，这个主要在上次的 word embedding 变形中提了一些（回复代码：GH006），又比如 NAACL 2015 Best Paper 之一，《Retrofitting Word Vectors to Semantic Lexicons》。Motivation 是将 lexicon relations （比如 synset 等等同义词啊这些的 relation 作为 additional information）去“supervised” word vectors。注意，supervised 这个词，通篇都没有出现，是我自己加的。而且这个 idea 不是他们首创的，他们自己在论文里也说了，是 follow 14年的很多 short 工作（比如 Mo Yu 等人的工作），他们只是把它们变得通用了一点。这个工作有 Two Approaches: 一种是如题目一样，retrofit，就是任何已经 pre-trained 的 word vectors，别管你咋 train 出来的，我都可以再给你增强一下。另一种是从头开始，用另一种 learning method，边增强 lexicon relation constraints 边学 word vectors。使用的 Method: 可以直接看 Figure 1，就是用 relation dictionary（knowledge base）中的 counterpart words，作为一种镜像的映射。用 dictionary/knowledge base 中的词和词之间的 connection 关系，让需要 inferred 的 word vectors 中的对应的词更 closed——从而认为提升了语义表达。关于 Two Algorithms: 对应于 retrofit，因为是 convex 的，所以直接求解就好；对应于边 learn 边 retrofit，则比较麻烦，他们叫 lazy method of MAP + periodic method + NCE + AdaGrad。



比如这次 ACL 2015 上的：《SensEmbed: Learning Sense Embeddings for Word and Relational Similarity》来自 Ignacio Iacobacci, Mohammad Taher Pilehvar and Roberto Navigli。这篇主要解决两个问题，

However, word embeddings inherit two important limitations from their antecedent corpus- based distributional models: (1) they are unable to model distinct meanings of a word as they conflate the contextual evidence of different meanings of a word into a single vector; and (2) they base their representations solely on the distributional statis- tics obtained from corpora, ignoring the wealth of information provided by existing semantic resources.

所以针对第一个，他们基于 BabelNet 这个 lexical resources，建立了初步的 multi senses，然后又基于别人的算法把 corpora 给自动标记成多 senses 的。后面又改造了不同种的 similarity metrics，为了增强 similarity performances。都是“修修补补”的工作。比较有意思的就是我发现越来越多的人都在用 BabelNet 了。



再比如依然是 ACL 2015 上的：《Revisiting Word Embedding for Contrasting Meaning》来自 Zhigang Chen, Wei Lin, Qian Chen, Xiaoping Chen, Si Wei, Hui Jiang and Xiaodan Zhu。这篇论文 小S 个人非常喜欢，因为感到文章中的闪光点很多，能看到作者认认真真思考过这个工作，而不是随便想到什么赶紧做点差不多的实验就发出来。文章主要是针对基于 distributional hypothesis 假设的 word embedding models 无法解决的 contrasting meaning word pairs 提出自己的一个 embedding 框架。这个框架乍看有点复杂，但其是完全使用 lexical resources，而没有 distributional hypothesis/corpora statistics 的：

Unlike what was suggested in previous work, where relatedness statistics learned from corpora is often claimed to yield extra gains over lexicon-based models, we obtained this new state-of-the-art result relying solely on lexical re- sources (Roget’s and WordNet), and corpus statis- tics does not seem to bring further improvement. To provide a comprehensive understanding, we constructed our study in a framework that exam- ines a number of basic concerns in modeling con- trasting meaning. We hope our efforts would help shed some light on future directions for this basic semantic modeling problem

主要建模思想依然和 word2vec 无异，就是用更符合 main goal 的 pair 应该更”近“，其他更不近就好——

The general aim of the models is to enforce that in the embedding space, the word pairs with higher degrees of contrast will be put farther from each other than those of less contrast.

但是这也不是他们的唯一思想，他们参考了许多相关建模工作，对于被 word embedding 刷屏的各位是一股清流，看看以前的人都是怎么做 relation embedding 的。也就是文章 Section 3.2-3.5 的不不分。比如他们就考虑到，虽然一对 constrasting word，比如 good 和 bad，意思是完全相反的，但是他俩很可能出现在相同的语境中。也就是说，他俩都可能和另一个词语比如说 C semantically closed。所以这时候我们就要考虑 constrasting + semantic 两种相关距离。与此同时，nonlinearity 也非常重要。最后作者也验证了一下到底 distributional hypothesis 下的 model 能做到什么程度，又为什么不能超过 lexical based。结论和 DAN（Deep Averaging Networks） 那篇还蛮像的。



还有 ACL 2015 的《Hubness and Pollution: Delving into Cross-Space Mapping for Zero-Shot Learning》来自 Angeliki Lazaridou, Georgiana Dinu and Marco Baroni。这篇论文很有意思，讨论的有点像上面提到的 constrasting meaning 那篇相反的问题——在 space 中，离的很近的点，往往很难区分，也就很难准确得出它们的表达（它们之间的区别）——这种点一般叫 hubness，是一个从至少 10年（ref 中有两篇）就被人提出过的问题。大概就是一些非常 general 的 items。这种 hubness 的 cause 和初步解决方法都在 Section 3 中提到，大概是我们常用的 LS 的 objective function 是会加剧这种效应的（十分好理解，毕竟公式就放在那里，ignore low variance），solution 也已经被“不经意地”发现了，那就是 Socher 等人用 max-margin loss “误打误撞”解决了这种效应。本篇论文中用实验证明了是 max-margin helps。



lexical resources



说完第一个方向，第二个方向则更直观一点。lexical relation 的很多过往研究都是基于 high quality 的 human annonatation 的，那么我们有没有办法把基于 statistical/distributional 的 word embedding model 的方法和已有的人工标注的 lexical resources 结合在一起呢？用 lexical resources 的高质量信息/知识，来完善、提高 word embedding 质量呢？



这方面其实在 NAACL 2015 上已有相关的工作，比如 NAACL 2015 Best Student Paper Awards 得主之一，《Unsupervised Morphology Induction Using Word Embeddings》。Google 出品的，个人感觉是他们在工作中真的有这个需求。整个文章做法虽然宏观上很直观，很简洁，但是细节处，各种 threshold 也比较多，总的来说是一篇偏 linguistic 的论文。Model: 基于 SkipGram 改造的。Motivation: a) 基于 Mikolov 等人的 semantic relation （king-man+woman=queen），作者认为 word embeddings space 里也可以 induce 出 morphological relation；b) 传统的 morphological induction 或者 generation 的方法，基本基于 linguistic rule，而 linguistic rule 的不符合的案例太多，不太 robust，且费时费力；他们这个方法可以说依然是基于统计的（frequency）。Algorithm: a) frequency-ranked equation，挑选出 candidates。这一步用了两种 metric，rank+cosine。个人理解这是基于 word analogy 的一种改造，比如 king-man+woman=queen这种 word analogy，那么 king-man的这个距离，就可以认为是一种已知的衡量标杆，把它们分别认为是 w 和 w'。我们就可以通过 w 和 w' 的距离来衡量 w1（queen）和 w2（woman）的距离。由此他们自己定义了一个公式（Equation 1）；b) 第二步，有了 rank 和 cosine 两个 metric，才能保证这些候选的 morphological rule candidates 是既常见的（lexicalized）和符合当前带评测 w1, w2 的真实关系的（meaning preservation）；c) 这个多种的 candidates，在他们论文里叫 multiple directions，有点像 Huang'12 年的一词多义问题。Task: a) 很自然的，有了 candidates，就去 induce 1-1 的map；b) 之后就更可以运用到 unseen/rare words 和 OOV 上。Evaluation: 用 word similarity 的 datasets 做评测，涉及到了6种语言，9个 datasets。这里也可以一定程度证明这个方法的简单有效，因为多种语言的话，去 handmade morphological rule 就很繁琐耗时。整体来看，文章思路直观，而且我感觉应用很广。毕竟 relation 这个东西，不仅存在于 semantic 和 morphological 上，还存在于各种问题上。这也是为什么现在 relation embedding 也是一个比较热的方向的原因。PS. 文章中说他们是使用自己实现的（slightly different）版本的 SkipGram，不是原始 word2vec 里面的。



再比如这次的 ACL 2015 Best Student Paper Awards 得主，《AutoExtend: Extending Word Embeddings to Embeddings for Synsets and Lexemes》。论文想探究的是三种 data type，word, synset, lexeme，这三种 data type 都常见于 Lexical Resources，比如 WordNet，Freebase, Wiktionary 等等。作者想通过他们在 这种 resources 中的关系，来作为 constraints，去把 word embedding，synset embedding, lexeme embedding 一起学在同一个空间里。同时，论文基于我们任何已有的 word embedding，和任何已有的 resources，不需要额外的 training corpus，就可以得到 synset, lexeme embedding。先来说三种 data type：word，不用说了。synset，一组同义词，由多个与不同 word 有关的 lexeme 组成；lexeme，不知道中文叫啥，反正既有一词多义的意思，也有一词多种形态的意思（syntactic）。具体举例可以见 Section 2 的第二段。基于三种 data type，作者给出了两个 motivation 和 两个 observation 和两个 assumption（都是一个东西），然后这个东西就可以用来做 constraints 了，就是公式（1）（2），也是 Figure 1 架构的主要顺序。word->lexeme->synset->lexeme->word。除了这俩 motivation 和 这俩 constraints，作者还有第三个 motivation 和 第三个 constraints，而 constraints 第三个则是基于 resources 的性质，在 Section 2.4，用于解决的是当 word 没有 synset 时的问题。所以重新整理一下就是：

Motivation: 1) 公式（1），一个 word 由多个 lexeme 组成；2) 公式（2），一个 synset 也由多个 lexeme 组成；3) 一个 word embedding 也可以认为是它不同 sense 的 embedding 的加和。

Constraints: 1) 公式（1），一个 word 由多个 lexeme 组成；2) 公式（2），一个 synset 也由多个 lexeme 组成；3) 公式（25），相关联的 synset 应该有相近的 embedding，这个 constraints 用于解决 word 没有 synset 或者只有一个 synset word 时的问题。

Model: 基于这几种 constraints，就可以设计一个 encoding - decoding autoencoder 的 NN，从 input 到 output，把 synsets 当 words 的 encoding。然后公式（10）到公式（17）就是整个 autoencoder 的 NN 的每一步骤的公式。可以看出，encoding - decoding 的两种表达之间的差值就是我们的 objective 函数了，即公式 （17）。

Implementation: 这个论文的另一个卖点除了这种很优美的 relation constraints 外，是他充分利用了 sparseness 去加速求解。他们把 word synset 之间，用 autoencoder 的 encoding 和 decoding part 中的 lexeme 为中间体，分别组成了一个 rank 4 的 tensor，即 E 和 D。E 和 D 也是 autoencoder 中要 learned 的 parameter。但是他们假设了 E 和 D 中的每一个维度之间是 no interaction 的，且又由于很多 lexeme 并不存在，所以更增加了 E 和 D 的 sparseness——最后的结果就是 E 和 D 的实际有效的维度大大降低——计算大大提速。但是我现在没想清楚这个 assumption 是否合理。另外还有一个实现细节是 Section 2.6。

Problem: 1) 就是上面说到的 no interaction 假设；2) 另一个不太优雅的地方是他们把 三种 constraints 用线性加权组合起来，即 Section 2.5 的地方，这个东西在他们这个框架下是比其他人的线性加权要合理的，因为他们假设 word, synset, lexeme 三者都是在同一个 embedding space。而且他们在实验中也讨论了这三个的权重，还算 OK 了。



还比如上面第一个方向中提到的 ACL 2015 的《Revisiting Word Embedding for Contrasting Meaning》来自 Zhigang Chen, Wei Lin, Qian Chen, Xiaoping Chen, Si Wei, Hui Jiang and Xiaodan Zhu，内容简介见上方。



beyond words



这个方向相信大家已经不陌生了，从 Mikolov 2013 年放出 word2vec toolkit 源码并同时发表两篇 word2vec 连环弹鼻祖 paper 后，研究者们就开始群策群力地纷纷发表了 paragraph2vector, sentence2vector, document2vector。众所周知，这些工作和原始的 word2vec 差异不大，几乎是完全 follow 的 idea，变换一下 apply 的 unit。这样“粗略”的改进并不能达到真正的好效果。所以可以说，beyond words 这个方向依然有待研究。



最近一篇名字很 fancy 也很“囧”（被 Gordberg 说是个烂名字）的 paper 就是相关的工作，叫 thought vector，“思想向量”——来自 arXiv pre-print 论文《Skip-Thought Vectors》，Ryan Kiros, Yukun Zhu, Ruslan Salakhutdinov 等人的工作。Motivation: 很简单，想像 skip-gram 用中心词预测周围词一样，用中心句子预测周围句子。Model: 直接看 Figure 1，具体使用是 RNN-RNN 的 encoder-decoder 模型；其中两个 RNN 都用了 GRU 去“模拟” LSTM 的更优表现。在 encoder 阶段，只是一个 RNN；在 decoder 阶段，则是两个（分别对应前一个句子和后一个句子——也就是说不能预测多个前面的句子和后面的句子）。这样的模型可以保留一个 encoding for each sentence，这个 encoding 会很有用，就被称为 skip-thoughts vector，用来作为特征提取器，进行后续 task。注意是 Figure 1 中所谓的 unattached arrows，对应在 decoder 阶段，是有一个 words conditioned on previous word + previous hidden state 的 probability 束缚。同时，因为 decoder 也是 RNN，所以可用于 generation（在论文结尾处也给出了一些例子）。Mapping: 本文的另一个贡献是 vocabulary mapping。因为 RNN 的复杂性，但作者又不希望不能同时 learn word embedding，所以只好取舍一下——我们 learn 一部分 word embedding（words in training vocabulary）；对于没出现的部分，我们做一个 mapping from word embedding pre-trained from word2vec。这里的思想就是 Mikolov'13 年那篇 word similarity for MT 的，用一个没有正则的 L2 学好 mapping。在实验中，他们用此方法将 20K 的 vocabulary 扩充到了 930K。Experiments: 实验做的很多，我觉得做得还挺 solid 的，没什么 unfair 的（但我对实验一向不太了解，请大家了解的多看看）。

In our experiments we consider 8 tasks: semantic-relatedness, paraphrase detection, image-sentence ranking and 5 standard classification benchmarks. In these experiments, we extract skip-thought vectors and train linear models to evaluate the representations directly, without any additional fine-tuning. As it turns out, skip-thoughts yield generic representations that perform robustly across all tasks considered.

首先是他们有三种 feature vectors，uni-skip/bi-skip/combine-skip。分别对应 encoder 是 unbidirectional，bidirectional，和 combine 的。分别都是 4800 dimensions。对于不同的 task，可能用不同的 feature indicator，比如把两个 skip-thoughts-vectors u 和 v，点乘或者相减，作为两个 feature，再用 linear classifier(logistic)。





beyond English



最后我们来说第四个方向，这个方向也是 ACL 2015 workshop 上，Yoav Goldberg 在其 talk 《word embeddings: what, how and whither》 上重点提及的，那就是现有的 word embedding 工作，放出来的已经 train 好的 vectors，绝绝绝绝绝大多数都是 English 的。可是即便是按照大的语系划分，世界上的语言也有太多不共通的性质。所以如果仅仅去研究 English 上的 word embedding 的改进，比如 compositional, morphological, 是远远不够的。



其实，beyond English 有两种分支，一种是完全抛弃 English，用另一种语言的语料，做一个新问题或者老问题。第二种分支就是 cross-lingual，都知道 English 是 rich-resource 的语言，也就是所谓的富语料，有充足的资源，cross-lingual 的一大优点就是可以用 rich-resource 的性质去弥补 low-resource 这边的不足。这也是为什么，cross-lingual 从来都会占据各大会议的一席之地的原因。



关于 beyond English 这个方向的研究除了 Yoav Goldberg 给的 talk 里提到的一些 Hebrew 的性质外，还有比如这次 ACL 2015 上的《A Generalisation of Lexical Functions for Composition in Distributional Semantics》，来自 Antoine Bride, Tim Van de Cruys and Nicholas Asher 等人的工作。一作是 relation embedding 的“鼻祖”，贡献了一堆 relation embedding 的 paper。这篇论文的一大贡献是他们给出了两组 datasets，一个是 adj-noun 的，一个是 noun-noun 的。分别是英文和法语的。
