# AI 时代程序员的职业前景与角色转变

## 项目概述

本项目是一个基于 AgentForge 架构的多智能体研究系统，目标是生成一篇关于"AI 时代程序员职业前景"的公众号文章。

### 核心论点

**AI 不会让程序员失业，而是重新定义程序员的角色——从"写代码的人"转变为"做架构决策的人"。**

### 研究问题

1. 以 Gemini 3 为代表的最新 AI 编程能力达到了什么水平？
2. 为什么很多人认为程序员要失业？这些观点的依据是什么？
3. 为什么"能开发"就必须"能维护"？AI 在代码维护方面有什么局限？
4. 程序员的角色如何向架构师转变？架构决策为什么不能被 AI 取代？

## 语言设置

- **智能体蓝图语言**：中文
- **报告输出语言**：中文

## 目录结构

```
ai-era-programmer-future-2025/
├── agents/                      # 智能体蓝图
│   ├── 00.orchestrator.md       # 主编排器
│   ├── 01.data_collector.md     # 数据收集智能体
│   ├── 02.analyzer.md           # 分析智能体
│   └── 03.reporter.md           # 报告生成智能体
│
├── data/                        # 运行时数据
│   ├── 01.materials/            # 收集的原始数据
│   ├── 02.analysis/             # 分析结果
│   └── 03.reports/              # 最终报告
│
├── references/                  # 参考资料
│   ├── research-overview.md     # 研究概述
│   ├── data-sources.md          # 数据源描述
│   ├── analysis-methods.md      # 分析方法
│   ├── report-template.md       # 报告模板
│   └── style-guide.md           # 写作风格指南
│
├── wip/                         # 工作笔记
│   └── notes.md                 # 执行过程记录
│
└── README.md                    # 本文件
```

## 如何运行

### 启动系统

在 Claude Code 中执行：

```
请使用 ai-era-programmer-future-2025/agents/00.orchestrator.md 开始执行研究任务
```

### 执行流程

系统将自动完成三个阶段：

1. **数据收集**：并行收集 4 个主题的数据
   - Gemini 3 能力与 AI 编程现状
   - "程序员失业论"的来源与论据
   - 软件维护的本质与 AI 局限
   - 架构决策的不可替代性

2. **数据分析**：两阶段分析
   - 分主题深度分析
   - 整合论证链

3. **报告生成**：生成公众号文章
   - 3000-4000 字
   - 五段式结构
   - 符合写作风格要求

### 查看结果

- 原始数据：`data/01.materials/`
- 分析结果：`data/02.analysis/`
- 最终文章：`data/03.reports/final-article.md`

## 最终产出

一篇公众号文章，包含以下结构：

1. **引子**：Gemini 3 带来的震撼
2. **恐慌的来源**：为什么很多人认为程序员要失业
3. **被忽视的真相**：开发能力 = 维护能力
4. **程序员的新角色**：人人都是架构师
5. **结语**：拥抱变化，重新定位

## 调整与优化

- 调整数据收集策略：修改 `agents/01.data_collector.md`
- 调整分析方法：修改 `agents/02.analyzer.md` 或 `references/analysis-methods.md`
- 调整文章结构：修改 `agents/03.reporter.md` 或 `references/report-template.md`
- 调整写作风格：修改 `references/style-guide.md`

## 注意事项

1. 所有智能体都被限制在项目目录内工作，不会访问外部文件
2. 中间结果完全保留，可以在任何阶段进行人工审查和干预
3. 如果某个阶段的输出不满意，可以修改相应的智能体蓝图后重新执行
