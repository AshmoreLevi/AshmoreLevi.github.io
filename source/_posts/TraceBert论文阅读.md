---
title: TraceBert论文阅读
catalog: false
author: Levi
header-img: /img/contact-bg.jpg
date: 2022-10-16 20:12:55
tags:
    - 论文阅读
---

## 论文阅读TraceBert

## 背景

### 作者

Alessandro Crivellari @Department of Computer Science and Engineering, Southern University of Science and Technology（计算机科学与工程系,南方科技大学）

### 动机

## BERT

##### Pre-training

预训练任务：MLM（masked language model）与NSP（Next Sentence Prediction）

 

###### Param

L（blocks）：transformer块个数

H：隐藏层hidden size

A：number of self-attention heads

###### Input/Output

一个句子或一个句子对（拼接 ），采用WordPiece embedding。30000 token。

[CLS] [SEP]

Token+Segment+**Position** Embedding

## 方法

### 问题定义

目标：系统从汇总的历史人类行动数据中自动处理识别出隐含的轨迹模式，从而能够从个人的不完整轨迹中重建出完整版轨迹。

定义：Given an individual user’s trajectory, sampled at a given time step, affected by spatial information gaps in correspondence of some specific time spans, our modeling solution allows filling of the gaps by inferring the unknown visited locations at those points in time. 给出以某种时间采样的个人轨迹，轨迹中有些时间段为空缺，有缺隙。模型需要在这些时间点将空隙填补。

### 方法设计

1. **Trajectory pre-processing.** raw traces are pre-processed into discrete location  sequences;

2. **Location masking.** the training set is defined by randomly hiding a portion of locations in each trajectory, replacing their unique identifiers with a masking token in the corresponding position along the sequence. 训练集被定义为在每条轨迹中随机将部分地点掩码，取代为masking token。

3. **Bert model training.** the BERT model is trained through backpropagation, by feeding the partially hidden location sequences with the goal of optimizing the correct prediction in the masked positions. Bert模型的训练通过优化掩码位置的正确预测来进行。

   ![](2022-10-16-20-18-11.png)

   Transformer Encoder：

   - multi-head self-attention layer：编码每个元素与序列中其他各元素的关系，给更重要的元素以更高的相关权重
   - position-wise fully connected feed-forward network：前馈网络将自身并行应用于每个结果元素的输出向量
   - 

   

   > **MLM** 任务包括为 BERT 提供“部分被屏蔽的序列”，并以此优化其权重，以正确显示该序列的被屏蔽元素作为输出。
   >
   > 以往的方法使用非双向的预测，或者结合从左到右与从右到左两种模式的训练来拟合双向。

4. **Location gap inference.** the model is evaluated by means of testing trajectories, leading to an automatic gap-filling of the missing locations along each trace.



## 实验

### 数据集

a real-world large-scale trajectory dataset of non-repetitive short-term tourists.非重复

seven months of anonymized mobile phone call detail records (CDRs) of roamers in Italy

1. 与日常型轨迹高度依赖历史周期性中**频繁访问**地点不同，该实验使用旅行轨迹作为数据集，因此轨迹中基本是不熟悉、未曾涉足的区域。
2. a large-scale movements则需要分析**广泛区域**内的轨迹数据，这是在尝试解决数据稀疏问题与大规模位置点问题。

选择在该区域内停留时间仅在两周内的游客用户。

预处理后最终数据集：每小时位置序列，共有5903个区域内离散点。将轨迹划分为7小时的时段，得到由140万个用户产生的1300万条轨迹。

###### 基础评价Baseline

Personal Markov model：表现最差

Global Markov model：表现不错，与TraceBERT相当

Global location co-visits

##### 不同移动特性的实验

###### travel distance

随着总移动距离的增加，各种模型的表现都下降

###### radius of gyration

随着回转半径

###### different hours of the day

时间上，夜间行为恢复效果更好，因为行动更有规律。

###### the amount of missing information

其实就是缺失率。被掩码的位置数目对结果的影响。随着确实率的提高，所有模型恢复的准确性都会下降。TraceBERT相较而言在高缺失的条件表现较其他好。

###### misprediction on the same corresponding masked location

TraceBERT除了能得到更好的准确度分数，还提供更短的误差距离。

## 启示

好句：

“The most straightforward use would be aimed to improve the data quality for subsequent downstream tasks, generating complete trajectories out of sparse recording observations or missing recording gaps. Such newly generated traces can be then utilized in a multitude of implementations involving trajectory data.” 最直接的用途将旨在提高后续下游任务的数据质量，从稀疏的记录观察或丢失的记录间隙中生成完整的轨迹。

“Among many options, correctly reconstructing missing mobility information of single individuals can lead to potential improvements in the quality of personalized recommendations and touristic experiences, assuming that the previously visited venues and attractions intrinsically carry information on the user’s characteristics and potential future trips, further leading to promotions, service opportunities and demand estimations.” 在众多选项中，假设先前访问过的场所和景点内在地携带有关用户特征和**潜在未来旅行的信息**，正确重建单个个体缺失的移动信息可以**潜在地提高个性化推荐和旅游体验**的质量，进一步导致**促销、服务机会和需求估计集体移动性发掘**的重要性。

这种非重复轨迹的集合导致基于转移概率的马尔可夫模型总体上优于完全基于位置共访的方法，突出了位置排序和方向性的重要性。

作者总结的未来方向：

- 不同时间和空间分辨率规模下的轨迹重建
- 探索轨迹数据的更多信息，如个人特征或明确时间特征（环境属性）
- 语义层面的理论解释