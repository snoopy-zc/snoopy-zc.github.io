---
title: 【生物信息学】笔记11新基因鉴定及演化分析
date: 2026-08-16T00:00:00+08:00
author: snoopy-zc
cover: cover.jpg
images:
- cover.jpg
categories:
- 生物信息学
- 学习笔记
---


本章主要介绍新基因鉴定及演化分析，主要包括概念与实例、大脑演化的驱动力、一个与成瘾相关的人类特异的从头起源的新基因、从非编码RNA起源的从头起源新基因等内容。

<!--more-->


## 1 新基因鉴定及演化分析- 概念与实例
 
总结

1. A new gene is a gene that originated recently in a genome and can be identified by syntenic alignment of genomic sequences from a group of closely species. (新基因是指在基因组中近期起源的基因，可以通过对一组近缘物种的基因组序列进行共线性比对来鉴定。)

2. A number of molecular mechanisms can generate new genes and more than one mechanisms can be involved in making one new gene. (多种分子机制可以产生新基因，而且不止一种机制可能参与形成一个新基因。)

3. New genes can be biologically important as old or ancient genes. In fruitflies, essential functions can evolve rapidly any time in evolution. (新基因可以像古老基因一样具有重要的生物学意义。在果蝇中，必需功能可以在进化过程中的任何时候快速演化。)

## 2 新基因鉴定及演化分析- 大脑演化的驱动力

Q: 我们祖先的基因组发生了什么的遗传变异在驱动着物种进化？ \
e.g. the role of new genes in brain evolution

演化速度
- Average Rate = 20 genes / million years
- Primate Rate = 30 genes / million years
- Human Rate = 80 genes / million years

总结

1. Evolution of brain was accompanied with origin of new genes. (大脑的进化伴随着新基因的起源。)

2. New genes are upregulated in the neocortex, in particular the prefrontal cortex regions, throughout evolution of vertebrates. (在脊椎动物的整个进化过程中，新基因在新皮层中上调表达，特别是在前额叶皮层区域。)

3. Many new genes, in particular human-specific, new genes expressed in the prefrontal cortex and temporal lobe, the brain structure involved for cognitive functions. (许多新基因，特别是人类特异性的新基因，在前额叶皮层和颞叶中表达，这些脑结构参与认知功能。)

## 3 一个与成瘾相关的人类特异的从头起源的新基因

1. 现有编码区研究较多，花更多时间研究调控区的基因。

2. An SNP on the 3'UTR  of FLJ33706 is statistically significant in two GWAS of nicotine addiction and implicated in two linkage analyses. \
-> It is located in the middle of 12 binding sites of miRNA *let-7*.

3. FLJ33706 is a human-specific *de novo* protein-coding gene. （找不到现有记录和研究）

4. **TaqMan-based Real-Time PCR**: FLJ33706 mRNA is enriched in human brain regions. 

5. **Western blot** assay using an antibody designed against a 17-amino-acid peptide confirmed expression of FLJ33706 protein.
    - (A) The band was not detected in pre-immune serum or in the presence of excess synthetic antigenic peptides. \
    条带在未免疫血清（pre-immune serum）或过量合成抗原肽存在时未被检测到。

    - (B) The band was detected only after transformation of FLJ33706 recombination plasmids in *E. coli* (a) His-tag specific antibody and (b) anti-FLJ33706. \
    条带仅在FLJ33706重组质粒转化大肠杆菌（*E. coli*）后被检测到：(a) His标签特异性抗体和(b) anti-FLJ33706抗体。

    - (C) The band was detected in human cortex, midbrain, and cerebellum, but not in mouse. \
    条带在人大脑皮层（cortex）、中脑（midbrain）和小脑（cerebellum）中被检测到，但在小鼠中未检测到。

    - (D) FLJ33706 expression can be detected in the cortex of seven different human individuals. \
    FLJ33706的表达可在七个不同人类个体的大脑皮层中检测到。

6. **Immunohistochemistry studies** of human cortex slides showed enrichment in cytoplasm of neuronal cells.

7. 该基因编码区更有趣。 The DNA segment emerged in eutherian mammals.

8. Insertion of *Alu* elements generated splicing sites.
    - Human
    - Chimp
    - Orangutan
    - Rhesus
    - Marmoset
    - Tarsier
    - Mouse lemur
    - Bushbaby

9. Two changes in human escaped two stop codons.

10. 进而使用UCSC工具观察上游调控区
    - There are signals of enhancer and transcription factor binding sites in the 5kb upstream region
    - Promoter region is absent in chicken/zebrafish, emerged in mouse, and is similar in rhesus and chimpanzee

11. The Open Reading Frame is intact in Neadertal genome.

12. 该基因的一些有趣特征
    - 195个氨基酸
    - FLJ33706 has high PI (11.8).

13. 推断其功能
    - 同样PI比较高的蛋白有哪些？
    - GO enrichment of proteins with PI > 11 (FDR <= 0.05)，很多都和RNA有关
    - 功能提示：跟人的脑功能关联起来的完全从头起源、人特有的编码基因

14. 推断蛋白的三维结构
    - Predicted Secondary Structure include four helices & one beta strand 
    - 完全没有同源蛋白，只能从头预测三维机构，I-TASSER，(probably not reliable).

## 4 从非编码RNA起源的从头起源新基因

### How many other human-specific *de novo* genes are there?

设计了一个生物信息学的流程
Genome-wide identification of human- and human-chimpanzee- specific *de novo* genes. 
1. 首先DNA序列在演化上是什么时期产生的? \
Inferring the origination times of human gene loci.
2. 然后确认读码框在什么时候产生的? \
Inference of age of ORF(Open reading frames)
3. 人的基因产生有更严格的判断
    - 基因结构相对完整：完整的开放阅读框（ORF），在至少一种人类组织中的RNA-Seq RPKM值大于0.5；具有标准的起始密码子和终止密码子，且内含子长度不少于18个核苷酸。
    - 至少有一个肽段的支持：在PeptideAtlas或PRIDE数据库的质谱数据中，至少有一个独特的支持性肽段。
    - 其他物种里没有完整的读码框：BLASTP和Ensembl在其他物种中未发现同源蛋白，在人类中也未发现旁系同源蛋白（E值阈值设为10⁻⁶）。
    - 已有数据里近缘种不能有任一转录本：近缘种中不存在完整的ORF。（恒河猴中因剪接导致含终止密码子的外显子被切除的基因被排除。）
    - 多个近缘种有一个共同的失活突变。
4. 根据以上标准，得到鉴定结果
    - 11 encode proteins only in human
    - 7 encode proteins in both human and chimpanzee
    - 6 encode proteins in human, chimpanzee and orangutan
5. 分析这些基因的特征
    - 氨基酸序列都比较短，长度<400
    - 24个基因里，18个只有一个外显子，另外6个有多个外显子
    - Alu elements 重复序列贡献了8个基因的外显子和其中2个基因的剪切位点
    - 表达量比基因组整体水平更低
    - 19 of the 24 *de novo* genes showed evidence to co-opt the transcriptional context such as antisense and bi-directional promoters.

### Where did they originate from?

How did hominoid-specific *de novo* protein-coding genes originate from ancestral non-coding DNAs?


1. ORF-first or transcription-first?

    - origination of ORF -> transcription -> translation \
    vs \
    transcription of noncoding RNA -> acquisition of ORF -> translation

    - We integrated and analyzed RNA-Seq data from 19 tissues from human, chimpanzee, and rhesus macaque. \
    -> find out that: 20 out of the 24 hominoid-specific *de novo* protein coding genes exist as noncoding RNA in outgroup species. \
    -> So, transcription-first!

2. ORF fist or regulated transcription first?

    - transcription leakage/noise until ORF \
    vs \
    regulated transcriptional profile and structure of ncRNA

    - Non-coding genes tend to have similar gene structure with their protein-coding orthologs

    - Non-coding genes tend to have similar tissue expression profile as their protein-coding orthologs

    - Non-coding genes tend to have correlated, but lower, transcription level than their protein-coding orthologs

新基因在哪些组织表达得更多? \
*de novo* genes have enriched expression in brain and testis.

The PI values of the gene products are higher. 更多参与RNA功能。

总结

生物信息学方法在演化生物学研究中发挥了重要作用
- Identify interesting novel candidates at genome scale
- Discover genome-wide patterns
- Discover cross-species patterns

## 参考文献

1. [【视频】生物信息学  11-1 新基因鉴定及演化分析- 概念与实例](https://www.bilibili.com/video/BV13t411G7oh/?p=63)
2. [【视频】生物信息学  11-2 新基因鉴定及演化分析- 大脑演化的驱动力](https://www.bilibili.com/video/BV13t411G7oh/?p=64)
3. [【视频】生物信息学  11-3 一个与成瘾相关的人类特异的从头起源的新基因](https://www.bilibili.com/video/BV13t411G7oh/?p=65)
4. [【视频】生物信息学  11-4 从非编码RNA起源的从头起源新基因](https://www.bilibili.com/video/BV13t411G7oh/?p=66)

