---
name: superpowers-zh
description: AI 编程超能力中文增强版。20 个子技能覆盖完整开发周期：头脑风暴、TDD、系统调试、编写方案、子智能体驱动开发、完工前自查、请求/接收代码审查、中文系列（提交规范/文档/git 工作流）、git worktree 隔离开发。收到任何消息后立即评估可用的子技能。
---

# Superpowers ZH

AI 辅助编程的 20 个超能力，中文优化，覆盖从需求到交付的全流程。

## 设计模式

本 skill 是 **Meta-skill**：收到用户消息后自动扫描关键词，匹配并加载对应子技能。

核心元规则：**哪怕只有 1% 可能性也得先评估可用子技能。**

## 子技能索引

### 开发流程

| 子技能 | 触发词 | 适用阶段 |
|--------|--------|----------|
| brainstorming | 脑暴、头脑风暴、想法 | 需求探索 |
| test-driven-development | TDD、写测试、先写测试 | 编码 |
| systematic-debugging | 调试、bug、异常、为什么 | 排错 |
| writing-plans | 写计划、方案设计、架构 | 设计 |
| executing-plans | 执行计划、按步骤 | 实施 |
| subagent-driven-development | 子智能体、并行任务 | 大任务拆分 |
| dispatching-parallel-agents | 子智能体并行、多个独立任务 | 并行执行 |
| verification-before-completion | 完工前检查、交付前验证 | 交付 |

### 代码审查

| 子技能 | 触发词 | 适用阶段 |
|--------|--------|----------|
| requesting-code-review | code review、审查、review | 提交前 |
| receiving-code-review | 接受 review、review 反馈 | 收到反馈后 |

### 中文系列

| 子技能 | 触发词 | 适用场景 |
|--------|--------|----------|
| chinese-commit-convention | 提交规范、commit message | Git 提交 |
| chinese-documentation | 中文文档、项目文档 | 文档编写 |
| chinese-git-workflow | git 工作流、分支管理 | Git 操作 |
| chinese-code-review | 中文代码审查 | 代码审查 |

### 工程实践

| 子技能 | 触发词 | 适用场景 |
|--------|--------|----------|
| using-git-worktrees | git worktree、分支隔离 | 多分支并行开发 |

## Gotchas

- **即使只有 1% 可能性也要触发**：宁可多加载也不漏掉——这是最核心的元规则
- **优先级**：用户指令 > Superpowers 子技能 > 系统默认行为
- **子技能可能有重叠**：同时匹配多个时，按开发流程阶段选最合适的
- **不要假设用户知道子技能名**：用户说"帮我看看这个 bug"，你应该加载 `systematic-debugging`，而不是问"要不要用 systematic-debugging"

## 工作流

```text
路由进度：
- [ ] 步骤 1：扫描用户消息关键词
- [ ] 步骤 2：匹配子技能（可能多个）
- [ ] 步骤 3：按优先级选择
- [ ] 步骤 4：加载并执行子技能
- [ ] 步骤 5：回到主流程
```

### 步骤 1：关键词扫描

对照触发词表扫描用户消息。中英文都匹配。

### 步骤 2-3：匹配与选择

如果匹配到多个子技能：
- 用户当前在编码 → 优先 TDD / debugging
- 用户要交付 → 优先 verification / code-review
- 用户在做设计 → 优先 brainstorming / writing-plans

### 步骤 4-5：加载执行

加载子技能的 SKILL.md，按子技能工作流执行，完成后回到主流程。

## 输出要求

- 简要说明加载了哪个子技能及原因（一句话）
- 子技能的具体输出按各自规范

## 参考资料

- 所有子技能的 SKILL.md 在 `skills/superpowers-zh/` 目录下
- 原始 superpowers skill（英文版）
