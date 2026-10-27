---
title: 【生信Agent】基础5单细胞数据库检索
date: 2026-10-27T00:08:00+08:00
author: snoopy-zc
cover: cover.jpg
math: true
images:
- cover.jpg
categories:
- 生信Agent
- 学习笔记
---

利用Agent开展单细胞数据检索、聚类、注释...

<!--more-->

## 1 单细胞简介

- bulk RNA-seq
    - 一列：一个样本
    - 组织内所有细胞的平均表达
    - 适合：总体差异、通路变化、队列研究
    - 局限：难以区分信号来自哪类细胞

- scRNA-seq
    - 一列：一个细胞
    - 同时保留sample/donor/condition
    - 适合：细胞组成、稀有细胞、细胞状态
    - 注意：细胞多≠生物学重复多

**单细胞基础分析流程**
1. 读取数据
2. 质量控制
3. 归一化
4. 高变基因
5. PCA（线性降维，捕获表达变化）
6. 样本整合
7. 聚类/UMAP
8. marker/注释

QC阈值、整合方法和注释标签都要经过人工检查

**最终应保留的核心结果**
1. 单细胞对象 \
    原始counts、QC后对象、完整metadata、软件版本与随机种子
2. 整合对照 \
    整合前后PCA/UMAP；按sample、group、cluster着色
3. marker证据
    每群maker表、DotPlot、FeaturePlot、ViolinPlot与Top maker热图
4. 注释审核表
    候选标签、支持/矛盾maker、参考支持、置信度、人工决定与最终标签


## 2 数据检索下载


```
#提示词

你是一名熟悉GEO数据库的单细胞生物信息学专家。
请联网检索适合进行 scRNA-seq 多样本整合、聚类和细胞注释的公开数据集，并逐条访问官方数据页面核实，不允许仅凭记忆给出编号。
我的研究方向是：【慢阻肺疾病和正常对照】；物种：【人】；组织：【肺组织】
要求：
1. 检索符合条件的GEO数据集，严禁编造数据集编号；
2. 至少包含 2 个样本；如用于病例与对照比较，优先每组不少于 3 个独立 donor
3. 必须能获得基因×细胞表达矩阵，优先 raw count matrix；说明是 10x mtx、h5、h5ad、RDS 还是其他格式
4. 输出候选数据表，包括：数据库、数据集编号、标题、官方链接、物种、组织、疾病/处理、样本数、donor 数、细胞数、平台、文件格式、raw counts、metadata、作者注释、下载方式、整合可行性、风险和推荐等级。
将检索结果保存为 `dataset_candidates.xlsx`，同时在报告中保留每条信息的来源链接和访问日期。
```

## 3 整合和聚类

**质控**
1. nFeature_RNA 检测到的基因数
2. nCount_RNA 总UMI/reads
3. percent.mt 线粒体基因比例
4. doublet 两个细胞混入同一液滴
5. ambient RNA 环境RNA污染 

要求agent：先报告建议阈值和预计删除比例->人工确认->再过滤

逐样本读取与QC -> 未整合PCA/UMAP -> 选择整合方法CCA/RPCA/Harmony -> 聚类/UMAP -> JoinLayers RNA assay marker

整合空间用于对齐、建图和聚类；maker解释回到可解释的RNA表达层

整合不足->相同细胞类型仍按batch分开
合理整合->同类细胞对齐，真实状态仍保留
过度整合->疾病或刺激信号被一并抹去

```
#提示词（一）

你是熟悉 Seurat、多样本 scRNA-seq 质量控制、整合和聚类的生物信息学助手。请优先依据 Seurat 官方文档，并检查当前可用的单细胞分析技能。
请读取 `sample_manifest.csv` 和 `raw_data` 中的数据，使用 R 和 Seurat 完成可复现分析。不要跳过检查，也不要用固定阈值直接过滤。
第一阶段要求：

1. 在results文件夹下创建SingleCell文件夹，单细胞全部结果放在该文件夹下
2. 核实每个文件的格式、基因 ID、细胞 barcode 和样本对应关系；检查基因名是否重复。
3. 为每个样本创建独立对象，写入 sample、donor、condition、batch、tissue 和 technology。
4. 计算 nFeature_RNA、nCount_RNA、percent.mt，并按样本输出 QC 小提琴图和散点图。
5. 评估 doublet 和环境 RNA 风险；如需额外工具，先说明方法和依赖。
6. 根据每个样本的指标分布提出过滤阈值，报告预计保留和删除的细胞数量及比例。
7. 到此暂停，不要执行过滤；先把 QC 建议保存到 `report/QC_review.md`，等待我确认。

###关键边界：先提出阈值，不要未经确认直接删除细胞
```

```
#提示词（二）

QC 阈值确认后继续：
1. 保留 raw counts，执行过滤，保存每个样本 QC 后对象。
2. 选择 LogNormalize 或 SCTransform，说明理由；设置随机种子并记录版本。
3. 先运行未整合 PCA / UMAP，按 sample、condition、cluster 着色。
4. 在 CCA、RPCA、Harmony 等方法中选择主方法，说明依据和过度校正风险。
5. 在整合低维空间运行邻居图、UMAP 和聚类；比较至少 3 个 resolution，报告 cluster 稳定性。
6. 输出整合前后 UMAP；报告各 cluster 的 sample、donor、condition 构成。
7. Seurat差异表达前按官方流程 JoinLayers；在 RNA assay 上寻找 marker。
8. 每群输出 marker 表及 DotPlot、FeaturePlot、Top marker 热图。
9. 保存对象、表格、PNG/PDF、R 脚本和中文报告；暂不命名细胞类型。

###关键边界：先完成无监督聚类与 marker 证据，暂不进行细胞注释
```

## 4 交互式注释

注释是证据整合的过程

```
#提示词（一）

你是熟悉【组织/疾病】单细胞注释的生物信息学助手。请基于marker表、证据图、样本构成和作者metadata进行主要细胞类型注释，不细分亚型，也不要修改最终标签。
要求：
1.综合多个经典marker判断，区分细胞类型；
2.每个cluster给出候选标签、支持及矛盾marker、参考注释、置信度和备选标签；
3.互斥谱系marker同时表达时标记为Doublet-like，证据不足时标记为Uncertain；
4.自动注释仅作为辅助证据；
5.生成results/annotation/annotation_review.csv和候选注释UMAP、marker证据图；
6.暂不执行RenameIdents，等待我确认。

原则：宁可保留宽泛的主要细胞类型，也不要过度细分。
```

```
#提示词（二）

按照XXX进行最终注释。
要求：
1. 保留原始 cluster 编号；新增 celltype，不得覆盖原列。
2. 未确认 cluster 保留 Uncertain，不自动补全。
3. 输出最终注释 UMAP：按 sample、group着色。
4. 输出各细胞类型在每个 sample和group的数量和比例，生成条形图；比例用于描述，不把细胞当作独立生物学重复进行显著性检验。
5. 保存最终 Seurat 对象、注释映射表、marker 图、PNG/PDF、R 脚本和中文报告。
6. 报告自动候选、人工修改、低置信度标签、未解决问题、软件版本和随机种子。。
```

## 总结
1. 检索核实（实际数据网页、donor、counts、metadata）
2. QC确认（按样本看分布、阈值先审核）
3. 整合检查（批次减少、生物学信号保留）
4. 候选注释（maker、反证、参考、置信度）
5. 人工确认（确认/修改/暂缓、全程留痕）

整合不是把所有样本混匀；注释不是给每个cluster强行取名字。\
Agent很强，但最终把关的人永远是你。

