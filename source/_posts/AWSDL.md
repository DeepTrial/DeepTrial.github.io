---
title: AWS深度学习环境配置
date: 2020-01-20 19:41:28
categories: python
cover_img: https://res.cloudinary.com/dmqrfncz7/image/upload/v1579533650/timg_3_bmydxg.jpg
tags:
- python
- 深度学习
description: 介绍在AWS上搭建深度学习环境的方法
keywords: aws, 深度学习, 环境配置
---

# AWS介绍
AWS即Amazon Web Service，亚马逊云服务。在中国区已经有宁夏和北京两个站点，作为全球最大的云服务提供商，里面的数据我就不吹了。AWS因为提供竞价服务器，所以我们用户可以以比较低的价格租赁GPU服务器，价格大概0.3～0.7 USD 一小时，无论是GCP，阿里云，腾讯云什么的都比这个要贵。由于价格优势，所以很多研究者都是在此租用服务器进行研究的。

# 前期准备
首先需要有AWS外区账号，国区因为各种问题不提供给个人使用，只面向组织机构使用。其次需要想AWS申请，放开GPU实例的限制（普通账号不可以竞价购买GPU势力，需要申请开通）[参考链接](https://www.cnblogs.com/eniac1946/p/7804212.html)

# 安装具体环境
由于服务器租赁好之后还需要具体安装深度学习的环境，每次手动安装都十分麻烦，所以在我的github仓库内有我自己写的自动安装脚本，每次服务器租好之后，运行脚本，就可配置完成项目。

