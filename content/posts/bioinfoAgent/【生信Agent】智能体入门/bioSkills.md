以下是该 README 文件的完整中文翻译：

---

# 本仓库已归档。其结构仍然有效，但我们鼓励分叉和自定义，以将您自己的专业知识编码到技能中。我们将不再进行更新或代码修复。

# bioSkills

一套指导 AI 编程代理（Claude Code、OpenAI Codex、Google Gemini、OpenCode、OpenClaw）完成常见生物信息学任务的技能集合。

## 项目目标

本仓库为 AI 代理提供生物信息学工作流的专家知识。每个技能包含代码模式、最佳实践和示例，帮助代理为常见任务生成正确、地道的代码。

目标用户范围从学习计算生物学的本科生到处理大规模数据的博士研究人员。技能涵盖从基础序列操作到单细胞 RNA 测序和群体遗传学等高级分析的完整谱系。

## 性能

评估摘要报告可在 [bioskills_eval_20260328.pdf](resources/bioskills_eval_20260328.pdf) 查看。评估基于 [Bio-Task Bench](https://github.com/GPTomics/bioTaskBench) 数据集执行。

![benchmark_performance_20260328](resources/benchmark_performance_20260328.png)

## 需求

### Python
- Python 3.9+
- biopython, pysam, cyvcf2, pybedtools, pyBigWig, scikit-allel, anndata

```bash
pip install biopython pysam cyvcf2 pybedtools pyBigWig scikit-allel anndata mygene
```

### R/Bioconductor
差异表达、单细胞、通路分析和甲基化技能需要。

```r
if (!require('BiocManager', quietly = TRUE))
    install.packages('BiocManager')
BiocManager::install(c('DESeq2', 'edgeR', 'Seurat', 'clusterProfiler', 'methylKit'))
```

### CLI 工具
```bash
# macOS
brew install samtools bcftools blast minimap2 bedtools

# Ubuntu/Debian
sudo apt install samtools bcftools ncbi-blast+ minimap2 bedtools

# conda
conda install -c bioconda samtools bcftools blast minimap2 bedtools \
    fastp kraken2 metaphlan sra-tools bwa-mem2 bowtie2 star hisat2 \
    manta delly cnvkit macs3 macs2 genrich tobias rgt-hint idr picard \
    preseq deeptools chromap subread fithichip gatk4
```

## 安装

### Claude Code

```bash
git clone git@github.com:GPTomics/bioSkills.git
cd bioSkills
./install-claude.sh                              # 全局安装
./install-claude.sh --project /path/to/project   # 或安装到特定项目
./install-claude.sh --categories "single-cell,variant-calling"  # 安装特定类别
./install-claude.sh --list                       # 列出可用技能
./install-claude.sh --validate                   # 验证所有技能
./install-claude.sh --update                     # 仅更新已更改的技能
./install-claude.sh --uninstall                  # 移除所有 bio-* 技能
```

### Codex CLI

```bash
./install-codex.sh                               # 全局安装
./install-codex.sh --project /path/to/project    # 或安装到特定项目
./install-codex.sh --categories "single-cell,variant-calling"  # 安装特定类别
./install-codex.sh --list                        # 列出可用技能
./install-codex.sh --validate                    # 验证所有技能
./install-codex.sh --update                      # 仅更新已更改的技能
./install-codex.sh --uninstall                   # 移除所有 bio-* 技能
```

### Antigravity CLI

Antigravity CLI 替代 Gemini CLI（已于 2026-06-18 停用），使用开放的 Agent Skills 标准。全局安装位于 `~/.gemini/antigravity/skills/`；项目安装位于 `.agents/skills/`。

```bash
./install-antigravity.sh                              # 全局安装
./install-antigravity.sh --project /path/to/project   # 或安装到特定项目
./install-antigravity.sh --categories "single-cell,variant-calling"  # 安装特定类别
./install-antigravity.sh --list                       # 列出可用技能
./install-antigravity.sh --validate                   # 验证所有技能
./install-antigravity.sh --update                     # 仅更新已更改的技能
./install-antigravity.sh --uninstall                  # 移除所有 bio-* 技能
```

### OpenCode

```bash
./install-opencode.sh                            # 全局安装到 ~/.config/opencode/skills/
./install-opencode.sh --project /path/to/project # 或安装到特定项目
./install-opencode.sh --categories "single-cell,variant-calling"  # 安装特定类别
./install-opencode.sh --list                     # 列出可用技能
./install-opencode.sh --validate                 # 验证所有技能
./install-opencode.sh --update                   # 仅更新已更改的技能
./install-opencode.sh --uninstall                # 移除所有 bio-* 技能
```

OpenCode 还会自动从 `~/.claude/skills/` 和 `~/.agents/skills/` 发现 Agent Skills，因此 `install-claude.sh` 或 `install-codex.sh` 产生的安装无需重新运行即可在 OpenCode 中工作。

### OpenClaw

直接从 [ClawHub](https://clawhub.ai/djemec/bioskills) 安装，或使用安装脚本：

```bash
./install-openclaw.sh                            # 全局安装所有技能
./install-openclaw.sh --categories "single-cell,variant-calling"  # 安装特定类别
./install-openclaw.sh --project /path/to/workspace  # 安装到工作区
./install-openclaw.sh --tool-type-metadata       # 添加 OpenClaw 依赖元数据
./install-openclaw.sh --dry-run                  # 预览安装 + Token 估算
./install-openclaw.sh --list                     # 列出可用技能
./install-openclaw.sh --validate                 # 验证所有技能
./install-openclaw.sh --update                   # 仅更新已更改的技能
./install-openclaw.sh --uninstall                # 移除所有 bio-* 技能
```

所有安装程序都支持 `--categories` 进行选择性安装，以及 `--dry-run` 进行预览。Codex、Gemini 和 OpenCode 转换为 Agent Skills 标准（`examples/` -> `scripts/`，`usage-guide.md` -> `references/`）。OpenClaw 保留原始目录结构，并可选择通过 `--tool-type-metadata` 添加依赖元数据。

## 技能分类

| 分类 | 技能数 | 主要工具 | 描述 |
|----------|--------|---------------|-------------|
| **sequence-io** | 9 | Bio.SeqIO | 读取、写入、转换 FASTA/FASTQ/GenBank 及 40+ 种格式 |
| **sequence-manipulation** | 7 | Bio.Seq, Bio.SeqUtils | 转录、翻译、基序搜索、序列属性 |
| **database-access** | 15 | Bio.Entrez, BLAST+, SRA toolkit, UniProt API, STRINGdb | NCBI/UniProt 查询、SRA 下载、BLAST、同源性搜索、互作数据库 |
| **alignment-files** | 10 | samtools, pysam | SAM/BAM/CRAM 查看、排序、过滤、统计、验证、扩增子剪切 |
| **variant-calling** | 13 | bcftools, GATK, DeepVariant, Manta, Delly, VEP | 胚系/SV  calling、DRAGEN-GATK 模式、VQSR/硬过滤、MANE 注释、ACMG 解读 |
| **alignment** | 7 | Bio.Align, MAFFT, MUSCLE5, Foldseek, ClipKIT | MSA 工具（包括 BAli-Phy 联合 MSA+树共估计）、成对比对、结构比对（Foldseek/Foldseek-Multimer/TM-align/US-align/DALI/Foldmason）、MSA 后修剪（ClipKIT/trimAl/BMGE/PhyIN）、比对 I/O、MSA 统计 |
| **phylogenetics** | 8 | Bio.Phylo, IQ-TREE2, RAxML-NG, MrBayes, BEAST2, ASTRAL-III | 树 I/O、最大似然/贝叶斯推断（支持度而非准确度）、分歧年代测定、溯祖物种树、一致因子 |
| **differential-expression** | 6 | DESeq2, edgeR, ggplot2, pheatmap | RNA-seq 差异表达、可视化、批次校正 |
| **structural-biology** | 10 | Bio.PDB, ESMFold, AlphaFold DB, PDBFixer, fpocket | PDB/mmCIF 解析、SMCRA 导航、几何、界面分析、结构验证、制备（加氢/质子化）、结合位点检测、ML 结构预测 |
| **single-cell** | 17 | Seurat, Scanpy, Pertpy, Cassiopeia, MeboCost | scRNA-seq 质控、聚类、轨迹、通讯、注释、扰动测序、谱系追踪、代谢物通讯、差异丰度、CNV 推断、哈希解复用 |
| **pathway-analysis** | 6 | clusterProfiler, ReactomePA, rWikiPathways, enrichplot, SPIA | 决策级功能富集：ORA、GSEA 和 SPIA 通路拓扑，涵盖 GO/KEGG/Reactome/WikiPathways/MSigDB、背景 universe 选择、排序指标选择、实时数据库可重复性、冗余折叠可视化 |
| **restriction-analysis** | 5 | Bio.Restriction | 限制位点、图谱、酶选择、片段/凝胶分析、Golden Gate（IIS 型）组装 |
| **methylation-analysis** | 10 | Bismark, methylKit, dmrseq, sesame, minfi, EpiDISH, methylclock, meffil | 亚硫酸氢盐 + Infinium 芯片 DNA 甲基化：比对、calling、单 CpG 检验、DMR、芯片预处理/质控、细胞类型反卷积、表观遗传时钟、EWAS 设计 |
| **chip-seq** | 12 | MACS3, ChIPseeker, DiffBind | 峰 calling、注释、差异结合、基序、质控、超级增强子 |
| **metagenomics** | 8 | Kraken2, MetaPhlAn, Bracken, HUMAnN, AMRFinderPlus, inStrain, decontam | 基于读段的分类/功能分析、丰度、耐药组、菌株追踪、污染控制 |
| **long-read-sequencing** | 9 | Dorado, minimap2, Clair3, modkit, IsoSeq3 | 碱基识别、比对、抛光、变异 calling、SV calling、甲基化、Iso-Seq |
| **read-qc** | 7 | FastQC, MultiQC, fastp, Cutadapt, FastQ Screen, umi_tools, RSeQC | 质量报告、接头/质量修剪、污染筛查、UMI 处理、RNA-seq 质控 |
| **genome-intervals** | 8 | bedtools, pybedtools, pyranges, gffutils, deepTools, pyBigWig | 坐标系统、区间运算、重叠显著性、GTF/GFF、邻近性、覆盖度、bedGraph/bigWig 轨道 |
| **population-genetics** | 7 | PLINK 1.9/2.0, BOLT-LMM, SAIGE, regenie, ADMIXTURE, scikit-allel | 等位基因感知质控、LD 修剪/聚类、PCA/混合（使用 ratio-of-averages FST）、单变异 GWAS 和混合模型（PC vs LMM、SPA/Firth、LOCO）、罕见变异基于基因的检验（burden/SKAT/SKAT-O/ACAT/STAAR）、考虑人口结构的选择扫描 |
| **rna-quantification** | 4 | featureCounts, Salmon, kallisto, tximport | 基因/转录本定量、计数矩阵质控 |
| **read-alignment** | 4 | bwa-mem2, bowtie2, STAR, HISAT2 | 决策级短读段比对，用于 DNA 和 RNA-seq：读段组、ALT/诱饵分析集、双通和链特异性、各工具 MAPQ、以及读段组/去重约定 |
| **expression-matrix** | 5 | pandas, anndata, DESeq2, edgeR, biomaRt | 计数矩阵处理、标准化、基因 ID 映射 |
| **copy-number** | 11 | CNVkit, GATK4, ASCAT, Sequenza, FACETS, PURPLE, PureCN, DNAcopy, GISTIC2, scarHRD, AmpliconArchitect, Battenberg, TITAN, AnnotSV, ClassifyCNV | 读深度 CNV calling（CNVkit/GATK）、CBS/HMM 分割和深度偏差校正、考虑纯度/倍性的等位基因特异性拷贝数、复发性和驱动 CNV（GISTIC2）和拷贝数特征、基因/临床注释、ACMG/ClinGen 胚系 CNV 解读、HRD 基因组瘢痕评分、局灶扩增和 ecDNA 结构、亚克隆 CN 和全基因组倍增、CNV 可视化 |
| **phasing-imputation** | 4 | Beagle, SHAPEIT5, Minimac4, IMPUTE5, GLIMPSE2, bcftools | 参考面板选择和链/构建协调、统计单倍型定相、基因型推断（芯片和低覆盖度 WGS）为剂量形式、以及 MAF 分层推断质控 |
| **atac-seq** | 12 | MACS3, DiffBind, csaw, chromVAR, TOBIAS, scprinter, ArchR, Signac, SnapATAC2, Cicero, ABC, chromBPNet, BPNet, scBasset, Enformer, WASP, GATK ASEReadCounter, RASQUAL | 峰 calling（MACS/Genrich/HMMRATAC）、ENCODE 4 质控（含 spike-in/性染色体）、固定宽度共识峰集、差异可及性（置换/spike-in/Hi-C 锚定）、TF 足迹（偏差校正包括 chromBPNet）、基序变异性（chromVAR/scBasset）、核小体定位（NucleoATAC/V-plot/H2A.Z）、单细胞 ATAC（Signac/ArchR/SnapATAC2/scArches）、顺式调控共可及性（Cicero/SCENIC+）、深度学习（chromBPNet/BPNet/scBasset/Enformer；计算机变异效应；TF-MoDISco 基序发现）、增强子-基因关联（ABC、ENCODE-rE2G、HiChIP、CRISPRi-FlowFISH 验证）、等位基因特异性可及性（WASP、GATK、RASQUAL caQTL） |
| **genome-assembly** | 9 | GenomeScope2, SPAdes, Flye, hifiasm, metaFlye, Pilon, YaHS, CheckM2, FCS-GX, QUAST, BUSCO, Merqury | 组装前 k-mer 分析、短读/长读/HiFi 和宏基因组组装、抛光、Hi-C 支架、污染检测、三轴质量评估 |
| **primer-design** | 4 | primer3-py | PCR/qPCR 引物设计、探针协同设计、热力学验证、基因组特异性（计算机 PCR） |
| **spatial-transcriptomics** | 12 | Squidpy, SpatialData, cell2location, scimap | Visium/Xenium I/O、分割、反卷积、高分辨率分箱、区域、空间统计、通讯、多组学、蛋白质组学 |
| **hi-c-analysis** | 9 | cooler, cooltools, pairtools, HiCExplorer, chromosight, FitHiChIP | 读对处理和文库质控、cooler 矩阵、ICE/KR 平衡和 P(s) 预期、A/B 区室、TAD、环、可视化、差异比较、蛋白质导向 3C（HiChIP/PLAC-seq/Capture Hi-C） |
| **alternative-splicing** | 9 | rMATS-turbo, leafcutter, MAJIQ, SpliceAI, FRASER 2.0, FLAIR, IsoformSwitchAnalyzeR | 定量、差异剪接、异构体转换/DTU、sashimi 可视化、剪接质控、单细胞剪接、剪接变异预测（SpliceAI）、异常值检测（FRASER2/DROP）、长读剪接 |
| **chemoinformatics** | 20 | RDKit, GNINA, ADMETlab 3.0, DiffDock-L, Boltz-2, REINVENT 4, AiZynthFinder, chemprop, OpenFE | 分子 I/O 和策略感知标准化；构象和描述符；相似性、形状、药效团和骨架分析；反应枚举和逆合成；QSAR、生成设计和 ADMET；经典和 ML 对接及姿态验证；自由能、共价抑制剂和 PROTAC 工作流 |
| **liquid-biopsy** | 7 | ichorCNA, fgbio, VarDict, FinaleToolkit, MethylDackel | cfDNA 预处理（UMI/双链）、分析验证/检测限、ctDNA 突变 + CHIP、片段组学、肿瘤分数、甲基化检测 + 组织来源、纵向监测/MRD |
| **workflows** | 41 | 多种（工作流特定） | 端到端流程：RNA-seq、变异、ChIP-seq、scRNA-seq、空间、Hi-C、蛋白质组学、微生物组、CRISPR、代谢组学、多组学、免疫治疗、疫情、代谢建模、剪接、液体活检、基因组注释、GRN、因果基因组学、时间序列、eDNA、临床试验 |
| **proteomics** | 9 | pyOpenMS, DIA-NN, limma, DEqMS, MSstats | 质谱数据导入、肽段鉴定、蛋白质推断、定量、质控、差异丰度、PTM、DIA、谱图库 |
| **microbiome** | 6 | DADA2, phyloseq, ALDEx2, QIIME2 | 16S/ITS 扩增子：ASV 推断、分类学、多样性、成分差异丰度、PICRUSt2 功能预测、QIIME2 溯源 |
| **multi-omics-integration** | 5 | MOFA2, mixOmics, SNFtool | 整合设计、跨组学协调、因子分析、监督特征、网络融合 |
| **crispr-screens** | 15 | MAGeCK, BAGEL2, drugZ, JACKS, Chronos, CRISPRcleanR, CRISPResso2, Pertpy, PRIDICT2 | 文库设计和六阶段质控、方法匹配的命中 calling、拷贝数和批次校正、组合旁系同源筛选、单细胞 Perturb-seq、碱基/先导编辑、体内筛选 |
| **metabolomics** | 9 | XCMS, MS-DIAL, matchms, SIRIUS, ropls, lipidr, IsoCor | 决策级 LC-MS/GC-MS：特征检测、置信度级别注释（MSI/Schymanski）、质控/漂移/标准化、置换验证多变量统计、mummichog/ORA 通路映射、脂质组学结构分辨率诚实性、MRM/ICH-M10 靶向定量、13C/15N 同位素示踪 |
| **imaging-mass-cytometry** | 7 | steinbock, CATALYST, deepcell, squidpy, napari, diffcyt | IMC 预处理、NNLS 溢出补偿、分割、表型分析、空间分析、患者水平差异分析、注释、质控 |
| **flow-cytometry** | 8 | flowCore, CATALYST, CytoML | FCS 处理、补偿、门控、聚类、差异分析、质控 |
| **reporting** | 6 | RMarkdown, Quarto, Jupyter, MultiQC, matplotlib | 可重复报告、质控聚合、发表级图表 |
| **experimental-design** | 5 | designit, RNASeqPower, ssizeRNA, qvalue, sva | 随机化/区组、假重复、功效分析、样本量、多重检验（FDR）、批次设计 |
| **workflow-management** | 5 | Snakemake, Nextflow, nf-core, cwltool, Cromwell/miniwdl | 可重复流程引擎：编写、运行 nf-core、溯源、可恢复缓存 |
| **data-visualization** | 20 | ggplot2, matplotlib, plotly, ComplexHeatmap, patchwork, scico (Crameri), Okabe-Ito, EnhancedVolcano, apeglm/ashr, qqman, locuszoomr, metafor, ggalluvial, ComplexUpset, ggseqlogo, maftools, NetworkX, pyGenomeTracks | 博士级图表：感知有效性（Cleveland-McGill 1984）、Crameri/cividis 色觉缺陷安全调色板（Wong 2011, Crameri 2020）、ward.D2 + 最优叶排序（Murtagh-Legendre 2014, Bar-Joseph 2001）、apeglm LFC 收缩（Zhu 2019）、Manhattan/QQ 图（含 lambdaGC + LDSC（Bulik-Sullivan 2015））、oncoprint + lollipop + 序列 logo 用于队列基因组学、raincloud（Allen 2019）+ Weissgerber 2015 条形图批评、森林/漏斗图（含 REML 和等高线增强偏倚（Egger 1997））、CONSORT 2010 + 冲积流、UMAP/t-SNE（含 Kobak-Berens 2019 初始化 + Chari-Pachter 2023 注意事项）、ChIP-Rx spike-in 通过 --scaleFactor（而非 --normalizeUsing）、Kaleido v1 静态导出、Type-42 字体嵌入 |
| **tcr-bcr-analysis** | 6 | MiXCR, VDJtools, immunarch, Immcantation（alakazam/shazam/scoper/dowser/tigger）, scirpy, tcrdist3, OLGA | 预设/化学匹配的 V(D)J 组装（含 UMI/单细胞处理及 4.x 许可证门槛）；深度标准化多样性（Hill 谱 q=0/1/2，比较前降采样）和重叠（Morisita-Horn/F2 深度稳健 vs Jaccard 不是）；BCR 克隆聚类使用数据衍生的 distToNearest->findThreshold 切割（非硬编码 0.15），CreateGermlines 在 SHM 之前，BASELINe 选择，Dowser/IgPhyML 谱系；单细胞克隆型定义（TCR 用一致性 vs BCR 用 normalized_hamming 聚类），awkward-array AIRR 链配对质控及多链过滤扩增偏倚权衡；抗原特异性作为假设而非标签，VDJdb/GLIPH2/tcrdist3 聚类由 OLGA Pgen 零值门控 |
| **small-rna-seq** | 6 | cutadapt, miRDeep2, miRge3, DESeq2, miRanda, MINTmap | miRNA/isomiR/tRF/piRNA 分析、连接偏倚感知预处理、发现、成分感知差异表达、靶点预测 |
| **ribo-seq** | 6 | riboWaltz, RiboCode, Ribo-TISH, riborex | 核糖体分析、周期性质控、ORF 检测、翻译效率、起始位点定位 |
| **epitranscriptomics** | 5 | STAR, HISAT2, deepTools, PreSeq, exomePeak2, MeTPeak, MACS3, QNB, RADAR, m6Anet, xPore, Nanocompore, ELIGOS, Dorado, nanopolish, minimap2, Guitar, ChIPseeker, ComplexHeatmap, ggcoverage, pyGenomeTracks, ggseqlogo, HOMER | MeRIP-seq 预处理（明确约定非 UMI MeRIP 不去重，PreSeq 饱和曲线用于跨库比较）；m6A 峰 calling（exomePeak2 转录本感知 GC 校正 GLM、MeTPeak HMM、MACS3 宽峰），DRACH 基序作为合理性检查（而非过滤）；差异 m6A 通过 exomePeak2 的四 BAM 向量接口、QNB beta-二项式（小 N）、RADAR 的 countReads -> normalizeLibrary -> adjustExprLevel -> filterBins -> diffIP -> reportResult 工作流，含化学计量 vs 表达 vs IP 效率混杂处理及 McIntyre 2020 可重复性下限效应量护栏；ONT 直接 RNA m6A calling（m6Anet 仅 DRACH 含 `mod_ratio` 化学计量列、xPore Bayesian diffmod、Nanocompore 比较 GMM、Dorado 原生 RNA004 含模型版本固定），nanopolish eventalign --scale-events --signal-index 必需对、cDNA vs DRS 化学区分；Guitar 转录本特征元基因（以终止密码子富集作为生物学质控锚点（Dominissini 2012 / Meyer 2012））、pyGenomeTracks 可重复浏览器图、DRACH 序列 logo；m6A vs m6Am 5'UTR 峰交叉反应（PCIF1 / CAPAM 帽 +1 vs METTL3 内部）；METTL3 vs METTL16 vs METTL5 底物区分；FTO 多底物区室依赖性生物学（Jia 2011 / Mauer 2017 / Wei 2018）；抗体批次追踪元数据用于跨批次协调 |
| **clip-seq** | 12 | CLIPper, PureCLIP, Skipper, STAR, umi_tools, HOMER, mCross, PEKA, RBNS, ChIPseeker, RBP-Maps, DEWSeq, miCLIP2 + m6Aboost, GLORI, DART-seq, m6Anet, STAMP, Bullseye, Hyb, chimeric eCLIP / miR-eCLIP, HEAP, RBPNet, RNAProt, GraphProt2, CLAM | 协议特异性预处理（eCLIP 10nt UMI / iCLIP NNNXXXXNN / PAR-CLIP T->C 感知）、ENCODE STAR 比对块（含 CLAM 多比对救援用于重复结合 RBP）、峰 calling 涵盖 CLIPper / Skipper（多 210-320% 位点；beta-二项式 GC 分层）/ PureCLIP HMM / Piranha / omniCLIP / CTK CIMS-CITS（含 ENCODE log2 FC >= 3 + -log10 p >= 3）、单 nt 交联检测（截断 vs 缺失 vs T->C 化学）、基序分析（CL 位置注册的 mCross / PEKA / RBNS Kd 验证）、ChIPseeker + RBP-Maps 剪接调控元基因 + RepeatMasker 轴、综合质控五门（预处理 -> 比对 -> 复杂度 -> FRiP -> IDR）按 ENCODE、DEWSeq 窗口级差异（含 `~ type + condition + type:condition` 交互）、m6A 分析（miCLIP2 + m6Aboost / GLORI 无抗体化学计量 / DART-seq / m6Anet 纳米孔）、STAMP/scSTAMP/TRIBE 无抗体编辑分析、AGO-CLIP miRNA 靶点通过 chimeric eCLIP / miR-eCLIP / CLEAR-CLIP / HEAP（含种子和 3' 补偿配对）、深度学习（RBPNet 序列到信号单 nt / RNAProt / GraphProt2 / DeepCLIP）用于变异效应预测 |
| **clinical-databases** | 12 | myvariant, requests, cyvcf2, PharmCAT, Cyrius, T1K, OptiType, HLA-LA, SigProfilerAssignment, MSIsensor-pro, LDpred2, PRS-CSx, pgsc_calc, InterVar, GeneBe | ClinVar（VCV/SCV/RCV + ClinGen VCEPs + 2024 XML）、dbSNP Build 156 + SPDI、gnomAD v4 grpmax FAF95 + LOEUF、ACMG/AMP（含 Tavtigian 评分系统 + Pejaver 2022 校准）、变异优先级排序（DeNovoGear、Exomiser、ACMG SF v3.2）、药物基因组学（CPIC + DPWG + Caudle 2020 + Cyrius 用于 CYP2D6 SV）、PRS（LDpred2/SBayesRC/PROSPER/MUSSEL + Ding 2023 连续祖先 + Hingorani 2023 批评）、体细胞特征（COSMIC v3.4 + MuSiCal + HRDetect）、TMB（Vega 2021 校准）、MSI（MSIsensor-pro + Lynch 工作流）、HLA 分型（T1K I+II+KIR + StarPhase 长读） |
| **genome-engineering** | 5 | CRISPOR, Cas-OFFinder, PrimeDesign, BE-Hive, primer3-py | 结果感知 sgRNA 敲除设计（上下文验证的 on-target 评分、移码/NMD 外显子生物学）、off-target 提名（含 CFD/变异感知筛选和高保真核酸酶）、CBE/ABE 碱基编辑（按窗口/旁观者纯度）、先导编辑 pegRNA 面板（PE2/PE3b/PE5max/PE7 选择）、HDR 供体（含密码子检查的阻断突变） |
| **systems-biology** | 7 | cobrapy, CarveMe, gapseq, memote, troppo, corda, MICOM, SMETANA, StrainDesign, cameo | FBA/FVA/pFBA/无环/采样，基于欠定 LP 替代最优陷阱（生物量稳健，内部通量不是；13C-MFA 测量 FBA 仅预测的）；草图重建（CarveMe 自上而下 BiGG vs gapseq 自下而上 ModelSEED），含 draft-is-a-hypothesis / gap-fill-forces-growth 原则及 BiGG-vs-ModelSEED 命名空间协调；memote 整理作为一致性而非正确性（古德哈特定律），含多货币产能循环检测；基因必需性作为模型和培养基相关的预测（GPR 同工酶掩蔽、 cutoff 扫描、FBA vs MOMA/ROOM 按突变时间尺度、MCC 非准确度）；情境特异性提取（GIMME/iMAT/CORDA 通过 troppo/corda），其中方法 x 阈值主导数据加上非生长组织生物量目标陷阱和 scRNA-seq 缺失警告；群落建模（MICOM 合作权衡、SMETANA MRO/MIP 交叉喂养），含区室合并伪影；生长耦合菌株设计（StrainDesign OptKnock/RobustKnock/MCS、OptKnock 乐观 vs RobustKnock） |
| **epidemiological-genomics** | 5 | AMRFinderPlus, hAMRonization, mlst, chewBBACA, Pangolin, Nextclade, TreeTime, BEAST2（BDSKY + MASCOT + BICEPS）, TransPhylo, outbreaker2, Freyja, TB-Profiler, Kleborate, MOB-suite, Gubbins | 获得性和染色体点突变 AMR（含 WHO Mtb 第 2 版目录（TB-Profiler + Mykrobe）及 hAMRonization 到 PHA4GE）、MGE 上下文（MOB-suite + PlasmidFinder + MobileElementFinder）、病原体分型（7 位点 + cgMLST + chewBBACA + SISTR/SeqSero2/Kleborate/SeroBA/spa+SCCmec、Coll/Napier MTBC 条形码、Pangolin UShER + Nextclade 含 pangolin-data 版本固定）、系统动力学（TreeTime + BEAST2 BDSKY/BICEPS/MASCOT，含 Gubbins / ClonalFrameML 重组掩蔽、TempEst + 日期随机化质控、UShER + matUtils 用于疫情规模）、传播推断（outbreaker2 / TransPhylo / phybreak / SCOTTI / BadTrIP / transcluster，含病原体特异性 SNP 阈值 Walker 2013 / Coll 2017 / Eyre 2013 / Snitkin 2012；HIV-TRACE 亚型感知）、变异监测（Nextstrain Augur + Auspice、Freyja / COJAC 废水反卷积含条形码仅正向纪律、ARTIC V3 / V4.1 / V5.3.2 / Midnight 引物方案意识） |
| **immunoinformatics** | 6 | MHCflurry, NetMHCpan, NetMHCIIpan, pVACtools, NeoFox, BepiPred, tcrdist3 | MHC I/II 结合、新抗原鉴定、免疫原性排序、表位预测、TCR 特异性 |
| **comparative-genomics** | 13 | OrthoFinder3, PAML, HyPhy, MCScanX, JCVI, GENESPACE, SyRI, Progressive Cactus, Minigraph-Cactus, PGGB, PGR-TK, wgd v2, KsRates, ALE, GeneRax, AleRax, Dsuite, TreeMix, qpAdm, AdmixTools v2, HGTector v2, AvP, TOGA, CESAR 2.0, LiftOff, CAFE5, Count, Panaroo, PPanGGOLiN, PEPPAN, skani, FastANI, GTDB-Tk | 祖先状态重建（序列/离散/连续、GRASP indel 感知）、直系同源推断（OrthoFinder3 HOGs、Quest-for-Orthologs 2025）、正选择（PAML + HyPhy BUSTED-MH/MEME/aBSREL/RELAX、GARD 预筛选、gBGC 感知）、共线性（MCScanX/JCVI/GENESPACE/SyRI、WGD 感知）、基因树-物种树协调（ALE/GeneRax/AleRax、ALE 定根）、全基因组比对（Progressive Cactus/Minigraph-Cactus/LASTZ/AnchorWave）、全基因组复制定年（wgd v2 + KsRates）、泛基因组（Panaroo/PPanGGOLiN/PEPPAN 细菌、Minigraph-Cactus/PGGB/PGR-TK 真核）、ANI/物种界定（skani + GTDB-Tk r220、95% ANI + AF >= 0.5）、基因渗入（Dsuite/AdmixTools/TreeMix/QuIBL/HyDe、ILS 感知）、基因家族演化（CAFE5/Count/BadiRate）、HGT（ALE/GeneRax + HGTector v2/AvP）、比较注释投射（TOGA + CESAR 2.0、LiftOff） |
| **genome-annotation** | 7 | Bakta, BRAKER3, RepeatModeler2, Infernal, eggNOG-mapper, BUSCO, Liftoff | 重复序列屏蔽、原核/真核基因预测、ncRNA、功能分配、注释质控（BUSCO/OMArk/CheckM2）、注释转移 |
| **gene-regulatory-networks** | 6 | pySCENIC, SCENIC+, WGCNA, CellOracle, VIPER | 共表达网络、批量 GRN 推断和 TF 活性、regulon 推断、多组学 GRN、扰动模拟 |
| **causal-genomics** | 11 | TwoSampleMR, MendelianRandomization, coloc, susieR, CAUSE, LHC-MR, LDSC, LDAK, HDL, LAVA, FUSION, MetaXcan, FOCUS, MAGMA, PoPS, GenomicSEM, MTAG | 孟德尔随机化（含 MVMR、cis-MR 药物靶点、CHP 感知 CAUSE/LHC-MR/LCV）、共定位（coloc.abf/susie、SMR/HEIDI、eCAVIAR、PWCoCo、moloc、HyPrColoc）、精细定位（SuSiE/SuSiE-inf、FINEMAP、PolyFun、SuSiEx）、中介（CMAverse 4 向、HIMA2 高维 EWAS、MR-中介）、多效性（UHP vs CHP）、TWAS 含三角测量、遗传力分区（LDSC/LDAK、baseline-LD、Finucane 2018 细胞类型）、蛋白质组 MR 用于药物靶点（UKB-PPP/deCODE）、效应基因优先级排序（L2G/MAGMA/PoPS/cS2G）、遗传相关（LDSC/HDL/LAVA）、GenomicSEM 共同因子 GWAS |
| **rna-structure** | 4 | ViennaRNA, Infernal, ShapeMapper2, R-scape | RNA 二级结构预测（集合 vs MFE/质心/MEA、假结和长 RNA 路线）、ncRNA 同源性搜索含协方差模型（Rfam GA/clan 分辨率）、SHAPE-MaP/DMS-MaPseq 结构探测、及保守结构协变验证（R-scape 功效感知裁决） |
| **temporal-genomics** | 6 | CosinorPy, MetaCycle, LimoRhyde, dryR, scipy/astropy, Mfuzz, mgcv, tradeSeq, ruptures, dynGENIE3, bnlearn | 决策级时间序列组学：已知周期节律检测（cosinor/JTK/eJTK/ARSER/RAIN/MetaCycle）、条件间差异节律性（LimoRhyde/dryR/compareRhythms、获得/丢失/相位/振幅、无检测后 Venn）、未知周期发现（广义 Lomb-Scargle、小波锥形影响）、时间谱聚类（Mfuzz/DTW）、GAM + 变点轨迹建模（NB/自相关感知）、假设级动态 GRN（Granger/dynGENIE3/DBN）；含采样设计、多重检验和因果上限护栏 |
| **ecological-genomics** | 6 | OBITools3, iNEXT, vegan, LEA, hierfstat, ASAP | eDNA 宏条形码、生物多样性指标、群落生态学、景观基因组学、保护遗传学、物种界定 |
| **machine-learning** | 6 | scikit-learn, scikit-survival, shap, scvi-tools, boruta | 决策级组学 ML：生物标志物发现、p>>n 分类、防泄漏验证和校准、SHAP 解释、生存预测、单细胞图谱映射 |
| **clinical-biostatistics** | 12 | statsmodels, scipy, tableone, pyreadstat, lifelines; R mmrm, rbmi, gMCP, rpact, RBesT, BOIN, survival | CDISC SDTM/ADaM 数据处理、逻辑回归（含 FDA 2023 边际 vs 条件）、分类检验（Boschloo、mid-p McNemar、Wilson/MN CI）、效应测量、亚组分析（含现代 HTE（因果森林、EXNEX））、ICH E9(R1) 估计目标下的试验报告、生存（Cox/RMST/竞争风险/MaxCombo）、缺失数据敏感性（MMRM、基于参考的 MI、Permutt  tipping point）、功效/样本量、图形多重性、适应性设计、贝叶斯试验（BOIN、MAP 先验、RWE） |

**总计：63 个分类中的 561 个技能**

## 示例用法

技能部署后，自然地询问您的代理。以下是常见工作流中的示例；完整集合涵盖 63 个分类中的 561 个技能：

```
# RNA-seq 与差异表达
"我有处理组 vs 对照组的 RNA-seq 计数——找出差异表达基因"
"从我的 FASTQ 文件运行完整的 RNA-seq 流程到 DE 基因列表"
"我的上调基因中富集了哪些生物学通路？"
"运行 GSEA 查看我的处理中整个通路是上调还是下调"
"用 STAR 将我的双端 RNA-seq 读段比对到人类基因组"
"从我的比对 BAM 文件按基因计数读段"

# 单细胞分析
"我刚拿到 10X scRNA-seq 数据——过滤低质量细胞并标准化"
"聚类我的单细胞数据并帮我识别细胞类型"
"为每个聚类找到标记基因以便我注释细胞类型"
"重建分化轨迹并找到分支点"
"哪些配体-受体对显示我的细胞类型间活跃通讯？"

# 变异 Calling 与临床基因组学
"从我的肿瘤-正常 BAM 文件 call 体细胞变异"
"我在患者中发现了一个 BRCA1 变异——按 ACMG 指南它是致病的吗？"
"我的哪些变异在 ClinVar 中已知是致病的？"
"这个变异在 gnomAD 中的群体频率是多少？"
"用基因名、功能效应和临床数据库注释我的 VCF"
"在我的 WGS 数据中找到结构变异如缺失和重复"
"我的患者有 CYP2D6 变异——他们的代谢表型是什么？"
"用 SpliceAI 扩展窗口评分预测这个深内含子变异是否创建假外显子"
"应用 ClinGen SVI 2023 剪接阈值将变异分类为 PP3 支持/中等/强"

# 表观基因组学与染色质
"从我的 ChIP-seq 数据 call 这个转录因子的峰"
"运行 ENCODE 4 ATAC-seq 流程，跨重复和伪重复自一致性 IDR"
"构建 Corces 2018 固定宽度共识峰集（501 bp）在差异可及性检验之前"
"运行 TOBIAS 三步足迹并验证 CTCF 聚合显示干净的 V 形"
"用 chromBPNet 在匹配细胞类型上预训练为 100 个 GWAS SNP 评分染色质效应"
"用 ABC 模型结合 ATAC + H3K27ac + Hi-C 预测增强子-基因调控连接"
"运行 WASP 校正的等位基因特异性可及性分析以映射染色质 QTL"
"用 Signac 处理 10X scATAC（TF-IDF + LSI dims=2:30 跳过深度）并按聚类 call 峰"
"找到肿瘤和正常之间的差异甲基化区域"
"从我的 Hi-C 接触矩阵识别 TAD 和染色质环"

# 实验设计与质控
"检测 2 倍变化需要多少重复才能达到 80% 功效？"
"开始分析前检查我的测序数据质量"
"我的 BAM 文件中的比对率和覆盖质量如何？"
"生成 MultiQC 报告汇总我所有的流程输出"

# 蛋白质与结构
"用 AlphaFold 预测我的蛋白质序列的 3D 结构"
"找到我的处理条件之间差异丰度的蛋白质"

# CRISPR 与基因组工程
"设计 gRNA 以最小 off-target 敲除 TP53"
"分析我的 CRISPR  dropout 筛选以找到必需基因"

# 流程与可重复性
"设置 Snakemake 工作流以便我可以在 50 个样本上重新运行此分析"
"运行完整的生物标志物发现流程并进行适当的交叉验证"
"端到端注释我的新基因组组装，从重复序列到功能注释"
"对我的摘要统计运行后 GWAS 因果推断"

# 序列与数据库
"为我的基因列表从 NCBI 下载基因序列和注释"
"设计 PCR 引物以扩增该基因的 500bp 区域"
"读取我的 FASTA 文件并提取特定序列"

# 空间与组织分析
"识别我的 Visium 数据中的空间不同组织区域"
"我的宏基因组样本中存在哪些物种？"

# 长读测序
"用高精度为我的 Oxford Nanopore fast5 文件碱基识别"
"评估我的基因组组装是否完整且高质量"
"用 IsoQuant 或 Bambu 从我的 PacBio HiFi 或 ONT R10.4.1 数据发现全长异构体"

# 专业分析
"分析差异外显子使用以检测选择性剪接变化"
"用 FRASER 2.0 检测我的罕见病患者的异常剪接"
"找到我的条件之间具有 NMD 或结构域后果的异构体转换"
"从我的 T 细胞 RNA-seq 提取和分析 TCR 序列"
"构建生存模型以找到与患者结局相关的基因"
"用机器学习发现预测治疗反应的生物标志物"
"用适当的交叉验证验证我的预测模型以避免过拟合"

# 免疫治疗与癌症
"从肿瘤突变预测用于免疫治疗的新抗原"
"从 RNA-seq 确定 HLA 型以用于新抗原预测"
"检测我的液体活检 cfDNA 中的超低频突变"

# 基因组注释
"用 Bakta 注释我新组装的细菌基因组"
"在我的真核组装上运行 BRAKER3 基因预测"
"用 eggNOG-mapper 和 InterProScan 分配功能注释"

# 基因调控网络
"用 pySCENIC 从我的单细胞数据推断转录因子 regulon"
"用 WGCNA 构建共表达网络并找到枢纽基因"
"模拟如果我敲除这个转录因子会发生什么"

# 因果基因组学
"运行孟德尔随机化以测试 BMI 是否导致心脏病，含完整 UHP+CHP 敏感性（CAUSE、LHC-MR、MR-PRESSO、Egger NOME 校正）"
"用 coloc.susie 和 p12 敏感性网格测试我的 GWAS 命中和 eQTL 是否共享同一因果变异"
"用 SuSiE-RSS 精细定位我的 GWAS 位点，包含 LD 不匹配诊断，并添加 PolyFun 功能先验"
"用 UKB-PPP 运行 PCSK9 的 cis-pQTL MR 对冠心病，并用 coloc PP.H4 三角测量"
"用 LDSC + baseline-LD 估计分层遗传力并优先选择性状相关组织"
"用 S-PrediXcan、cis-eQTL MR、coloc.susie 和 FOCUS 精细定位三角测量 TWAS 命中"
"用 GenomicSEM 构建精神性状的共同因子 GWAS 并报告 Q_SNP 异质性"

# RNA 结构
"预测我的 RNA 序列的二级结构和折叠能"
"在我的转录本中用 Rfam 搜索 ncRNA 同源物"

# 时间序列分析
"测试我的时间序列数据中哪些基因有昼夜表达模式"
"测试我的野生型和敲除小鼠之间的节律是否不同"
"按表达谱形状聚类我的时间可变基因"
"在我的不均匀采样时间序列中找到未知周期的周期性模式"

# 生态基因组学
"处理我的 eDNA 水样以识别存在的鱼类物种"
"使用 Hill 数稀疏化比较我的采样点之间的生物多样性"
"找到跨海拔梯度的局部适应位点"
"估计我的濒危物种的有效群体大小"

# 临床生物统计学
"在我的临床试验数据上运行逻辑回归，控制年龄和性别，并提取比值比"
"用卡方检验疫苗接种状态和疾病严重程度之间的关联"
"跨患者亚组分析治疗效果并生成森林图"

# 序列比对
"用最准确的 MSA 方法比对这 50 个蛋白质序列"
"为 PAML 的选择分析准备密码子比对"
"这些蛋白质 12% 一致；通过预测结构而非序列比对"
"在系统发育推断前修剪此 MSA 并告诉我用哪个修剪器"
"用互信息 APC 校正检测共进化残基对"
"比对这两个 DNA 序列并为规模选择合适的成对库"
"计算每列的 Capra-Singh JSD 保守性并标记功能残基"
"将我的 Stockholm 比对转换为 PHYLIP-relaxed 用于 IQ-TREE 输入"

# 系统发育与演化
"构建系统发育树并可视化演化关系"
"在脊椎动物物种中找到我的人源基因的直系同源物"

# 比较基因组学
"构建 30 个哺乳动物基因组的 Progressive Cactus 比对，并用 TOGA + CESAR 2.0 跨所有物种投射注释"
"用 Dsuite Dtrios + Fbranch 检测 Heliconius 物种间的基因渗入，并用 Twisst 确认窗口级信号"
"用 wgd v2 + KsRates 及多个外群识别大豆谱系中的全基因组复制事件"
"用 GARD 重组预筛选测试灵长类免疫基因的正选择，然后用 BUSTED-MH 和 MEME 及 PAML M8 vs M8a 交叉验证"
"跨 100 个细菌基因树运行 ALE 无日期协调并排序物种树根；报告每分支 HGT 计数"
"用 GTDB-Tk + skani 将 200 个 MAG 分类到 GTDB-r220 分类学，应用 95% ANI + AF >= 0.5 物种阈值"
"用 Panaroo 严格模式和 PPanGGOLiN 分区构建 200 个大肠杆菌基因组的细菌泛基因组，然后运行 Scoary 泛 GWAS 用于抗生素耐药性"
"将 PGR-TK 应用于 HPRC 单倍型跨 MHC II 类位点；标记 PANGEA（DGI / Diploid Genomics）为继任者"
"用 CAFE5 找到鲸类中的谱系特异性基因家族扩增，并通过 RERconverge 三角测量趋同速率转换"
"用 GRASP 重建祖先细胞色素 c 用于蛋白质复活，并在模糊位点提出 8 个替代构建体"
"用 TOGA + CESAR 2.0 将基因注释从 GRCh38 投射到新灵长类组装并报告完整性代码"
"用 minimap2 -x asm5 比对两个拟南芥基因组并用 SyRI + plotsr call 结构变异"
```

代理将根据上下文选择适当的工具。有关可用技能的完整列表，请参见上面的技能分类表。
