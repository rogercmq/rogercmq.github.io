---
layout: post
title: CUDA -- Day5 CUDA编程一
categories: [CUDA]
description: 
keywords: 
---

从本章开始介绍CUDA编程。

GPGPU:   图形处理单元上的通用计算 (General-purpose computing on graphics processing units)

CUDA 三大特点: 1. 层次化的线程集合；2. 共享存储；3.同步

| 术语   | 解释                                                         |
| ------ | ------------------------------------------------------------ |
| host   | 主机端，通常指CPU                                            |
| device | 设备端，通常指GPU（数据可并行）                              |
| kernel | 数据并行处理函数，在主机端通过kernel函数在设备端创建轻量级硬件管理线程（线程由硬件负责创建并调度），类似于OpenCL的shader |

线程层次：

1. grid
2. block
   1. 一个grid里面的每个block的线程数是一样的
   2. block 内部的每个线程可以：同步；访问共享存储器
   3. two threads from two different blocks cannot cooperate

# 矩阵element-wise加 (1 thread block, 2D block, 线程索引threadIdx)

![](/images/CUDA/24.png)

# 矩阵element-wise加 (16x16 thread block, 2D block, 块索引blockIdx)

![](/images/CUDA/25.png)

![](/images/CUDA/26.png)

线程块（block）之间彼此独立执行，可并行可串行（并不一定按照编号）—— 被任意数量的处理器以任意顺序调度，因此处理器的数量具有可拓展性。

一个块内部的线程：

- 共享容量有限的低延迟存储器（shared memory）
- 同步执行
  - 合并访存
  - \_\_syncThreads()

![](/images/CUDA/27.png)

![](/images/CUDA/28.png)

# CUDA内存传输

cudaMalloc() 在设备端分配global memory

cudaFree()

![](/images/CUDA/29.png)

![](/images/CUDA/30.png)

cudaMemcpy()

![](/images/CUDA/31.png)

# 矩阵相乘算法

![](/images/CUDA/32.png)

![](/images/CUDA/33.png)

![](/images/CUDA/34.png)

在算法框架中添加CUDA transfer：

![](/images/CUDA/35.png)

![](/images/CUDA/36.png)

CUDA C编程实现：

![](/images/CUDA/37.png)

![](/images/CUDA/38.png)

CUDA C编程调用kernel：

![](/images/CUDA/39.png)

![](/images/CUDA/40.png)

