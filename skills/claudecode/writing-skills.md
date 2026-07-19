---
name: writing-skills
description: Master the art of clear, effective writing. Use when the user wants to improve their writing, needs help with grammar, style, tone, or structure, or asks for writing tips, editing advice, or how to write better. Triggers on: writing, edit, grammar, style, tone, structure, clarity, proofread, revise.
allowed-tools: Read, Write, Edit, Bash
---

# Writing Skills

系统化的写作指导，覆盖清晰表达、结构优化、风格选择三大维度。

## 设计模式

本 skill 是 **Best Practice + Reviewer**：
- 提供核心写作原则和检查清单
- 审查用户文本并给出具体修改建议
- 不自动改写——先指出问题，用户确认后再改

## 核心原则

### 1. 清晰第一

- 用简单直接的语言，不用 jargon
- 一句话只讲一个点
- 复杂概念拆成 2-3 句

### 2. 结构优先

- 最重要的信息放最前面
- 段落是一个想法单元，不是视觉分隔
- 有逻辑流：问题 → 分析 → 结论

### 3. 主动语态

- 主语明确，动词有力
- 具体 > 抽象（"30 个用户反馈了 X" 比 "多数用户不满意" 好）
- 展示 > 告知（给例子而不是形容词）

## Gotchas

- **不要为了"看起来专业"用复杂词**：写 "use" 不写 "utilize"，写 "结束" 不写 "画上圆满的句号"
- **中文写作特别注意**：避免"在 XXX 时代背景下""具有重要意义"等模板句——这些是 AI 痕迹
- **技术文档不是论文**：不需要"引言-文献综述-方法论"结构，直接讲"这是做什么的 → 怎么用 → 注意什么"
- **修改前先问目标受众**：写给老板的报告和写给同事的文档语气完全不同
- **不要过度编辑**：用户只是问"有没有语法错误"，不要主动改风格

## 风格选择

| 风格 | 适用场景 | 特征 |
|------|----------|------|
| 正式 | 报告、论文、公文 | 完整句、无缩写、精确词汇 |
| 技术 | 文档、README、API | 清晰定义、步骤化、示例驱动 |
| 创意 | 博客、故事、文案 | 形象描述、句式变化、情感共鸣 |
| 简洁 | 邮件、通知、Slack | 短句、要点优先、可快速扫描 |

## 常见问题 & 修复

### 啰嗦

```
❌ "In order to accomplish the task of processing the data..."
✅ "To process the data..."
```

### 歧义

```
❌ "This indicates that the system needs improvement."
✅ "The 3-second response time indicates a caching issue."
```

### 被动语态

```
❌ "The report was written by the team."
✅ "The team wrote the report."
```

### 中文 AI 模板句

```
❌ "在当今数字化转型的时代背景下，人工智能技术具有重要的应用价值"
✅ "AI 可以帮我们自动分类客服工单，每天省 3 小时"
```

## 编辑 Checklist

- [ ] 第一句能让读者知道这篇文章讲什么？
- [ ] 每段只讲一个想法？
- [ ] 有没有可以删掉的不必要词？
- [ ] 主动语态占比 > 70%？
- [ ] 技术术语有没有解释？
- [ ] 例子具体吗（有数字/名字/场景）？
- [ ] 语气适合目标受众吗？

## 配合

- 中文去 AI 痕迹：`humanizer-zh`（单次处理）/ `batch-humanizer`（批量多轮）
- 代码注释审查：`ai-slop-cleaner`
- 学术论文：`academic-essay`（内置字数验证 + .docx 输出）
