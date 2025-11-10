# User Input

Please provide the following information, and the generator will generate your research multi-agent system accordingly.

## Language Settings

**Agent Blueprint Language**:

```
中文
```

**Report Output Language**:

```
中文
```

---

## Research Project Basic Information

**Project Identifier**:

```
backend-architectures-2016-2025
```

**Research Topic and Core Questions**:

```
研究近十年（约 2016-2025）后端各类架构设计及其差异。

核心问题：
1. 主流后端架构范式有哪些？
2. 每种架构的来源/思想渊源、要解决的核心问题与典型适用场景是什么？
3. 各架构的大致实现方式（模块划分、数据流/控制流、边界/依赖、部署形态）是什么？
4. 优势、劣势与权衡点分别是什么？在什么组织与约束下更合适？
5. 架构之间如何演进或组合（如“分层+六边形”“模块化单体→微服务”“DDD+CQRS/ES”等）？
6. 深入研究未来可行的架构发展趋势，及结合AI可能的架构发展方向

研究意义：
帮助技术负责人与架构师在不同业务阶段与团队条件下进行理性架构选型与演进规划，并向未来的架构演进方向提出合理预测。
```

**Preliminary Direction and Insights**:

```
根据我的初步了解，主流的后端架构范式可能包括
- 传统 MVC 架构
- 整洁架构（Clean Architecture）
- DDD 架构
- Smart Domain 架构。

近十年的后端架构实践显示：复杂度治理、团队规模与发布频率是主要驱动因素。
候选架构家族（不完全，可能有遗漏，需要你帮忙注意到缺失的架构范式）：
- 经典：分层/传统 MVC、SOA、微内核/插件
- 领域中心：DDD（战术/战略）、Smart Domain（务实富领域模型）
- 端口驱动：六边形/端口与适配器、整洁架构（环形依赖反转）
- 分布式：微服务、服务网格、Serverless、事件驱动（EDA）、CQRS/事件溯源
- 形态改良：模块化单体、BFF、Reactive/Actor 模型

初步假设：
- “模块化单体 + 端口化边界”在多数中小型团队具备最佳性价比。
- DDD 更适合“高变业务 + 复杂规则”，非银弹；Smart Domain 为 DDD 的务实落地变体。
- 组织结构（Conway 定律）与平台能力（CI/CD、可观测性）强烈影响架构上限。

我假设架构技术正在快速演进，新工具、新理念不断涌现，技术路线可能有显著差异。
AI技术的显著发展也可能影响架构范式。
我希望通过这个研究验证这些假设，关注其背后的思想演进和思想渊源，并发现我尚未注意到的新趋势。
```

---

## Phase One: Data Collection

**Data Sources**:

```
1. 经典著作与论文：
   - 包括但不限于《Domain-Driven Design》, 《Clean Architecture》, 《Building Microservices》, 《Monolith to Microservices》
2. 技术会议与行业报告：
   - 包括但不限于 QCon/InfoQ、ThoughtWorks 技术雷达、GOTO、Gartner/Forrester 选读
3. 大厂工程博客与案例：
   - 包括但不限于 Netflix/Uber/Airbnb/Shopify/Cloudflare/Microsoft/AWS/GCP/Meta 工程博客
4. 社区与实践经验：
   - 包括但不限于 Hacker News、Reddit r/microservices、Stack Overflow、掘金/少数派/InfoQ 中文
5. 开源与参考实现：
   - 包括但不限于 GitHub：awesome-* 列表、参考骨架（hexagonal、clean-architecture、modular-monolith、cqrs、event-sourcing）
6. 官方文档与白皮书：
   - 包括但不限于 Spring、NestJS、ASP.NET、Dapr、Kafka、RabbitMQ、Temporal、Service Mesh 等
7. 各个架构范式的官方网站和文档
```

**Data Collection Objectives**:

```
对每种架构/组合收集：
- 基本信息：名称、提出者/来源、出现时间
- 核心问题：要解决的痛点/动机
- 思想：架构代表的思想及渊源
- 实现概览：模块与边界、依赖方向、数据流/控制流、部署形态
- 技术栈/常见实现：框架/中间件/模式（如 DI、Aggregator、Saga、Outbox）
- 适用场景与前置条件：团队规模、组织与工具要求
- 优势与劣势：性能/一致性/演进性/认知负担/成本
- 成功/失误案例摘要与链接
- 近年动态（2016-2025）

 详细程度：每个架构/组合收集 300-800 字的结构化信息即可，不需要完整文档。
```

**Data Collection Process Design**:

```
并行抓取与去重合并：
1. 按“架构范式”建立初始清单（不完全，可能有遗漏，需要你帮忙注意到缺失的架构范式）（MVC、Clean、DDD、Smart Domain、六边形、模块化单体、微服务、Serverless、EDA、CQRS/ES、微内核、BFF、Reactive/Actor）。
2. 每个来源并行收集，然后进行去重（同一架构范式可能在多个来源出现），按名称与同义词映射去重（如：六边形=端口与适配器）。
3. 聚合字段：时间线、实现要点、适用/不适用、案例与参考。
4. 标注可信度与时效性（高/中/低）与证据类型（一手实践/二手评述）。
5. 关注 2016-2025 的材料，必要时补充历史脉络。

```

**Data Storage Format**:

```
JSON（每种架构或组合一个文件），包含标准字段：
{
  "name": "架构名称",
  "aliases": ["别名1","别名2"],
  "origin": { "proposer": "提出者/来源", "year": 2014, "references": ["..."] },
  "problem_solved": ["痛点A","痛点B"],
  "implementation_overview": "模块、边界与依赖方向、控制/数据流、部署形态概述",
  "thoughts": ["代表/表达的主要思想1", "代表/表达的主要思想2", ...]
  "tech_stack": ["常见框架/中间件/模式"],
  "category": ["领域中心","分布式","端口化","形态改良"],
  "when_to_use": ["适用条件/组织/规模/节奏"],
  "when_not_to_use": ["不适用情形/反模式"],
  "tradeoffs": { "pros": ["..."], "cons": ["..."] },
  "costs": { "infra": "基础设施成本", "cognitive": "认知负担", "ops": "运维成本" },
  "org_requirements": ["团队/治理/平台要求"],
  "case_studies": [{"org":"示例公司","summary":"一句话结论","link":"..."}],
  "recent_updates": "2016-2025 期间的要点",
  "related_patterns": ["CQRS","Saga","Outbox","BFF","模块化单体"],
  "maturity_score": 0-5,
  "evidence_confidence": "high|medium|low"
}

```

**Existing Reference Materials**:

```
无
```

---

## Phase Two: Analysis

**Analysis Methods**:

```
1. 分类矩阵：
   - 按范式分类
   - 按复杂度/演进成本：低→高
   - 按依赖反转与边界清晰度：弱→强

2. 决策与评分：
   - 维度：业务复杂度、代表思想：成熟与先进性、变更频率、团队规模、数据一致性需求、发布频率、平台成熟度、SLA

3. 权衡与失败模式分析：
   - 常见反模式：贫血模型、耦合地狱、分布式单体、错误拆分、过度微服务化（等等）
   - 成本分解：认知/治理/运维/观测/数据一致性（等等）

4. 组合与演进路径：
   - 比较不同架构范式的核心差异，例如模块化单体→微服务、MVC→Clean/六边形→DDD/Smart Domain
   - 识别各种架构范式的思想演进

5. 趋势对比（2016 vs 2025）：
   - 工具链成熟度、云原生能力、平台/服务网格影响、事件中台/编排框架兴起
   
6. 演进预测
   - 通过现有的调研、分析、结论，研究未来可行的架构发展趋势，及结合AI可能的架构发展方向
```

**Analysis Process Design**:

```
两阶段分析：
1. 标注与统计：为每种架构进行分类标注、补齐字段与评分，产出分类分布与决策矩阵。
2. 深度对比：围绕“为何存在/代表思想/解决什么/成本在哪/如何失败”展开，形成演进建议与组合策略。
3. 深度预测：进行深度对比分析，识别未来可行的架构发展趋势，及结合AI可能的架构发展方向
```

**Analysis Results Storage**:

```
Markdown 文档：
- classification.md：架构家族与特征矩阵（含评分表）
- comparison.md：关键维度对比与决策表（含示例情境）
- trends.md：2016-2025 趋势与工具链演进
- market-landscape.md：实践版图（组织规模 × 架构复杂度热力）
- future-structure-with-ai.md：未来可行的架构发展趋势，及结合AI可能的架构发展方向
```

---

## Phase Three: Report Generation

**Report Format**:

```
Markdown文档
```

**Report Structure**:

```
1. 执行摘要（1-3 页）
   - 背景与范围（2016-2025）
   - 主要发现（4-8 个要点）
   - 关键结论
2. 架构概览
   - 家族与谱系图
   - 各自解决的问题与边界强度
   - 各自代表/表达的主要思想
3. 分类分析
   - 按范式、复杂度、组织前置条件分布
   - 评分与决策矩阵解读
4. 深度对比
   - 按有关联性地对比进行分析，包括但不限于：
     - 传统 MVC vs Clean/六边形：依赖方向与可测试性
     - DDD vs Smart Domain：战术/战略 vs 务实富领域模型
     - 模块化单体 vs 微服务：发布独立性与运维成本
     - 事件驱动/CQRS/ES：一致性、可审计与复杂度权衡
   - 按照思想纬度进行对比分析
5. 组合与演进
   - 典型路径与里程碑（含反模式预警）
   - 组织/平台/数据三要素协同
   - 思想纬度的演进
6. 趋势洞察（2016-2025）
   - 2016 - 2025 年的主要趋势
   - 架构演进方向预测
   - 结合AI的架构演进的可能性
7. 结论与建议
   - 对架构师、开发者的选择建议
   - 对利益干系人的选择建议
8. 附录
   - 完整范式列表
   - 定义与术语
   - 数据来源说明（完整参考与案例索引）
```

**Writing Style**:

```
专业分析报告风格：
- 语言：简洁、客观、专业
- 结构：逻辑清晰，层次分明
- 数据：用数据和事实支撑观点
- 可视化：适当使用表格和分类展示
- 洞察：不仅描述"是什么"，更要分析"为什么"和"意味着什么"
- 受众：面向技术决策者和开发者
- 风格：不要罗列bullet points，不像个文章的样子。除非必要，尽量不用bullet points，用通顺的段落来组织。平实准确简练，不要起高调，不要乱打比方，不要啰嗦讲废话。原则上一件事只讲一遍，不要反复重复

参考风格：类似 Gartner 分析报告或 ThoughtWorks 技术雷达
```

---

## Other Ideas and Additional Notes

```
无
```
