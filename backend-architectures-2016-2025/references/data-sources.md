# 数据源说明

## 概述

本研究使用多个高质量数据源进行并行收集，覆盖经典理论、工业实践、开源案例和社区讨论，确保全面理解后端架构的理论基础与实践权衡。

---

## 主要数据源

### 1. 经典著作与论文

**用途**：获取架构的理论基础、思想渊源和权威定义

**重点资源**：（包括但不限于）
- 《Domain-Driven Design》（Eric Evans, 2003）
- 《Implementing Domain-Driven Design》（Vaughn Vernon）
- 《Clean Architecture》（Robert C. Martin）
- 《Building Microservices》（Sam Newman）
- 《Monolith to Microservices》（Sam Newman）
- 《Microservices Patterns》（Chris Richardson）
- 《Patterns of Enterprise Application Architecture》（Martin Fowler）
- 《Enterprise Integration Patterns》
- 《Reactive Design Patterns》
- Alistair Cockburn 的六边形架构论文

**收集重点**：
- 架构提出的背景和动机
- 核心思想和设计原则
- 适用场景和局限性

---

### 2. 技术会议与行业报告

**主要来源**：（包括但不限于）
- QCon/InfoQ（架构专题、案例研究、趋势报告）
- ThoughtWorks 技术雷达（2016-2025 历年对比）
- GOTO Conference（架构设计专题）
- Gartner/Forrester 报告（架构趋势分析）

**收集重点**：
- 架构实践的成熟度和采纳情况
- 行业趋势和未来方向
- 专家对各架构的评价

---

### 3. 大厂工程博客与案例

**主要来源**：（包括但不限于）
- Netflix（微服务、Chaos Engineering）
- Uber（微服务演进、领域模型）
- Airbnb（SOA 到微服务的演进）
- Shopify（模块化单体实践）
- Spotify（组织与架构协同）
- Amazon/AWS（服务化架构）
- Google/GCP（分布式系统、SRE）
- Meta（大规模单体与服务化）
- Cloudflare（边缘计算架构）
- Microsoft（Azure 云架构模式）

**收集重点**：
- 架构选型的业务背景
- 演进过程和关键决策点
- 遇到的问题和解决方案
- 性能、成本、组织等多维度权衡

---

### 4. 社区与实践经验

**主要来源**：（包括但不限于）
- Hacker News（架构讨论、案例分享）
- Reddit r/microservices（微服务实践）
- Stack Overflow（实现问题和解决方案）
- Dev.to（架构博文）
- 掘金、少数派、InfoQ 中文

**收集重点**：
- 开发者对各架构的真实评价
- 常见的坑和反模式
- 实施难点和经验教训

---

### 5. 开源与参考实现

**主要来源**：（包括但不限于）
- awesome-architecture、awesome-microservices、awesome-ddd、awesome-clean-architecture
- hexagonal-architecture、clean-architecture、modular-monolith、cqrs、event-sourcing 参考项目
- 各语言的 DDD 框架
- 事件驱动框架（Axon, EventStore）

**收集重点**：
- 模块划分和边界设计
- 依赖方向和控制流
- 常用技术栈和模式
- 部署形态

---

### 6. 官方文档与白皮书

**主要来源**：（包括但不限于）
- Spring、NestJS、ASP.NET、Django/FastAPI
- Dapr、Kafka、RabbitMQ、Temporal、Service Mesh（Istio, Linkerd）
- AWS Architecture Center、Azure Architecture Patterns、GCP Architecture Framework

**收集重点**：
- 框架对架构模式的支持
- 推荐的架构实践
- 技术选型指南

---

### 7. 各个架构范式的官方网站和文档

**用途**：获取架构范式的官方定义和权威解释

---

## 数据收集流程

### 1. 并行抓取与去重合并

1. 按"架构范式"建立初始清单（可能有遗漏，需注意识别）
2. 每个来源并行收集，然后去重（按名称与同义词映射，如：六边形=端口与适配器）
3. 聚合字段：时间线、实现要点、适用/不适用、案例与参考
4. 标注可信度与时效性（高/中/低）与证据类型（一手实践/二手评述）
5. 关注 2016-2025 的材料，必要时补充历史脉络

### 2. 质量要求

- **准确性**：信息来自权威或可信来源
- **完整性**：每个架构 300-800 字的结构化信息
- **深度性**：理解思想渊源，关注"为什么"和"权衡点"
- **时效性**：优先收集 2016-2025 年的信息
- **可追溯性**：记录信息来源，标注证据类型

---

## 特殊说明

### 架构范式的识别

1. **识别遗漏的架构范式**：初始清单可能不完整，发现新的架构范式时及时补充
2. **识别架构的变体和组合**：如"DDD + CQRS/ES"、"模块化单体 + 六边形架构"
3. **注意同义词和别名**：确保去重准确，统一术语表述
