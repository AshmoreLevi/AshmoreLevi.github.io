---
title: Python基础知识补全
catalog: false
author: Levi
header-img: /img/contact-bg.jpg
date: 2022-10-24 22:18:48
tags:
---


##### 关于VS Code调试Python时的路径问题

在 VS Code 中执行 py 文件时，默认是从当前打开的文件夹目录为执行路径 os.getcwd()（文件读写相对路径和这个有关），但是 Python 环境变量 sys.path[0] 默认是 py 文件所在目录（模块查找路径和这个有关）。如果 main 入口在子文件夹就会有些问题，比如相对路径导入模块时会报错。

解决方法：

```py
import os, sys
os.chdir(sys.path[0])
```

##### Python 中的 Special Variables 与 Function Variables

类似__xx__，以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，它不是 private 变量。

__init__(self,…):构造函数

##### Python enumerate()

enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。

```
>>> seq = ['one', 'two', 'three']233
>>> for i, element in enumerate(seq):
...     print i, element
...
0 one
1 two
2 three
```

##### Python set()
set() 函数创建一个无序不重复元素集，可进行关系测试，删除重复数据

##### Python算数运算符

```
** 乘方
// 地板除
```

##### zip()

``` py
# zip()
a = [1,2,3]
b = [4,5,6]
c = [7,8,9,10]

zipped = zip(a,b)

a1,b1 = zip(*zipped)

print(a1)
print(b1)
```