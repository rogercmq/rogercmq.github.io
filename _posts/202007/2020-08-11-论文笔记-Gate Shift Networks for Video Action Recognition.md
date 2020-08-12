---
layout: post
title: 论文笔记 -- Gate-Shift Networks for Video Action Recognition (精品)
categories: [PaperNotes, ActionRecognition]
description: 
keywords: 
---

Gate-Shift Networks for Video Action Recognition (CVPR2020), 本篇笔记在 Related Works 部分做了疯狂总结.

作者提出了一个轻量级模块 Gate-Shift Module (GSM)，将 2D 卷积替换为高效的 spatio-temporal feature extractor.

<img src="/images/posts/GSM/0.png" style="zoom:50%;" />

# 1. Introduction

视频领域依然无法像图像领域一样有突破性进展，主要原因依然在于如何获取数据的时空信息。文中提到了一个词语叫做时序推理 (temporal reasoning)，之后可以调研一下 NLP 领域是否有类似的动机。

> A key challenge lies in the space-time nature of the video medium that requires temporal reasoning for fine-grained recognition.

UCF101 和 Kinetics 数据集并不太需要 temporal reasoning，因为大多数类别通过静态场景和物体就可以识别，甚至打乱帧顺序得到的识别结果也差不多。 

<img src="/images/posts/GSM/1.png" style="zoom:43%;" />

Figure 1 描述了几种3D卷积神经网络解耦方案。方案 1-5 的架构设计都是在模型训练以前硬性规定的，原文称 “ **There is no data dependent decision taken at any point in the network to route features selectively through different branches**.” 

> A most intuitive approach is to factorize 3D spatio-temporal kernels into 2D spatial plus 1D temporal, resulting in a structural decomposition that disentangles spatial from temporal interactions (P3D[31], R(2+1)D[40], S3D [46]). 
>
> > *[46] Rethinking spatio-temporal feature learning: Speed-accuracy trade-offs in video classification. (ECCV2018)* 本工作在 [我的讲座笔记]([https://rogercmq.github.io//2020/06/19/%E8%AE%B2%E5%BA%A7%E7%AC%94%E8%AE%B0-VALSE-Action-Recognition(3)/](https://rogercmq.github.io//2020/06/19/讲座笔记-VALSE-Action-Recognition(3)/) 中有所记录。本工作的两大内容是: 1) 2d+1d 代替所有 3d 卷积; 2)  参考 SENet 的思想提出了 3d 的 feature gating mechanism。 
> >
> > <img src="/images/VALSE/actionRecognization15.png" style="zoom:40%;" />
>
> An alternative design is separating channel interactions and spatio-temporal interactions via group convolution (CSN [39]), or modeling both spatial and spatio-temporal interactions in parallel with 2D and 3D convolution on separated channel groups (GST [27]). 
>
> > *[39] Video Classification With Channel-Separated Convolutional Networks. (ICCV2019)* 本工作在 [我的讲座笔记]([https://rogercmq.github.io//2020/06/19/%E8%AE%B2%E5%BA%A7%E7%AC%94%E8%AE%B0-VALSE-Action-Recognition(3)/](https://rogercmq.github.io//2020/06/19/讲座笔记-VALSE-Action-Recognition(3)/) 中有所记录。本工作的两大内容: 1)  分解3D卷积通过分开通道间相互作用和时空域信息的交互将对于提高准确率和节省计算量有很好的帮助; 2) 将3D卷积进行 depthwise 这种方法从某种程度上说可以等效成一种正则化，虽然在训练集上的准确率不高，但在测试集上表现出高准确率。
> >
> > <img src="/images/VALSE/actionRecognization16.png" style="zoom: 40%;" />
> >
> > *[27] Grouped Spatial-Temporal Aggregation for Efficient Action Recognition. (ICCV2019)* 本工作硬核地将特征拆分为用3D卷积建模的 Temporal feature 和用2D卷积建模的 Spatial feature，然后 concatenate 所有特征。似乎与上一篇CSN深度可分离卷积解耦方案思路一致。
> >
> > <img src="https://img-blog.csdnimg.cn/20200112004847986.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FtYXppbmdyZW4=,size_16,color_FFFFFF,t_70" style="zoom:40%;" />
>
> Temporal convolution can be constrained to hard-coded time-shifts that move some of the channels forward in time or backward (TSM [25]). 
>
> > *[25] Temporal Shift Module for Efficient Video Understanding.  (ICCV2019)* 本工作在 [我的讲座笔记]([https://rogercmq.github.io//2020/06/19/%E8%AE%B2%E5%BA%A7%E7%AC%94%E8%AE%B0-VALSE-Action-Recognition(3)/](https://rogercmq.github.io//2020/06/19/讲座笔记-VALSE-Action-Recognition(3)/) 中有所记录。
> >
> > <img src="https://picb.zhimg.com/80/v2-27eff0b884ddb445fd1fee1e472a98ac_720w.jpg" style="zoom: 67%;" />
> >
> > 本段内容来自 [知乎笔记](https://zhuanlan.zhihu.com/p/64525610) : 在图2a中，我们描述了一个包含C通道和T帧的张量。不同时间戳的特征在每行中表示为不同的颜色。传统的二维CNN在不同的信道间进行操作，即在不进行时间融合的情况下，沿每一行单独进行操作。在时间维度上，我们将1 / 4通道移动了- 1个单位，将另一个单位移动了+1个单位，剩下的一半没有移动(图2b)。“四分之一”是我们将在消融研究中讨论的超参数(3.3节)。哪一1/4shift并不重要，因为下一层的权重会在训练中适应。因此，我们将帧t - 1、t和t + 1的时间信息混合在一起，类似于核大小为3的一维卷积，但计算成本为零。乘法累加被推到下一层。利用二维卷积的信道间融合能力，实现了原始的时域间融合。 

本工作提出的 Gate-Shift Module (GSM)：

<img src="/images/posts/GSM/2.png" style="zoom:43%;" />

# 2. Related Work

## Fusing appearance and flow

介绍了双流网络（单帧图片 + 光流图）

> A popular extension of 2D CNNs to handle video is the Two-Stream architecture by Simonyan and Zisserman [33]. Their method consists of two separated CNNs (streams) that are trained to extract features from **a sampled RGB video frame paired with the surrounding stack of optical flow images**, followed by a late fusion of the prediction scores of both streams. The image stream encodes the appearance information while the optical flow stream encodes the motion information, that are often found to complement each other for action recognition. Several works followed this approach to find a suitable fusion of the streams at various depths [9] and to explore the use of residual connections between them [8]. These approaches rely on optical flow images for motion information, and a single RGB frame for appearance information, which is limiting when reasoning about the temporal context is required for video understanding.

## Video as a set or sequence of frames

如标题所示

> Later, other approaches were developed using multiple RGB frames for video classification. These approaches sparsely sample multiple frames from the video, which are applied to a 2D CNN followed by a late integration of frame-level features using average pooling [42], multilayer perceptrons [49], recurrent aggregation [5, 24], or attention [12, 34]. To boost performance, most of these approaches also combine video frame sequence with externally computed optical flow. This shows to be helpful, but computationally intensive.

## Modeling short-term temporal dependencies

> Other research has investigated the middle ground between late aggregation (of frame features) and early temporal processing (to get optical flow), by modeling short-term dependencies. This includes differencing of intermediate features [29] and combining Sobel filtering with feature differencing [36]. Other works [6, 30] develop a differentiable network that performsTV-L1[47], a popular optical flow extraction technique. The work of [21] instead uses a set of fixed filters for extracting motion features, thereby greatly reducing the number of parameters. DMC-Nets [32] leverage motion vectors in the compressed video to synthesize discriminative motion cues for two-stream action recognition at low computational cost compared to raw flow extraction.
>
> > *[21]  Motion feature network: Fixed motion filter for action recognition. (ECCV2018)*
> >
> > 本段内容来自 [CSDN博客]( https://blog.csdn.net/weixin_41648477/article/details/106113394 ) :  之前为了抓取motion信息，使用的是光流作为CNN的输入。而本文作者的目标是**基于光流算法来表示去寻找能够帮助分类动作识别任务的temporal特征**，而不是去寻找光流的最优解。 
> >
> > <img src="https://img-blog.csdnimg.cn/20200517104457305.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTY0ODQ3Nw==,size_16,color_FFFFFF,t_70" style="zoom:70%;" />
> >
> > 本段内容来自 [知乎](https://zhuanlan.zhihu.com/p/87035777) : **本工作基于 Limin Wang 的 TSN (Temporal Segment Networks)**  提出了 motion blocks 编码 spatial-temporal 信息．上图中也可以看到，帧先过base_cnn，文章称为appearance block．之后联立两帧的feature计算运动特征，再sum/concatenate 两个特征．此为一个完整的motion block.迭代多个motion block构成文章的模型．  
> >
> > *[32] DMC-Net: Generating discriminative motion cues for fast compressed video action recognition. (CVPR2019)*
> >
> > <img src="https://img-blog.csdnimg.cn/20190918172832701.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1Mzc0Njc0,size_16,color_FFFFFF,t_70" style="zoom:47%;" />
> >
> > 与 Motion Vector 相比, DMC 生成的特征噪声更少更有效。
> >
> > <img src="https://img-blog.csdnimg.cn/20190918221416559.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1Mzc0Njc0,size_16,color_FFFFFF,t_70" style="zoom:50%;" />

---

## Video as a space-time volume





## Spatial-temporal modeling