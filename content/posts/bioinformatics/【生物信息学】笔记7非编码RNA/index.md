---
title: 【生物信息学】笔记7非编码RNA
date: 2026-08-02T00:00:00+08:00
author: snoopy-zc
cover: cover.jpg
images:
- cover.jpg
categories:
- 生物信息学
- 学习笔记
---


本章主要介绍非编码RNA、长非编码RNA的鉴定等内容。

<!--more-->

## 1 非编码RNA

**非编码RNA** (non-coding RNA, ncRNA) 是指任何无需翻译成蛋白质即可发挥作用的RNA分子。

多种ncRNA共同调控细胞的生长发育凋亡等一系列重要的生理过程。

非编码RNA对应的基因组区域，常被称为非编码RNA基因或简称RNA基因。

参与基因表达调控

- microRNA (miRNA)
    - 通常长度为21-23（或者20-25）bp
    - 多种肿瘤的发生和发展中起着调控作用

- Xist (X inactive-specific transcript) 

- SCA8
    - 其突变与髓小脑共济失调症相关

Target：
- 基因组中有多少ncRNA？
- 这些ncRNA的功能是什么？

## 2 长非编码RNA的鉴定

数据挖掘方法，鉴定->视为分类

特征与特性有关就行，不用对应

非编码RNA的鉴定可以使用的特征：
- 已知的生物学特性，二级结构（如preRNA的发卡结构，对于长非编码RNA不适用）
- 序列本身的特征

筛选特征的方法
- 完全搜索（如，广度优先搜索，能找到最优解，但所需时间较多）
- 启发式搜索（如，前向搜索，可以适用较大的特征集合，可能陷入局部最优）
- 随机搜索（如，模拟退火算法，最终性能高度依赖于初始值及参数选择）

最终筛选出的六个特征
- (Conceptually) Translated Product
    - Coverage
    - ORF(open reading frame) Integrity
    - LOG-ODD score (the higher, the better the quality of the ORF)
- Homologous
    - num of BLASTX hits
    - Hit Score
    - Frame Score

CPC! (Coding Potential Calculator) 确保准确率的前提下未牺牲速度，运行速度是同样基于SVM算法的CUNC工具的10倍以上，正确的特征选择作用凸显。<http://cpc.cbi.pku.edu.cn>




## 参考文献

1. [【视频】生物信息学  7-1非编码RNA](https://www.bilibili.com/video/BV13t411G7oh/?p=32)
2. [【视频】生物信息学  7-2长非编码RNA的鉴定](https://www.bilibili.com/video/BV13t411G7oh/?p=33)




