---
title: 深度学习调参方法
date: 2020-01-20 19:41:28
categories: 智能算法
tags: 深度学习
description: 深度学习神经网络的调参方法
keywords: 神经网络, 参数调整
---

# 深度学习神经网络调参方法
由于深度学习模型每次运行都需要消耗大量时间，所以无目的、无规则地调整模型参数是非常费时费力的。以下是我对神经网络调参方法的整理。

## 可调参数

- learning rate

学习率将影响网络的收敛。太大的学习率容易导致网络不收敛，太小的学习率会使网络收敛速度太慢。
![](https://i.imgur.com/JyILpQY.png)

- batch_size

本质上batch_size的作用是平衡网络的性能以及计算中内存消耗的变量。通过下图可以看出batch_size的大小对于网络收敛情况的影响。红线代表batch_size为1时模型的收敛情况。蓝线代表batch_size为整个数据集大小时的收敛情况。绿线是batch_size大小在1到整个数据集之间的情况。batch_size通常取[16,128]之间。
![](https://i.imgur.com/CZIAwh9.png)
从上图可知，模型对batch_size的大小非常敏感，在调整时需要十分小心。

- epochs

模型在整个数据集上迭代的过程。

- weight initialization

模型中参数的初始化方式。不同的初始化方式有时会对模型结构产生较大的影响。

- regularization

卷积层等的参数正则项，用来控制模型的复杂程度。

- loss function

一般来说分类就是Softmax, 回归就是L2的loss. 但是要注意loss的错误范围(主要是回归), 预测一个label是10000的值, 模型输出0, 你算算这loss多大, 这还是单变量的情况下. 一般结果都是nan. 所以不仅仅输入要做normalization, 输出也要这么弄.+ 多任务情况下, 各loss想法限制在一个量级上, 或者最终限制在一个量级上, 初期可以着重一个任务的loss



- dropout

dropout参数常设置为0.3,0.5,1


## 调参方法

### 可视化激活层结果
激活层的输出结果应当具有稀疏性和局部性。如果卷积层后的激活层输出的可视化结果和输入图片差不多时，则代表这个卷积并没有学到多少有价值的信息。

### 可视化loss，acc曲线

当网络部分收敛时，可以分为两种情况：欠拟合和过拟合。

train set|val test|problem
:-:|:-:|:-:
error small|error too large|overfitting
error large|irrelevant|underfitting
error small|error small|idea

如果模型出现欠拟合现象，后续参数调整的方向主要是增强模型的拟合能力。例如**增加网络层数，增加节点数，减少dropout值，减少L2正则化，加大batch_size**等。

而针对过拟合现象，则只需要反向操作，如**加大dropout值，使用L2正则化，batch normlization**.

当网络完全不收敛时，可以分为模型错误、数据错误两种。

通常需要对输入值进行正则化，让特征都保持在0均值和1方差。


