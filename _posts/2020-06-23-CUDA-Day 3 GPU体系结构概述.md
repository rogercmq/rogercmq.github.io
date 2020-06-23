---
layout: post
title: CUDA -- Day3 GPU体系结构概述
categories: [CUDA]
description: 
keywords: 
---

**本节内容：为什么需要GPU？三种方法提升GPU的处理速度？实际GPU设计举例（GTX480 Fermi & GTX680 Kepler）？GPU的存储器设计？**

名词解释：

1. FLOPS: Floating-point Operations per Second
2. GFLOPS, TFLOPS

GPU是一个异构（heterogeneous）的多处理器（multi-processor）芯片，为图形图像处理优化。

执行单元（execute shader）：Fetch/Decode，ALU，Execution Context。GPU 是一种“CPU-style Cores”，但与 CPU 不同的是 CPU 核具有巨大的 data cache，以及 out-of-order control logic，fancy branch predictor，memory pre-fetcher —— 这些部分占用了CPU大部分芯片面积。

三种提升GPU的处理速度：

1. slimming down