---
layout: post
title: 论文笔记 -- EagleEye Fast Subnet Evaluation for Efficient Neural Network Pruning
categories: [PaperNotes, NetworkPruning]
description: 
keywords: 
---

《EagleEye: Fast Subnet Evaluation for Efficient Neural Network Pruning (ECCV 2020)》。投稿了ICCV2020（题目是《FNNP: Fast Neural Network Pruning Using Adaptive Batch Normalization》）但是撤稿了。

题目是《EagleEye: Fast Subnet Evaluation for Efficient Neural Network Pruning (ECCV 2020)》。曾经投稿ICCV 2020（题目是《FNNP: Fast Neural Network Pruning Using Adaptive Batch Normalization》）但是主动撤稿了，毕竟给分全是 weak reject。OpenReview 指路： https://openreview.net/forum?id=rJeUPlrYvr 

> **其中一位评审的评语：ABN 动机不明确，过于empirical**
>
> - My major concern of this paper is that it fails to state the motivation to adopt adaptive BN clearly. Based on the existing statements, ABN would be fast since it recalculates the statistics for BN based on a small part of training data. And It may be accurate since this evaluation module establishes a strong correlation between the sub-nets accuracies and their converged accuracy. **However, the key reason why the global BN can cause week correlations and why adaptive BN can establish a strong connection is never pointed out.** It is not convincing to simply experimentally evaluate the baselines achieve lower correlations to support the claim.   



![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-01.png)



![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-02.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-03.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-04.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-05.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-06.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-07.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-08.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-09.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-10.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-11.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-12.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-13.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-14.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-15.png)





![](/images/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning/ECCV2020_EagleEye_Fast_Subnet_Evaluation_for_Efficient_Neural_Network_Pruning-16.png)