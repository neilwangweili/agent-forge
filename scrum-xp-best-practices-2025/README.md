# Scrum + XP + AI 最佳实践研究项目

## 项目简介

本项目是一个基于 AgentForge 架构的研究多智能体系统，旨在撰写一篇倡导性的技术文章，推荐并论证 **Scrum + XP + AI 方法论**作为现代软件开发的最佳实践。

通过数据收集、深度分析和专业写作，本系统将展示如何将敏捷项目管理、极限编程实践与 AI 技术深度融合，实现高效、高质量的软件交付。

## 研究目标

1. 论证 Scrum 相比传统软件开发方法（如瀑布模型）的显著优势
2. 论证 Extreme Programming (XP) 相比传统编码方式的质量保障优势
3. 展示 Scrum + XP 结合的协同效应和完整实践流程
4. 说明 Smart Domain 模式和小对象模式如何进一步提升代码质量
5. 论证 AI 技术（特别是 Multi-Agent System）带来的革命性优化

## 语言设置

- **Agent 蓝图语言**：中文
- **报告输出语言**：中文

所有 Agent 蓝图、参考文档和最终报告均使用中文。

## 目录结构

```
scrum-xp-best-practices-2025/
├── agents/                       # Agent 蓝图（中文）
│   ├── 00.orchestrator.md         # 主协调者
│   ├── 01.data_collector.md       # 数据收集 Agent
│   ├── 02.analyzer.md             # 分析 Agent
│   └── 03.reporter.md             # 报告生成 Agent
│
├── data/                         # 运行时数据
│   ├── 01.materials/              # 收集的原始数据（JSON 格式）
│   ├── 02.analysis/               # 分析结果（Markdown 格式）
│   └── 03.reports/                # 最终报告（Markdown 格式）
│
├── references/                   # 参考资料
│   ├── research-overview.md       # 研究概览
│   ├── data-sources.md            # 数据源描述
│   ├── analysis-methods.md        # 分析方法
│   ├── report-template.md         # 报告模板
│   └── style-guide.md             # 写作风格指南
│
├── wip/                          # 工作进行中的笔记
│   └── notes.md                   # 杂项记录
│
└── README.md                     # 项目文档（本文件）
```

## 如何运行

### 首次运行

在 Claude Code 中，输入以下命令启动系统：

```
请使用 agents/00.orchestrator.md 开始执行研究任务
```

### 执行流程

协调者将自动执行以下三个阶段：

1. **数据收集阶段**（Phase 1）
   - 协调者读取 `references/` 下的参考文档
   - 并行启动多个数据收集 Agent，收集 Scrum、XP、传统方法、TDD、Smart Domain、小对象模式、CI/CD、AI MAS 等主题的详细信息
   - 输出：`data/01.materials/*.json`

2. **分析阶段**（Phase 2）
   - 分析 Agent 读取收集的数据
   - 进行三个子阶段的分析：单主题深度分析、对比与整合分析、AI 增强分析
   - 输出：`data/02.analysis/chapter1-scrum.md`、`chapter2-xp.md`、`chapter3-scrum-xp-practices.md`、`chapter4-ai-optimization.md`、`appendix-data.md`

3. **报告生成阶段**（Phase 3）
   - 报告生成 Agent 读取分析结果
   - 根据报告模板和写作风格指南，撰写倡导性技术文章
   - 输出：`data/03.reports/final-report.md`（中文）

### 查看结果

运行完成后，最终报告位于：
```
data/03.reports/final-report.md
```

所有中间数据都保存在 `data/01.materials/` 和 `data/02.analysis/` 中，完全透明可追溯。

## 系统架构特点

### 声明式多智能体架构

- **Prompt-Defined Agent**：Agent 行为由自然语言蓝图定义
- **Orchestrated Agent Pipeline**：任务分解为三阶段流水线
- **Filesystem Data Bus**：Agent 通过文件系统传递数据
- **Parallel Instance Execution**：数据收集阶段支持并行执行
- **Reference Data Configuration**：领域知识外部化为参考文件

### 工作空间隔离

每个 Agent 都被严格限制在项目目录内工作：
- 不会读取项目目录之外的任何文件
- 不会写入项目目录之外的任何文件
- 确保系统隔离，避免上下文污染

### 质量保障

- 每个 Agent 蓝图中嵌入质量标准
- 协调者在每个阶段进行质量检查
- 所有中间输出可人工审查和干预

## 如何调整和优化

### 调整数据收集策略

修改 `agents/01.data_collector.md` 或 `references/data-sources.md`

### 调整分析方法

修改 `agents/02.analyzer.md` 或 `references/analysis-methods.md`

### 调整报告格式

修改 `agents/03.reporter.md` 或 `references/report-template.md`

### 调整写作风格

修改 `references/style-guide.md`

### 添加领域知识

在 `references/` 目录下添加新文件，并在相应 Agent 蓝图中引用

## 核心方法论

本研究倡导的核心方法论是：

### Scrum（敏捷项目管理框架）
- 快速迭代，缩短反馈周期
- 拥抱变化，降低变更成本
- 持续交付价值，提升客户满意度

### Extreme Programming（卓越的工程实践）
- TDD 提升代码质量和测试覆盖率
- Pair Programming 知识共享，减少缺陷
- 持续集成早期发现问题

### Smart Domain 模式与小对象模式
- 富领域模型，业务逻辑内聚
- 拒绝原始类型偏执，使用 Value Objects
- 类型安全、业务语义清晰

### AI Multi-Agent System
- 从一句话需求到自动化验收的一体化流程
- 多个专业 Agent 协同工作
- 效率、质量、一致性的全面提升

## 实践流程

1. 利用领域建模 + 用户故事地图进行需求分析
2. 编写用户故事（User Stories）和验收标准（AC）
3. 使用 TDD 在集成测试和端到端测试中与 AC 对照，完成编码
4. 通过端到端测试、验收测试和 CI/CD 实践进行回归测试
5. 通过 CI/CD 进行自动化部署

在 AI 介入后，实现了从"一句话需求 → 用户故事 → AC → 测试代码、开发代码 → 自动回归验收"的一体化流程。

## 注意事项

- 本系统需要连接互联网，以便使用 WebSearch 工具收集数据
- 数据收集阶段可能需要较长时间（取决于数据源数量和网络速度）
- 所有中间输出都会保存，可随时中断和恢复
- 系统是可进化的，可以根据初次运行结果调整 Agent 蓝图和参考文档

## 适用场景

本架构特别适合：
- 信息密集型研究（需要大量数据收集和分析）
- 周期性研究（可重复运行）
- 质量优先研究（可接受一定时间成本）
- 需要透明可追溯的研究（所有过程可见）

## 技术栈

- **运行时**：Claude Code（基于 Claude Sonnet 4.5）
- **数据格式**：JSON（原始数据）、Markdown（分析和报告）
- **架构模式**：声明式多智能体、三阶段流水线、文件系统数据总线

## 许可证

本项目基于 AgentForge 架构生成。

---

**开始研究**：请使用 `agents/00.orchestrator.md` 启动系统。
