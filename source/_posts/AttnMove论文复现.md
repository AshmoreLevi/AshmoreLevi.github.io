---
title: AttnMove论文复现
catalog: false
author: Levi
header-img: /img/home-bg.jpg
date: 2022-09-27 21:11:30
tags:
    - 论文复现
    - 时空数据挖掘
    - 轨迹恢复 
---

# 代码目录结构

```
.
├── README.md
├── baselines
│   ├── Embedder.py
│   ├── README.md
│   ├── baseline.py
│   ├── dataset_utils.py
│   ├── model_utils.py
│   └── self_attn_hyperparams_region.py
├── data
│   ├── README.md
│   ├── pos.test.txt
│   ├── pos.train.txt
│   ├── pos.validate.txt
│   ├── pos.vocab.txt
│   └── region_data
│       ├── 116.1_116.7_39.7_40.2_counter10.png
│       ├── README.md
│       ├── region_beijing_countfilter10.zip
│       └── show_region.py
├── log
│   ├── README.md
│   └── analyse_data
│       └── README.md
└── model
    ├── Embedder.py
    ├── README.md
    ├── dataset_utils.py
    ├── main.py
    ├── model_utils.py
    └── self_attn_hyperparams_region.py
```

# 实验设置

## 数据集

> Geolife: This open data is collected from Microsoft Research Asia Geolife project by 182 users from April 2007 to August 2012 over all the world. Each trajectory is represented by a sequence of time-stamped points, containing longitude and altitude (Zheng et al. 2010).

在实验中，处理40用户的896条轨迹，轨迹点共有3439个。

> 预处理：将北京地图划分为10665块，每块面积平均 0.265 $km^2$。将时间间隔设置为30分钟。过滤少于34个时隙的轨迹（一天的70%）

# 实验结果

![](2022-09-29-20-31-18.png)