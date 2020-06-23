---
layout: post
title: 讲座笔记 -- VALSE Webinar Network Compression(1)
categories: [LectureNotes, NetworkPruning]
description: 
keywords: 
---

## 2020-06-23-讲座笔记-VALSE Network Compression(1)

VALSE Webinar 2020-14 期

> VALSE： http://valser.org/article-368-1.html 
>
> 录播地址：https://www.bilibili.com/video/av710990098/ 

#  AI on the Edge —— 王云鹤（华为诺亚）讲座摘录

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

# Ultra-low-bit Neural Network Quantization —— 王培松（中科院自动化所）讲座摘录

**主要是讲定点量化的工作。**定点数硬件友好，因此可提速并节省芯片面积。

![](/images/VALSE/modelCompression8.png)

![](/images/VALSE/modelCompression9.png)

**Sparsity-inducing Binarized Neural Networks. AAAI, 2020**

将激活量化为01，权重依然为±1。可以通过位运算进行加速。

![](/images/VALSE/modelCompression10.png)

±1量化可以以0作为阈值点，但是01量化就不可，于是引入了互信息去找到阈值点theta。下图为实验结果，实际硬件加速非常明显：

![](/images/VALSE/modelCompression11.png)

**Soft Threshold Ternary Networks. IJCAI, 2020**

两个binary加起来可以得到一个ternary，所以变成了量化两个binary kernel。

![](/images/VALSE/modelCompression12.png)

**Hardware Acceleration of CNN with One-Hot Quantization of Weights and Activations. DATE 2020**

**Towards Accurate Post-training Network Quantization via Bit-Split and Stitching. ICML, 2020**

# Panel

> https://mp.weixin.qq.com/s/EZFjwqM5YEss61dw8MtdSw

