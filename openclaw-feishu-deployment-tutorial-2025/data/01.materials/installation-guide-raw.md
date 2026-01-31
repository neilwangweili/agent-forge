# OpenClaw 官方安装指南

## 来源
URL: https://clawd.org.cn/start/wizard
采集时间: 2026-02-01

## 内容

### 入门向导 (CLI)

入门向导是在 macOS、Linux 或 Windows（通过 WSL2；强烈推荐）上设置 OpenClaw 的推荐方式。它在一个引导流程中配置本地网关或远程网关连接，以及通道、技能和工作区默认设置。

**主要入口点：**

```bash
openclaw-cn onboard
```

**后续重新配置：**

```bash
openclaw-cn configure
```

**推荐设置：** 设置一个 Brave Search API 密钥，以便代理可以使用 `web_search`（`web_fetch` 不需要密钥即可工作）。最简单的路径：`openclaw-cn configure --section web`，它会存储 `tools.web.search.apiKey`。

---

## 快速启动 vs 高级

向导从快速启动（默认）vs 高级（完全控制）开始。

**快速启动**保持默认设置：
- 本地网关（回环）
- 工作区默认（或现有工作区）
- 网关端口 18789
- 网关认证令牌（自动生成，即使是回环）
- Tailscale 暴露关闭
- Telegram + WhatsApp 私信默认为白名单（系统会提示您输入电话号码）

**高级**暴露每一步（模式、工作区、网关、通道、守护进程、技能）。

---

## 向导的作用

**本地模式（默认）**引导您完成以下步骤：

1. **模型/认证**（OpenAI Code (Codex) 订阅 OAuth、Anthropic API 密钥（推荐）或 setup-token（粘贴），以及 MiniMax/GLM/Moonshot/AI 网关选项）
2. **工作区位置** + 引导文件
3. **网关设置**（端口/绑定/认证/tailscale）
4. **提供商**（Telegram、WhatsApp、Discord、Google Chat、Mattermost（插件）、Signal）
5. **守护进程安装**（LaunchAgent / systemd 用户单元）
6. **健康检查**
7. **技能**（推荐）

**远程模式**仅配置本地客户端以连接到其他地方的网关。它不会在远程主机上安装或更改任何内容。

---

## 模型/认证选项

- **Anthropic API 密钥（推荐）**：如果存在则使用 `ANTHROPIC_API_KEY` 或提示输入密钥，然后保存以供守护进程使用。
- **Anthropic OAuth（Claude Code CLI）**：在 macOS 上向导检查钥匙串项目 "Claude Code-credentials"；在 Linux/Windows 上重用 `~/.claude/.credentials.json`。
- **Anthropic 令牌（粘贴 setup-token）**：在任何机器上运行 `claude setup-token`，然后粘贴令牌。
- **OpenAI Code（Codex）订阅**：如果 `~/.codex/auth.json` 存在，向导可以重用它。
- **OpenAI API 密钥**：如果存在则使用 `OPENAI_API_KEY` 或提示输入密钥。
- **OpenCode Zen（多模型代理）**：提示输入 `OPENCODE_API_KEY`。
- **MiniMax M2.1**：配置自动写入。
- **Moonshot（Kimi K2）**：配置自动写入。
- **跳过**：尚未配置认证。

OAuth 凭据位于 `~/.openclaw/credentials/oauth.json`；认证配置文件位于 `~/.openclaw/agents/<agentId>/agent/auth-profiles.json`。

---

## 工作区

- 默认 `~/clawd`（可配置）
- 提供代理引导仪式所需的工区文件
- 完整工作区布局 + 备份指南：代理工作区

---

## 网关

- 端口、绑定、认证模式、tailscale 暴露
- **认证建议**：即使是回环也要保持令牌，这样本地 WS 客户端必须进行认证
- 仅当您完全信任每个本地进程时才禁用认证
- 非回环绑定仍需要认证

---

## 通道配置

- **WhatsApp**：可选 QR 登录
- **Telegram**：机器人令牌
- **Discord**：机器人令牌
- **Google Chat**：服务账户 JSON + webhook 受众
- **Mattermost（插件）**：机器人令牌 + 基础 URL
- **Signal**：可选 signal-cli 安装 + 账户配置
- **iMessage**：本地 imsg CLI 路径 + 数据库访问
- **私信安全**：默认为配对。第一次私信发送代码；通过 `openclaw-cn pairing approve <channel> <code>` 批准或使用白名单。

---

## 守护进程安装

- **macOS**：LaunchAgent 需要登录的用户会话；对于无头模式，使用自定义 LaunchDaemon（未提供）。
- **Linux（和通过 WSL2 的 Windows）**：systemd 用户单元。向导尝试通过 `loginctl enable-linger <user>` 启用持久化，以便网关在注销后保持运行。
- **运行时选择**：Node（推荐；WhatsApp/Telegram 必需）。不推荐使用 Bun。

---

## 健康检查

- 启动网关（如果需要）并运行 `openclaw-cn health`
- 提示：`openclaw-cn status --deep` 将网关健康探测添加到状态输出

---

## 技能（推荐）

- 读取可用技能并检查要求
- 让您选择节点管理器：npm / pnpm（不推荐 bun）
- 安装可选依赖项（一些在 macOS 上使用 Homebrew）

---

## 非交互模式

使用 `--non-interactive` 自动化或脚本化入门：

```bash
openclaw-cn onboard --non-interactive \
  --mode local \
  --auth-choice apiKey \
  --anthropic-api-key "$ANTHROPIC_API_KEY" \
  --gateway-port 18789 \
  --gateway-bind loopback \
  --install-daemon \
  --daemon-runtime node \
  --skip-skills
```

添加 `--json` 以获得机器可读摘要。

---

## 向导写入的内容

`~/.openclaw/openclaw.json` 中的典型字段：

- `agents.defaults.workspace`
- `agents.defaults.model` / `models.providers`
- `gateway.*`（模式、绑定、认证、tailscale）
- `channels.telegram.botToken`、`channels.discord.token`、`channels.signal.*`、`channels.imessage.*`
- 通道白名单
- `skills.install.nodeManager`
- `wizard.lastRunAt`、`wizard.lastRunVersion`、`wizard.lastRunCommit`、`wizard.lastRunCommand`、`wizard.lastRunMode`

WhatsApp 凭据位于 `~/.openclaw/credentials/whatsapp/<accountId>/` 下。
会话存储在 `~/.openclaw/agents/<agentId>/sessions/` 下。

---

## 一键安装命令

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
# npm 全局安装
npm install -g openclaw-cn@latest

# pnpm 全局安装
pnpm add -g openclaw-cn@latest

# 使用国内镜像
npm install -g openclaw-cn@latest --registry https://registry.npmmirror.com

# 运行向导
openclaw-cn onboard
```

---

## 系统要求

- **Node.js**：v22.0.0 或更高版本
- **操作系统**：macOS、Linux、Windows（通过 WSL2）
- **包管理器**：npm（推荐）或 pnpm

---

## 相关文档

- macOS 应用入门：入门
- 配置参考：网关配置
- 提供商：WhatsApp、Telegram、Discord、Google Chat、Signal、iMessage
- 技能：技能、技能配置
