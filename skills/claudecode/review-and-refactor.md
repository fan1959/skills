---
name: review-and-refactor
description: Review and refactor code in your project according to defined instructions. Use when completing tasks, implementing major features, or before merging to verify work meets requirements.
allowed-tools: Read, Glob, Grep, Edit, Write, Bash
---

# Review and Refactor

审查代码质量并执行必要的重构，确保代码干净、可维护、符合项目规范。

## 设计模式

本 skill 采用 **Reviewer** 模式：
- 先读取项目的编码规范（`.github/instructions/*.md`、`CLAUDE.md`、`.clang-format` 等）
- 再审查目标代码的命名、结构、重复逻辑、潜在 bug
- 给出问题列表，按严重程度排序
- 确认后逐项修复

## Gotchas

- **先读规范再动手**：每个项目有自己的编码风格，不要用个人偏好替代项目规范
- **不要顺手重构无关代码**：只改目标范围内的代码，遵循 Surgical Changes 原则
- **不要破坏测试**：修改后必须跑相关测试，失败就回退
- **重构不是重写**：保持现有 API 和文件结构不变，除非用户明确说要拆文件
- **三个相似的 if 比一个 premature abstraction 好**：不要为了"优雅"引入不必要的抽象层

## 工作流

```text
审查进度：
- [ ] 步骤 1：读取编码规范
- [ ] 步骤 2：审查目标代码
- [ ] 步骤 3：列出问题（按严重度排序）
- [ ] 步骤 4：用户确认修改方案
- [ ] 步骤 5：执行重构
- [ ] 步骤 6：验证测试通过
```

### 步骤 1：读取规范

快速扫描项目中的编码规范文件：
- `.github/instructions/*.md`
- `.github/copilot-instructions.md`
- `CLAUDE.md`
- `.clang-format` / `.eslintrc` / `.prettierrc`
- 项目的 `CONTRIBUTING.md`

如果没有任何规范文件，用业界通用最佳实践作为默认标准。

### 步骤 2：审查代码

重点检查：
- **命名**：变量/函数/类名是否清晰、一致
- **重复**：是否有 copy-paste 代码可以提取
- **复杂度**：单个函数是否过长（> 50 行）
- **错误处理**：边界条件、null 检查、异常处理
- **安全**：SQL 注入、XSS、硬编码密钥
- **测试**：关键路径是否有测试覆盖

### 步骤 3：列出问题

每项问题标注：
- **严重度**：🔴 必须修 / 🟡 建议修 / 🟢 可选
- **位置**：文件名 + 行号
- **问题描述**：一句话说清楚
- **修复建议**：具体的代码改动方向

### 步骤 4：确认方案

把问题清单呈现给用户，询问哪些要修。**不要擅自修改。**

### 步骤 5：执行重构

逐项修复已确认的问题。保持每次改动最小化。

### 步骤 6：验证

```bash
# 跑相关测试
npm test -- --related  # 或项目对应的测试命令
```

测试失败立即排查，不通过不交付。

## 输出要求

- 问题清单（严重度 + 位置 + 描述 + 建议）
- 修改后的文件 diff
- 测试结果（PASS/FAIL）
- 不做的问题注明原因
