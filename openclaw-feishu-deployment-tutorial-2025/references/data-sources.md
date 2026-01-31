# 数据源清单

## 官方文档（优先级：高）

### 1. OpenClaw 安装向导
- **URL**: https://clawd.org.cn/start/wizard
- **内容**: 完整的本地安装步骤
- **采集要点**: 环境要求、依赖项、配置方法、步骤详解
- **输出文件**: `installation-guide-raw.md`

### 2. OpenClaw 飞书对接文档
- **URL**: https://clawd.org.cn/channels/feishu
- **内容**: 飞书机器人对接教程
- **采集要点**: 飞书开放平台操作、OpenClaw 配置、权限设置、测试方法
- **输出文件**: `feishu-integration-raw.md`

### 3. OpenClaw 官方网站
- **URL**: https://clawd.org.cn
- **内容**: 项目介绍、功能概览
- **采集要点**: 项目定位、核心功能、支持的 AI 模型、支持的聊天渠道
- **输出文件**: `project-overview.md`

## 补充信息（优先级：中）

### 4. 项目背景资料
- **来源**: 技术博客、知乎、CSDN 等
- **搜索关键词**: "OpenClaw"、"ClawdBot"、"Peter Steinberger"、"开源 AI 助手"
- **采集要点**:
  - OpenClaw 的更名历程（ClawdBot → Moltbot → OpenClaw）
  - 创始人 Peter Steinberger 与项目愿景
  - 项目热度与社区规模
- **输出文件**: `project-background.md`

### 5. 常见问题与注意事项
- **来源**: GitHub Issues、社区讨论、技术博客
- **采集要点**:
  - 安装过程中的常见错误与解决方案
  - 飞书对接的常见问题
  - 安全注意事项
- **输出文件**: `faq-and-tips.md`

## 数据存储格式

所有采集结果以 Markdown 格式存储在 `data/01.materials/` 目录下。

## 采集流程

### 第一阶段：官方文档爬取
1. 爬取 https://clawd.org.cn/start/wizard 获取安装指南
2. 爬取 https://clawd.org.cn/channels/feishu 获取飞书对接教程
3. 爬取 https://clawd.org.cn 获取项目概览
4. 提取关键信息，保持原始结构

### 第二阶段：补充信息收集
1. 通过 Web 搜索收集项目背景资料
2. 收集用户反馈和常见问题
3. 整理安全注意事项
