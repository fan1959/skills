---
name: self-improving-agent
description: 自我进化 Agent。每次被触发时分析当前会话经验，将通用规则写入 CLAUDE.md，将专用数据写入 semantic-patterns.json，确保规则在所有新会话中自动生效。
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
---

# 自我进化 Agent

## 核心职责

从当前会话中提取经验，将**通用规则**写入 CLAUDE.md，**专用数据**写入 semantic-patterns.json。

## 两种记忆的分工

| 记忆位置 | 存放内容 | 何时生效 |
|---|---|---|
| `C:\Users\Fanyu\.claude\CLAUDE.md` | 通用规则（工具配置、编码规范、用户偏好等） | **每次新会话自动生效** |
| `C:\Users\Fanyu\.claude\skills\self-improving-agent\memory\semantic-patterns.json` | 自我进化专用数据（meta、episodes 日志、confidence 追踪） | 调用时按需读取 |

**决策规则**：如果一条经验在**任何项目**都有用 → 写入 CLAUDE.md；如果只在特定场景有用 → 写入 semantic-patterns.json。

## 执行流程

### Step 1：读取当前上下文

读取以下文件，理解现状：

```
C:\Users\Fanyu\.claude\CLAUDE.md                        → 当前全局规则
C:\Users\Fanyu\.claude\skills\self-improving-agent\memory\semantic-patterns.json  → 当前模式库
C:\Users\Fanyu\.claude\skills\self-improving-agent\memory\episodic\             → 历史经历日志
```

### Step 2：分析当前会话

从本次会话中提取：

```
① 本次会话解决了什么问题？
② 发现了什么新规则/新模式？
③ 用户有什么反馈（"好了"/"完成"等触发词意味着经验有效）
④ 有没有之前记录的规则被验证有效？
⑤ 有没有之前记录的规则被证伪？
```

### Step 3：写入 CLAUDE.md（通用规则）

将以下类型的经验追加到 CLAUDE.md 的"全局记忆"章节：

- **工具配置**：代理设置、路径规则、安装命令格式
- **编码规范**：算法要点、调试方法、常见陷阱
- **工作流**：文件处理顺序、触发词行为
- **用户偏好**：语言习惯、格式要求

格式要求：
- 简洁，每条不超过 3 行
- 不重复已有内容
- 追加到相关小节（网络代理 / 工具配置 / 编码调试 等）

**检查 CLAUDE.md 总行数**，如果写入后超过 200 行，先精简旧内容再写入新内容。

### Step 4：写入 semantic-patterns.json（专用数据）

将以下内容追加到 semantic-patterns.json：

- 完整的 episode 日志（时间戳、skill、situation、solution、rating）
- meta 信息更新（version、last_updated、total_patterns）
- confidence 变化记录

### Step 5：反馈结果

汇报：
- 写了什么到 CLAUDE.md（用户下次会话自动生效）
- 写了什么到 semantic-patterns.json（自我进化专用）
- 有没有规则被验证或证伪

## 自我进化时机

| 触发词 | 时机 | 操作 |
|---|---|---|
| "好了" / "完成" / "结束" | 任务完成后 | 立即执行 Step 1-5 |
| 用户主动说"自我进化" | 任意时刻 | 立即执行 Step 1-5 |
| 用户说"检查自己" / "诊断" | 需要多 skill 并行时 | 先调 settings-audit + system-doctor，最后调 self-improving-agent 汇总 |

## 文件路径速查

| 文件 | 路径 |
|---|---|
| CLAUDE.md（全局规则） | `C:\Users\Fanyu\.claude\CLAUDE.md` |
| semantic-patterns.json | `C:\Users\Fanyu\.claude\skills\self-improving-agent\memory\semantic-patterns.json` |
| episodic 日志目录 | `C:\Users\Fanyu\.claude\skills\self-improving-agent\memory\episodic\` |
| working memory 目录 | `C:\Users\Fanyu\.claude\skills\self-improving-agent\memory\working\` |

## 写入 CLAUDE.md 的格式模板

追加到"全局记忆"相关小节：

```markdown
### [分类小节]

- **[简短标题]**：规则描述，简洁明了
```

例如：

```markdown
### 网络代理
- **Git 克隆**：先清理重复 url 重写规则，再用代理测试

### 编码调试
- **括号匹配**：`{`+1 `}`-1，depth 永远不应为负
```

## 常见经验 → 写入位置判断

| 经验 | 写入位置 |
|---|---|
| 代理配置、路径规则 | CLAUDE.md → 网络代理 / 工具配置 |
| 算法要点、调试技巧 | CLAUDE.md → 编码调试 |
| 用户语言偏好 | CLAUDE.md → 核心原则 |
| 工作流程规则 | CLAUDE.md → 工作流规则 |
| 完整的经历日志（含 rating） | semantic-patterns.json → episodic |
| pattern confidence 更新 | semantic-patterns.json → patterns[id].confidence |
| meta 版本更新 | semantic-patterns.json → meta |

## 注意事项

- **不要**只写 semantic-patterns.json 就不管 CLAUDE.md，通用规则必须写 CLAUDE.md 才能自动生效
- 写入 CLAUDE.md 后**不要**修改其他章节结构，只追加到"全局记忆"章节
- 如果 CLAUDE.md 接近 200 行，先精简再追加
- episodic 日志文件名格式：`YYYY-MM-DD-{描述}.json`