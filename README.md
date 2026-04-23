# Skills

这是 Stitch 的 OpenClaw Skills 集合，基于 [chujianyun/skills](https://github.com/chujianyun/skills) 的格式规范整理。

每个 skill 不只是一个说明文件，而是围绕某一类任务组织起来的可复用能力单元。

---

## Skill 地图

### 1. 平台集成类（Tool Wrapper）

连接第三方平台和服务，把 API 包装成可按需触发的工具。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [feishu-doc](skills/feishu/SKILL.md) | Tool Wrapper | 飞书文档读写、块操作 |
| [feishu-drive](skills/feishu/SKILL.md) | Tool Wrapper | 飞书云文档管理 |
| [feishu-perm](skills/feishu/SKILL.md) | Tool Wrapper | 飞书权限管理 |
| [feishu-wiki](skills/feishu/SKILL.md) | Tool Wrapper | 飞书知识库操作 |
| [qqbot-channel](skills/qqbot/SKILL.md) | Tool Wrapper | QQ 频道管理、成员、发帖 |
| [qqbot-media](skills/qqbot/SKILL.md) | Tool Wrapper | QQ 富媒体收发（图片/语音/视频/文件） |
| [qqbot-remind](skills/qqbot/SKILL.md) | Tool Wrapper | QQ 定时提醒（一次性/周期性） |
| [discord](skills/discord/SKILL.md) | Tool Wrapper | Discord 消息操作 |
| [slack](skills/slack/SKILL.md) | Tool Wrapper | Slack 反应、置顶操作 |
| [notion](skills/notion/SKILL.md) | Tool Wrapper | Notion 页面和数据库操作 |
| [obsidian](skills/obsidian/SKILL.md) | Tool Wrapper | Obsidian 笔记库管理 |
| [spotify-player](skills/spotify-player/SKILL.md) | Tool Wrapper | Spotify 播放控制 |
| [sonoscli](skills/sonoscli/SKILL.md) | Tool Wrapper | Sonos 音箱控制 |
| [openhue](skills/openhue/SKILL.md) | Tool Wrapper | Philips Hue 灯光控制 |
| [wacli](skills/wacli/SKILL.md) | Tool Wrapper | WhatsApp 消息发送 |
| [xurl](skills/xurl/SKILL.md) | Tool Wrapper | Twitter/X API 操作 |

---

### 2. 信息获取类（Tool Wrapper / Generator）

搜索、提取和总结信息。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [weather](skills/weather/SKILL.md) | Tool Wrapper | 天气查询（当前/预报） |
| [summarize](skills/summarize/SKILL.md) | Tool Wrapper | URL、播客、本地文件的摘要提取 |
| [blogwatcher](skills/blogwatcher/SKILL.md) | Tool Wrapper | 博客和 RSS/Atom 订阅监控 |
| [tavily](skills/tavily/SKILL.md) | Tool Wrapper | Tavily 网络搜索和研究工具 |
| [github](skills/github/SKILL.md) | Tool Wrapper | GitHub issues、PRs、CI 状态查询 |
| [gh-issues](skills/gh-issues/SKILL.md) | Tool Wrapper / Pipeline | GitHub issues 自动化处理 |
| [goplaces](skills/goplaces/SKILL.md) | Tool Wrapper | Google Places 查询 |
| [gifgrep](skills/gifgrep/SKILL.md) | Tool Wrapper | GIF 搜索和下载 |

---

### 3. 内容创作类（Generator）

生成媒体内容。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [sag](skills/sag/SKILL.md) | Generator | ElevenLabs TTS（文本转语音） |
| [songsee](skills/songsee/SKILL.md) | Generator | 音频频谱图和特征可视化 |
| [video-frames](skills/video-frames/SKILL.md) | Generator | 视频帧和短片段提取 |
| [nano-pdf](skills/nano-pdf/SKILL.md) | Generator | PDF 自然语言编辑 |

---

### 4. 编码与自动化类（Tool Wrapper / Pipeline）

代码生成、审查和工作流自动化。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [coding-agent](skills/coding-agent/SKILL.md) | Pipeline | 委托 Codex/Claude Code/Pi 等编码 Agent |
| [skill-creator](skills/skill-creator/SKILL.md) | Pipeline | 创建、编辑、审查 AgentSkills |
| [taskflow](skills/taskflow/SKILL.md) | Pipeline | 跨分离任务的长时工作流编排 |
| [taskflow-inbox-triage](skills/taskflow-inbox-triage/SKILL.md) | Pipeline | 收件箱分类工作流示例 |
| [mcporter](skills/mcporter/SKILL.md) | Tool Wrapper | MCP 服务器/工具调用管理 |
| [model-usage](skills/model-usage/SKILL.md) | Tool Wrapper | Codex/Claude 按模型费用统计 |
| [session-logs](skills/session-logs/SKILL.md) | Tool Wrapper | 搜索和分析历史会话日志 |

---

### 5. 运维与排障类（Runbook / Tool Wrapper）

处理"系统坏了、服务挂了、命令不会用"的场景。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [healthcheck](skills/healthcheck/SKILL.md) | Runbook | 主机安全加固、审计、防火墙检查 |
| [node-connect](skills/node-connect/SKILL.md) | Runbook | OpenClaw 节点连接和配对诊断 |
| [openclaw-session-cleaner](skills/openclaw-session-cleaner/SKILL.md) | Runbook | 清理膨胀的 session 文件 |
| [diffs](skills/diffs/SKILL.md) | Tool Wrapper | 生成可分享的 diff 视图 |

---

### 6. macOS/Apple 生态类（Tool Wrapper）

Apple 平台相关工具。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [imsg](skills/imsg/SKILL.md) | Tool Wrapper | iMessage/SMS 发送和历史查询 |
| [apple-notes](skills/apple-notes/SKILL.md) | Tool Wrapper | Apple Notes 管理 |
| [apple-reminders](skills/apple-reminders/SKILL.md) | Tool Wrapper | Apple Reminders 管理 |
| [things-mac](skills/things-mac/SKILL.md) | Tool Wrapper | Things 3 任务管理 |
| [bear-notes](skills/bear-notes/SKILL.md) | Tool Wrapper | Bear 笔记管理 |
| [peekaboo](skills/peekaboo/SKILL.md) | Tool Wrapper | macOS UI 自动化 |
| [bluebubbles](skills/bluebubbles/SKILL.md) | Tool Wrapper | iMessage via BlueBubbles |
| [camsnap](skills/camsnap/SKILL.md) | Tool Wrapper | RTSP/ONVIF 摄像头捕获 |
| [tmux](skills/tmux/SKILL.md) | Tool Wrapper | tmux 会话远程控制 |

---

### 7. 命令行工具类（Tool Wrapper）

各种 CLI 工具封装。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [1password](skills/1password/SKILL.md) | Tool Wrapper | 1Password CLI（op）管理密码和密钥 |
| [himalaya](skills/himalaya/SKILL.md) | Tool Wrapper | 邮件 IMAP/SMTP 管理 |
| [gog](skills/gog/SKILL.md) | Tool Wrapper | Google Workspace（Gmail、Calendar、Drive） |
| [eightctl](skills/eightctl/SKILL.md) | Tool Wrapper | Eight Sleep  Pod 控制 |
| [ordercli](skills/ordercli/SKILL.md) | Tool Wrapper | 订餐订单历史查询 |
| [canvas](skills/canvas/SKILL.md) | Tool Wrapper | OpenClaw Canvas 内容展示 |
| [voice-call](skills/voice-call/SKILL.md) | Tool Wrapper | OpenClaw 语音通话 |
| [blogwatcher](skills/blogwatcher/SKILL.md) | Tool Wrapper | 博客/RSS 监控更新 |
| [openai-whisper](skills/openai-whisper/SKILL.md) | Tool Wrapper | 本地语音转文字（Whisper CLI） |
| [openai-whisper-api](skills/openai-whisper-api/SKILL.md) | Tool Wrapper | OpenAI Whisper API 转录 |
| [sherpa-onnx-tts](skills/sherpa-onnx-tts/SKILL.md) | Tool Wrapper | 本地离线 TTS |
| [gemini](skills/gemini/SKILL.md) | Tool Wrapper | Gemini CLI 一站式问答 |
| [oracle](skills/oracle/SKILL.md) | Tool Wrapper | Oracle CLI 最佳实践 |
| [blucli](skills/blucli/SKILL.md) | Tool Wrapper | BluOS CLI 控制 |

---

### 8. 知识管理类（Tool Wrapper）

笔记和知识库维护。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [obsidian-vault-maintainer](skills/obsidian-vault-maintainer/SKILL.md) | Tool Wrapper | Obsidian 风格记忆知识库维护 |
| [wiki-maintainer](skills/wiki-maintainer/SKILL.md) | Tool Wrapper | OpenClaw 记忆知识库维护 |
| [prose](skills/prose/SKILL.md) | Pipeline | OpenProse 多 Agent 工作流编排 |

---

## 安装

### Method 1: 使用 OpenClaw 内置 skills 命令

将 skills 目录放入 `~/.openclaw/skills/` 即可。

### Method 2: 从 GitHub 安装

```bash
git clone https://github.com/fan1959/skills.git ~/.openclaw/skills
```

### Method 3: 使用 openskills

```bash
openskills install fan1959/skills --global
```

---

## 仓库结构

```
skills/
├── 1password/              # 1Password CLI
├── apple-notes/            # Apple Notes
├── apple-reminders/        # Apple Reminders
├── bear-notes/             # Bear 笔记
├── blogwatcher/            # 博客/RSS 监控
├── blucli/                 # BluOS 控制
├── bluebubbles/            # iMessage (BlueBubbles)
├── camsnap/                # 摄像头捕获
├── canvas/                 # OpenClaw Canvas
├── clawhub/                # ClawHub CLI
├── coding-agent/           # 编码 Agent 委托
├── diffs/                  # Diff 视图生成
├── discord/                # Discord 集成
├── eightctl/               # Eight Sleep
├── feishu/                 # 飞书全家桶
├── gemini/                 # Gemini CLI
├── gh-issues/              # GitHub issues 自动化
├── gifgrep/                # GIF 搜索
├── github/                 # GitHub CLI
├── gog/                    # Google Workspace
├── goplaces/              # Google Places
├── healthcheck/            # 主机安全加固
├── himalaya/              # 邮件管理
├── imsg/                  # iMessage
├── mcporter/              # MCP 管理
├── memory-wiki/           # 知识库维护
├── model-usage/           # 模型费用统计
├── nano-pdf/              # PDF 编辑
├── node-connect/          # 节点连接诊断
├── notion/                # Notion
├── obsidian/              # Obsidian
├── obsidian-vault-maintainer/ # Obsidian 知识库
├── openai-whisper/        # 本地语音转文字
├── openai-whisper-api/    # OpenAI Whisper API
├── openclaw-ops/          # OpenClaw 运维（参考）
├── openclaw-session-cleaner/ # Session 清理
├── openhue/               # Hue 灯光
├── oracle/                # Oracle CLI
├── ordercli/              # 订餐查询
├── peekaboo/              # macOS UI 自动化
├── prose/                 # OpenProse 工作流
├── qqbot/                 # QQ Bot 全家桶
├── sag/                   # ElevenLabs TTS
├── session-logs/          # 会话日志搜索
├── sherpa-onnx-tts/       # 离线 TTS
├── skill-creator/         # Skill 创建
├── slack/                 # Slack 集成
├── songsee/               # 音频可视化
├── sonoscli/              # Sonos 控制
├── spotify-player/        # Spotify 控制
├── summarize/             # 内容摘要
├── taskflow/              # 工作流编排
├── taskflow-inbox-triage/ # 收件箱分类
├── tavily/                # Tavily 搜索
├── things-mac/            # Things 3
├── tmux/                  # tmux 控制
├── trello/                # Trello
├── video-frames/          # 视频帧提取
├── voice-call/             # 语音通话
├── wacli/                # WhatsApp
├── weather/               # 天气查询
└── xurl/                 # Twitter/X API
```

---

## License

All Skill files in this project are licensed under [CC BY-NC-SA 4.0](LICENSE) (Attribution-NonCommercial-ShareAlike).

For commercial use, please contact the author for authorization.
