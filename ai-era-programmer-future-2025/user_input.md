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
ai-era-programmer-future-2025
```

**Research Topic and Core Questions**:
```
研究 AI 时代程序员的职业前景与角色转变。

核心问题:
1. 以 Gemini 3 为代表的最新 AI 编程能力达到了什么水平？
2. 为什么很多人认为程序员要失业？这些观点的依据是什么？
3. 为什么"能开发"就必须"能维护"？AI 在代码维护方面有什么局限？
4. 程序员的角色如何向架构师转变？架构决策为什么不能被 AI 取代？

研究意义:
帮助程序员理性看待 AI 的冲击，理解自身核心价值，明确能力转型方向。最终产出一篇公众号文章，立场是"AI 不会让程序员失业，而是重新定义程序员的角色"。
```

**Preliminary Direction and Insights**:
```
初步假设:
- Gemini 3 等最新 AI 在编程能力上有质的飞跃，能独立完成复杂编码任务
- 恐慌来源于：AI 编码能力提升、Vibe Coding 现象（非程序员也能写程序）、媒体渲染
- 软件工程的本质是维护而非创造，80% 的时间在维护代码
- AI 生成代码存在问题：上下文理解局限、技术债务累积、缺乏全局视野
- "能写代码 ≠ 能维护代码系统"是关键洞察
- 架构决策涉及业务理解、非功能性需求、团队能力匹配、历史包袱等，AI 难以替代
- 程序员的角色从"怎么实现"转向"实现什么、为什么这样实现"
- AI 是放大器，不是替代品；淘汰的是"只会写代码"的程序员

我希望通过研究验证这些假设，收集数据和案例支撑论点。
```

---

## Phase One: Data Collection

**Data Sources**:
```
1. Gemini 3 相关信息:
   - Google 官方发布信息、技术博客
   - 技术媒体评测（The Verge、TechCrunch、Ars Technica）
   - 开发者社区反馈（Hacker News、Reddit r/programming）

2. AI 编程工具与能力:
   - Cursor、Claude Code、GitHub Copilot 等工具的最新能力
   - AI 编程 benchmark 和评测数据
   - Vibe Coding 相关讨论和案例

3. 程序员失业论的观点来源:
   - 科技公司高管/投资人的预测言论
   - 媒体报道和舆论走向
   - 行业调研报告（如 Stack Overflow Developer Survey、GitHub Octoverse）

4. 软件工程与代码维护:
   - 软件维护成本研究（经典数据：80% 时间在维护）
   - AI 生成代码的质量问题案例
   - 技术债务、代码腐化相关研究

5. 架构决策与程序员角色:
   - 架构师能力模型
   - 架构决策的复杂性（ADR、Trade-off Analysis）
   - 大厂工程实践（Google、Netflix、Uber 等）
```

**Data Collection Objectives**:
```
对每个核心问题收集:
- 事实数据：能力指标、市场数据、调研结果
- 典型案例：成功案例、失败案例、反例
- 专家观点：行业专家的洞察（支持和反对的观点都要）
- 常见误区：需要澄清的认知偏差

详细程度：每个主题收集 300-500 字的结构化信息，重点是数据和案例，避免空洞观点。
```

**Data Collection Process Design**:
```
按主题并行收集:
1. Gemini 3 能力与 AI 编程现状
2. "程序员失业论"的来源与论据
3. 软件维护的本质与 AI 局限
4. 架构决策的不可替代性

时间范围：重点关注 2024-2025 年的信息。
标注观点来源的可信度（官方数据/权威研究/行业共识/个人观点）。
```

**Data Storage Format**:
```
JSON 格式，按主题组织，包含：事实数据、案例、专家观点、来源链接等字段。
```

**Existing Reference Materials**:
```
无
```

---

## Phase Two: Analysis

**Analysis Methods**:
```
1. 论点-论据匹配:
   - 整理"程序员失业论"的主要论点及其依据
   - 分析每个论点的逻辑漏洞或局限性

2. 对比分析:
   - AI 编码能力 vs 代码维护能力
   - 写代码 vs 架构决策的复杂度差异
   - Vibe Coding 产物 vs 可维护的生产代码

3. 因果链分析:
   - 为什么"能开发"必须"能维护"
   - 为什么架构决策不能被 AI 取代

4. 案例分析:
   - AI 快速搭建 vs 长期维护的差距案例
   - 架构决策失误的代价案例
```

**Analysis Process Design**:
```
两阶段分析:
1. 分主题深度分析：提取关键发现、数据支撑、典型案例
2. 整合论证：构建完整论证链，从 Gemini 3 → 恐慌来源 → 维护能力 → 架构师角色 → 结论
```

**Analysis Results Storage**:
```
Markdown 文档，按文章结构组织分析结果。
```

---

## Phase Three: Report Generation

**Report Format**:
```
Markdown 文档（适合公众号发布）
```

**Report Structure**:
```
1. 引子：Gemini 3 带来的震撼
   - Gemini 3 的能力展示
   - AI 编程能力的质变
   - 引出问题：程序员真的要被取代了吗？

2. 恐慌的来源：为什么很多人认为程序员要失业
   - AI 编码能力的飞速提升
   - Cursor、Claude Code、GitHub Copilot 等工具的普及
   - Vibe Coding 现象
   - 媒体渲染和耸人听闻的预测

3. 被忽视的真相：开发能力 = 维护能力
   - 软件工程的本质：80% 的时间在维护
   - AI 生成代码的问题（上下文局限、技术债务、碎片化方案）
   - 能写代码 ≠ 能维护代码系统
   - 案例：用 AI 快速搭建 vs 长期维护的差距

4. 程序员的新角色：人人都是架构师
   - 架构决策为什么不能被 AI 取代（业务理解、非功能性需求、团队匹配、历史包袱）
   - 程序员的核心能力转变（从"怎么实现"到"实现什么、为什么这样实现"）
   - AI 是放大器，不是替代品

5. 结语：拥抱变化，重新定位
   - 焦虑是正常的，但方向比焦虑重要
   - 程序员需要提升的能力（系统思维、AI 协作、业务理解）
   - AI 淘汰的不是程序员，而是"只会写代码"的程序员
```

**Writing Style**:
```
公众号文章风格:
- 语言：专业但不晦涩，有观点但不偏激
- 篇幅：3000-4000 字
- 开头：用 Gemini 3 的震撼引入，抓住读者注意力
- 论证：多用具体例子和类比，避免空洞说教
- 基调：不贩卖焦虑，也不盲目乐观，保持理性分析
- 结尾：给出明确的方向和行动建议
- 风格：用通顺的段落组织，除非必要尽量不用 bullet points。平实准确简练，不要起高调，不要乱打比方，不要啰嗦讲废话

目标读者：程序员、技术从业者、对 AI 发展感兴趣的人群
```

---

## Other Ideas and Additional Notes

```
关键要求:

1. 立场明确：文章立场是"AI 不会让程序员失业，而是重新定义程序员的角色"，但论证要客观理性，不能回避 AI 的强大
2. 数据支撑：用数据和案例说话，避免空洞的鸡汤或口号
3. 反直觉洞察：突出"能写代码 ≠ 能维护代码"这个被忽视的关键点
4. 可操作性：结尾给出具体的能力提升方向，而不是泛泛而谈
5. 时效性：以 Gemini 3 为切入点，体现文章的时效性和热点关联
6. 不贩卖焦虑：承认 AI 的冲击是真实的，但焦点放在"如何应对"而非"多么可怕"

写作忌讳:
- 不要写成技术文档或学术论文
- 不要罗列 bullet points，要有文章的流畅感
- 不要用"首先、其次、最后"这种机械结构
- 不要反复重复同一个观点
```
