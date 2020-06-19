---
layout: post
title: 讲座笔记 -- VALSE Webinar Action Recognization (3)
categories: [LectureNotes, ActionRecognization]
description: 
keywords: 
---

# 乔宇：复杂视频序列的深度表征与理解方法 (3)

## Inflated 3D (I3D) ConvNets

> Joao Carreira et al., Quo Vadis, Action Recognition? A New Model and the Kinetics Dataset, CVPR2017
>
> Reference: [简书](https://www.jianshu.com/p/f02baee5e7fb )

<img src="https://pic4.zhimg.com/80/v2-dc5297034846dda63c66e4cba7e37543_720w.jpg"  />

**背景：3D卷积**

<img src="https://upload-images.jianshu.io/upload_images/12412176-0017e5363ef3a4d9.png?imageMogr2/auto-orient/strip|imageView2/2/w/554/format/webp" style="zoom:120%;" />

<img src="https://pic3.zhimg.com/v2-86e2bd970d07f9d6e1d921b248e45a3a_b.webp" style="zoom:40%;" />

**有趣的地方：2D卷积拓展为3D**：本文选用的网络结构为 BN-Inception (上一篇深度时序分割模型 TSN 也是)，但做了一些改动。如果 2D 滤波器为 NxN 的，那么 3D 的则为 NxNxN 的。具体做法是沿着时间维度重复 2D 滤波器权重 N 次，并且通过除以 N 将它们重新缩放。这样来确保滤波器的响应相同。**每一个卷积层的输出在时域上是固定的，对于非线性层和池化层和2D的相同。**

> 2D 卷积其实包含了 x 和 y 两个方向，一般来说这两个方向的步长可以一致，但对于 3D 来说，时间维度不能缩减地过快或过慢。因此改进了 BN-Inception 的网络结构。在前两个池化层上将时间维度的步长设为了1，空间还是2x2。最后的池化层是 2x7x7。训练的时候将每一条视频采样 64 帧作为一个样本，测试时将全部的视频帧放进去最后 average_score。除最后一个卷积层之外，在每一个都加上 BN 层和 Relu。
>
> 文章中的 3D 网络并不是随机初始化的，而是将**在 ImageNet 训好的 2D 模型参数展开成 3D**，之后再训练。因此叫 Inflating 3D ConvNets。

**实验结果如下：**

![](https://pic4.zhimg.com/80/v2-7b36ff93c321b3d9f35e59512467e973_720w.jpg)

## Spatiotemporal Separable 3D (S3D) Convolutions

> Saining Xie et al., Rethinking Spatiotemporal Feature Learning For Video Understanding, arxiv, 2017

3D卷积网络与2D卷积网络相比，始终存在着网络参数量太大而且计算效率不高的问题，但是3D卷积网络的准确率又明显好于2D卷积网络，所以为了解决这个问题，我们需要思考以下几个点：

- 3D卷积网络中是否需要全部都是3D卷积核？是否可以设计一个网络同时包含 2D卷积核和3D卷积核，来达到准确率与计算效率的 trade-off 呢？
- 是否可以通过分解3D卷积核为 2D+1D 卷积核的形式来解决这个问题呢？

设计了两种 2D+3D 的 I3D 网络。

![](https://img-blog.csdnimg.cn/20181224200235280.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6bXNodWFp,size_16,color_FFFFFF,t_70)

![](/images/VALSE/actionRecognization15.png)

## R(2+1)D, TODO

> Tran, Du, et al. "A closer look at spatiotemporal convolutions for action recognition." Proceedings of the IEEE conference on Computer Vision and Pattern Recognition. 2018.