---
title: GDXray数据集介绍
date: 2020-01-20 19:41:28
cover_img: https://res.cloudinary.com/dmqrfncz7/image/upload/v1579533847/timg_4_ogjnu4.jpg
categories: 智能算法
tags: 
- 深度学习
- 数据集
description: 介绍GDXray数据集情况
keywords: 深度学习，数据集
---


# GDXray数据集介绍

## 数据集概况
GDXray是一个X-ray综合数据集，共包含19407张图像，整个数据集约3.5GB。数据集包含5种子类别：casting,welds,baggage,natural objects,settings.具体情况如下：

![](https://i.imgur.com/s249NuW.png)


## 数据命名规则
数据集中5种子类的缩写为C,W,B,N,S,每一种子类的命名规则为Xssss，其中X为子类缩写，ssss是子类计数，如baggage中第一种类别为B0001。对于类别中每一张图片采用Xssss_nnnn.png格式，如baggage中第一类的第一张图片名称为B0001_0001.png。


