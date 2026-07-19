# Skills

> 一个 OpenClaw + Claude Code Skills 集合仓库：100 个可复用 skill（60 个 OpenClaw + 40 个 Claude Code），覆盖平台集成、工作流编排、内容创作、安全审计、Prompt 工程、Claude Code 自动化等。

## 简介

本仓库是 Stitch 用过的所有 Claude / Agent Skill 集合，分两大系列：

- **OpenClaw Skills（60 个）** — 基于 [chujianyun/skills](https://github.com/chujianyun/skills) 格式规范，平台集成（飞书 / QQ / Discord / Slack / Spotify 等）+ 工具封装
- **Claude Code Skills（40 个）** — Anthropic 官方 skill 格式，专门为 Claude Code 工作流设计

每个 skill 不只是一个说明文件，而是围绕某一类任务组织起来的可复用能力单元。

- **数量**：100 个 skill
- **协议**：CC BY-NC-SA 4.0（Attribution-NonCommercial-ShareAlike）
- **来源**：fork 自 [chujianyun/skills](https://github.com/chujianyun/skills)

## 目录

- [OpenClaw Skills（60 个）](#openclaw-skills60-个)
- [Claude Code Skills（40 个）](#claude-code-skills40-个)
- [安装](#安装)
- [使用](#使用)
- [更新日志](#更新日志)
- [协议](#协议)

---

## OpenClaw Skills（60 个）

### 平台集成（12 个）

feishu / qqbot / discord / slack / notion / obsidian / spotify-player / sonoscli / openhue / wacli / xurl / trello

### 信息获取（10 个）

weather / summarize / blogwatcher / tavily / github / gh-issues / goplaces / gifgrep / gemini / oracle

### 内容创作（4 个）

sag / songsee / video-frames / nano-pdf

### 编码与自动化（9 个）

coding-agent / skill-creator / taskflow / taskflow-inbox-triage / mcporter / model-usage / session-logs / open-prose / clawhub

### 运维与排障（4 个）

healthcheck / node-connect / openclaw-session-cleaner / diffs

### macOS / Apple 生态（9 个）

imsg / apple-notes / apple-reminders / things-mac / bear-notes / peekaboo / bluebubbles / camsnap / tmux

### 命令行工具（11 个）

1password / himalaya / gog / eightctl / ordercli / canvas / voice-call / openai-whisper / openai-whisper-api / sherpa-onnx-tts / blucli

### 知识管理（1 个）

memory-wiki

---

## Claude Code Skills（40 个）

### Prompt 工程（5 个）

prompt-factory / prompt-optimizer / prompt-caching / humanizer-zh / batch-humanizer

### Claude Code 工作流（10 个）

context-mode / context-mode-ops / planning-with-files-zh / self-improving-agent / memory-management / claude-md-improver / review-and-refactor / ralph-loop / claude-automation-recommender / opencli-usage

### 扩展开发（10 个）

hook-factory / command-development / plugin-structure / mcp-builder / mcp-integration / skill-creator / skill-development / skill-install / find-skills / writing-skills

### 安全与审计（4 个）

reins / security-review / quality-auditor / ai-slop-cleaner

### 内容与文档（6 个）

docx / pdf-to-markdown / ppt-master / academic-essay / academic-researcher / api-docs

### 浏览器 / 测试（2 个）

agent-browser / playwright

### UI 设计（2 个）

ui-design / ui-design-system

---

## 安装

### OpenClaw 用户

```bash
# Method 1: OpenClaw skills 命令
# 将 skills/ 目录放入 ~/.openclaw/skills/

# Method 2: 从 GitHub 安装
git clone https://github.com/fan1959/skills.git ~/.openclaw/skills

# Method 3: openskills
openskills install fan1959/skills --global
```

### Claude Code 用户

```bash
# 复制到 Claude skills 目录
cp -r skills/claudecode/* ~/.claude/skills/
```

---

## 使用

### 直接在对话中引用

> 用 feishu-doc 读我的飞书文档
> 用 humanizer-zh 改我的论文
> 用 tavily 搜索 Qt 6 迁移指南

agent 会自动加载对应 skill。

### 链式组合

```
1. 用 tavily 搜索 Qt 6 迁移指南
2. 用 ppt-master 把搜索结果生成 PPT
3. 用 humanizer-zh 改 PPT 文案
```

### 手动调用

每个 skill 目录下有 `SKILL.md`，包含使用说明 + 示例 + 触发词。

---

## 更新日志

| 日期 | 变更 |
|---|---|
| 2026-07-19 | README 重写为基于实际 100 个 skill（60 OpenClaw + 40 Claude Code）的清单；删去虚构分类；用紧凑格式避免一个一个列 |
| 2025-04-22 | 初始 fork 自 [chujianyun/skills](https://github.com/chujianyun/skills) |

---

## 协议

All Skill files in this project are licensed under [CC BY-NC-SA 4.0](LICENSE) (Attribution-NonCommercial-ShareAlike).

For commercial use, please contact the author for authorization.

---

## 仓库

- **GitHub**: https://github.com/fan1959/skills
- **来源**: fork 自 [chujianyun/skills](https://github.com/chujianyun/skills)
- **协议**: CC BY-NC-SA 4.0