---
title: 【生物信息学】笔记9本体论与分子通路
date: 2026-08-10T00:00:00+08:00
author: Chen Z
cover: cover.jpg
images:
- cover.jpg
categories:
- 生物信息学
- 学习笔记
---


本章主要介绍基因本体论、KEGG分子通路数据库、GO注释、分子通路鉴定、药物成瘾共同分子通路的鉴定等内容。

<!--more-->

## 1 本体论和基因本体论

本体论（ontology）
- 一个领域内的概念集，通过共享词汇来定义表示概念的类型和属性，以及它们之间的关系

e.g. \
WNT1 \
WNT-1 \
INT1 \
WINGLESS-TYPE MMTV INTEGRATION SITE FAMILY, MEMBER 1 \
wingless \
wg 

e.g. \
Saccharomyces cerevisiae: CDC2(now POL3) \
Drosophila melanogaster: DNApol-delta \
Mus musculus: Pold1 


For computer what is needed: **hierachical, common, controlled vocabulary !** 

The use of ontology:
- Communication
- Computation
- Discovery of Patterns

---
Open Biomedical Ontologies (OBO)
- Gene Ontology
- Anatomical Entity Ontology
- Disease Ontology
- Sequence Ontology
- System Biology Ontology

[Open Biological and Biomedical Ontology Foundry](http://www.obofoundry.org)

[Gene Ontology overview](https://geneontology.org/docs/ontology-documentation/)


```
OBO File Format:

[Term]
id
name
namespace
def
synonym
```

The relationship between items:
- is a
- part of
- regulates
- positively regulates
- negatively regulates


## 2 KEGG分子通路数据库

Main types of biological pathways :
- Metabolic pathways (原料采购员)
- Gene regulation pathways (生产管理员)
- Signal trasduction pathways (市场调研员)

Pathway databases :
- [KEGG PATHWAY](https://www.kegg.jp/kegg/)
- BioCarta
- BioCyc
- Protein ANalysis THrough Evolutionary Relationships(PANTHER)
- Pathway Interaction Database (PID)
- Reactome

## 3 GO（Gene Ontology）注释

Three types of GO annotations :
- Annotation through manually-reviewed experimental evidence
- Annotation through manually-reviewed computational analysis evidence
- Annotation by electronically-generated computational analysis evidence

[Guide to GO evidence codes](https://geneontology.org/docs/guide-go-evidence-codes/)


## 4 分子通路鉴定

实验里的一组基因，属于哪一个通路？最有意义的通路是哪一个？

两种研究方法（各有利弊，互为补充）
- ab？ initial prediction
- homology mapping

基因数很多、数据量很少的情况下，有效的方法：借助现有数据库

### 通路鉴定

三大类方法
- Over-Representation Analysis (ORA)
    - Tools: KOBAS, DAVID, PAGED
- Functional Class Scoring (FCS)
    - Tools: GSEA
- Pathway Topology (PT)
    - Tools: SPIA

这里主要介绍北京大学开发的KOBAS工具

两种方法：Mapping an inptu gene to pathway(s)
- ID mapping
    - Genbank GI
    - Entrez Gene ID
    - Ensembl Gene ID
    - UniprotKB AB
- Sequence similarity mapping
    - newly discovered genes
    - genes in a poorly annotated species
    - how ? BLAST !

```
Query Sequence 
+ KEGG GENES    
---NCBI BLAST---> BLAST Output 
---blask2ko---> BLAST hits

condition:
evalue < 10^-5
rank <= 5
```

Evaluation of Pathway Annotation by Sequence Similarity

$$
precision = \frac{TP}{TP + FP} 
\\
\
\\
coverage = \frac{TP}{N}
$$

### 通路富集

把实验中300个基因按以上方法贴上通路注释之后，有时候80%~90%注释率，有时候只有一半基因能注释到通路。then，哪些通路是重要的？

有可能结果全是噪音，如何分开通路噪音？
- 找最富集的通路

e.g.
```
N: the total number of genes
    - For example, the whole genome
    - Often called "background"
    - Only consider genes mapped to pathways
M: the number of genes in this pathway
n: the total number of query genes
    - Often called "foreground"
m: the number of query genes in this pathway
```

Null hypothesis: 零假设，没有生物学意义（随机发生，没有显著规律）

p值：在假设Null hypothesis为真的情况下，数据由随机因素产生的概率。

如果p值非常小（<0.01，有时是<0.05），那么你的观测不太可能是偶然发生的。则这个特定的通路很可能对实验具有特殊意义，推翻null hypothesis。

p值越小效果越好！（p<0.01 即假结果的概率小于1%）

当你从总共有N个基因的集合中随机抽取n个基因，其中i个基因属于某个特定通路（大小为M）的概率是多少？

- 这是一个超几何分布问题： $$\frac{ \binom{M}{i} \binom{N-M}{n-i} }{ \binom{N}{n} }$$

则p值计算公式为：
$$
\begin{align}
p &= \sum^{M}_{i=m} 
\frac{ \binom{M}{i} \binom{N-M}{n-i} }{ \binom{N}{n} }
\\
&=1 - \sum^{m-1}_{i=0} 
\frac{ \binom{M}{i} \binom{N-M}{n-i} }{ \binom{N}{n} }
\end{align}
$$

单次为0.01假阳性，若进行360次,则全都是假阳性的概率为1-(0.99)^360，结果可信度大幅下降，则需要：**多假设检验校正**

False discovery rate (FDR) = 1 - precision = FP / (TP + FP)

通路富集工具：[北京大学KOBAS 3.0](http://bioinfo.org/kobas/)

## 5 应用：药物成瘾共同分子通路的鉴定

Q:哪些基因和成瘾相关?
- 近30年文献，两个策略：遗传策略、分子生物学策略

从生物信息学角度，整合所有数据后，有1500个人类基因与成瘾性相关，其中396个有超过两条证据

最后，使用BOBAS找到18条显著通路

Q：对于不同物质成瘾，有没有共同的分子通路?
- 提取数据库中的metadata, 关联分析 \
- 发现5条通路对Cocaine、Alcohol、Opioids、Nicotine都显著    
    - Neuroactive ligand-receptor interaction
    - Long-term potentiation
    - GnRH signaling pathway
    - MAPK signaling pathway
    - Gap junctions
- 其中GnRH signaling pathway、Gap junctions从未被报道过


> 文献：Li CY, Mao X, Wei L, Genes and (Common) Pathways Underlying Drug Addiction, Plos Computational Biology, 2008, Jan 4;4(1):e2. 
(This work was featured by Science Signaling, the Economist, Reuters, and ~100 other scientific and public media.)

### 总结

为便于交流和计算
- 任何时候尽可能将数据存于数据库中
- 为这些数据定义ontology（本体）
- 同时收集这些的数据的metadata（元数据）

在一组基因或者基因产品里，为发现更高层次的模式
- 识别最重要的通路和功能分类
- 开展统计分析，例如KOBAS


## 参考文献

1. [【视频】生物信息学  9-1 本体论和基因本体论](https://www.bilibili.com/video/BV13t411G7oh/?p=49)
2. [【视频】生物信息学  9-2 KEGG分子通路数据库](https://www.bilibili.com/video/BV13t411G7oh/?p=50)
3. [【视频】生物信息学  9-3 GO注释](https://www.bilibili.com/video/BV13t411G7oh/?p=51)
4. [【视频】生物信息学  9-4 分子通路鉴定](https://www.bilibili.com/video/BV13t411G7oh/?p=52)
5. [【视频】生物信息学  9-5 应用：药物成瘾共同分子通路的鉴定](https://www.bilibili.com/video/BV13t411G7oh/?p=53)


