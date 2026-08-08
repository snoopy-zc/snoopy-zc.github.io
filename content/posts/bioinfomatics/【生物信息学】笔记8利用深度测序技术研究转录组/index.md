---
title: 【生物信息学】笔记8利用深度测序技术研究转录组
date: 2026-08-04T00:00:00+08:00
author: Chen Z
cover: cover.jpg
images:
- cover.jpg
categories:
- 生物信息学
- 学习笔记
---


本章主要介绍转录组、RNA测序数据回贴与组装、RNA-seq 数据分析、转录组数据挖掘、差异表达与聚类分析等内容。

深度测序技术(NGS, next generation sequencing) 即第二代测序技术

<!--more-->

## 1 转录组介绍

转录组
- mRNA (message RNA)
- miRNA (micro RNA)
- lncRNA (long non-coding RNA)

研究内容
- 定性：鉴定出所有表达的转录
- 定量：确定这些转录各自的表达量

研究技术
- Real-Time qRT-PCR
    - 基于互补杂交反应，广泛公认为“金标准”
    - 缺点：吞吐量低；需要事先知道转录本序列，难以用来发现未知的转录
- Microarray（微阵列、基因芯片）
    - 用于基于互补杂交反应的基因表达分析
    - 标记靶标：来自生物样本的RNA
    - 探针：大量有序的固定核苷酸分子，具有已知序列
    - 缺点：需要事先知道转录本序列
- Expressed Sequence Tag (EST)
    - 随机对cDNA文库中的单个克隆体进行测序
        - 短“标签”：60~500bp
        - 一次性测序：易出错（~1%）
    - 优点：无需预先知道转录本序列（不仅能测量，还能发现新转录）
    - 通量限制，只能得到几千个转录序列（1991）
- RNA-Seq
    - Sample RNA --(逆转录+PCR)-->Amplified cDNA--(打碎)-->cDNA fragments--(测序仪)-->reads
    - 可以同时对转录组定性定量研究
    - 本质上是对转录本序列的随机采样，因此检测效果和灵敏度高度依赖于检测的深度
    - \# of mapped reads ∝ 表达量
    - \# of mapped reads ∝ 转录长度
    - \# of mapped reads ∝ 测序深度

通常将原始reads数目进行归一化处理，其中一种方法：RPKM（the \# of mapped **R**eads **p**er **K**B per **m**illion reads.）

$$
RPKM=10^9 \frac{C}{NL}
$$

- C: the \# of mapped reads for specified transcript.
- N: the \# of total mapped reads.
- L: the length of the specified transcript.

Tips：分析前搞清楚，如何分链的！使用不同的方法reads方向不同

--- 
### PCR

**PCR** 是 **Polymerase Chain Reaction** 的缩写，中文译为 **聚合酶链式反应**。
一种在体外快速扩增特定 DNA 片段的分子生物学技术。通过温度循环，利用 DNA 聚合酶将微量的目标 DNA 指数级扩增到可检测的量。

#### 基本原理（三步循环）

| 步骤 | 温度 | 作用 |
|------|------|------|
| **变性（Denaturation）** | ~94–98°C | 双链 DNA 解开为单链 |
| **退火（Annealing）** | ~50–65°C | 引物与单链 DNA 的互补序列结合 |
| **延伸（Extension）** | ~72°C | DNA 聚合酶沿模板合成新链 |

每完成一轮循环，DNA 量理论上翻倍，经过 **25–35 个循环**后可扩增数百万倍。

#### 关键组分
- **模板 DNA**：含目标序列的 DNA 样本
- **引物（Primers）**：与目标序列两端互补的短单链 DNA，决定扩增特异性
- **DNA 聚合酶**：常用 *Taq* 酶（耐高温）
- **dNTPs**：四种脱氧核苷酸（A、T、C、G）
- **缓冲液**：提供适宜的 pH 和离子环境（如 Mg²⁺）

#### 主要应用
- **基因克隆**：获取大量目的 DNA 片段
- **基因检测**：诊断遗传病、病原体感染（如新冠核酸检测）
- **法医鉴定**：DNA 指纹分析
- **突变分析**：检测基因突变或多态性
- **测序准备**：为测序反应提供足够模板

#### 常见衍生技术
- **RT-PCR**：以 RNA 为模板，先逆转录为 cDNA，再进行 PCR
- **qPCR / RT-qPCR**：实时定量 PCR，可定量检测 DNA/RNA 的初始拷贝数
- **巢式 PCR、 touchdown PCR**：提高特异性或灵敏度的改良方法

## 2 RNA测序数据回贴与组装


### mapping
junction reads: 跨过剪切位点的reads

- "Join exon" 无法应对未知的exon和未知的基因
- "Split reads" 策略

### assembly 
- 将转录的组装问题描述为对一个有向图的便利问题
- Cufflinks工具


## 3 RNA-seq 数据分析


## 4 转录组数据挖掘


## 5 差异表达与聚类分析



## 参考文献

1. [【视频】生物信息学  8-1 转录组介绍](https://www.bilibili.com/video/BV13t411G7oh/?p=35)
2. [【视频】生物信息学  8-2 RNA测序数据回贴与组装](https://www.bilibili.com/video/BV13t411G7oh/?p=36)
3. [【视频】生物信息学  8-3 RNA-seq 数据分析](https://www.bilibili.com/video/BV13t411G7oh/?p=37)
4. [【视频】生物信息学  8-4 转录组数据挖掘](https://www.bilibili.com/video/BV13t411G7oh/?p=38)
5. [【视频】生物信息学  8-5 差异表达与聚类分析](https://www.bilibili.com/video/BV13t411G7oh/?p=39)
