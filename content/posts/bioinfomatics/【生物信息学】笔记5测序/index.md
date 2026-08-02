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


## 其他知识点

### BWA & BWT 压缩比对算法

- 无损压缩
- 使用轮转的方法对字符矩阵进行排序（按字母序）和变换，使其更容易被压缩
    - 例如，序列ACTG轮转后为[ACTG,CTGA,TGAC,GACT]，排序后为[ACTG,CTGA,GACT,TGAC]
    - 取出排序矩阵最后一列，GATC，原始序列ACTG对应排序后的序列第一行，故设I=1
- 使用反向字符的方法检验是否存在匹配的区域
- 不能处理gap

### 检出变异工具
    - samtools
        - mpileup + bcftools
    - GATK
        - UnifiedGenotyper
        - HaplotypeCaller

#### GATK测序流程
![https://gatk.broadinstitute.org/hc/theming_assets/01HZPKW2HXTR2JFMVD55S4VNTY](https://gatk.broadinstitute.org/hc/theming_assets/01HZPKW2HXTR2JFMVD55S4VNTY)


### 似然函数、贝叶斯方法

- 似然函数
    - 统计模型参数的函数
- 贝叶斯方法
    - 

统计模型在实际使用过程中并没有对错之分，只有依据对数据的拟合和刻画能力，以及看实际的结果和正确率
由于实际数据中有时存在不符合经典模型假设的情况，所以真实使用的模型常常会显得较为复杂，还可能涉及一些算法设计实现上的细节

### 相关工具的原始文献
 **Models for SNP Calling and Genotyping**

- **MAQ**
  - Li, H., Ruan, J., and Durbin, R. (2008). Mapping short DNA sequencing reads and calling variants using mapping quality scores. *Genome Research* 18, 1851–1858.

- **samtools**
  - Li, H. (2011). A statistical framework for SNP calling, mutation discovery, association mapping and population genetical parameter estimation from sequencing data. *Bioinformatics* 27, 2987–2993.

- **GATK**
  - McKenna, A., Hanna, M., Banks, E., Sivachenko, A., Cibulskis, K., Kernytsky, A., Garimella, K., Altshuler, D., Gabriel, S., Daly, M., et al. (2010). The Genome Analysis Toolkit: A MapReduce framework for analyzing next-generation DNA sequencing data. *Genome Research* 20, 1297–1303.
  - DePristo, M.A., Banks, E., Poplin, R., Garimella, K.V., Maguire, J.R., Hartl, C., Philippakis, A.A., del Angel, G., Rivas, M.A., Hanna, M., et al. (2011). A framework for variation discovery and genotyping using next-generation DNA sequencing data. *Nature Genetics* 43, 491–498.

- **SNVMix**
  - Goya, R., Sun, M.G.F., Morin, R.D., Leung, G., Ha, G., Wiegand, K.C., Senz, J., Crisan, A., Marra, M.A., Hirst, M., et al. (2010). SNVMix: predicting single nucleotide variants from next-generation sequencing of tumors. *Bioinformatics* 26, 730–736.


SNP 是 Single Nucleotide Polymorphism 的缩写，中文译为 单核苷酸多态性。指在基因组水平上，由单个核苷酸（A、T、C、G）的变异所引起的 DNA 序列多态性。简单来说，就是不同个体（或同一物种不同样本）在同一基因组位置上，某个碱基发生了替换（如 A→G）、缺失或插入。



