---
title: Cam_Traj_Rec论文复现
catalog: false
author: Levi
header-img: /img/contact-bg.jpg
date: 2022-10-16 20:12:27
tags:
    - 论文复现
---

# KDD’22 Cam_Traj_Rec

---

## 论文简介

## 复现细节

### 文件结构

### 数据文件

#### camera_info.pkl

```
class: list
len(): 147
# 例：000: {'id':0, 'node_id':1228}
# 有一部分的id前带有'camera'
```

#### road_graph.pkl

```

```
#### records_100w_pca_64.pkl

```py
class: list
len(): 999654
# 例：{
    'vehicle_id': None, 
    'camera_id': 88, 
    'car_feature': array([-3.5037674e-02, -1.5768880e-02,  4.0063962e-02,  6.2312847e-03,
       -5.0646484e-02, -3.4165952e-02, -7.1852408e-02,  4.0639136e-03,
       -1.2009477e-04, -4.3527661e-03, -2.4399173e-02, -3.6135782e-02,
        1.9503264e-02, -3.9249066e-02,  9.6481234e-02, -8.6406693e-02,
       -1.0230435e-02, -1.3215089e-01,  5.0576232e-02, -1.9055100e-02,
       -3.0239424e-02, -6.1923801e-04,  5.0271440e-02, -2.4731858e-02,
       -1.0424526e-03,  5.6518514e-02,  2.6984716e-02, -2.4589464e-02,
        2.5609093e-02, -9.6780574e-03, -1.8288985e-02,  3.2427087e-02,
       -3.6027280e-03, -3.3669520e-02,  2.9647321e-02, -2.9521914e-02,
        1.0191399e-02, -3.7233617e-02,  4.1315429e-02,  1.1902056e-02,
       -3.7582777e-02, -1.0578616e-02, -3.4287002e-02, -7.5835055e-03,
       -4.2379178e-02,  5.1208910e-02, -2.2433985e-02,  8.7926164e-02,
       -9.3611227e-03,  7.7165209e-02, -8.2266703e-03, -3.7514783e-02,
       -7.8368120e-02, -1.3725712e-02, -3.1114252e-02,  1.7932989e-02,
       -2.8715754e-02,  2.8470850e-02,  2.3698460e-03, -3.4678895e-02,
       -2.4395386e-02, -1.6717903e-02,  8.4505491e-03, -2.4319584e-02],
      dtype=float32), 
    'plate_feature': None, 
    'plate_text': None, 
    'time': 67032, 
    'record_id': 3701679
    }
# car_feature的size为64    
```
#### matched_traj.pkl


> A data format example for "matched_traj.pkl"
The file "matched_traj.pkl" which is readed in "calculate_speed.py" is the map-matched historical trajectories.
It also involves original GPS points thus is not open access.
If you' re interested in running "calculate_speed.py", you have to prepare your map-matched trajectories.
Here shows the data format of each item in "matched_traj.pkl" for your convenience.

```
lon, lat = 111, 22

{
 'index': 64074,
 'path': [
          [901,   # 路网中的edge_id, 匹配路径的第一条路
           [      # 匹配到这条路上的所有轨迹点
            {'order': 0,  # 轨迹点在原始经纬度轨迹中的索引
             'orig_point': [lon, lat, 6467.0],  # 原始轨迹点[lon, lat, t]
             'point': [lon, lat, 6467.0]},      # 匹配后投影到路上的轨迹点
            {'order': 1,
             'orig_point': [lon, lat, 6478.0],
             'point': [lon, lat, 6478.0]},
            {'order': 2,
             'orig_point': [lon, lat, 6547.0],
             'point': [lon, lat, 6547.0]}
           ]      
          ],
          [325,   # 路网中的edge_id, 匹配路径的第二条路
           [
            {'order': 3,
             'orig_point': [lon, lat, 6557.0],
             'point': [lon, lat, 6557.0]},
            {'order': 4,
             'orig_point': [lon, lat, 6567.0],
             'point': [lon, lat, 6567.0]},
            {'order': 5,
             'orig_point': [lon, lat, 6578.0],
             'point': [lon, lat, 6578.0]}
           ]
          ]
        ],
 'start_end_portion': (
    0.1663753030146705,  # 第一条路被通过的比例(即第一条路上, 第一个轨迹点及之后的部分的占比)
    0.5463860908881429   # 最后一条路被通过的比例(即最后一条路上, 最后一个轨迹点及之前的部分的占比)
  )  
}
```
### run.py运行过程

#### 整体迭代过程

```
---------- iter 0 -----------
clustering...
2022-10-12 15:01:32.845 INFO Normalize
100%|█████████████████████| 999654/999654 [00:21<00:00, 45754.56it/s]
2022-10-12 15:01:54.694 INFO Search topk
2022-10-12 15:04:05.015 INFO Clustering
100%|█████████████████████| 999654/999654 [08:45<00:00, 1902.23it/s]
2022-10-12 15:12:50.544 INFO done
clustering consume time: 686.0012559890747
------------------
clusters: 435545
precision: 0.8620717334683076
recall:    0.797085689430187
fscore:    0.8283060165176034
expansion: 3.8071065989847717
------------------
cluster merging...
merging consume time: 118.32811117172241
```
先通过SigCluster进行聚类操作

#### SigCluster类

通过FlatSearcher指定好GPU相关后，通过进入fit()函数，获取到cluster的结果。

```
fit(
        self,
        data,
        initial_labels=None,
        weights=[0.1, 0.9],
        similarity_threshold=0.88,
        topK=128,
        normalized=True,
    )

labels = cluster.fit(
                [[a, b, c] for a, b, c in zip(f_car, f_plate, f_emb)], # data，其len为999654
                weights=[0.1, 0.8, 0.1], # 每个特征赋予一个权重
                similarity_threshold=s, # 相似度阈值，大于这个阈值的就被聚类为一类
                topK=topK,# 聚类搜索时搜索topK项
            )    

```

特征的维度为[64,64,64]，即通过将car_feature、plate_feature、plate_text三个维度的数据，进行车辆聚类。

```
f_car = [x["car_feature"] for x in records]
f_plate = [x["plate_feature"] for x in records]
f_emb = deepcopy(f_car)
```

data_:将data转化为3个维度，每个维度999654条数据，即相当于解压成3个特征

对于data_中的某个特征维度i，再解压为f特征和f_id特征序号

循环结束后分别加入到fs（3\*特征总数\*特征维数64）与f_ids（3\*特征总数）

f_topks内：对于每个特征的向量，找最相似的128个向量（这个过程非常耗时，运算维度很大）

运算好后的f_topks:(3\*特征总数，每个特征后求出相似度在前128的其他特征)

