---
author: "me"
title: "A Simple Framework for Contrastive Learning of Visual Representations"
date: "2021-11-28T20:44:00-07:00"
description: ""
tags: ["Contrastive Learning", "Machine Learning"]
categories: ["Paper reading"]
# series: [""]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
---


### Framework
- 核心思想：对同一个样本做不同的数据增强构造样本，通过对比Loss 最大化同源的数据增强样本之间的 Agreement。可类比人脸识别。
- 四个过程：Data Augmentation -> Base Encoder -> Projection Head -> Contrastive Loss
  - Base Encoder：比如ResNet；
  - Projection Head：简单的单隐层MLP；
  - Contrastive Loss

![framework of simclr]({{ '/assets/images/framework_of_clr.png' | relative_url }})
{: style="width: 400px; max-width: 100%;"}

### Main Contributions
- **数据增强**：组合很重要，相比有监督学习，数据增强对无监督对比学习增益更大；
- **任务解耦**：在表示向量和对比Loss 之间加入可学习非线性变换很重要；
- **对比Loss**：归一化Embedding 和温度参数有收益；
- 更大的Batch 和更长的训练有收益，更深或更宽的模型有收益

### Data Augment
- 数据增强操作分为两大类：空间/几何变换、外观变换
- 最优的组合：Crop + Color distort
  - Crop + Resize：从图片的不同部分提取特征；
  - Color distort：避免模型过拟合到颜色直方图上
- 数据增强对非监督学习更有用

### Nonlieanr Projection Layer
- 非线性 = 线性 + 3% = None + 10%
- 非线性层之前 = 非线性之后 + 10%
- 非线性映射层之后更任务相关，泛化差；
- 经过非线性映射层之后，信息量损失很大，通过转换矩阵的秩得出这个结论；
- 大多数CV预训练模型都是这样处理的；

### Contrastive Loss
- NT-Xent (the normalized temperature-scaled cross entropy loss
- 结果
- L2 和 温度的重要性、Contrastive acc 与 Top 1 acc 并不总是一致

### Batch Size 与 Epochs 影响

### Results
- 与无监督
- 与半监督、有监督
- 迁移学习：在ImageNet 上预训练，在其它任务上迁移

#### Reference

---