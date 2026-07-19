# Skills

这是 Stitch 公开维护的一组 Agent Skills，偏实战、偏工作流，主要服务于 AI 工具使用、文档解读、项目配置、运维排障与技能分发。

和"技能清单"相比，这个仓库更适合被理解成一张**能力地图**：每个 skill 不只是一个说明文件，而是围绕某一类任务组织起来的可复用能力单元。

仓库包含 **110 个 skill**（60 个 OpenClaw 平台集成与工具封装 + 50 个 Claude Code 工作流与自动化）。

---

## Skill 地图

### 1. 平台集成类（Tool Wrapper / Pipeline）

这类 skill 把飞书、QQ、Discord、Slack、Notion 等外部平台的操作封装成可按需触发的上下文。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [feishu](skills/feishu/SKILL.md) | Tool Wrapper | 飞书文档、消息、审批等操作 |
| [qqbot](skills/qqbot/SKILL.md) | Tool Wrapper | QQ Bot 消息发送与接收 |
| [discord](skills/discord/SKILL.md) | Tool Wrapper | Discord 消息与频道管理 |
| [slack](skills/slack/SKILL.md) | Tool Wrapper | Slack 消息、频道、文件操作 |
| [notion](skills/notion/SKILL.md) | Tool Wrapper | Notion 页面与数据库操作 |
| [trello](skills/trello/SKILL.md) | Tool Wrapper | Trello 看板管理 |
| [obsidian](skills/obsidian/SKILL.md) | Tool Wrapper | Obsidian vault 读写操作 |
| [spotify-player](skills/spotify-player/SKILL.md) | Tool Wrapper | Spotify 音乐播放控制 |
| [sonoscli](skills/sonoscli/SKILL.md) | Tool Wrapper | Sonos 音箱控制 |
| [openhue](skills/openhue/SKILL.md) | Tool Wrapper | Philips Hue 灯光控制 |
| [wacli](skills/wacli/SKILL.md) | Tool Wrapper | WhatsApp 消息发送 |
| [xurl](skills/xurl/SKILL.md) | Tool Wrapper | URL 短链接与展开 |
| [imsg](skills/imsg/SKILL.md) | Tool Wrapper | iMessage 消息收发 |
| [voice-call](skills/voice-call/SKILL.md) | Tool Wrapper | 语音通话控制 |

---

### 2. 信息获取类（Tool Wrapper）

这类 skill 把外部信息源的查询能力固化为可复用流程。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [weather](skills/weather/SKILL.md) | Tool Wrapper | 天气查询 |
| [summarize](skills/summarize/SKILL.md) | Tool Wrapper | 网页/文本摘要 |
| [blogwatcher](skills/blogwatcher/SKILL.md) | Tool Wrapper | 博客更新监控 |
| [tavily](skills/tavily/SKILL.md) | Tool Wrapper | AI 搜索引擎 |
| [github](skills/github/SKILL.md) | Tool Wrapper | GitHub API 操作 |
| [gh-issues](skills/gh-issues/SKILL.md) | Tool Wrapper | GitHub Issues 管理 |
| [goplaces](skills/goplaces/SKILL.md) | Tool Wrapper | Google Places 查询 |
| [gifgrep](skills/gifgrep/SKILL.md) | Tool Wrapper | GIF 搜索 |
| [gemini](skills/gemini/SKILL.md) | Tool Wrapper | Google Gemini API |
| [oracle](skills/oracle/SKILL.md) | Tool Wrapper | Oracle 数据库查询 |

---

### 3. Prompt 工程类（Reviewer / Generator / Pipeline）

这类 skill 的核心是：**把模糊需求转成高质量 Prompt，或把 AI 生成文本改得更自然**。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [prompt-factory](skills/claudecode/prompt-factory.md) | Generator | 生成世界级 Prompt，69 个预设覆盖 15 个专业领域 |
| [prompt-optimizer](skills/claudecode/prompt-optimizer.md) | Reviewer / Generator | 优化 Prompt、改进 AI 指令、匹配提示词框架 |
| [prompt-caching](skills/claudecode/prompt-caching.md) | Best Practice | Prompt 缓存策略与优化 |
| [humanizer-zh](skills/claudecode/humanizer-zh.md) | Pipeline | 去除中文文本 AI 痕迹，基于维基百科 AI 写作特征指南 |
| [batch-humanizer](skills/claudecode/batch-humanizer.md) | Pipeline | 批量中文文档去 AI 味，多轮迭代 |
| [ai-slop-cleaner](skills/claudecode/ai-slop-cleaner.md) | Pipeline / Reviewer | AI 生成代码 slop 清理，回归安全删除优先 |

---

### 4. Claude Code 工作流类（Pipeline / Reviewer / Advisor）

这类 skill 的重点不是"直接干活"，而是**先诊断、先规划、再执行**，覆盖编码全生命周期。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [superpowers-zh](skills/superpowers-zh/SKILL.md) | Meta-skill | AI 编程超能力路由，20 个子技能覆盖脑暴→TDD→调试→审查→交付 |
| [planning-with-files-zh](skills/claudecode/planning-with-files-zh.md) | Pipeline | 基于文件的任务规划与进度跟踪 |
| [context-mode](skills/claudecode/context-mode.md) | Best Practice | 大输出场景上下文管理 |
| [context-mode-ops](skills/claudecode/context-mode-ops.md) | Pipeline | GitHub Issues/PR/Release 并行编排 |
| [self-improving-agent](skills/claudecode/self-improving-agent.md) | Pipeline | 自我进化 Agent，分析会话经验写入 CLAUDE.md |
| [memory-management](skills/claudecode/memory-management.md) | Tool Wrapper | 双层记忆系统（CLAUDE.md + memory/ 知识库） |
| [claude-md-improver](skills/claudecode/claude-md-improver.md) | Reviewer | CLAUDE.md 审计与改进 |
| [claude-automation-recommender](skills/claudecode/claude-automation-recommender.md) | Advisor | 分析代码库推荐 Claude Code 自动化方案 |
| [claude-obsidian](skills/claude-obsidian/SKILL.md) | Meta-skill | Obsidian 知识库集成路由，6 个子技能 |
| [karpathy-claude](skills/karpathy-claude/SKILL.md) | Best Practice | 5 条 LLM 编码避坑规则 |
| [ralph-loop](skills/claudecode/ralph-loop.md) | Pipeline | 自动化 Agent 驱动的开发循环 |
| [opencli-usage](skills/claudecode/opencli-usage.md) | Tool Wrapper | OpenCLI 使用指南 |
| [review-and-refactor](skills/claudecode/review-and-refactor.md) | Reviewer | 代码审查与重构 |

---

### 5. 扩展开发类（Generator / Documentation）

这类 skill 覆盖 Claude Code 插件、MCP Server、Hook、Skill 的完整开发流程。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [hook-factory](skills/claudecode/hook-factory.md) | Generator | 交互式 Hook 工厂，10 模板覆盖 7 种事件类型 |
| [hookify](skills/hookify/SKILL.md) | Tool Wrapper | Hook 创建，支持 9 种事件类型的安全管控 |
| [writing-hookify-rules](skills/writing-hookify-rules/SKILL.md) | Documentation | Hookify 规则语法参考 |
| [command-development](skills/claudecode/command-development.md) | Documentation | Claude Code 斜杠命令开发指南 |
| [plugin-structure](skills/claudecode/plugin-structure.md) | Documentation | Claude Code 插件结构与 manifest |
| [mcp-builder](skills/claudecode/mcp-builder.md) | Generator | MCP Server 构建指南（Python/Node） |
| [mcp-integration](skills/claudecode/mcp-integration.md) | Documentation | MCP Server 集成到 Claude Code 插件 |
| [skill-creator](skills/claudecode/skill-creator.md) | Generator | Skill 创建、优化、评测 |
| [skill-development](skills/claudecode/skill-development.md) | Documentation | Skill 结构与渐进式披露 |
| [skill-install](skills/claudecode/skill-install.md) | Tool Wrapper | Skill 安装与备用方案 |
| [find-skills](skills/claudecode/find-skills.md) | Tool Wrapper | 从 skills.sh 发现与安装技能 |

---

### 6. 安全与审计类（Reviewer / Tool Wrapper）

这类 skill 适合代码安全检查、质量评分和运行时管控。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [reins](skills/claudecode/reins.md) | Tool Wrapper | 运行时安全管控，PreToolUse/PostToolUse Hook + Watchtower |
| [security-review](skills/claudecode/security-review.md) | Reviewer | 安全审查清单与最佳实践 |
| [quality-auditor](skills/claudecode/quality-auditor.md) | Reviewer | 12 维质量审计与评分 |
| [system-doctor](skills/system-doctor/SKILL.md) | Tool Wrapper | 系统性能诊断（CPU / 内存 / 磁盘） |

---

### 7. 文档与内容生成类（Generator / Pipeline）

这类 skill 的核心是：**把结构化内容转成 Word / PDF / PPT / 网页交付**。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [docx](skills/claudecode/docx.md) | Generator | Word 文档生成，含目录、页码、格式 |
| [pdf-to-markdown](skills/claudecode/pdf-to-markdown.md) | Tool Wrapper | PDF 转 Markdown，支持 OCR |
| [ppt-master](skills/claudecode/ppt-master.md) | Generator | AI 多角色协作生成 PPT |
| [ppt-template-creator](skills/ppt-template-creator/SKILL.md) | Meta-skill | 从 .pptx 模板创建可复用 PPT Skill |
| [pptx-manipulation](skills/pptx-manipulation/SKILL.md) | Tool Wrapper | 编辑已有 .pptx 文件 |
| [gomoku-defense-ppt](skills/gomoku-defense-ppt/SKILL.md) | Generator | 五子棋毕设答辩 PPT（SCU 模板） |
| [guizang-ppt-skill](skills/guizang-ppt-skill/SKILL.md) | Generator | 横向翻页网页 PPT（瑞士风/杂志风） |
| [academic-essay](skills/claudecode/academic-essay.md) | Generator | 中英文学术论文，内置字数验证 |
| [academic-researcher](skills/claudecode/academic-researcher.md) | Reviewer / Generator | 学术文献综述与论文分析 |
| [api-docs](skills/claudecode/api-docs.md) | Generator | API 文档生成（JSDoc + OpenAPI） |
| [writing-skills](skills/claudecode/writing-skills.md) | Best Practice | 写作技巧与语法风格指导 |

---

### 8. 内容创作类（Generator / Pipeline）

这类 skill 把音乐、视频、音频文件的处理固化为可执行工作流。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [sag](skills/sag/SKILL.md) | Generator | AI 歌曲生成 |
| [songsee](skills/songsee/SKILL.md) | Tool Wrapper | 歌曲信息查询 |
| [video-frames](skills/video-frames/SKILL.md) | Tool Wrapper | 视频帧提取 |
| [nano-pdf](skills/nano-pdf/SKILL.md) | Tool Wrapper | 轻量 PDF 处理 |
| [openai-whisper](skills/openai-whisper/SKILL.md) | Tool Wrapper | 本地 Whisper 语音转文字 |
| [openai-whisper-api](skills/openai-whisper-api/SKILL.md) | Tool Wrapper | OpenAI Whisper API 语音转文字 |
| [sherpa-onnx-tts](skills/sherpa-onnx-tts/SKILL.md) | Tool Wrapper | 本地 TTS 文字转语音 |

---

### 9. 编码与自动化类（Tool Wrapper / Pipeline）

这类 skill 适合把日常开发中的固定操作固化为可复用流程。

| Skill | 模式 | 适用场景 |
|---|---|---|
| [coding-agent](skills/coding-agent/SKILL.md) | Pipeline | 编码 Agent 配置与优化 |
| [taskflow](skills/taskflow/SKILL.md) | Pipeline | 任务流管理 |
| [taskflow-inbox-triage](skills/taskflow-inbox-triage/SKILL.md) | Pipeline | 收件箱分类任务流 |
| [mcporter](skills/mcporter/SKILL.md) | Tool Wrapper | Minecraft 服务器管理 |
| [model-usage](skills/model-usage/SKILL.md) | Tool Wrapper | AI 模型用量监控 |
| [session-logs](skills/session-logs/SKILL.md) | Tool Wrapper | 会话日志管理 |
| [open-prose](skills/open-prose/SKILL.md) | Tool Wrapper | 开放文本处理 |
| [clawhub](skills/clawhub/SKILL.md) | Tool Wrapper | ClawHub 集成 |
| [n8n-skills](skills/n8n-skills/SKILL.md) | Meta-skill | n8n 工作流全栈路由，14 个子技能 |
| [openclaw-session-cleaner](skills/openclaw-session-cleaner/SKILL.md) | Tool Wrapper / Runbook | 清理 OpenClaw 膨胀的 session 文件 |

---

### 10. 浏览器与测试类（Tool Wrapper / Best Practice）

| Skill | 模式 | 适用场景 |
|---|---|---|
| [agent-browser](skills/claudecode/agent-browser.md) | Tool Wrapper | 浏览器自动化，网页操作、截图、爬取 |
| [playwright](skills/claudecode/playwright.md) | Best Practice | Playwright E2E 测试最佳实践 |

---

### 11. UI 设计类（Generator）

| Skill | 模式 | 适用场景 |
|---|---|---|
| [ui-design](skills/claudecode/ui-design.md) | Generator | UI 设计探索与灵感 |
| [ui-design-system](skills/claudecode/ui-design-system.md) | Generator | React UI 组件系统（TailwindCSS + Radix + shadcn/ui） |

---

### 12. 运维与排障类（Runbook / Tool Wrapper）

这类 skill 适合处理"系统坏了、服务挂了、命令不会用"的场景。

**这类 skill 的共同原则：**
- 先做状态检查，再决定是否修复
- 高影响动作（重启、repair、更新、配置修改）应先说明再执行

| Skill | 模式 | 适用场景 |
|---|---|---|
| [healthcheck](skills/healthcheck/SKILL.md) | Tool Wrapper | 服务健康检查 |
| [node-connect](skills/node-connect/SKILL.md) | Tool Wrapper | Node 服务连接管理 |
| [diffs](skills/diffs/SKILL.md) | Tool Wrapper | Git diff 增强工具 |

---

### 13. macOS / Apple 生态类（Tool Wrapper）

| Skill | 模式 | 适用场景 |
|---|---|---|
| [apple-notes](skills/apple-notes/SKILL.md) | Tool Wrapper | Apple Notes 读写 |
| [apple-reminders](skills/apple-reminders/SKILL.md) | Tool Wrapper | Apple Reminders 管理 |
| [things-mac](skills/things-mac/SKILL.md) | Tool Wrapper | Things 3 任务管理 |
| [bear-notes](skills/bear-notes/SKILL.md) | Tool Wrapper | Bear Notes 操作 |
| [peekaboo](skills/peekaboo/SKILL.md) | Tool Wrapper | 屏幕监控 |
| [bluebubbles](skills/bluebubbles/SKILL.md) | Tool Wrapper | BlueBubbles iMessage 服务 |
| [camsnap](skills/camsnap/SKILL.md) | Tool Wrapper | 摄像头快照 |
| [tmux](skills/tmux/SKILL.md) | Tool Wrapper | Tmux 会话管理 |

---

### 14. 命令行与工具类（Tool Wrapper）

| Skill | 模式 | 适用场景 |
|---|---|---|
| [1password](skills/1password/SKILL.md) | Tool Wrapper | 1Password CLI 密码管理 |
| [himalaya](skills/himalaya/SKILL.md) | Tool Wrapper | 终端邮件客户端 |
| [gog](skills/gog/SKILL.md) | Tool Wrapper | GOG 游戏平台 CLI |
| [eightctl](skills/eightctl/SKILL.md) | Tool Wrapper | 8x8 管理 CLI |
| [ordercli](skills/ordercli/SKILL.md) | Tool Wrapper | 命令行订单管理 |
| [canvas](skills/canvas/SKILL.md) | Tool Wrapper | Canvas 画布操作 |
| [blucli](skills/blucli/SKILL.md) | Tool Wrapper | 蓝牙 CLI 工具 |

---

### 15. 性格与知识类（API Wrapper / Tool Wrapper）

| Skill | 模式 | 适用场景 |
|---|---|---|
| [soultrace](skills/soultrace/SKILL.md) | API Wrapper | 5 色心理模型性格测试，25 种原型 |
| [memory-wiki](skills/memory-wiki/SKILL.md) | Tool Wrapper | 个人知识库管理 |

---

## 使用建议

### 什么时候优先选哪类 skill？

- **想接飞书/QQ/Discord/Slack 等平台** → 先看平台集成类 skill
- **想优化 Prompt / 去 AI 痕迹** → 先看 Prompt 工程类 skill
- **想在 Claude Code 里做开发全流程** → 先加载 `superpowers-zh` meta-skill
- **想开发 Claude Code 插件/Hook/MCP** → 用扩展开发类 skill
- **想做安全检查/质量评分** → 用安全审计类 skill
- **想生成 Word/PDF/PPT/网页** → 用文档内容生成类 skill
- **想把音乐/视频/音频加工处理** → 用内容创作类 skill
- **服务出问题、要排障** → 用运维排障类 skill
- **做性格测试/个人知识管理** → 用性格与知识类 skill
- **不确定用哪个** → 从 `superpowers-zh` 开始，它会自动路由

---

## 仓库设计原则

这批公有 skill 默认遵循这些原则：

1. **description 是给模型看的触发规则，不只是简介**
2. **SKILL.md 负责调度，细节尽量拆到 references / scripts / assets**
3. **默认先交付初稿，不自动做超出用户预期的后续动作**
4. **需要高影响操作时，先说明再执行**
5. **能脚本化的重复动作，尽量不要只写成文字说明**
6. **持续沉淀 Gotchas，降低误触发和翻车概率**

### 新增 skill 时建议遵循的规范

如果后面继续往这个仓库加新 skill，建议统一按这套来：

- **frontmatter 只保留 `name` 和 `description`**
- `description` 要同时写清：
  - 做什么
  - 什么时候触发
  - 必要时写一句不适用场景
- `SKILL.md` 优先写：
  - 适用边界
  - 设计模式（如 Tool Wrapper / Generator / Reviewer / Inversion / Pipeline / Meta-skill / Best Practice）
  - Gotchas
  - 工作流
  - 输出要求
- 如果 skill 逻辑较长，优先拆到：
  - `references/`：规范、模板、清单、补充文档
  - `scripts/`：可执行脚本
  - `assets/`：固定模板、示例资源
- 如果 skill 涉及高影响动作、自动复查、定时任务、外部写操作，要明确写出**确认门槛**
- 如果 skill 只是审查或规划类，默认遵循：**先审查 / 诊断，再出计划，确认后再修改**

---

## 安装

### Method 1: Claude Code plugin marketplace

在 Claude Code 中先添加这个仓库作为 plugin marketplace：

```bash
/plugin marketplace add fan1959/skills
```

然后通过 `/plugin` 交互界面浏览并安装需要的 plugin。

### Method 2: Ask a skill installer agent

如果你使用的 Agent 内置了 skill 安装器，可以直接发送指令：

- 安装全部：`安装 https://github.com/fan1959/skills 所有 skills`
- 安装某个：`安装 https://github.com/fan1959/skills 中的 mermaid skill`

### Method 3: Using [openskills](https://github.com/numman-ali/openskills)

```bash
openskills install fan1959/skills --global
```

### Method 4: 手动复制

```bash
git clone https://github.com/fan1959/skills.git
# Claude Code skills
cp -r skills/claudecode/* ~/.claude/skills/
# OpenClaw skills
cp -r skills/*/ ~/.openclaw/skills/
```

---

## 更新日志

| 日期 | 变更 |
|---|---|
| 2026-07-19 | README 重写为 chujianyun/skills 格式：15 类按模式+场景分组的表格 + 设计原则 + 使用建议；新增 12 个 Claude Code skill（claude-obsidian / gomoku-defense-ppt / guizang-ppt-skill / hookify / karpathy-claude / n8n-skills / ppt-template-creator / pptx-manipulation / soultrace / superpowers-zh / system-doctor / writing-hookify-rules），Claude Code skill 从 38 → 50，总数从 100 → 110 |
| 2025-04-22 | 初始 fork 自 [chujianyun/skills](https://github.com/chujianyun/skills) |

---

## License

All Skill files in this project are licensed under [CC BY-NC-SA 4.0](LICENSE-CC-BY-NC-SA) (Attribution-NonCommercial-ShareAlike).

For commercial use, please contact the author for authorization.
