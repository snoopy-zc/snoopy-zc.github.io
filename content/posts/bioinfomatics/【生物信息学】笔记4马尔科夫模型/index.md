---
title: 【生物信息学】笔记4马尔科夫模型
date: 2026-07-26T00:00:00+08:00
author: Chen Z
cover: cover.jpg
images:
- cover.jpg
categories:
- 生物信息学
- 学习笔记
---


本章主要介绍马尔科夫链、隐马尔科夫模型等内容。


<!--more-->


## 1 从状态到马尔科夫链

**Markov Chain** （1906）

- A Markov chain describes a **discrete stochastic process at successive times**. The transitions from one state to all other states, including itself, are governed by **a probability distribution**

- 马尔可夫链描述的是连续时刻上的离散随机过程。从一个状态到所有其他状态（包括其自身）的转移，都由一个概率分布所支配。

![Alt text](eg-markov-chain.jpg)

上图右下角即为状态转移的概率分布矩阵。

---

## 2 隐马尔科夫模型


- The **observable symbols** ("tokens", y(t)) are generated according to their **corresponding states** (x(t)).    
（**可观察符号**（"标记/token"，y(t)）根据其**对应的状态**（x(t)）生成。）


- In addition to State **Transition Probability**, each state of HMM has a probability distribution over the possible output tokens (**Emission Probability**).
（除了状态**转移概率**之外，HMM的每个状态对可能的输出标记都有一个概率分布（**输出概率**）。）

- Thus, a HMM is consist of **two strings of information**.
  （因此，HMM由**两条信息链**组成。）
  - The **state path**（状态路径）
  - The **token path** (emitted sequence).（标记路径/输出序列）

**结构示意图：**

```
State Path（状态路径）:   X₁  →  X₂  →  ...  →  Xₙ₋₁  →  Xₙ
                         ↓      ↓             ↓        ↓
Token Path（标记路径）:   Y₁     Y₂    ...     Yₙ₋₁     Yₙ
```

- **State Path（状态路径）**：隐藏的状态序列 X₁, X₂, ..., Xₙ
- **Token Path（标记路径）**：可观察的输出序列 Y₁, Y₂, ..., Yₙ
- 箭头表示状态之间的转移以及状态到标记的生成关系


---

### HMM 核心概念总结

| 概念 | 英文 | 含义 |
|------|------|------|
| 状态路径 | State Path | 隐藏的、不可直接观察的状态序列 X = (X₁, X₂, ..., Xₙ) |
| 标记路径 | Token Path | 可观察的输出序列 Y = (Y₁, Y₂, ..., Yₙ) |
| 转移概率 | Transition Probability | 从一个状态转移到另一个状态的概率 P(Xₜ₊₁ \| Xₜ) |
| 发射概率 | Emission Probability | 在某个状态下生成特定标记的概率 P(Yₜ \| Xₜ) |

---

> ZC:  核心思想
> - 状态与观测相分离
> - 状态与状态之间存在转移概率，转移概率分布
> - 每个状态都可以产生一组可以观测的符号，生成概率分布
> - 建模的目标是，通过一组符号反推状态路径

## 3 利用隐马尔科夫模型建立预测模型



