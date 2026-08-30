---
title: 【生信Agent】平台测试
date: 2026-08-22T00:08:00+08:00
author: snoopy-zc
cover: cover.jpg
math: true
images:
- cover.jpg
categories:
- 生信Agent
- 学习笔记
---


主要记录一些Agent平台搭建测试...

<!--more-->

| 项目          | Stars | 协议         | 最适合           | 来源                 |
| ----------- | ----- | ---------- | ------------- | ------------------ |
| Biomni      | 2,900 | Apache-2.0 | 通用生物医学平台      | Stanford SNAP Lab  |
| MedgeClaw   | 856   | MIT        | 临床 / 医学研究     | xjtulyc            |
| ClawBio     | 678   | MIT        | 本地优先生信        | ClawBio org        |
| BioClaw     | 323   | MIT        | 社区生信          | Runchuan-BU        |
| CellVoyager | 202   | MIT        | 单细胞 RNA-seq   | Stanford Zou Group |
| BioMaster   | 91    | MIT        | 多 agent 生信协调  | ai4nucleome        |
| BioMedAgent | 57    | MIT        | paper 锚定、同行评议 | 独立作者               |
| Darwin      | 1     | MIT        | 系统综述 + 临床证据   | yejunbin           |

---
## Open Science Desktop

构建组合：Open Science Desktop(web版) + deepseek V4 flash + BioClaw Skills

优点：
- 跨平台（windows, macOS, Linux）
- 能够部署web版本

缺点：
- web版本页面无法创建项目，也无法上传文件，使用不方便，只适合本地使用
- 自带的技能组ai4s-research/ai4s-skills只能用于写报告，功能性不足
- 安装新kills之后需要重启整个平台服务
- pdf预览只支持桌面版




