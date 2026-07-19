---
name: karpathy-claude
description: Andrej Karpathy 编码经验提炼的 5 条 LLM 编码避坑规则。写代码、改代码、debug、refactor、simplify、review code 等任何编码任务前必须先读。规则：Think Before Coding / Simplicity First / Surgical Changes / Goal-Driven Execution / Verify Before Shipping。
---

# Karpathy Claude

Karpathy 的 LLM 编码实战教训，浓缩为 5 条规则。每次编码前过一遍，避免踩坑。

## 设计模式

本 skill 是 **Best Practice** 清单，不生成代码，不调用工具——只在脑内执行检查。

## 五条规则

### 1. Think Before Coding
拿到需求先想清楚：输入是什么？输出是什么？边界条件有哪些？不要上来就写代码。

### 2. Simplicity First
能用 3 行解决的问题不写 30 行。不要为"未来可能需要"的功能提前抽象。三个相似的 if 比一个 premature 的 strategy pattern 更好。

### 3. Surgical Changes
改什么就只动什么。不要顺手重构周围代码、不要统一命名风格、不要删"看起来没用"的注释。每次改动范围越小，引入 bug 的概率越低。

### 4. Goal-Driven Execution
每步操作前问自己：这一步让代码离目标更近了吗？如果答案不是明确的"是"，停下来重新想。

### 5. Verify Before Shipping
写完代码后必须验证：编译通过？测试通过？核心路径手动跑过？不要赌"应该没问题"。

## Gotchas

- 这 5 条是心智模型，不是 Checklist——不需要逐条打勾，但每次编码前扫一眼
- 第 3 条（Surgical Changes）和第 2 条（Simplicity First）容易冲突：重构是好事，但"顺手重构"是坏事
- 如果用户明确说"顺带重构"，听用户的——这不是顺手，是有意为之
- 5 条规则的优先级：Goal-Driven > Surgical > Simplicity > Think > Verify

## 触发词

以下任一关键词出现在用户消息中时立即加载本 skill：
- `写代码` `加功能` `实现` `新增`
- `改 bug` `修 bug` `修复` `调试` `debug`
- `重构` `refactor` `简化` `simplify`
- `review` `审查` `检查代码`

## 输出要求

本 skill 不产生文件输出。在脑内执行规则检查后转入正常编码流程。
