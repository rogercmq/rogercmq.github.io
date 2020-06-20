---
layout: post
title: 讲座笔记 -- VALSE Webinar Action Recognition (4)
categories: [LectureNotes, ActionRecognition]
description: 
keywords: 
---

# 乔宇：复杂视频序列的深度表征与理解方法 (4)

## 递归姿态注意网络

![](/images/VALSE/actionRecognization23.png)

这是一篇视频动作识别的论文，但值得注意的是，他**利用pose estimation的信息**，即视频中人物的关节点的信息。论文没有在常见的 HMDB 和 UCF101 上测试，而是在两个带有关节点信息的小数据集上进行了测试（Sub-JHMDB 和 PennAction）

![](/images/VALSE/actionRecognization24.png)

![](/images/VALSE/actionRecognization25.png)

