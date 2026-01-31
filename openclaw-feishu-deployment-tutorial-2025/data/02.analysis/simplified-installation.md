# 简化后的安装步骤

## 准备工作

在开始之前，请确认以下几项：

1. **一台电脑**：Mac、Windows 或 Linux 均可
2. **一个 AI 模型的 API Key**：推荐使用 Anthropic 的 Claude API Key（相当于 AI 的"通行证"，需要在 Anthropic 官网注册获取）
3. **网络连接**：安装过程需要联网下载

> 注意：Windows 用户需要使用 PowerShell 执行安装命令，不要使用"命令提示符（CMD）"。

---

## 安装步骤

### 第一步：运行一键安装命令

打开终端（Mac/Linux）或 PowerShell（Windows），复制并粘贴以下命令，然后按回车键执行。

**Mac / Linux 用户**：

```bash
curl -fsSL https://clawd.org.cn/install.sh | bash -s -- --registry https://registry.npmmirror.com
```

**Windows 用户**：

```powershell
iwr -useb https://clawd.org.cn/install.ps1 -OutFile install.ps1; ./install.ps1 -Registry https://registry.npmmirror.com
```

这条命令会自动帮你安装 Node.js（OpenClaw 运行所需的底层工具）和 OpenClaw 本身。使用的是国内镜像，下载速度更快。

你会看到：终端中出现一系列安装进度信息，最后提示安装完成。

> 注意：安装过程可能需要几分钟，请耐心等待，不要中途关闭终端窗口。

---

### 第二步：验证安装是否成功

在终端中输入以下命令：

```bash
openclaw-cn --version
```

你会看到：终端显示一个版本号，例如 `v2026.1.31`。

> 注意：如果提示 `openclaw-cn: command not found`，说明安装路径没有被系统识别。请关闭终端窗口，重新打开一个新的终端窗口再试一次。如果仍然不行，参考下方"常见问题"中的解决办法。

---

### 第三步：运行设置向导

输入以下命令，启动 OpenClaw 的初始设置向导：

```bash
openclaw-cn onboard
```

向导会用交互式的问答方式，引导你完成所有配置。

你会看到：终端中出现一系列选择题和输入框。

---

### 第四步：选择"快速启动"模式

向导的第一个问题会让你选择模式。

**请选择"快速启动"（Quick Start）**。这个模式会自动帮你设好大部分配置，你只需要填入关键信息即可。

你会看到：向导继续往下走，询问你的 AI 模型认证信息。

---

### 第五步：填入 AI 模型的 API Key

向导会问你用哪个 AI 模型。

**推荐选择 "Anthropic API Key"**，然后粘贴你提前准备好的 Claude API Key。

你会看到：向导提示认证信息已保存，继续下一步。

> 注意：粘贴 API Key 时，终端可能不会显示你粘贴的内容（这是正常的安全行为），直接按回车确认即可。

---

### 第六步：完成向导并启动健康检查

向导会自动完成剩余的配置项（工作区、网关端口等），最后执行一次健康检查。

你会看到：终端显示健康检查结果，所有项目都是绿色的对勾或 "OK" 标识。

> 注意：如果健康检查出现红色的叉号，不要紧张。记下错误信息，参考下方"常见问题"或在社区寻求帮助。

---

### 第七步：确认 OpenClaw 正在运行

输入以下命令，查看运行状态：

```bash
openclaw-cn gateway status
```

你会看到：终端显示网关状态为 "running"（运行中）。

到这里，OpenClaw 已经在你的电脑上运行起来了。接下来可以继续配置飞书对接，让它成为你飞书里的 AI 助手。

---

## 常见问题

### 输入命令后提示 `openclaw-cn: command not found`

这是最常见的问题。原因是系统找不到 OpenClaw 的安装路径。

**解决步骤**：

1. 在终端输入 `npm config get prefix`，记下返回的路径
2. 打开你的 Shell 配置文件（Mac 用户通常是 `~/.zshrc`）
3. 在文件末尾添加一行：`export PATH="$PATH:上一步的路径/bin"`
4. 保存文件，关闭终端，重新打开终端再试

### 提示 Node.js 版本过低

OpenClaw 需要 Node.js v22.0.0 或更高版本。访问 [Node.js 官网](https://nodejs.org/) 下载最新版本安装即可。

### Mac 上安装时 `sharp` 报错

在终端输入以下命令后重试安装：

```bash
npm install -g node-gyp
```

### 之前安装过 Clawdbot 或 Moltbot

OpenClaw 曾经叫做 Clawdbot 和 Moltbot。如果之前装过旧版本，需要先清理：

```bash
npm uninstall -g clawdbot moltbot openclaw
npm cache clean --force
npm install -g openclaw-cn@latest
```
