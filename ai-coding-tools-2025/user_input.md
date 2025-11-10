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
ai-coding-tools-2025
```

**Research Topic and Core Questions**:

```
我想研究 2024-2025 年 AI 编程工具的市场格局。

核心问题：
1. 当前市场上主流的 AI 编程工具有哪些？
2. 它们各自的技术特点和定位是什么？
3. 市场呈现出什么样的竞争格局和趋势？

这个研究对于理解 AI 编程工具的发展方向、帮助开发者选择合适的工具具有重要意义。
```

**Preliminary Direction and Insights**:

```
根据我的初步了解，AI 编程工具可能包括：
- 代码补全类工具（如 GitHub Copilot）
- AI 编程助手（如 Cursor、Claude Code）
- 代码审查和质量工具

我假设这个市场正在快速演进，新工具不断涌现，技术路线可能有显著差异。
我希望通过这个研究验证这些假设，并发现我尚未注意到的新趋势。
```

---

## Phase One: Data Collection

**Data Sources**:

```
1. Product Hunt - 搜索 AI coding、AI programming 等关键词，找到相关工具
2. GitHub Trending - 查看 AI 编程相关的热门项目
3. Hacker News - 搜索相关讨论
4. 技术博客和评测文章（如 The Verge, TechCrunch）
5. 各工具的官方网站和文档
```

**Data Collection Objectives**:

```
对于每个 AI 编程工具，需要收集：
- 基本信息：名称、开发商、发布时间
- 核心功能：主要用途和特性
- 技术路线：使用的 AI 模型、技术架构
- 定价模式：免费/付费、价格区间
- 用户反馈：主要评价和使用场景
- 最新动态：2024-2025 的更新和发展

详细程度：每个工具收集 200-500 字的结构化信息即可，不需要完整文档。
```

**Data Collection Process Design**:

```
并行收集多个数据源，然后去重合并：
1. 同时从 5 个数据源收集信息
2. 对收集到的工具列表进行去重（同一工具可能在多个来源出现）
3. 对于重复的工具，合并信息
4. 时间范围：重点关注 2024-2025 年的信息，但也包含重要的历史背景
```

**Data Storage Format**:

```
JSON 格式，每个工具一个 JSON 文件，包含标准字段：
{
  "name": "工具名称",
  "developer": "开发商",
  "release_date": "发布时间",
  "category": "类别",
  "core_features": ["功能1", "功能2"],
  "tech_stack": "技术栈描述",
  "pricing": "定价信息",
  "user_feedback": "用户反馈摘要",
  "recent_updates": "最近更新"
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
1. 分类统计：
   - 按功能类别分类（代码补全、AI 助手、代码审查等）
   - 按技术路线分类（使用的 AI 模型类型）
   - 按定价模式分类（开源/闭源、免费/付费）

2. 趋势分析：
   - 识别 2024-2025 年的新兴工具和趋势
   - 对比与 2023 年的变化

3. 特征对比：
   - 比较不同类别工具的核心差异
   - 识别各工具的独特卖点

4. 市场格局分析：
   - 识别市场领导者和挑战者
   - 分析竞争态势
```

**Analysis Process Design**:

```
两阶段分析：
1. 第一阶段：对每个工具进行分类标注，统计各类别的数量和分布
2. 第二阶段：进行深度对比分析，识别趋势和竞争格局
```

**Analysis Results Storage**:

```
Markdown 文档，包含：
- classification.md - 分类统计结果
- comparison.md - 特征对比表
- trends.md - 趋势分析
- market-landscape.md - 市场格局分析
```

---

## Phase Three: Report Generation

**Report Format**:

```
Markdown文档
```

**Report Structure**:

```
1. 执行摘要（1-2 页）
   - 研究背景
   - 主要发现（3-5 个要点）
   - 关键结论

2. 市场概览
   - 工具数量和分布
   - 主要类别说明

3. 分类分析
   - 按功能类别的详细分析
   - 按技术路线的分析
   - 按定价模式的分析

4. 竞争格局
   - 市场领导者
   - 新兴挑战者
   - 竞争态势图

5. 趋势洞察
   - 2024-2025 年的主要趋势
   - 技术演进方向
   - 市场发展预测

6. 结论和建议
   - 对开发者的选择建议
   - 对投资者的参考意见

7. 附录
   - 完整工具列表
   - 数据来源说明
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
