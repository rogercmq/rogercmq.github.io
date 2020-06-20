---
layout: post
title: 讲座笔记 -- VALSE Webinar Action Recognition (3)
categories: [LectureNotes, ActionRecognition]
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

**设计了两种 2D+3D 的 I3D 网络。**

![](https://img-blog.csdnimg.cn/20181224200235280.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6bXNodWFp,size_16,color_FFFFFF,t_70)

![](/images/VALSE/actionRecognization15.png)

## R(2+1)D

> Tran, Du, et al. "A closer look at spatiotemporal convolutions for action recognition." Proceedings of the IEEE conference on Computer Vision and Pattern Recognition. 2018.

作者是FAIR的工作人员，其中包括 Du Tran(C3D) 作者，Heng Wang(iDT) 作者和 Yann LecCun 等。

<img src="https://pic3.zhimg.com/80/v2-9d4e68ea46b17754fa70cf13c03be526_720w.jpg" style="zoom:80%;" />

R 代表 ResNet， 即残差网络。

关于 R2D ：

- 第一种将时间维度合并到 channel 维度中，比如将 C×T×H×W 的输入转变成 CT×H×W 的输入，然后直接输入到2D卷积网络中就可以得到最后的分类结果。这种方法称为R2D。
- 第二种方法不将时间维度和 channel 维度合并，而是**使用参数共享的 2D 卷积网络得到输入视频中每一帧的分类结果，最后对所有帧的结果融合得到最终的结果**，这种方法称为 f-R2D 的方法。
- 实验表明纯2D网络（包括R2D和f-R2D）比含3D的网络（包括R3D, MCx,rMCx, R(2+1)D）性能要差

关于 MC 和 rMC：

- 有一种观点认为卷积网络较低层对motion的建模比较好，而高层由于特征已经很抽象了，motion和时序信息建模是不需要的，因此作者提出了MCx网络，即将第x以及后面的3D卷积group换为2D的卷积group。注意此时MC1等效于f-R2D，即所有的层都是2D卷积。
- 同时还有一种假设认为高层的信息需要用3D卷积来建模，而底层的信息通过2D卷积就可以获取，因此作者提出了rMCx结构，前面的r代表reverse。rMCx表示前面的5-x层为2D卷积，后面的x层为3D卷积。
- 实验表明 MCx 性能优于 rMCr，因此说明在网络底层的3D卷积层更有用，而后面用2D卷积更合理。

关于 R(2+1)D：

<img src="https://pic1.zhimg.com/80/v2-97ca15743a303e8b2c51c99aec99d1d4_720w.jpg" style="zoom:60%;" />

- 增加了非线性的层数，原先的1个卷积变成2个卷积，而2个卷积之间多了非线性层（通过ReLU来得到）， 因此总体的非线性层增加了。用同样的参数来得到增加非线性的目的。
- 使得网络优化更容易，实验表明 R(2+1)D 的训练错误率比 R3D 更低，说明网络更易于训练。

**消融实验结果**

<img src="https://pic4.zhimg.com/80/v2-71b59cd73a7e94af9a7b761c1661280f_720w.jpg" style="zoom: 50%;" />

作者采用了8，16，24，32，40和48帧的clip进行实验，对clip-level的结果和video-level的结果进行分析，得到的准确率如Figure 5所示。可以看到，clip-level的准确率随着clip的长度增长在持续上升，而video-level的准确率则在24帧的时候达到最高，后面反倒有所下降，作者分析随着clip长度的增加，不同clip之间的相关性增加（甚至可能会产生重叠），所以video-level的准确率增益越来越小。 为了分析video-level准确率下降的原因，作者又做了两个实验：

1. 采用8帧的clip训练网络，然后在32帧的的clip上测试，发现结果相比用8帧的clip做测试，clip-level的准确率下降2.6%
2. 在8帧的clip上训练的网络的基础上，采用32帧的clip进行fine tune，得到的clip-level的准确率与32帧从头训练的结果相差不多（56.8% vs 58.5%），而比8帧的clip的clip-level结果高4.4%。因此用长的clip结果更高说明学到了long-term的时间域上的信息

 作者采用了224x224的输入训练网路，发现和112x112的输入结果只有微小的差距。 

## Channel-Separated Convolutional Network (CSN)

> Tran, Du, et al. "Video classification with channel-separated convolutional networks." Proceedings of the IEEE International Conference on Computer Vision. 2019.

![](/images/VALSE/actionRecognization16.png)

## ARTNet

> Limin Wang et al., Appearance-and-Relation Networks for Video Classification, CVPR2018

![](/images/VALSE/actionRecognization17.png)

ARTNet是由多个名为SMART的block堆叠而成。SMART模块的目标是从RGB帧中分别学习到appearance和relation。它包含两个部分，appearance branch用于对spatial建模，relation branch用于对temporal建模。

- **Appearance branch.** 这个分支作用于单帧的图像上，即对输入的视频帧使用 2D conv 来捕获每一帧的 spatial 信息。然后后面接 BN 和 ReLU。
- **Relation branch.** 这个分支作用在 stacked连续帧 上，用于捕获帧与帧之间的关系。在paper中有讨论过对于Relation的建模用 multiplication interactions 比较合适（具体看原文），所以文章提出了 square-pooling 的结构用于建模 temporal 的信息。具体地，首先在视频上用 3D conv，然后做 square，再 cross-channel pooling。 

## Non-local

> Wang, Xiaolong, et al. "Non-local neural networks." Proceedings of the IEEE conference on computer vision and pattern recognition. 2018.

![](/images/VALSE/actionRecognization18.png)

深层神经网络中，捕获远距离相关性是至关重要的：对于顺序数据(例如语音、语言)，递归操作是建模远程依赖性的主要解决方案；对于图像数据，长距离依赖关系是由深层次的卷积运算所形成的大感受野来建模的。

卷积操作和递归操作都会在空间或时间上处理一个局部邻域；因此，只有反复应用这些操作，逐步通过数据传播信号时，才能捕捉到长距离依赖关系。



但重复进行本地操作会有几个限制

首先，计算效率很低
其次，会造成优化方面的困难
最后，使得多跳跃的依赖性建模变得困难，例如，当需要在远程位置之间来回传递信息时。


在本文中，我们将非局部运算作为一种有效的、简单的、通用的部件来使深层神经网络捕获远距离依赖关系

我们提出的非局部运算是经典的非局部平均运算在计算机视觉中的推广
直观地说，非局部操作将某个位置的响应计算为输入特征映射中所有位置的特征的加权和。

位置可以是在空间、时间或时空中，这意味着我们的操作适用于图像、序列和视频问题

使用非局部操作有几个优点：

与循环和卷积操作的渐进行为相反，非本地操作通过直接计算任意两个位置之间的交互关系来捕获远程依赖性，不论它们的位置距离如何
非局部操作效率很高，即使网络只有很少层也能取得最佳效果
非局部操作输入大小是非固定的，可以很容易地与其他操作相结合（例如使用的卷积操作）