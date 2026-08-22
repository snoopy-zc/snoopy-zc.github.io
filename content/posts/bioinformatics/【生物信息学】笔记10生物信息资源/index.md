---
title: 【生物信息学】笔记10生物信息资源
date: 2026-08-15T00:00:00+08:00
author: snoopy-zc
cover: cover.jpg
images:
- cover.jpg
categories:
- 生物信息学
- 学习笔记
---


本章主要介绍生物信息资源概览、美国国家生物信息中心(NCBI)、欧洲生物信息中心(EBI)、UCSC基因组浏览器、其他主要生物信息资源等内容。

<!--more-->

## 1 生物信息资源概览

Q: 生物信息数据库分为哪几级,每一级是如何让定义的,每一级各包含哪些数据库? \
A: 数据库分为两级
- 一级数据库: \
数据库中的数据直接来源于试验所获得原始数据,只经过简单的归类整理和注释。包括基因组数据库、核酸和蛋白质一级结构数据库、生物大分子(主要是蛋白质)三维空间结构数据库。
- 二级数据库: \
对原始生物分子数据进行整理、分类的结果,是在一级数据库、实验数据和理论分析的基础上针对特定的应用目标而建立的。

(1)国际信息中心(三大门户网站):
- NCBI National Center for Biotechnology Information (US)
    - 开发以GenBank为代表的数据库
- EBI European Bioinformatics Institute (EU)
    - 通过EMBL核酸数据库提供了序列搜索的服务
- SIB Swiss Institute of Bioinformatics (Switzerland, ExPASy)
    - 提供蛋白质专家分析系统: SWISS-PROT, ExPASy(Expert Protein Analysis System)。

(2)核酸数据库
- EMBL 欧洲分子生物学实验室
- GenBank 美国生物技术信息中心
- DDBJ 日本遗传研究所
    - 三个数据库中的数据基本一致,仅在数据格式上有所差别,对于特定的查询,三个数据库的响应结果一样。
    - 这三个数据库是综合性的DNA和RNA序列数据库,每条记录代表一个单独、连续、附有注释的DNA或RNA片段。

(3)蛋白质数据库
- PIR(Protein Information Resource)
- SWISS-PROT
- TrEMBL:
    - 是与SWISS-PROT相关的一个数据库。包含从EMBL核酸数据库中根据编码序列(CDS)翻译而得到的蛋白质序列,并且这些序列尚未集成到SWISS-PROT数据库中。
- UniProt:
    - 包括:Swiss-Prot、TrEMBL、PIR 。用户可以通过文本查询数据库,可以利用BLAST程序搜索数据库,也可以直接通过FTP 下载数据。
- NCBI——使用最多

(4)生物大分子数据库
- PDB (Protein Data Bank)
- MMDB (Molecular Modeling Database)



### **NCBI/EBI/UCSC Summary Table**

| | **NCBI** | **EBI** | **UCSC** |
|---|---|---|---|
| **Tools** | BLAST | BLAST<br>Exonerate<br>ClustalW2 | BLAT<br>In-Silico PCR |
| **Data Repository** | GenBank<br>GEO<br>SRA | ArrayExpress<br>ENA<br>PDBe | ENCODE |
| **DNA/Genome** | Genome | Ensembl | Ideogram<br>Recombination Rate<br>GC Content |


### **NCBI/EBI/UCSC Summary Table (Cont'd)**

| | **NCBI** | **EBI** | **UCSC** |
|---|---|---|---|
| **Expression** | UniGene | Expression Atlas | Affy Exon Array<br>Caltech RNA-seq<br>Allen Brain |
| **Regulation** | | | Transcription<br>TFBS<br>Epigenetics<br>DNasel HS |
| **Literature** | PubMed | | |
| **Ontology** | | Gene Ontology | |


### **Examples of individual Resources**

| **Analyses** | **Databases and tools** |
|---|---|
| **DNA/Genome** | |
| Gene prediction | GENSCAN, Glimmer |
| Genetic and Somatic Variations | COSMIC, SIFT, PolyPhen, SAPRED |
| **Expression regulation** | |
| Transcription factors & binding | TRANSFAC |
| RNA annotation | Rfam |
| microRNA annotation | miRBase |
| **Protein sequence and expression** | |
| Protein annotation | UniProt |
| Protein domain | PROSITE, STRING |
| Mass spectrometry | The Global Proteome Machine |
| **Macromolecule structure** | |
| Nucleotide structure | Mfold |
| Nucleotide interaction | RNAhybrid |
| Protein structure | PDB, Swiss Model |
| **Epigenetics** | |
| DNA methylation | MethylomeDB |
| **Pathway & network** | |
| Pathway | KOBAS, DAVID, KEGG, PANTHER, PID, BioCyc |
| **Evolution** | |
| Conservation | GERP++, PHYML |


### **Other examples of individual resources & utilities**

| **Purpose** | **Databases and tools** |
|---|---|
| **Model Organisms** | |
| Genome and gene annotations | Flybase, Wormbase, ZFIN, TAIR |
| **Large-scale studies** | |
| Cancer | TCGA, CGP |
| Epigenetics | Roadmap Epigenomics Project |
| Human population studies | GTEx |
| Brain | Allen Brain Atlas, Human Connectome project |
| **Tools to assist wet-lab experiments** | |
| Primer design | Primer3/Primer3Plus, Electronic PCR |
| **Software programming utilities** | |
| Standalone | EMBOSS |
| R package | Bioconductor |
| Perl package | BioPerl |
| Python package | BioPython |
| **Workflow** | |
| Workflow platform | Galaxy |
| Workflow construction | Taverna |


## 2 美国国家生物信息中心(NCBI)资源

<http://ncbi.nlm.nih.gov>

## 3 欧洲生物信息中心(EBI)资源

<https://www.ebi.ac.uk/>

<https://www.ensembl.org/>

<https://www.uniprot.org/>

<https://www.ebi.ac.uk/intact>

<http://www.clustal.org/omega>

<https://www.ebi.ac.uk/interpro/>

## 4 UCSC基因组浏览器

<https://genome.ucsc.edu/>

<https://genome.ucsc.edu/cgi-bin/hgTracks>

BLAT
- BLAT on DNA is designed to quickly find sequences of 95% and greater similarity of length 25 bases or more. It may miss more divergent or shorter sequence alignments. It will find perfect sequence matches of 20 bases. BLAT on proteins finds sequences of 80% and greater similarity of length 20 amino acids or more. In practice DNA BLAT works well on primates, and protein BLAT on land vertebrates. 

In-Silico PCR
- In-Silico PCR V39x1 searches a sequence database with a pair of PCR primers, using the BLAT index for fast performance. See an example video on our YouTube channel.


## 5 其他主要生物信息资源

- PDB 
    - <http://www.rcsb.org>

- GERP++
    - <http://mendel.stanford.edu/SidowLab/downloads/gerp>
    - <https://github.com/tvkent/GERPplusplus>

- CNVnator
    - <http://sv.gersteinlab.org>

- rfam
    - <http://rfam.sanger.ac.uk>

- Bioconductor
    - R程序包，使用前先看内容并验证，不要被人家上传的错误代码误导了
    - <http://bioconductor.org/>

- BioPerl
    - Perl程序包
    - <http://bioperl.org>

- BioPython
    - Python程序包
    - <http://biopython.org>

## 参考文献

1. [【视频】生物信息学  10-1 生物信息资源概览](https://www.bilibili.com/video/BV13t411G7oh/?p=57)
2. [【视频】生物信息学  10-2 美国国家生物信息中心(NCBI)资源](https://www.bilibili.com/video/BV13t411G7oh/?p=58)
3. [【视频】生物信息学  10-3 欧洲生物信息中心(EBI)资源](https://www.bilibili.com/video/BV13t411G7oh/?p=59)
4. [【视频】生物信息学  10-4 UCSC基因组浏览器](https://www.bilibili.com/video/BV13t411G7oh/?p=60)
5. [【视频】生物信息学  10-5 其他主要生物信息资源](https://www.bilibili.com/video/BV13t411G7oh/?p=61)


