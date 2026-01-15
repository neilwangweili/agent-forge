# Claude Skills 机制解析

## 数据来源

### 官方文档与技术博客
- Claude Code 官方文档: https://code.claude.com/docs/zh-CN/skills
- [Claude 新王牌 "Skills" 深度解析：让你的 AI 秒变行业专家，告别重复劳动](https://zhuanlan.zhihu.com/p/1966598753134842902)
- [解锁AI的"职业技能树"：Claude Skills深度技术解析——从原理到实战的完全指南](https://blog.csdn.net/u012094427/article/details/153583017)
- [Claude Code Agent Skills 深度解析：从加载到执行的完整生命周期](https://zhuanlan.zhihu.com/p/1984015383276041355)
- [LLM - 从 Claude Code Agent Skills 看通用代理的现实路径：设计理念、工程实现与未来形态](https://blog.csdn.net/yangshangwei/article/details/156064042)
- [Claude Skills 详解：从入门到精通，彻底搞懂AI编程新范式](https://aicoding.csdn.net/695008d9836da321448833b1.html)
- [Claude Skills的简介(并对比Projects/MCP/Custom)](https://blog.csdn.net/qq_41185868/article/details/153884153)
- [Claude Code Skill 设计机制深度分析](https://www.53ai.com/news/LargeLanguageModel/2025122234901.html)

## 核心内容

### Claude Skills 的定义

Claude Skills 是将重复性工作流程（如公司品牌风格、代码规范、报告格式）打包成可复用的指令，让 Claude 能自动、可靠地完成任务，无需每次都重复提醒。本质上是一种**可执行知识包**，能将专业知识、标准操作流程(SOP)、最佳实践沉淀为可执行的技能模块。

**核心定位**:
- Claude Skills 就像是给 Claude 安装的 "专家记忆包"，能将它从一个通用 AI 变为精准执行特定任务的专家
- 一个 Skill 就是一个带说明书 (SKILL.md) 的文件夹
- Skills 本质上是 prompt 模板，通过注入对话上下文和修改执行上下文来工作

### 渐进式加载机制 (Progressive Disclosure)

Claude Skills 的核心创新在于**渐进式披露**机制，通过三级加载(元数据→核心指令→按需资源)显著优化上下文窗口利用率，降低 80-95% 的 Token 消耗。

#### 三层加载架构

**Level 1: 元数据层**
- 仅加载 `name` 和 `description`（约100词）
- 始终加载到上下文
- 用于决定何时触发技能
- 初始加载时，每个 Skill 只占用几十个 Token 来存储其元数据

**Level 2: 核心指令层 (SKILL.md)**
- 详细工作流程和指南（<5k词）
- 仅在技能激活时加载
- 包含完整的 prompt 内容和执行指南

**Level 3: 资源层**
- `scripts/`：可执行脚本
- `references/`：参考文档
- `assets/`：模板和资源文件
- 无限制大小
- 脚本可不加载直接执行

#### 工作原理

Skills 其实就是一个文件夹，里面包含了 Claude 在需要时可以加载的指令、脚本和资源等。只有当 Claude 认为某个 Skill 和当前任务相关时，它才会启用，按需加载。

这种设计使得 Skills 的 token 消耗与实际使用成正比，而非与安装数量成正比。按需加载技能插件，而不是全部加载到上下文中，有效减少了占用上下文的长度。

**技术优势**:
- 用户可以安装大量 Skills 而不会影响性能
- Claude 会根据任务需求智能地选择和加载相应的技能包
- 解决了 LLM 的核心限制：上下文窗口有限
- 避免了将所有可能需要的知识预先塞入 prompt

### 模型自主调用机制 (Model-Invoked)

Skill 的核心设计理念是 **model-invoked（模型自主调用）**，与 Slash Commands 的 user-invoked（用户显式调用）形成鲜明对比。

#### 核心特点

**自主识别与触发**:
- Agent Skills 的最大特点是模型调用（Model-invoked）
- 用户不需要显式输入命令
- Claude 根据对话内容自动判断是否需要启用某个 Skills
- Skills 没有像 Slash Commands 那样「输入固定 /xxx 就必定执行」的触发机制
- 主要由模型依 description 做相似度判断来决定要不要启用

**技术实现**:
- 根据分析，没有算法路由或意图分类
- 完全是纯 LLM 推理
- 模型理解任务上下文，自主判断是否需要某个技能

**用户体验优势**:
- 用户体验更自然：无需记忆命令，自然语言即可触发
- 知识可复用：团队专业知识被编码和共享
- 上下文高效：按需加载，避免 prompt 膨胀

### Skills 的三种部署类型

**Personal Skills (个人技能)**:
- 安装位置: 用户目录
- 作用范围: 所有项目
- 适用场景: 个人工作习惯、通用能力

**Project Skills (项目技能)**:
- 安装位置: 项目目录
- 作用范围: 特定项目
- 适用场景: 项目特定的工作流程、团队协作标准

**Plugin Skills (插件技能)**:
- 来源: 社区共享
- 特点: 标准化、可复用
- 适用场景: 通用技能包

### Skills 的文件结构

一个完整的 Skill 包含:

```
skill-name/
├── SKILL.md              # 核心指令文件 (YAML frontmatter + 详细说明)
├── scripts/              # 可执行脚本
│   └── *.py, *.sh       # Python、Shell 等脚本
├── references/           # 参考文档
│   └── *.md, *.json     # 领域知识、规范
└── assets/               # 模板和资源
    └── templates/       # 模板文件
```

**SKILL.md 结构**:
```markdown
---
name: skill-name
description: 技能简短描述(用于元数据层)
---

# 详细的技能说明

## 你的角色
[定义智能体的身份和总体职责]

## 核心工作内容
[详细的任务描述、策略、流程]

## 输出要求
[明确的产出标准]
```

### Skills 与其他机制的对比

#### Skills vs Slash Commands
- **触发方式**: Skills 是模型自主调用，Slash Commands 是用户显式调用
- **复杂度**: Skills 更适合复杂的多步骤能力，Commands 适合简单操作
- **自然度**: Skills 提供更自然的用户体验

#### Skills vs MCP (Model Context Protocol)
- **知识类型**: Skills 教会 Claude "如何做" 一件事（内部知识和流程），MCP 让 Claude "去做" 一件事（调用外部数据或执行动作）
- **Token 效率**: Skills 通过 "渐进式披露" 机制实现了极高的 Token 效率。相比之下，一些 MCP 的实现可能需要在提示中加载数万 Token 的 API 文档和定义
- **适用场景**: Skills 把"人类流程/SOP"转为可触发的模块，擅长程序化写作、格式化、合规、数据整理等"内部可编码"的流程

#### Skills vs Projects
- **范围**: Projects 针对单个项目的完整知识库，Skills 是可复用的技能模块
- **粒度**: Skills 更细粒度、更模块化

### 可执行代码支持

除了文本指令，Skills 还可以捆绑可执行的 Python 脚本。对于需要确定性和高可靠性的任务，让 Claude 直接运行预先写好的代码比实时生成代码更高效、更可靠。

**设计理念**: 把"知识"与"执行"解耦，知识放在 Markdown，执行通过脚本和代码解释器完成，两者由大模型自己编排。

### 路径解析机制

通过逆向工程分析，Claude 通过 tool response 被显式告知 Base Path，而不是自己推断。这是一个优雅的设计，将路径解析的责任从 LLM 转移到了运行时。

## 关键引用

### 关于渐进式披露的价值

> "Claude Skills 的核心创新在于'渐进式披露'机制，通过三级加载(元数据→核心指令→按需资源)显著优化上下文窗口利用率，降低80-95%的Token消耗。"
>
> 来源: [解锁AI的"职业技能树"：Claude Skills深度技术解析](https://blog.csdn.net/u012094427/article/details/153583017)

### 关于模型自主调用

> "Skill 的核心设计理念是 model-invoked（模型自主调用），与 Slash Commands 的 user-invoked（用户显式调用）形成鲜明对比。根据分析，没有算法路由或意图分类，完全是纯 LLM 推理。"
>
> 来源: [LLM - 从 Claude Code Agent Skills 看通用代理的现实路径](https://blog.csdn.net/yangshangwei/article/details/156064042)

### 关于可执行知识

> "将 '新人指南''最佳实践' 沉淀为可执行的技能包，而非散落的文档，可提升一致性、可复用性与审计可见性。"
>
> 来源: [Claude 新王牌 "Skills" 深度解析](https://zhuanlan.zhihu.com/p/1966598753134842902)

### 关于设计哲学

> "传统的提示词工程就像教AI'临时抱佛脚'，而Skills系统则是给AI建立了一套'职业技能树'——可以随时装载、系统化、可复用的专业能力模块。"
>
> 来源: [解锁AI的"职业技能树"：Claude Skills深度技术解析](https://blog.csdn.net/u012094427/article/details/153583017)

### 关于现代 agents 的本质

> "现代agents工作不是因为巧妙的工程，而是因为模型被训练成为agent。"
>
> 来源: [LLM - 从 Claude Code Agent Skills 看通用代理的现实路径](https://blog.csdn.net/yangshangwei/article/details/156064042)

## 实践案例

### 团队协作标准化

当 Skill 被安装在团队工作空间时，团队成员的协作获得了标准化——不是通过制度文档，而是通过可执行的技能包。这是一种全新的知识共享与协作模式。

### 个人效率提升

个人可以将自己的工作流程、代码规范、写作风格封装成 Personal Skills，在所有项目中复用，大幅提升工作效率和一致性。

### 领域专家知识沉淀

领域专家可以将专业知识、判断标准、最佳实践封装成 Skills，让 AI 获得领域专家的能力，降低专业服务的门槛。

## 采集者注释

### 核心洞察

1. **渐进式加载是关键创新**: 通过三层加载机制，Skills 解决了 LLM 上下文窗口有限的核心问题，使得可以安装大量技能而不影响性能。

2. **模型自主调用体现智能**: 与传统的显式命令不同，Skills 依靠模型理解上下文自主判断是否需要某个技能，这体现了真正的智能。

3. **知识与执行解耦**: Skills 将"知识"（Markdown 中的说明）与"执行"（scripts 中的代码）分离，由 LLM 自己编排，是一种优雅的设计。

4. **可执行知识的具体化**: Skills 是"可执行知识"概念的具体实现——知识不再只是文档，而是可以被安装、加载、执行的能力包。

5. **协作模式的革新**: 团队通过共享 Skills 而非文档来标准化协作，这是知识共享模式的根本性转变。

### 与研究主题的关联

Skills 机制完美体现了研究主题中的核心洞察:

- **知识的可执行性**: Skills 将知识封装为可安装、可执行的模块
- **协作的标准化**: 通过 Project Skills 实现团队协作标准化
- **声明式编程**: SKILL.md 使用声明式语言描述"做什么"而非"怎么做"
- **智能运行时**: Claude Code 理解 Skills 并智能执行

### 待深入的问题

1. Skills 的"第一性原理"是什么？为什么选择这种设计？
2. Skills 与 Agent Blueprint 的关系是什么？本质上是否是同一个概念？
3. 渐进式加载机制的理论基础是什么？是否有更广泛的适用性？
4. 模型自主调用的可靠性如何保证？如何避免误触发或漏触发？
