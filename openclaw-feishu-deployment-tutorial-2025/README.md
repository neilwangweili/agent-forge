# OpenClaw + 飞书部署教程研究项目

## 项目标识

`openclaw-feishu-deployment-tutorial-2025`

## 项目概述

本项目是一个基于 AgentForge 架构的研究多智能体系统，目标是生成一篇帮助非技术人员部署 OpenClaw 并对接飞书的教程文章。

### 研究主题

帮助不懂代码的职场人士，在本地部署 OpenClaw（原 ClawdBot）并与飞书机器人对接，让飞书成为个人 AI 助手的入口。

### 核心问题

1. 如何让普通人也能拥有自己的 AI Agent？
2. 如何将 AI 能力无缝融入日常工作工具（飞书）？

---

## 语言设置

| 设置项 | 语言 |
|--------|------|
| 智能体蓝图语言 | 中文 |
| 报告输出语言 | 中文 |

---

## 目录结构

```
openclaw-feishu-deployment-tutorial-2025/
├── agents/                          # 智能体蓝图
│   ├── 00.orchestrator.md           # 编排者：协调三阶段流程
│   ├── 01.data_collector.md         # 数据收集者：爬取官方文档和补充信息
│   ├── 02.analyzer.md               # 分析者：简化步骤、提炼价值
│   └── 03.reporter.md               # 报告者：生成最终文章
│
├── data/                            # 运行时数据
│   ├── 01.materials/                # 收集的原始数据
│   ├── 02.analysis/                 # 分析结果
│   └── 03.reports/                  # 最终报告
│
├── references/                      # 参考资料
│   ├── research-overview.md         # 研究概述
│   ├── data-sources.md              # 数据源清单
│   ├── analysis-methods.md          # 分析方法说明
│   ├── report-template.md           # 报告结构模板
│   └── style-guide.md               # 写作风格指南
│
├── wip/                             # 工作过程记录
│   └── notes.md                     # 执行日志
│
└── README.md                        # 本文件
```

---

## 如何运行

### 启动系统

在 Claude Code 中发送以下指令：

```
请使用 openclaw-feishu-deployment-tutorial-2025/agents/00.orchestrator.md 开始执行研究任务
```

### 执行流程

编排者（Orchestrator）会自动：

1. **第一阶段：数据收集**
   - 爬取 OpenClaw 官方安装指南
   - 爬取飞书对接文档
   - 收集项目背景和常见问题
   - 输出到 `data/01.materials/`

2. **第二阶段：分析**
   - 简化安装步骤
   - 简化飞书对接步骤
   - 提炼场景价值和深远意义
   - 输出到 `data/02.analysis/`

3. **第三阶段：报告生成**
   - 整合分析结果
   - 按模板结构生成文章
   - 应用写作风格指南
   - 输出到 `data/03.reports/`

### 查看结果

- **原始数据**：`data/01.materials/`
- **分析结果**：`data/02.analysis/`
- **最终报告**：`data/03.reports/openclaw-feishu-tutorial.md`

---

## 如何调整

### 修改数据收集策略

编辑 `agents/01.data_collector.md` 或 `references/data-sources.md`

### 修改分析方法

编辑 `agents/02.analyzer.md` 或 `references/analysis-methods.md`

### 修改报告格式

编辑 `agents/03.reporter.md` 或 `references/report-template.md`

### 修改写作风格

编辑 `references/style-guide.md`

---

## 预期输出

一篇约 2500-3000 字的微信公众号文章，包含：

1. **开篇引入**（约 400 字）：介绍 OpenClaw 和为什么值得关注
2. **功能展示**（约 300 字）：2-3 个具体使用场景
3. **安装指南**（约 800 字）：简化的本地安装步骤
4. **飞书对接**（约 600 字）：简化的飞书对接步骤
5. **深远意义**（约 400 字）：从工具到入口、AI Agent 时代
6. **结语**（约 100 字）：鼓励尝试，附官方链接

---

## 注意事项

1. **数据源依赖**：系统依赖外部网站（clawd.org.cn），如网站不可访问可能影响数据收集
2. **内容时效性**：OpenClaw 项目可能更新，教程内容以采集时的官方文档为准
3. **读者定位**：目标读者是会用电脑和飞书但不会写代码的职场人士

---

## 技术架构

本系统基于 AgentForge 声明式多智能体架构：

- **声明式**：智能体蓝图用自然语言描述目标和标准，运行时智能选择执行方式
- **数据驱动**：领域知识外部化为参考文件，修改文件即可改变系统行为
- **透明可追溯**：所有中间输出完整保留，数据流清晰可见
- **质量内建**：质量标准嵌入智能体蓝图，执行过程中持续自检

---

## 相关链接

- OpenClaw 官网：https://clawd.org.cn
- OpenClaw 安装向导：https://clawd.org.cn/start/wizard
- OpenClaw 飞书对接：https://clawd.org.cn/channels/feishu
