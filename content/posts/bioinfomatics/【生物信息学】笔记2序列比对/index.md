---
title: 【生物信息学】笔记2序列比对
date: 2026-07-21T00:00:00+08:00
author: Chen Z
cover: cover.jpg
images:
- cover.jpg
categories:
- 生物信息学
- 学习笔记
---


本章主要介绍序列比对的基本概念、动态规划方法进行全局比对、全局比对和局部对比、考虑仿射空位的序列比对等。


<!--more-->


## 1 序列比对（Sequence Alignment）基础

### 研究对象

- **B**iology
   - What is the biological question or problem?
- **D**ata
  - What is the input data?
  - What other supportive data can be used?
- **M**odel
  - How is the problem formulated computationally?
  - Or, what's the data model?
- **A**lgorithm
  - What is the computational algorithm?
  - How about its performance/limitation?



### 生物学问题

**"How can we determine the similarity between two sequences?"**

"我们如何确定两条序列之间的相似性？"

**Why is it important?**（相似性为什么重要？）

- Similar sequence → Similar structure → Similar function（相似序列 → 相似结构 → 相似功能）
    - The "**Sequence-to-Structure-to-Function Paradigm**"（"序列-结构-功能范式"）

- Similar sequence → Common ancestor（相似序列 → 共同祖先）
    - "**Homology**"，即"**同源性**"


### 生物学中的序列比对（Sequence Alignment in Biology）

The purpose of a sequence alignment is to line up all residues in the inputted sequence(s) for **maximal level of similarity**, in the sense of **their functional or evolutionary relationship**.
（序列比对的目的是将输入序列中的所有残基排列起来，以达到**最大程度的相似性**，这种相似性是基于**它们的功能或进化关系**的。）



### 示例：序列比对实例与打分系统


![](eg1.png)

- 左侧：序列比对结果（HBA vs HBB 人类血红蛋白）
- 右上：BLOSUM62 替换矩阵
- 右下：仿射空位罚分（Affine gap penalty）

    **Affine gap penalty:** **opening** a gap receives a penalty of **d**; **extending** a gap receives a penalty of **e**. So the total Penalty for a gap with length n would be: 
    **Penalty = d + (n-1) * e**

- 底部：最终得分公式

    **Final Score = (sum of substitution scores) + (-1) * (sum of Gap Penalty)**
    
    最终得分 = 替换得分总和 + (-1) × 空位罚分总和）


## 2 动态规划方法进行全局比对



## 3 全局比对 VS 局部比对

- 全局比对（Global Alignment）
    - 算法：Needleman–Wunsch algorithm

- 局部比对（Local alignment）
    - 算法：Smith-Waterman algorithm

### 全局比对与局部比对的递推公式对比

#### 全局比对（Global alignment）

$$F(0,0) = 0$$

$$F(i,j) = \max \begin{cases} F(i-1, j-1) + s(x_i, y_j) \\ F(i-1, j) + d \\ F(i, j-1) + d \end{cases}$$

---

#### 局部比对（Local alignment）

$$F(0,0) = 0$$

$$F(i,j) = \max \begin{cases} F(i-1, j-1) + s(x_i, y_j) \\ F(i-1, j) + d \\ F(i, j-1) + d \\ \boxed{0} \end{cases}$$

（注：局部比对比全局比对多了一个取 **0** 的选项）

---

### 局部比对的动态规划示例(DP for Local alignment: Example)

**题目：**
> Find the optimal **local alignment** of AAG and AGC.
> Use a linear gap penalty of **d = -5**.

**赋分矩阵：**

|     | A   | C   | G   | T   |
|-----|-----|-----|-----|-----|
| **A** | 2   | -7  | -5  | -7  |
| **C** | -7  | 2   | -7  | -5  |
| **G** | -5  | -7  | 2   | -7  |
| **T** | -7  | -5  | -7  | 2   |

---

**动态规划递推关系示意图：**

```
        0
       / \
F(i-1,j-1)  F(i,j-1)
   ↘ s(xᵢ,yⱼ)  ↓ d
      → F(i,j) ←
     /
F(i-1,j) → d
```

---

**动态规划得分矩阵（DP Matrix）：**

|       |     | **A** | **A** | **G** |
|-------|-----|-------|-------|-------|
|       | **0** | **0** | **0** | **0** |
| **A** | 0   | 2     | 2     | 0     |
| **G** | 0   | 0     | 0     | **4** |
| **C** | 0   | 0     | 0     | 0     |

> （最优路径用红色虚线标出，最大得分 **4** 位于矩阵右下角区域）

---

#### 全局比对 vs 局部比对（Global vs. Local）

---

##### 全局比对公式（上方）

$$F(0,0) = 0$$

$$F(i,j) = \max \begin{cases} F(i-1, j-1) + s(x_i, y_j) \\ F(i-1, j) + d \\ F(i, j-1) + d \end{cases}$$

**全局比对结果示例：**

| A | A | G | - |
|---|---|---|---|
| - | A | G | C |

| A | A | G | - |
|---|---|---|---|
| A | - | G | C |

---

##### 局部比对公式（下方）

$$F(0,0) = 0$$

$$F(i,j) = \max \begin{cases} F(i-1, j-1) + s(x_i, y_j) \\ F(i-1, j) + d \\ F(i, j-1) + d \\ 0 \end{cases}$$

**局部比对结果示例：**

| A | G |
|---|---|
| A | G |

| A |
|---|
| A |



## 