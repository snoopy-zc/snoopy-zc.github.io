---
title: 【生信Agent】智能体入门
date: 2026-08-30T00:08:00+08:00
author: snoopy-zc
cover: cover.jpg
math: true
images:
- cover.jpg
categories:
- 生信Agent
- 学习笔记
---


从通用智能体开始，搭建分析平台...

<!--more-->

## 1 Agent智能体介绍

ChatGPT能做的事
- 回答技术问题
- 生成代码片段
- 解释分析原理

ChatGPT做不到的事
- 在电脑上运行代码
- 检查和修复报错
- 管理项目文件
- 完成完整分析流程

任务：完成bulk RNA-seq差异分析、GO/KEGG富集、GSEA分析，并整理结果

相关概念

- MCP
    - 让Agent能够标准化地调用外部工具和资源
    - MCP可以连接：文献数据库、文件系统、生信平台、在线数据
    - MCP给Agent扩展了“手”和“眼”
- Skills
    - 给Agent准备的“专业操作手册”
    - 价值：将复杂流程封装为可复用模块、保证分析标准一致、降低沟通成本
    - 示例：RNA-seq分析Skill
        - 质控→差异分析→富集分析→可视化

Agent是中心执行者，MCP扩展工具能力，Skills提供专业流程

## 2 Agent安装

Agent需要通过终端执行命令，完成分析任务（待商榷...）

Agent安装三原则
- 以官网为准（AI工具更新快）
- 安装必须验证（测试启动、测试登录、测试读取目录）
- 权限要受控（不给全盘权限、只给项目文件夹权限、更清晰安全）

典型基础Agent
- Claude code （教程示例）
- Codex
- DeepSeek harness（待尝试...）
- OpenClaw
- ...


Claude code安装流程（略）
1. 安装Git
2. 安装Node.js （大多数智能体都基于js运行环境）
3. 基于Node.js安装Claude code
4. 环境变量设置
5. 安装CC Switch（Claude code默认连接Claude大模型，该工具用于配置第三方大模型API，也可不借助工具手动配置。因国内使用，后文实际切换到了Deepseek V4 flash的API）
6. 运行（命令行输入claude命令，即可启动）

## 3 部分生信Skills介绍

### K-Dense-AI/scientific-agent-skills

- 🧬 **生物信息学与基因组学** — 序列分析、单细胞 RNA 测序、基因调控网络、变异注释、系统发育分析
- 🧪 **化学信息学与药物发现** — 分子性质预测、虚拟筛选、ADMET 分析、分子对接、先导化合物优化
- 🔬 **蛋白质组学与质谱分析** — LC-MS/MS 数据处理、肽段鉴定、谱图匹配、蛋白质定量
- 🏥 **临床研究与精准医学** — 临床试验、药物基因组学、变异解读、药物安全性、临床决策支持、治疗方案规划
- 🧠 **医疗 AI 与临床机器学习** — 电子病历分析、生理信号处理、医学影像、临床预测模型
- 🖼️ **医学影像与数字病理学** — DICOM 处理、全切片图像分析、计算病理学、放射学工作流
- 🤖 **机器学习与人工智能** — 深度学习、强化学习、时间序列分析、模型可解释性、贝叶斯方法
- 🔮 **材料科学与化学** — 晶体结构分析、相图、代谢建模、计算化学
- 🌌 **物理学与天文学** — 天文数据分析、坐标变换、宇宙学计算、符号数学、物理计算
- ⚙️ **工程与仿真** — 离散事件仿真、多目标优化、代谢工程、系统建模、过程优化
- 📊 **数据分析与可视化** — 统计分析、网络分析、时间序列、出版级质量图表、大规模数据处理、探索性数据分析（EDA）
- 🌍 **地理空间科学与遥感** — 卫星图像处理、GIS 分析、空间统计、地形分析、面向地球观测的机器学习
- 🧪 **实验室自动化** — 液体处理方案、实验设备控制、工作流自动化、LIMS 集成
- 📚 **科学传播** — 文献综述、同行评审、科学写作、文档处理、海报、幻灯片、示意图、引文管理
- 🔬 **多组学与系统生物学** — 多模态数据整合、通路分析、网络生物学、系统层面洞察
- 🧬 **蛋白质工程与设计** — 蛋白质语言模型、结构预测、序列设计、功能注释
- 🎓 **研究方法论** — 假设生成、科学头脑风暴、批判性思维、基金申请撰写、学者评估

<https://github.com/K-Dense-AI/scientific-agent-skills>

---

### K-Dense-AI/claude-scientific-writer

- 📝 文档生成
    - **科学论文** — 符合 IMRaD 结构（Nature、Science、NeurIPS 等期刊格式）
    - **临床报告** — 病例报告、诊断报告、试验报告、患者文档
    - **研究海报** — 基于 LaTeX 制作（beamerposter、tikzposter、baposter）
    - **基金申请** — NSF、NIH、DOE、DARPA 等机构特定格式
    - **文献综述** — 系统性引文管理
    - **科学示意图** — 由 Nano Banana 2 驱动（CONSORT 流程图、神经网络架构、生物通路、电路图等）—— 图像模型基准测试
- 🤖 AI 驱动能力
    - **实时研究检索** — 基于并行搜索与提取；验证的重要性详见《AI 联合科学家已到来，瓶颈在于验证》
    - **AI 智能绘图** — 从自然语言描述生成科学示意图
    - **智能论文识别** — 自动识别对现有文献的引用
    - **同行评审反馈** — 基于 ScholarEval 框架的 8 维度量化评分
    - **迭代编辑** — 上下文感知的修订建议
- 🔧 开发者友好
    - **程序化 API** — 完整的异步 Python API，附带类型提示
    - **命令行界面** — 支持进度跟踪的交互式命令行工具
    - **进度流式传输** — 生成过程中的实时更新
    - **全面结果输出** — 包含元数据、文件路径、引用的 JSON 输出
- 📦 数据与文件集成
    - **自动数据处理** — 将文件放入 data/ 目录，自动分类至 figures/ 或 data/
    - **文档转换** — 通过 MarkItDown 将 PDF、DOCX、PPTX、XLSX 转换为 Markdown
    - **参考文献管理** — 自动生成 BibTeX 并格式化引用
    - **图表集成** — 图片自动引用与组织管理

<https://github.com/K-Dense-AI/claude-scientific-writer>

---

### GPTomics/bioSkills （项目已于2026-08-15冻结）

一套用于指导 AI 编程智能体（Claude Code、OpenAI Codex、Google Gemini、OpenCode、OpenClaw）完成常见生物信息学任务的专业技能集合。

本仓库为AI智能体提供生物信息学工作流的专业知识。每项技能包含代码模式、最佳实践和示例，帮助智能体为常见任务生成正确、地道的代码。

目标用户涵盖从学习计算生物学的本科生到处理大规模数据的博士研究生。技能范围从基础序列操作到单细胞RNA测序和群体遗传学等高级分析。

- [63类561个技能](https://github.com/GPTomics/bioSkills/tree/main#skill-categories)
- [示例用法](https://github.com/GPTomics/bioSkills/tree/main#example-usage)

<https://github.com/GPTomics/bioSkills>

---

### Yuan1z0825/nature-skills

nature-skills 是一组围绕 SKILL.md 组织的可复用技能包。skills/ 下的每个顶层技能目录都是一个可安装单元，例如 nature-*；nature-shared 是供其他技能读取的共享支持包，默认不作为独立触发技能计入技能索引。

安装完成后，可以直接把论文、段落、审稿意见或任务描述交给 Agent。下面这些提示词可以直接复制使用：

| 想做什么 | 直接这样说 |
|---|---|
| 读论文 / 中英文对照 | `把这篇 PDF 做成图文对应的中英文对照 Markdown reader。` |
| 生成文献汇报 PPT | `把这篇论文做成中文组会汇报 PPT，保留关键图件和来源标注。` |
| 润色或翻译论文段落 | `把这段中文改写成 Nature 风格英文，保持学术含义不变。` |
| 写摘要、引言或讨论 | `根据这些结果和图件，帮我起草 Nature 风格的摘要和引言。` |
| 预投稿审稿模拟 | `从 Nature 审稿人视角评估这篇稿件，给出三份互盲 reviewer reports；全部定稿后再综合。` |
| 回复审稿意见 | `根据这封返修邮件，为每位互盲审稿人分别写逐点回复和 cover letter，并标出修改稿需要标红的位置。` |
| 查文献、他引和引用者画像 | `整理这篇文章的引用数、严格他引数、DOI，并看引用者里有没有院士、Fellow 或领域大牛。` |
| 做科研图或论文示意图 | `根据这段方法和结果，帮我生成投稿级科研图或论文示意图草稿。` |

如果你不确定该用哪个技能，直接描述任务即可；如果已经知道技能名，可以在提示词中明确写“使用 `nature-reader`”或“使用 `nature-response`”。

#### [技能列表](https://github.com/Yuan1z0825/nature-skills#6-%E6%8A%80%E8%83%BD%E7%B4%A2%E5%BC%95)

当前 `skills/` 下包含以下可触发技能；`skills/nature-shared/` 是共享内容目录，不计入技能索引。点击技能名或“详情页”可以进入每个 skill 的单独说明页面。

| 技能 | 状态 | 用途 | 触发词 | 详情页 |
|-------|--------|---------|-----------------|--------|
| [`nature-figure`](skills/nature-figure/README.md) | Stable | 面向 Nature / 高影响力期刊的 Python 或 R 投稿级科研图工作流，包含 Results 级多面板证据架构、渲染时子图对齐门、最终 PDF 自动文字/图形碰撞审计、第三方 figures4papers 参考示例、原创模板和 OpenRouter GPT Image 2 论文示意图草稿 | “Nature figure”, “投稿级图片”, “publication plot”, “scientific figure”, “figures4papers”, “论文示意图”, “GPT Image 2” | [详情](skills/nature-figure/README.md) |
| [`nature-polishing`](skills/nature-polishing/README.md) | Stable | 将学术文本润色、重构或翻译为 Nature 风格英文，并扫描全文术语、单位、数值精度和声称漂移 | “Nature style”, “润色”, “academic writing”, “论文英文” | [详情](skills/nature-polishing/README.md) |
| [`nature-writing`](skills/nature-writing/README.md) | Draft | 起草 Nature 风格手稿章节，并重建论文论证 | “Nature writing”, “写摘要”, “写引言”, “manuscript draft”, “论文写作” | [详情](skills/nature-writing/README.md) |
| [`nature-reviewer`](skills/nature-reviewer/README.md) | Draft | 从审稿人视角模拟 Nature 风格评审，输出三份互盲 reviewer reports、分级 Major/Minor 意见，并检查手稿内部一致性 | “Nature reviewer”, “预投稿评审”, “reviewer report”, “审稿人视角评估” | [详情](skills/nature-reviewer/README.md) |
| [`nature-citation`](skills/nature-citation/README.md) | Beta | 检索严格限定在 Nature / CNS 系列的支撑文献，并导出 ENW、RIS 或 Zotero RDF | “Nature citation”, “CNS citation”, “分段引用”, “支撑文献”, “Zotero RDF” | [详情](skills/nature-citation/README.md) |
| [`nature-data`](skills/nature-data/README.md) | Draft | 准备 Data Availability statement、数据仓储方案和 FAIR 检查 | “Data Availability”, “数据可用性”, “repository”, “FAIR metadata” | [详情](skills/nature-data/README.md) |
| [`nature-statistics`](skills/nature-statistics/README.md) | Draft | 审查、改写或起草统计报告，覆盖实验单位、重复数、p 值、多重比较、效应量、置信区间、图注统计和跨章节数值一致性 | “Nature statistics”, “统计审查”, “statistical analysis”, “p value”, “sample size”, “replicates”, “multiple comparisons”, “图注统计”, “统计分析小节” | [详情](skills/nature-statistics/README.md) |
| [`nature-reader`](skills/nature-reader/README.md) | Beta | 生成带来源锚点、图文对应、公式渲染和中英文对照的全文 Markdown reader | “nature reader”, “全文 Markdown”, “原文对照”, “图文对应”, “公式渲染”, “全文翻译” | [详情](skills/nature-reader/README.md) |
| [`nature-paper-card`](skills/nature-paper-card/README.md) | Beta | 精读单篇论文并生成有来源约束的 01–16 节 Paper Card，覆盖方法逻辑、实验—结论证据链、结论边界、批判性分析和可检验研究想法 | “nature paper card”, “论文精读”, “Paper Card”, “证据链”, “结论边界” | [详情](skills/nature-paper-card/README.md) |
| [`nature-response`](skills/nature-response/README.md) | Beta | 解析返修邮件，为互盲审稿人分别生成独立回复，并提供 cover letter、标红稿、LaTeX 模板和返修包一致性检查 | “response to reviewers”, “rebuttal letter”, “cover letter”, “major revision”, “返修邮件”, “审稿意见回复”, “修回信”, “LaTeX 模板” | [详情](skills/nature-response/README.md) |
| [`nature-paper2ppt`](skills/nature-paper2ppt/README.md) | Beta | 从科研论文生成中文 PPTX 文献汇报 deck | “paper PPT”, “journal club”, “paper to slides”, “论文汇报” | [详情](skills/nature-paper2ppt/README.md) |
| [`nature-image2ppt`](skills/nature-image2ppt/README.md) | Beta | 将幻灯片图片、扫描 PDF 和图片型 PPTX 重建为对象级可编辑 PowerPoint，并执行渲染 QA | “图片转可编辑PPT”, “截图还原PPT”, “扫描PDF转PPTX”, “image to editable PowerPoint” | [详情](skills/nature-image2ppt/README.md) |
| [`nature-paper-to-patent`](skills/nature-paper-to-patent/README.md) | Beta | 从论文、技术报告或项目材料生成有证据约束的中国发明专利草稿，并支持专利点挖掘、查新和技术交底书迭代 | “paper to patent”, “Chinese patent”, “论文转专利”, “权利要求书”, “技术交底书”, “专利点” | [详情](skills/nature-paper-to-patent/README.md) |
| [`nature-ref-verifier`](skills/nature-ref-verifier/README.md) | Stable | 参考文献多源交叉验证：逐字段对比作者/标题/年份/卷期/页码，标记卷年冲突、作者编造、页码偏差等 | “verify refs”, “校验文献”, “check references”, “文献验证”, “ref check” | [详情](skills/nature-ref-verifier/README.md) |
| [`nature-academic-search`](skills/nature-academic-search/README.md) | Beta | 多源文献检索、引用核验、严格他引审计、文章引用指标表、高影响力引用者画像和参考文献管理 | “search papers”, “find articles”, “literature search”, “查文献”, “verify DOI”, “严格他引”, “文章引用表”, “引用我的文章的人有没有大牛” | [详情](skills/nature-academic-search/README.md) |
| [`nature-downloader`](skills/nature-downloader/README.md) | Beta | 通过图书馆资源入口、Chrome 登录态和开放获取路径合法获取学术全文/PDF | “download papers”, “图书馆下载文献”, “CARSI”, “Web of Science”, “PDF 下载” | [详情](skills/nature-downloader/README.md) |
| [`nature-literature-pipeline`](skills/nature-literature-pipeline/README.md) | Stable | 自动化文献发现管线：多源检索、六维评分、精读推送和本地归档 | “literature pipeline”, “每日文献”, “文献推送”, “daily literature push”, “cron” | [详情](skills/nature-literature-pipeline/README.md) |
| [`nature-experiment-log`](skills/nature-experiment-log/README.md) | Draft | 标准化记录实验图片、语音和文字材料，生成带 YAML frontmatter 的 Obsidian 实验日志并归档原始材料 | “实验日志”, “记录实验”, “experiment log”, “Obsidian vault”, “飞书科研群” | [详情](skills/nature-experiment-log/README.md) |
| [`nature-proposal-writer`](skills/nature-proposal-writer/README.md) | Beta | proposal-first 科研写作状态机，先建立证据、论证和章节契约，再起草或审查文本 | “researchwrite”, “proposal”, “开题报告”, “研究方案”, “科研写作 QA” | [详情](skills/nature-proposal-writer/README.md) |


<https://github.com/Yuan1z0825/nature-skills>


