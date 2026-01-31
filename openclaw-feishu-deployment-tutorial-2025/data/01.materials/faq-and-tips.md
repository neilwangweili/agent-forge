# 常见问题与注意事项

## 信息来源

- [OpenClaw(旧称ClawdBot/Moltbot)下载安装使用，详细的图文教程](https://apifox.com/apiskills/openclaw-installation-and-usage-guide/)
- [玩转OpenClaw｜OpenClaw（原 Clawdbot）接入飞书保姆级教程-腾讯云](https://cloud.tencent.com/developer/article/2625073)
- [保姆级 OpenClaw （原 Clawdbot）飞书对接教程-CSDN](https://blog.csdn.net/qq_31470439/article/details/157578441)
- [GitHub - AlexAnys/feishu-openclaw](https://github.com/AlexAnys/feishu-openclaw)
- [Troubleshooting - OpenClaw](https://docs.openclaw.ai/gateway/troubleshooting)
- [clawdbot-ansible/docs/troubleshooting.md](https://github.com/openclaw/clawdbot-ansible/blob/main/docs/troubleshooting.md)
- [GitHub Issues - openclaw/openclaw](https://github.com/openclaw/openclaw/issues)

---

## 安装常见问题

### 问题 1: `openclaw: command not found`

**现象**：
安装完成后，终端提示 `openclaw: command not found` 或 `openclaw-cn: command not found`。

**原因**：
npm 全局安装目录没有被加到系统的 PATH 环境变量中。

**解决方案**：
1. 找到 npm 的全局路径：
   ```bash
   npm config get prefix
   ```
2. 将该路径添加到 Shell 配置文件中（如 `~/.zshrc` 或 `~/.bashrc`）：
   ```bash
   export PATH="$PATH:$(npm config get prefix)/bin"
   ```
3. 重启终端或执行 `source ~/.zshrc` 使其生效。

---

### 问题 2: Node.js 版本过低

**现象**：
安装或运行时提示版本不兼容。

**原因**：
Node.js 版本低于 v22.0.0。

**解决方案**：
访问 [Node.js 官网](https://nodejs.org/) 下载并安装 v22.0.0 或更高版本。

---

### 问题 3: `sharp` / `node-gyp` 安装失败

**现象**：
在 macOS 上使用 Node.js v22.22.0+ 安装时，`sharp@0.34.5` 安装失败，提示 "Please add node-gyp to your dependencies"。

**原因**：
sharp 的安装脚本无法使用预编译二进制文件，尝试从源码编译但缺少 node-gyp。

**解决方案**：
1. 全局安装 node-gyp：
   ```bash
   npm install -g node-gyp
   ```
2. 或者使用环境变量跳过 sharp 的 libvips 检查：
   ```bash
   SHARP_IGNORE_GLOBAL_LIBVIPS=1 npm install -g openclaw@latest
   ```

---

### 问题 4: Windows 插件安装失败 `spawn npm ENOENT`

**现象**：
在 Windows 上，使用 `openclaw plugins install` 安装插件时出现 `spawn npm ENOENT` 错误。

**原因**：
Windows 进程生成的问题，即使 Node.js 和 npm 已正确安装并在 PATH 中可用。

**解决方案**：
使用 CLI 命令行安装，而不是 Web UI：
```bash
openclaw plugins install @openclaw/matrix
```

---

### 问题 5: PATH 问题（Node.js 版本管理器）

**现象**：
使用 nvm/fnm/volta/asdf 等版本管理器安装的 Node.js 无法被 OpenClaw 服务识别。

**原因**：
在 Linux 上，OpenClaw 服务只搜索 `/usr/local/bin`、`/usr/bin`、`/bin`，不加载 shell 初始化脚本。

**解决方案**：
1. 运行 `openclaw doctor` 迁移到系统 Node.js 安装
2. 或设置 `tools.exec.pathPrepend` 添加额外路径
3. 将运行时变量（如 `DISPLAY`）放在 `~/.openclaw/.env` 中

---

### 问题 6: Clawdbot → Moltbot 更名冲突

**现象**：
卸载 Clawdbot 后安装 Moltbot/OpenClaw 时出现冲突。

**原因**：
残留的 Clawdbot 文件与新安装冲突。

**解决方案**：
```bash
# 卸载所有版本
npm uninstall -g clawdbot moltbot openclaw

# 清理缓存
npm cache clean --force

# 检查并删除残留文件
ls /usr/local/bin/clawdbot
ls /usr/local/lib/node_modules/clawdbot
rm -rf /usr/local/bin/clawdbot
rm -rf /usr/local/lib/node_modules/clawdbot

# 重新安装
npm install -g openclaw@latest
```

---

## 飞书对接常见问题

### 问题 1: 机器人能发消息但收不到消息

**现象**：
机器人可以发送消息，但无法接收用户消息。

**原因**：
事件订阅配置不正确，这是最常被遗漏的配置。

**解决方案**：
1. 登录飞书开放平台控制台
2. 进入 "事件与回调"（Events & Callbacks）
3. 事件配置选择 "长连接"（Long connection，推荐）
4. 确保添加了 `im.message.receive_v1` 事件

---

### 问题 2: 提示"未建立长连接"

**现象**：
配置长连接时提示"未建立长连接"。

**原因**：
App ID 和 App Secret 配置不正确，或网关未启动。

**解决方案**：
1. 检查 App ID 和 App Secret 是否正确配置
2. 确保网关正在运行：`openclaw-cn gateway status`
3. 确保已添加飞书渠道：`openclaw-cn channels add`

---

### 问题 3: 机器人在群组中不响应

**现象**：
机器人在私聊中正常工作，但在群组中不响应。

**原因**：
- 默认需要 @提及才响应
- 机器人未被添加到群组
- 群组策略被禁用

**解决方案**：
1. 确保在群组中 @机器人
2. 检查机器人是否已添加到群组
3. 检查配置中 `groupPolicy` 是否为 `"disabled"`
4. 查看日志获取详细信息：`openclaw-cn logs --follow`

---

### 问题 4: 飞书配置命令参数

**配置要点**：
```bash
openclaw-cn config set channels.feishu.appId "飞书 app id"
openclaw-cn config set channels.feishu.appSecret "飞书 app secret"
openclaw-cn config set channels.feishu.enabled true
# 推荐使用 websocket
openclaw-cn config set channels.feishu.connectionMode websocket
openclaw-cn config set channels.feishu.dmPolicy pairing
openclaw-cn config set channels.feishu.groupPolicy allowlist
openclaw-cn config set channels.feishu.requireMention true
```

---

### 问题 5: 必要权限配置

**需要勾选的权限**：
- `contact:user.base:readonly` - 用户信息（获取基础用户信息）
- `im:message` - 消息（全部勾选，用于发送和接收消息）
- `im:message.p2p_msg:readonly` - 私聊消息
- `im:message.group_at_msg:readonly` - 群聊消息
- `im:message:send_as_bot` - 以机器人身份发送消息
- `im:resource` - 媒体资源

---

## 其他常见问题

### 问题 1: 国内模型 API 配置

**现象**：
使用 Kimi、MiniMax、GLM 时无法连接。

**原因**：
OpenClaw 默认集成的是国际版接口地址，国内用户需要使用国内版控制台的 API Key。

**解决方案**：
1. 登录国际版控制台申请 API Key
2. 或调整 Base URL 为国内配置

---

### 问题 2: Gateway 稳定性问题

**现象**：
Web UI 无法与模型对话，或 gateway 启动异常。

**原因**：
- 旧版本稳定性问题
- gateway 启动方式问题

**解决方案**：
升级至最新版本：
```bash
npm update -g openclaw@latest
openclaw doctor --fix
```

---

### 问题 3: Docker 沙箱环境变量缺失

**现象**：
技能在主机上正常工作，但在 Docker 沙箱中失败，提示缺少 API 密钥。

**原因**：
沙箱化执行在 Docker 内运行，不继承主机 `process.env`。

**解决方案**：
在配置中设置 `agents.defaults.sandbox.docker.env`：
```json
{
  "agents": {
    "defaults": {
      "sandbox": {
        "docker": {
          "env": {
            "API_KEY": "your-api-key"
          }
        }
      }
    }
  }
}
```

---

### 问题 4: 日志查看位置

**日志文件位置**：
- 错误日志：`~/.openclaw/logs/feishu-bridge.err.log`（旧版）或通过 `openclaw-cn logs` 查看
- 正常输出：`~/.openclaw/logs/feishu-bridge.out.log`

**实时查看日志**：
```bash
openclaw-cn logs --follow
```

---

## 安全注意事项

### 1. Token 和凭据保护

**重要**：请勿泄露包含 Token 的完整 URL。该链接包含您的身份验证凭据，任何持有此链接的人都能直接绕过登录验证，获得您 OpenClaw 控制台的管理员权限。

### 2. App Secret 保护

- 妥善保管 App Secret，不要分享给他人
- 如果 App Secret 泄露，立即在飞书开放平台重置
- 更新配置文件中的 App Secret 并重启网关

### 3. 部署环境隔离

OpenClaw 运行在你自己的服务器上，所有数据都在本地存储，不会上传到第三方云端。但由于它具有系统级权限，建议：
- 在独立的服务器上部署
- 避免在生产环境或存储重要数据的机器上运行
- 考虑使用沙箱模式限制权限

### 4. 网关认证

- 即使是回环（localhost）也建议保持令牌认证
- 仅当您完全信任每个本地进程时才禁用认证
- 非回环绑定必须启用认证

---

## 使用建议

### 1. 推荐的中国插件

面向中国 IM 平台的 OpenClaw 扩展插件，支持飞书、钉钉、企业微信：

```bash
openclaw plugins install @openclaw-china/channels
```

**建议**：目前钉钉最容易配置，建议先尝试钉钉。

### 2. 诊断命令

安装后运行诊断检查：
```bash
openclaw doctor
```

如果有配置问题，使用修复命令：
```bash
openclaw doctor --fix
```

### 3. 查看完整状态

```bash
openclaw status --all
```

此命令会自动隐藏敏感信息（如 token），适合分享给他人获取支持。

### 4. 升级和更新

定期更新以获取最新功能和安全修复：
```bash
npm update -g openclaw@latest
openclaw plugins update
```

### 5. WebSocket vs Webhook

**推荐使用 WebSocket 长连接模式**：
- 无需公网 IP 或域名
- 无需配置内网穿透
- 机器人主动向飞书建立长连接接收消息
- 更稳定可靠

### 6. 配置文件备份

定期备份 `~/.openclaw/` 目录，包括：
- `openclaw.json` - 主配置文件
- `credentials/` - 认证凭据
- `agents/` - 代理配置和会话
