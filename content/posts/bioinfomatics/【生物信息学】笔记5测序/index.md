---
title: 【生物信息学】笔记5测序
date: 2026-07-28T00:00:00+08:00
author: Chen Z
cover: cover.jpg
images:
- cover.jpg
categories:
- 生物信息学
- 学习笔记
---


本章主要介绍新一代测序、序列回帖和变异鉴定等内容。


<!--more-->


## 1 新一代测序/深度测序技术

Next Generation Sequencing / Deep Sequencing（新一代测序/深度测序）

**Read**： A short DNA fragment
- DNA Sequence (symbols)
- Quality information 

> 常常将质量分数<20，即错误概率>0.01的碱基是不可靠的。
>
> 若这样的碱基超过整条read长度的20%，则考虑丢弃此条read


**Paired-end Reads**: 同时从两端进行测序，相应的read名称后加上“/1”和“/2”
- 如@test_fastq/1、@test_fastq/2


通过统计每个基因的reads数目可以估计基因的表达水平，进而进行差异表达分析

- RNA-seq
- ChIP-seq（Chromatin ImmunoPrecipitation Sequencing）

## 2 Reads Mapping

**Reads Mapping**：将reads定位到基因组上，两个优点
- reads is too short to be used/assembled de novo（克服reads较短的问题）
- Taking full usage of existing annotation/knowledge (以基因组位置作为桥梁，将测序得到的reads与前期研究成果进行有机的整合)

> Reads Mapping本质上是双序列比对问题
> 
> 但是，基因组很长，reads很短


> 在实际过程中，更多使用mapping quality而非序列比对分数来筛选真正的reads mapping的位置。

将reads正确map到基因组之后，就可以开始鉴定遗传变异
- 计数，一种朴素的方法












