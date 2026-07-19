---
name: claude-obsidian
description: Obsidian 知识库 + Claude Code 集成。子技能涵盖 vault 初始化、canvas 画布、会话存档、网页去杂、Obsidian Markdown 语法、Bases 数据库视图。当用户提到 Obsidian、wiki、canvas、保存对话、obsidian markdown 时自动路由到对应子技能。
---

# Claude Obsidian

把 Claude Code 会话中的知识和产物无缝写入 Obsidian 知识库。

## 设计模式

本 skill 是 **Meta-skill**，根据用户意图路由到 6 个子技能：

| 子技能 | 职责 |
|--------|------|
| wiki | 初始化 / 检查 vault 结构 |
| canvas | 创建或更新 visual canvas（图片、文本、PDF、笔记） |
| save | 将当前对话或洞察存档为结构化笔记 |
| defuddle | 剥离网页杂乱内容，输出干净 Markdown |
| obsidian-markdown | 编写正确的 Obsidian Flavored Markdown（wikilink、callout、embed 等） |
| obsidian-bases | 创建和编辑 .base 文件（动态表格、卡片视图、过滤、公式） |

## Gotchas

- 不要跳过路由直接操作 vault 文件——先判断用户意图再选子技能
- Wikilink 语法是 `[[页面名]]`，不是标准 Markdown 链接 `[text](url)`
- Canvas JSON 节点坐标是绝对像素值，新增节点时要避免重叠
- Callout 语法 `> [!type]` 的第一行决定了渲染样式，type 拼错整个块不渲染
- 保存对话时优先提取洞察和决策，不要整段复制聊天记录

## 工作流

```text
路由进度：
- [ ] 步骤 1：识别用户意图（新建/查询/存档/可视化？）
- [ ] 步骤 2：匹配子技能
- [ ] 步骤 3：加载子技能并执行
- [ ] 步骤 4：确认写入结果
```

### 步骤 1：识别意图

- 用户说 "obsidian" / "wiki" → 检查 vault 是否存在，不存在则 bootstrap
- 用户说 "canvas" / "画布" → 准备 canvas 操作
- 用户说 "save this" / "保存" → 提取当前对话精华
- 用户说 "defuddle" / "清洗" → 抓取 + 清洗 URL 内容
- 用户说 "wikilink 格式" / "callout" → 提供 OFM 语法参考
- 用户说 "base" / "数据库视图" → 创建 .base 文件

### 步骤 2：加载子技能

确定意图后，读取对应子技能的 SKILL.md 获取详细指令。

### 步骤 3：执行

按照子技能的工作流执行，不跳过 Gotchas 检查。

### 步骤 4：确认

操作完成后向用户报告：写入路径、文件大小、关键内容摘要。

## 输出要求

- 创建/修改文件后报告实际路径和行数
- Canvas 操作后说明添加了哪些节点
- 归档对话时给出笔记标题和 wiki 路径

## 参考资料

- [Obsidian Flavored Markdown 官方文档](https://help.obsidian.md)
- 子技能 SKILL.md 在各自目录下
