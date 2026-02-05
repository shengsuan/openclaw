# 🦞 Clawer — 个人 AI 助手

<p align="center">
    <picture>
        <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text-dark.png">
        <img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text.png" alt="Clawer" width="500">
    </picture>
</p>

<p align="center">
<strong>EXFOLIATE! EXFOLIATE! (剥离！脱胎换骨！)</strong>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT License"></a>
</p>

---

## 🌟 项目简介

**Clawer** 是 OpenClaw 的增强优化版，一款功能强大、开源的个人 AI 助手，旨在为你提供极致的智能交互体验。它不仅是一个聊天界面，更是你探索大语言模型（LLM）能力的利器。

### ✨ 核心特性

- **多模型支持**：无缝接入各类主流 LLM API（如 Claude, OpenAI 等）。
- **隐私至上**：你的数据由你掌控，支持本地部署。
- **极致体验**：简洁直观的用户界面，响应迅速。
- **高度可扩展**：支持自定义插件与功能扩展。

---

## 🚀 快速开始

### 安装

你可以通过以下命令快速克隆并安装项目：

```bash
npm install clawer@latest -g

clawer onboard --install-daemon

```

## 快速上手

Runtime: **Node ≥22**.

完整文档(auth, pairing, channels): [Getting started](https://docs.openclaw.ai/start/getting-started)

```bash
clawer onboard --install-daemon

clawer gateway --port 18789 --verbose

# 发送消息
clawer message send --to +1234567890 --message "Hello from Clawer"

# 与助手对话（可选择将对话返回到任何已连接的渠道：WhatsApp/Telegram/Slack/Discord/Google Chat/Signal/iMessage/BlueBubbles/Microsoft Teams/Matrix/Zalo/Zalo Personal/WebChat）
clawer agent --message "Ship checklist" --thinking high
```

你也可以通过以下命令快速克隆并打包项目：

```bash
git clone https://github.com/shengsuan/moltbot
cd moltbot
checkout clawer
pnpm install
pnpm ui:build # auto-installs UI deps on first run
pnpm build

pnpm clawer onboard --install-daemon

# Dev loop (auto-reload on TS changes)
pnpm gateway:watch
```

---

## 🤝 贡献指南

我们非常欢迎社区的贡献！无论是提交代码、改进文档，还是提出新的想法，你的帮助对 Clawer 至关重要。

1. **Fork** 本仓库。
2. 创建你的**特性分支** (`git checkout -b feature/AmazingFeature`)。
3. **提交**你的更改 (`git commit -m 'Add some AmazingFeature'`)。
4. **推送到**分支 (`git push origin feature/AmazingFeature`)。
5. 开启一个 **Pull Request**。

---

## 💬 社区支持

如果你遇到任何问题或有改进建议，欢迎加入我们的社区：

- **GitHub Issues**: [提交问题或需求](https://github.com/shengsuan/moltbot/issues)

---

## 📄 许可证

本项目基于相应的开源许可证发布。详情请参阅项目中的 `LICENSE` 文件。

---
