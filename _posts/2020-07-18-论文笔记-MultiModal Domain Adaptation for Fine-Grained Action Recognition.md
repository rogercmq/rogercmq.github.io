---
layout: post
title: 论文笔记 -- Multi Modal Domain Adaptation for Fine-Grained Action Recognition
categories: [PaperNotes, ActionRecognition]
description: 
keywords: 
---

(CVPR2020) Fine-grained action recognition datasets exhibit environmental bias, where multiple video sequences are captured from a limited number of environments. Training a model in one environment and deploying in another results in a drop in performance due to an unavoidable domain shift. Unsupervised Domain Adaptation (UDA) approaches have frequently utilised adversarial training between the source and target domains. However, these approaches have not explored the multi-modal nature of video within each domain. In this work we exploit the correspondence of modalities as a self-supervised alignment approach for UDA in addition to adversarial alignment (Fig. 1). We test our approach on three kitchens from our large-scale dataset, EPIC-Kitchens [8], using two modalities commonly employed for action recognition: RGB and Optical Flow. We show that multi-modal self-supervision alone improves the performance over source-only training by 2.4% on average. We then combine adversarial training with multi-modal self-supervision, showing that our approach outperforms other UDA methods by 3%.

![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-001.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-002.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-003.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-004.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-005.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-006.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-007.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-008.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-009.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-010.jpg)



![](/images/CVPR2020_MultiModal_Domain_Adaptation_for_FineGrained_Action_Recognition/A-page-011.jpg)