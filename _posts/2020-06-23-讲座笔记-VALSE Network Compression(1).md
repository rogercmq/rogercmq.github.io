---
layout: post
title: 讲座笔记 -- VALSE Webinar Network Compression(1)
categories: [LectureNotes, NetworkPruning]
description: 
keywords: 
---

## 2020-06-23-讲座笔记-VALSE Network Compression(1)

# VALSE Webinar 2020-14 期

> VALSE： http://valser.org/article-368-1.html 
>
> 录播地址：https://www.bilibili.com/video/av710990098/ 

##  AI on the Edge —— 王云鹤（华为诺亚）讲座摘录

压缩比≠加速比：Compressed networks can achieve the same performance compared to original baselines after fine-tuning. **Cannot directly obtain a considerable speed-up on mainstream hardwares.** 

![](/images/VALSE/modelCompression0.png)

DCT-based 方法的问题：工业上用不了。

![](/images/VALSE/modelCompression1.png)

同时输入到 teacher net 和 student net，把中间特征输入到判别器网络里。

![](/images/VALSE/modelCompression2.png)

![](/images/VALSE/modelCompression3.png)

TEC: 利用遗传算法对神经网络进行裁剪，对神经元（filter）01编码，提出了 fitness 的概念

![](/images/VALSE/modelCompression4.png)

CCG: 对GAN网络进行模型压缩（生成神经网络计算量更大，因为输入与输出size相同），具体做法：生成了两个种群。

![](/images/VALSE/modelCompression5.png)

 DAFL: data-free pruning technique。

![](/images/VALSE/modelCompression6.png)

AdderNet: ResNet50 可达到 top-1 76% 的准确率。

![](/images/VALSE/modelCompression7.png)

端侧 AI 必要性：地下车库，偏远地区。

## Ultra-low-bit Neural Network Quantization —— 王培松（中科院自动化所）讲座摘录

