---
layout: post
title: 讲座笔记 -- VALSE Webinar Action Recognition (2)
categories: [LectureNotes, ActionRecognition]
description: 
keywords: 
---

# 乔宇：复杂视频序列的深度表征与理解方法 (2)

![](/images/VALSE/actionRecognization3.png)

![](/images/VALSE/actionRecognization4.png)

![](/images/VALSE/actionRecognization5.png)

## 推荐的文章：轨迹池化卷积特征TDD (CVPR15, Limin Wang)

第一个在UCF和HMDB上全面超越传统浅层模型的深度学习方法。

![](/images/VALSE/actionRecognization6.png)

本论文提出一种新的视频表示方法，称作轨迹池化-深度卷积描述符（TDD），**共享手工制作的特征和深度学习特征**。

- TDDs是自动学习，并且与这些手工制作的特征相比具有高区分度的性能
- TDDs考虑时间维度的本质特征，介绍轨迹受限的采样和池化的策略加强深度学习特征。 

### （一）设计原理：

![](/images/VALSE/actionRecognization7.png)

### （二）轨迹跟踪（对应原文 Sec.3）

原始的轨迹跟踪算法：

<img src="https://oscdn.geek-share.com/Uploads/Images/Content/201911/04/520bdaeeda17c5abbd52dd88e8ce3775" style="zoom:80%;" />

改进方案：Improved trajectories 将机变信息考虑进去从而能够提高识别性能；通过 homography 矩阵，移除相机的机变重新计算光流，称作 warped flow，再用其计算P。

### （三）卷积网络（对应原文 Sec.4）

采用**双向的 ConvNets** **包括一个空间网络和一个时间网络**。空间网络用语捕获静态的外在线索，例如一些单个窗口里的图像；时间网络旨在描述动态的运动信息，比如输入是一些堆积的光流。

#### 1. 时空正则化（对应原文 Sec.4.3）

![](/images/VALSE/actionRecognization8.png)

#### 2. 通道正则化（对应原文 Sec.4.3）

![](/images/VALSE/actionRecognization9.png)

#### 3. TDD（对应原文 Sec.4.3）

![](/images/VALSE/actionRecognization10.png)

### （四）特征编码

选择 Fisher vector 来编码 TDDs。

然后用一个线性的 SVM 做分类器。

为了训练 GMMs，我们首先用 PCA 来对 TDD 去耦合/降维。 

![](/images/VALSE/actionRecognization11.png)

## 推荐的文章：深度时序分割模型TSN (ECCV16, Limin Wang)

![](/images/VALSE/actionRecognization12.png)

> 论文笔记: [CSDN](https://blog.csdn.net/zhang_can/article/details/79618781)

本文旨在设计有效的卷积网络体系结构用于视频中的动作识别，并在有限的训练样本下进行训练。TSN 基于 two-stream 方法构建。论文主要贡献：提出了 TSN（Temporal Segment Networks），基于长范围时间结构（long-range temporal structure）建模，结合了稀疏时间采样策略（sparse temporal sampling strategy）和视频级监督（video-level supervision）来保证使用整段视频时学习得有效且高效。

two-stream 卷积网络对于长范围时间结构的建模无能为力，主要因为它仅仅操作一帧（空间网络）或者操作短片段中的单堆帧（时间网络），因此对时间上下文的访问是有限的。视频级框架 TSN 可以从整段视频中建模动作。

和 two-stream 一样，TSN 也是由空间流卷积网络和时间流卷积网络构成。**但不同于 two-stream 采用单帧或者单堆帧，TSN 使用从整个视频中稀疏地采样一系列短片段，每个片段都将给出其本身对于行为类别的初步预测，从这些片段的“共识”来得到视频级的预测结果。**

![](/images/VALSE/actionRecognization13.png)

针对时间（光流）和空间（RGB）分别提出了以下两种网络输入：

![](/images/VALSE/actionRecognization14.png)
