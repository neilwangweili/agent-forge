# OpenClaw 项目概览

## 来源
URL: https://clawd.org.cn
采集时间: 2026-02-01

## 内容

### OpenClaw - 真正能做事的 AI

OpenClaw 是一款开源免费的个人 AI 助手，能够清理收件箱、发送邮件、管理日历、办理登机手续。通过飞书、WhatsApp、Telegram 或任何你常用的聊天应用与其交互。

---

## 项目定位

OpenClaw 是一个开源、自托管的个人 AI 助理，可以直接在你的计算机上运行。它并非运行在云端的 SaaS 服务，而是部署在你自己的计算机上，让你能够完全掌控自己的数据与工作流。

---

## 核心功能列表

### 运行在你的设备上
Mac、Windows 或 Linux。Anthropic、OpenAI 或本地模型。默认私有——你的数据属于你自己。

### 任意聊天应用
通过飞书、WhatsApp、Telegram、Discord、Slack 或 iMessage 与它对话。支持私聊和群聊。

### 持久记忆
记住你的一切并成为独一无二的你的 AI。你的偏好、你的上下文、你的 AI。

### 浏览器控制
它可以浏览网页、填写表单、从任何网站提取数据。

### 完整系统访问
读写文件、运行 Shell 命令、执行脚本。完全访问或沙箱模式——由你选择。

### 技能与插件
使用社区技能扩展或自己构建。它甚至可以自己编写技能。

---

## 支持的 AI 模型

OpenClaw 支持任何大型语言模型（LLM），包括：

- **Anthropic Claude** - Claude 系列模型（推荐）
- **OpenAI** - GPT 系列模型、OpenAI Code (Codex)
- **MiniMax** - MiniMax M2.1
- **Moonshot** - Kimi K2、Kimi Code
- **OpenRouter** - 多模型代理
- **Vercel AI 网关** - 多模型代理
- **OpenCode Zen** - 多模型代理
- **本地模型** - 支持自定义 AI 供应商

---

## 支持的聊天渠道

| 渠道 | 状态 |
|------|------|
| 飞书 | 已支持 |
| WhatsApp | 已支持 |
| Telegram | 已支持 |
| Discord | 已支持 |
| Slack | 已支持 |
| Signal | 已支持 |
| iMessage | 已支持 |
| Mattermost | 已支持 |

---

## 项目优势

### 1. 完全开源免费
- 基于 MIT 许可发布
- 本项目是 openclaw/openclaw 的中文版分支
- 定期与上游仓库保持同步

### 2. 数据隐私保障
- 运行在你自己的设备上
- 所有数据本地存储
- 不会上传到第三方云端

### 3. 灵活的部署方式
- 支持多种操作系统
- 支持多种安装方式（脚本、npm、pnpm、Docker）
- 支持本地和远程网关模式

### 4. 强大的自动化能力
- 执行系统命令
- 浏览网页和填写表单
- 管理文件和日历
- 发送邮件

### 5. 丰富的扩展生态
- 社区技能库
- 插件系统
- 可自定义开发技能

---

## 伴侣应用

- **macOS 菜单栏应用** - 快捷访问和语音唤醒
- **iOS 应用** - Canvas 支持 + 语音唤醒
- **Android 应用** - Canvas + 聊天 + 相机

---

## 一键安装

### macOS / Linux

```bash
# 自动安装 Node.js 和所有依赖
curl -fsSL https://clawd.org.cn/install.sh | bash

# 使用国内镜像
curl -fsSL https://clawd.org.cn/install.sh | bash -s -- --registry https://registry.npmmirror.com
```

### Windows (PowerShell)

```powershell
# 在 PowerShell 中运行
iwr -useb https://clawd.org.cn/install.ps1 | iex

# 使用国内镜像
iwr -useb https://clawd.org.cn/install.ps1 -OutFile install.ps1; ./install.ps1 -Registry https://registry.npmmirror.com
```

### npm / pnpm 安装

```bash
# 全局安装
npm install -g openclaw-cn@latest

# 运行向导
openclaw-cn onboard
```

---

## 关于本项目

- **项目名称**：OpenClaw 中文版
- **GitHub 仓库**：https://github.com/jiulingyun/openclaw-cn
- **上游仓库**：https://github.com/openclaw/openclaw
- **许可证**：MIT
- **最新版本**：v2026.1.31（2026/1/31）

---

## 相关链接

- 官方文档：https://clawd.org.cn
- GitHub：https://github.com/jiulingyun/openclaw-cn
- Releases：https://github.com/jiulingyun/openclaw-cn/releases
- 上游仓库：https://github.com/openclaw/openclaw
