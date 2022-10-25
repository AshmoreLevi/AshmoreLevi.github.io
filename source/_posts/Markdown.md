---
title: Markdown
catalog: false
author: Levi
header-img: /img/home-bg.jpg
date: 2022-09-27 11:18:37
tags:
---

## 数学公式

测试行内 $y = x' \sin \theta + y'\cos \theta$

测试整行

$$\begin{aligned}
\frac{\partial^{2} \mathrm{f}}{\partial \mathrm{x}^{\prime 2}}=& \frac{\partial^{2} \mathrm{f}}{\partial \mathrm{x}^{2}} \cos ^{2}(\theta)+\frac{\partial}{\partial \mathrm{x}}\left(\frac{\partial \mathrm{f}}{\partial \mathrm{y}}\right) \sin (\theta) \cos (\theta)
+\frac{\partial}{\partial \mathrm{y}}\left(\frac{\partial \mathrm{f}}{\partial \mathrm{x}}\right) \sin (\theta) \cos (\theta)+\frac{\partial^{2} \mathrm{f}}{\partial \mathrm{y}^{2}} \sin ^{2}(\theta)
\end{aligned}$$

常用符号

- 记号

| markdown | 小写效果 | 大写效果 |
| :--: | :--: | :--: |
| \sigma | $\sigma$ | $\Sigma$ |
| \delta | $\delta$ | $\Delta$ | 
| \epsilon | $\epsilon$ | $\Epsilon$ | 
| \varepsilon | $\varepsilon$ |  |
| \lamda | $\lambda$ | $\Lambda$ |
| \gamma | $\gamma$ | $\Gamma$ |
| \xi | $\xi$ |  |
| \pi | $\pi$ | $\Pi$ |
| \rho | $\rho$ | $\Rho$ |
| \phi | $\phi$ | $\Phi$ |
| \varphi | $\varphi$ |  |
| \psi | $\psi$ | $\Psi$ |
| \omega | $\omega$ | $\Omega$ |
| \theta | $\theta$ | $\Theta$ |


- 字体
  
| markdown | 名称 | 效果 |
| :--: | :--: | :--: |
| \mathrm{ABCDabcd} | 罗马体 | $\mathrm{ABCDabcd123}$ |
| \mathcra{ABCDabcd} | 花体体 | $\mathscr{ABCDabcd123}$ |
| \mathbb{ABCDabcd} | 黑板体 | $\mathbb{ABCDabcd123}$ |
| \mathbf{ABCDabcd} | 黑体 | $\mathbf{ABCDabcd123}$ |
| \mathbf{ABCDabcd} | 德国字体 | $\mathfrak{ABCDabcd123}$ |
| \mathbf{ABCDabcd} | 手写体 | $\mathcal{ABCDabcd123}$ |
| \mathbf{ABCDabcd} | 打印机体 | $\mathtt{ABCDabcd123}$ |
| \mathbf{ABCDabcd} | 意大利体 | $\mathit{ABCDabcd123}$ |
| \mathbf{ABCDabcd} | 等线 | $\mathsf{ABCDabcd123}$ |



- 运算符

| markdown | 名称 | 效果 |
| :--: | :--: | :--: |
| \int | 积分 | $\int$、$\iint$ |
| \partial | 偏导 | $\partial$ |
| \sum | 求和 | $\sum$ |
| \prod | 连乘 | $\prod$ |
| \infty | 无限 | $\infty$ |
| \～arrow | 箭头 | $\leftarrow$、$\rightarrow$、$\leftrightarrow$、$\Leftrightarrow$ |
| \leq、\geq | 不等号 | $\leq$、$\geq$、$\leqq$、$\geqq$ |
| \sqrt | 根式 | $\sqrt{}$ |

- 矩阵
```
\begin{vmatrix}
x & y \\
z & v
\end{vmatrix}
```
$$\begin{vmatrix}
      x & y \\
      z & v
      \end{vmatrix}$$

- 条件等式
```
f(n) =
\begin{cases}
n/2, & \text{if }n\text{ is even} \\
3n+1, & \text{if }n\text{ is odd}
\end{cases}
```
$$f(n) =
      \begin{cases}
      n/2, & \text{if }n\text{ is even} \\
      3n+1, & \text{if }n\text{ is odd}
      \end{cases}$$

- 多行等式
```
\begin{align}
f(x) & = (a+b)^2\\
& = a^2+2ab+b^2
\end{align}    
```
$$\begin{array}{}
f(x) & = (a+b)^2 \\
& = a^2+2ab+b^2
\end{array}$$

## 基础语法

### 标题

```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

### 列表

无序列表

```
- 列表 1
  - 列表 1.1
    - 列表 1.1.1
  - 列表 1.2
- 列表 2
- 列表 3
```

- 列表 1
  - 列表 1.1
    - 列表 1.1.1
  - 列表 1.2
- 列表 2
- 列表 3

---

有序列表

```
1. 列表 1
   1. 列表 1.1
   2. 列表 1.2
2. 列表 2
3. 列表 3
```

1. 列表 1
   1. 列表 1.1
   2. 列表 1.2
2. 列表 2
3. 列表 3

### 引用

在引用文字前加上 `>` 并与文字保留一个字符的空格：

> 引用
>   > 嵌套引用


### 分割线

分割线可以由\* - \_（星号，减号，底线）这 3 个符号的至少 3 个符号表示:

---


### 链接与图片

链接：`[显示文本](链接地址)` 

图片：`![显示文本](图片链接地址)`

插入链接：
[链接示例](http://example.com/)

插入图片：
![图片示例](2022-09-27-18-00-56.png)

### 代码框

```python
print("Hello,wolrd!")
```

### 表格

```
| name | age | sex |
| :--: | :-- | --: |
| tony | 18  | 男  |
```

| name | age | sex |
| :--: | :-- | --: |
| tony | 18  |  男 |

### 强调

```
*字体倾斜*
**字体加粗**
~~删除文字~~
```

<div style="text-align:center;color:gray;">效果如下：</div>

_字体倾斜_

**字体加粗**

~~删除文字~~

### 待办
```
- [ ] 待办
- [x] 已完成 
```
- [ ] 待办
- [x] 已完成 

