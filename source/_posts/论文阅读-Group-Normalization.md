---
title: 论文阅读-Group Normalization
date: 2018-12-29 11:38:29
tags:
categories:
    - 论文
---

# 问题的提出

Batch Normalization虽然是一种较好的防止过拟合的方法<!-- more -->，但也有其缺陷：那就是随着批次的减小，BN的错误率会增加，但在一些cv任务中，又要求较小的批次，因此需要解决这个问题，伦文提出了一种Group Normalization的方法。

# 相关工作

1. Batch Normalization问题的产生：归根结底是不同阶段数据分布的不一致造成的，通常来说，训练阶段跟测试阶段的batch size是不同的，而现在大多数网络在测试阶段都是直接调用了训练阶段产生的均值与方差，这显然就是不合理的，因为数据分布出现了变化。
2. LN与IN避开了batch维度方面，有一定的效果，但仍然比不上本文的GN。
3. BR一定程度上减弱了批次小错误率高的问题，但仍没有从根本上解决。


# Group Normalization的设计

1. 论文表明，神经网络中的特征图进行语义表示其实也是成组的，那么，就可以对这些成组的特征图一起规范化。
2. 一般来说，规范化用公式表达如下：
$${\hat x_i} = \frac{1}{\sigma_i}({x_i} - {\mu_i})$$
主要是计算均值与方差，规范化之后，为了补偿表示能力可能有的损失，进行了一个线性变换：
$${y_i} = \gamma {({\hat x}_i)} + \beta $$
不同的方法进行规范化的方式如图所示：
![规范化方式](/img/GN.png)

# 总结
通过实验的对比，GN有着不错的效果，但由于目前BN是训练网络的一种十分有效的方法，许多超参数与结构对BN来说可能是最好的，但对于GN来说却可能不是最合适的，需要重新设计结构。
