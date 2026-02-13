🦞 **OpenClaw — 你的个人 AI 助手**

![OpenClaw Logo](https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text.png)

**去角质！去角质！**（EXFOLIATE! EXFOLIATE!）

[![CI 工作流状态](https://img.shields.io/github/actions/workflow/status/openclaw/openclaw/ci.yml?branch=main&style=for-the-badge)]()
[![GitHub 版本](https://img.shields.io/github/v/release/openclaw/openclaw?include_prereleases&style=for-the-badge)]()
[![Discord](https://img.shields.io/discord/1456350064065904867?label=Discord&logo=discord&logoColor=white&color=5865F2&style=for-the-badge)]()
[![许可证: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)]()

OpenClaw 是一个在你自己的设备上运行的个人 AI 助手。

它可以在你已经使用的各种渠道（如 WhatsApp、Telegram、Slack、Discord、Google Chat、Signal、iMessage、Microsoft Teams、WebChat）上为你提供答复，并且还支持 BlueBubbles、Matrix、Zalo 和 Zalo Personal 等扩展渠道。它能在 macOS/iOS/Android 设备上进行语音对话，并能渲染一个由你控制的实时画布（Canvas）。网关（Gateway）只是控制平面，产品本身是这个助手。

如果你想要一个感觉本地化、快速响应且始终在线的个人单用户助手，那就是它了。

[官方网站](https://openclaw.ai) · [文档](https://docs.openclaw.ai) · [DeepWiki](https://deepwiki.com/openclaw/openclaw) · [入门指南](https://docs.openclaw.ai/start/getting-started) · [更新指南](https://docs.openclaw.ai/install/updating) · [功能展示](https://docs.openclaw.ai/start/showcase) · [常见问题](https://docs.openclaw.ai/start/faq) · [向导](https://docs.openclaw.ai/start/wizard) · [Nix](https://github.com/openclaw/nix-openclaw) · [Docker](https://docs.openclaw.ai/install/docker) · [Discord](https://discord.gg/clawd)

**推荐设置**：在终端中运行引导向导 (`openclaw onboard`)。
该向导将逐步指导你完成网关、工作区、渠道和技能的设置。CLI 向导是推荐方式，适用于 macOS、Linux 和 Windows（通过 WSL2；强烈推荐）。

支持 npm、pnpm 或 bun。

**新用户安装？从这里开始**：[入门指南](https://docs.openclaw.ai/start/getting-started)

### 订阅服务 (OAuth)

- [Anthropic](https://www.anthropic.com/) (Claude Pro/Max)
- [OpenAI](https://openai.com/) (ChatGPT/Codex)

**模型说明**：虽然支持任何模型，但我强烈推荐使用 Anthropic Pro/Max (100/200) + Opus 4.6，以获得更强的长上下文处理能力和更好的提示注入（prompt-injection）抵抗力。详见 [Onboarding](https://docs.openclaw.ai/start/onboarding)。

### 模型（选择与认证）

- 模型配置与 CLI：[Models](https://docs.openclaw.ai/concepts/models)
- 认证配置文件轮换（OAuth vs API 密钥）及备用方案：[Model failover](https://docs.openclaw.ai/concepts/model-failover)

### 安装（推荐方式）

**运行环境**：Node.js ≥ 22。

```bash
npm install -g @coohu/openclaw@latest
# 或者: pnpm add -g @coohu/openclaw@latest

openclaw onboard --install-daemon
```

向导会安装网关守护进程（launchd/systemd 用户服务），使其保持运行。

### 快速开始（TL;DR）

**运行环境**：Node.js ≥ 22。
完整新手指南（认证、配对、渠道）：[Getting started](https://docs.openclaw.ai/start/getting-started)

```bash
openclaw onboard --install-daemon

openclaw gateway --port 18789 --verbose

# 发送一条消息
openclaw message send --to +1234567890 --message "Hello from OpenClaw"

# 与助手对话（可选择将回复发送回任何已连接的渠道：WhatsApp/Telegram/Slack/Discord/Google Chat/Signal/iMessage/BlueBubbles/Microsoft Teams/Matrix/Zalo/Zalo Personal/WebChat）
openclaw agent --message "Ship checklist" --thinking high
```

需要升级？请参考 [更新指南](https://docs.openclaw.ai/install/updating)（并运行 `openclaw doctor`）。

### 开发渠道

- **stable**：标记版本（`vYYYY.M.D` 或 `vYYYY.M.D-<patch>`），npm 分发标签为 `latest`。
- **beta**：预发布标签（`vYYYY.M.D-beta.N`），npm 分发标签为 `beta`（macOS 应用可能缺失）。
- **dev**：`main` 分支的最新代码，npm 分发标签为 `dev`（发布时）。

切换渠道（git + npm）：`openclaw update --channel stable|beta|dev`。
详情：[Development channels](https://docs.openclaw.ai/install/development-channels)。

### 从源码安装（开发）

建议使用 `pnpm` 从源码构建。Bun 可选，用于直接运行 TypeScript。

```bash
git clone https://github.com/shengsuan/openclaw.git
cd openclaw
git checkout -b pub origin/pub

pnpm install
pnpm ui:build # 首次运行时会自动安装 UI 依赖
pnpm build

pnpm openclaw onboard --install-daemon

# 开发循环（TS 文件更改时自动重载）
pnpm gateway:watch
```

注意：`pnpm openclaw ...` 通过 `tsx` 直接运行 TypeScript。`pnpm build` 会在 `dist/` 目录下生成产物，可用于通过 Node 或打包后的 `openclaw` 二进制文件运行。

### 安全默认设置（私信访问）

OpenClaw 连接到真实的即时通讯平台。请将收到的私信（DM）视为不可信输入。

完整安全指南：[Security](https://docs.openclaw.ai/gateway/security)

**Telegram/WhatsApp/Signal/iMessage/Microsoft Teams/Discord/Google Chat/Slack 的默认行为**：

- **配对模式** (`dmPolicy="pairing"`): 未知发件人会收到一个简短的配对码，机器人不会处理其消息内容。使用 `openclaw pairing approve <channel> <code>` 批准后，该发件人会被加入本地允许列表。
- **公开接收私信** 需要显式开启：设置 `dmPolicy="open"` 并在渠道允许列表 (`allowFrom`) 中包含 `"*"`。

运行 `openclaw doctor` 可以检查是否存在风险或配置错误的私信策略。

### 核心亮点

- **本地优先的网关**：用于会话、渠道、工具和事件的单一控制平面。
- **多渠道收件箱**：支持 WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, BlueBubbles (iMessage), iMessage (旧版), Microsoft Teams, Matrix, Zalo, Zalo Personal, WebChat, 以及 macOS, iOS/Android。
- **多智能体路由**：将来自不同渠道/账户/联系人的消息路由到隔离的智能体（工作区 + 每个智能体独立的会话）。
- **语音唤醒** + **对话模式**：在 macOS/iOS/Android 上通过 ElevenLabs 实现常驻语音交互。
- **实时画布**：由智能体驱动的可视化工作区，支持 A2UI。
- **一流的工具**：浏览器、画布、节点、定时任务、会话、Discord/Slack 操作等。
- **配套应用**：macOS 菜单栏应用 + iOS/Android 节点。
- **引导向导** + **技能**：通过向导驱动的设置流程，内置/托管/工作区技能。

### 星标历史

![Star History](https://api.star-history.com/svg?repos=openclaw/openclaw&type=date&legend=top-left)

### 我们迄今为止构建的一切

#### 核心平台

- **网关 WS 控制平面**：包含会话、在线状态、配置、定时任务、Webhook、控制界面和画布宿主。
- **CLI 界面**：`gateway`, `agent`, `send`, `wizard` 和 `doctor`。
- **Pi 智能体运行时**：RPC 模式，支持工具流和区块流。
- **会话模型**：`main` 用于直接聊天，群组隔离，激活模式，队列模式，回复返回。群组规则详见 [Groups](https://docs.openclaw.ai/concepts/groups)。
- **媒体管道**：图像/音频/视频，转录钩子，大小限制，临时文件生命周期。音频详情：[Audio](https://docs.openclaw.ai/nodes/audio)。

#### 渠道

- **渠道**：[WhatsApp](https://docs.openclaw.ai/channels/whatsapp) (Baileys), [Telegram](https://docs.openclaw.ai/channels/telegram) (grammY), [Slack](https://docs.openclaw.ai/channels/slack) (Bolt), [Discord](https://docs.openclaw.ai/channels/discord) (discord.js), [Google Chat](https://docs.openclaw.ai/channels/googlechat) (Chat API), [Signal](https://docs.openclaw.ai/channels/signal) (signal-cli), [BlueBubbles](https://docs.openclaw.ai/channels/bluebubbles) (iMessage, 推荐), [iMessage](https://docs.openclaw.ai/channels/imessage) (旧版 imsg), [Microsoft Teams](https://docs.openclaw.ai/channels/msteams) (扩展), [Matrix](https://docs.openclaw.ai/channels/matrix) (扩展), [Zalo](https://docs.openclaw.ai/channels/zalo) (扩展), [Zalo Personal](https://docs.openclaw.ai/channels/zalouser) (扩展), [WebChat](https://docs.openclaw.ai/web/webchat)。
- **群组路由**：提及门控、回复标签、按渠道分块和路由。渠道规则：[Channels](https://docs.openclaw.ai/channels)。

#### 应用与节点

- **macOS 应用**：菜单栏控制平面、语音唤醒/PTT、对话模式覆盖层、WebChat、调试工具、远程网关控制。
- **iOS 节点**：画布、语音唤醒、对话模式、相机、屏幕录制、Bonjour 配对。
- **Android 节点**：画布、对话模式、相机、屏幕录制、可选短信功能。
- **macOS 节点模式**：`system.run`/`notify` + 画布/相机暴露。

#### 工具与自动化

- **浏览器控制**：专用的 OpenClaw Chrome/Chromium，支持快照、操作、上传、配置文件。
- **画布**：A2UI 推送/重置、执行、快照。
- **节点**：相机拍照/录像、屏幕录制、`location.get`、通知。
- **定时任务 + 唤醒**；Webhook；Gmail Pub/Sub。
- **技能平台**：捆绑、托管和工作区技能，带有安装门控 + UI。

#### 运行时与安全

- **渠道路由**、**重试策略** 和 **流式传输/分块**。
- **在线状态**、**输入指示器** 和 **使用情况追踪**。
- **模型**、**模型故障转移** 和 **会话修剪**。
- **安全** 和 **故障排除**。

#### 运维与打包

- **控制界面** + **WebChat** 由网关直接提供服务。
- **Tailscale Serve/Funnel** 或 **SSH 隧道**，支持令牌/密码认证。
- **Nix 模式** 用于声明式配置；基于 **Docker** 的安装。
- **Doctor** 迁移、日志记录。

### 工作原理（简述）

```
WhatsApp / Telegram / Slack / Discord / Google Chat / Signal / iMessage / BlueBubbles / Microsoft Teams / Matrix / Zalo / Zalo Personal / WebChat
               │
               ▼
┌───────────────────────────────┐
│            网关 (Gateway)     │
│       (控制平面)              │
│     ws://127.0.0.1:18789      │
└──────────────┬────────────────┘
               │
               ├─ Pi 智能体 (RPC)
               ├─ CLI (openclaw …)
               ├─ WebChat UI
               ├─ macOS 应用
               └─ iOS / Android 节点
```

### 关键子系统

- **网关 WebSocket 网络**：用于客户端、工具和事件的单一 WS 控制平面（以及运维：[Gateway runbook](https://docs.openclaw.ai/gateway)）。
- **Tailscale 暴露**：通过 `tailscale serve`（仅限内网）或 `tailscale funnel`（公开）暴露网关仪表盘 + WS（远程访问：[Remote](https://docs.openclaw.ai/gateway/remote)）。
- **浏览器控制**：由 OpenClaw 管理的 Chrome/Chromium，通过 CDP 进行控制。
- **画布 + A2UI**：由智能体驱动的可视化工作区（A2UI 宿主）。
- **语音唤醒** + **对话模式**：常驻语音和连续对话。
- **节点**：画布、相机拍照/录像、屏幕录制、`location.get`、通知，以及仅限 macOS 的 `system.run`/`system.notify`。

### Tailscale 访问（网关仪表盘）

OpenClaw 可以自动配置 Tailscale Serve（仅限内网）或 Funnel（公开），同时网关仍绑定在本地回环地址。配置 `gateway.tailscale.mode`：

- `off`：不进行 Tailscale 自动化（默认）。
- `serve`：通过 `tailscale serve` 提供内网 HTTPS（默认使用 Tailscale 身份验证头）。
- `funnel`：通过 `tailscale funnel` 提供公开 HTTPS（需要共享密码认证）。

**注意**：

- 启用 Serve/Funnel 时，`gateway.bind` 必须保持为 `loopback`（OpenClaw 会强制执行）。
- 可以通过设置 `gateway.auth.mode: "password"` 或 `gateway.auth.allowTailscale: false` 强制 Serve 要求密码。
- Funnel 在未设置 `gateway.auth.mode: "password"` 时拒绝启动。
- （可选）`gateway.tailscale.resetOnExit` 可在关闭时撤销 Serve/Funnel。

详情：[Tailscale 指南](https://docs.openclaw.ai/gateway/tailscale) · [Web 界面](https://docs.openclaw.ai/web)

### 远程网关（Linux 非常适合）

在小型 Linux 实例上运行网关是完全可行的。客户端（macOS 应用、CLI、WebChat）可以通过 Tailscale Serve/Funnel 或 SSH 隧道进行连接，并且你仍然可以根据需要配对设备节点（macOS/iOS/Android）来执行设备本地的操作。

- **网关主机** 默认运行 `exec` 工具和渠道连接。
- **设备节点** 通过 `node.invoke` 运行设备本地操作（`system.run`、相机、屏幕录制、通知）。

简而言之：`exec` 在网关所在位置运行；设备操作在设备所在位置运行。

详情：[远程访问](https://docs.openclaw.ai/gateway/remote) · [节点](https://docs.openclaw.ai/nodes) · [安全](https://docs.openclaw.ai/gateway/security)

### 通过网关协议实现的 macOS 权限

macOS 应用可以以节点模式运行，并通过网关 WebSocket（`node.list` / `node.describe`）广播其功能和权限映射。客户端随后可以通过 `node.invoke` 执行本地操作：

- `system.run` 运行本地命令并返回 stdout/stderr/退出码；设置 `needsScreenRecording: true` 以要求屏幕录制权限（否则会返回 `PERMISSION_MISSING`）。
- `system.notify` 发送用户通知，如果通知权限被拒绝则会失败。
- `canvas.*`、`camera.*`、`screen.record` 和 `location.get` 也通过 `node.invoke` 路由，并遵循 TCC 权限状态。

**提升的 Bash（主机权限）与 macOS TCC 是分开的**：

- 使用 `/elevated on|off` 在启用并加入白名单的情况下，为每个会话切换提升的访问权限。
- 网关通过 `sessions.patch`（WS 方法）持久化每个会话的切换状态，以及 `thinkingLevel`、`verboseLevel`、`model`、`sendPolicy` 和 `groupActivation`。

详情：[节点](https://docs.openclaw.ai/nodes) · [macOS 应用](https://docs.openclaw.ai/platforms/macos) · [网关协议](https://docs.openclaw.ai/concepts/architecture)

### 智能体到智能体（sessions\_\* 工具）

使用这些工具可以在会话之间协调工作，而无需在不同的聊天界面间跳转。

- `sessions_list`：发现活跃的会话（智能体）及其元数据。
- `sessions_history`：获取某个会话的对话记录。
- `sessions_send`：向另一个会话发送消息；可选回复-返回乒乓模式和公告步骤（`REPLY_SKIP`, `ANNOUNCE_SKIP`）。

详情：[会话工具](https://docs.openclaw.ai/concepts/session-tool)

### 技能注册表（ClawHub）

ClawHub 是一个极简的技能注册表。启用 ClawHub 后，智能体可以自动搜索技能并在需要时拉取新的技能。
[ClawHub](https://clawhub.com)

### 聊天命令

在 WhatsApp/Telegram/Slack/Google Chat/Microsoft Teams/WebChat 中发送以下命令（群组命令仅限所有者）：

- `/status` — 简洁的会话状态（模型 + token，如有可用则显示费用）
- `/new` 或 `/reset` — 重置会话
- `/compact` — 压缩会话上下文（摘要）
- `/think <level>` — off|minimal|low|medium|high|xhigh（仅限 GPT-5.2 + Codex 模型）
- `/verbose on|off`
- `/usage off|tokens|full` — 每次回复的使用情况页脚
- `/restart` — 重启网关（群组中仅限所有者）
- `/activation mention|always` — 切换群组激活模式（仅限群组）

### 应用（可选）

仅网关本身就能提供出色的体验。所有应用都是可选的，并增加了额外功能。
如果你计划构建/运行配套应用，请遵循以下平台操作手册。

#### macOS (OpenClaw.app)（可选）

- 网关和健康状况的菜单栏控制。
- 语音唤醒 + 按键通话（PTT）覆盖层。
- WebChat + 调试工具。
- 通过 SSH 进行远程网关控制。

**注意**：为了使 macOS 权限在重建后依然有效，需要签名的构建（参见 `docs/mac/permissions.md`）。

#### iOS 节点（可选）

- 通过 Bridge 作为节点配对。
- 语音触发转发 + 画布界面。
- 通过 `openclaw nodes …` 控制。
- 操作手册：[iOS connect](https://docs.openclaw.ai/platforms/ios)。

#### Android 节点（可选）

- 通过与 iOS 相同的 Bridge 和配对流程进行配对。
- 提供画布、相机和屏幕捕获命令。
- 操作手册：[Android connect](https://docs.openclaw.ai/platforms/android)。

### 智能体工作区与技能

- **工作区根目录**：`~/.openclaw/workspace`（可通过 `agents.defaults.workspace` 配置）。
- **注入的提示文件**：`AGENTS.md`, `SOUL.md`, `TOOLS.md`。
- **技能**：`~/.openclaw/workspace/skills/<skill>/SKILL.md`。

### 配置

最小化的 `~/.openclaw/openclaw.json`（模型 + 默认值）：

```json
{
  "agent": {
    "model": "anthropic/claude-opus-4-6"
  }
}
```

[完整配置参考（所有键和示例）](https://docs.openclaw.ai/gateway/configuration)

### 安全模型（重要）

**默认**：工具在主会话的主机上运行，因此当只有你一人时，智能体拥有完全访问权限。
**群组/渠道安全**：设置 `agents.defaults.sandbox.mode: "non-main"`，以在每个会话的 Docker 沙箱中运行非主会话（群组/渠道）；此时 bash 会在这些会话的 Docker 中运行。

**沙箱默认**：

- **允许列表**：`bash`, `process`, `read`, `write`, `edit`, `sessions_list`, `sessions_history`, `sessions_send`, `sessions_spawn`。
- **拒绝列表**：`browser`, `canvas`, `nodes`, `cron`, `discord`, `gateway`。

详情：[安全指南](https://docs.openclaw.ai/gateway/security) · [Docker + 沙箱](https://docs.openclaw.ai/install/docker) · [沙箱配置](https://docs.openclaw.ai/gateway/configuration)

### 各渠道配置示例

（此处省略了各渠道如 WhatsApp, Telegram, Slack, Discord 等的具体配置说明，因其格式和内容已在上文核心亮点和渠道部分涵盖）

### 文档

当你完成引导流程后，可以使用这些更深入的参考资料。

- [从文档索引开始导航和了解“内容分布”](https://docs.openclaw.ai)
- [阅读架构概述以了解网关 + 协议模型](https://docs.openclaw.ai/concepts/architecture)
- [需要所有配置项和示例时，使用完整配置参考](https://docs.openclaw.ai/gateway/configuration)
- [按照运维手册规范地运行网关](https://docs.openclaw.ai/gateway)
- [了解控制界面/Web 界面的工作原理以及如何安全地暴露它们](https://docs.openclaw.ai/web)
- [了解如何通过 SSH 隧道或内网进行远程访问](https://docs.openclaw.ai/gateway/remote)
- [遵循引导向导流程进行分步设置](https://docs.openclaw.ai/start/wizard)
- [通过 webhook 界面连接外部触发器](https://docs.openclaw.ai/automation/webhook)
- [设置 Gmail Pub/Sub 触发器](https://docs.openclaw.ai/automation/gmail-pubsub)
- [了解 macOS 菜单栏配套应用的详细信息](https://docs.openclaw.ai/platforms/mac/menu-bar)
- [平台指南：Windows (WSL2), Linux, macOS, iOS, Android](https://docs.openclaw.ai/platforms/)
- [使用故障排除指南调试常见问题](https://docs.openclaw.ai/channels/troubleshooting)
- [在暴露任何服务前，务必阅读安全指南](https://docs.openclaw.ai/gateway/security)

### 高级文档（发现与控制）

（此处列出了一系列高级主题的文档链接，如 Discovery, Bonjour, Pairing, Remote Gateway, Control UI, Dashboard 等）

### 运维与故障排除

（此处列出了一系列运维和排错相关的文档链接，如 Health checks, Gateway lock, Background process, Browser troubleshooting, Logging 等）

### 深度解析

（此处列出了一系列关于内部机制的深度文档链接，如 Agent loop, Presence, TypeBox schemas, RPC adapters, Queue 等）

### 工作区与技能

（此处列出了一系列关于技能和工作区模板的文档链接）

### 平台内部

（此处列出了一系列关于各平台内部实现的文档链接，如 macOS dev setup, iOS node, Android node, Windows, Linux 等）

### 邮件钩子（Gmail）

[docs.openclaw.ai/gmail-pubsub](https://docs.openclaw.ai/automation/gmail-pubsub)

### Molty

OpenClaw 是为 Molty（一只太空龙虾 AI 助手）而构建的。🦞
由 Peter Steinberger 和社区共同打造。

[openclaw.ai](https://openclaw.ai)
[soul.md](https://soul.md)
[steipete.me](https://steipete.me)
[@openclaw](https://x.com/openclaw)

### 社区

有关贡献指南、维护者信息以及如何提交 PR，请参阅 [CONTRIBUTING.md](CONTRIBUTING.md)。
欢迎 AI/氛围编码（vibe-coded）的 PR！🤖

特别感谢 [Mario Zechner](https://mariozechner.at/) 的支持以及他的 [pi-mono](https://github.com/badlogic/pi-mono)。
特别感谢 Adam Doppelt 对 lobster.bot 的贡献。
