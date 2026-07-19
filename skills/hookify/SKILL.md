---
name: hookify
description: Claude Code Hook 创建与管理。支持 PreToolUse / PostToolUse / Stop / SubagentStop / SessionStart / SessionEnd / UserPromptSubmit / PreCompact / Notification 九种事件类型的钩子。用于阻止危险命令、添加审计日志、自定义工作流自动化。
---

# Hookify

为 Claude Code 创建事件驱动的钩子，实现安全管控和工作流自动化。

## 设计模式

本 skill 采用 **Tool Wrapper** 模式：
- 分析用户的安全/自动化需求
- 选择合适的 hook 事件类型
- 生成 hook 配置并写入 `.claude/settings.json`

## 支持的事件类型

| 事件 | 触发时机 | 典型用途 |
|------|----------|----------|
| PreToolUse | 工具调用前 | 阻止危险命令、权限检查 |
| PostToolUse | 工具调用后 | 审计日志、自动提交 |
| Stop | 会话停止时 | 清理临时文件、通知 |
| SessionStart | 会话开始时 | 环境检查、状态恢复 |
| UserPromptSubmit | 用户提交 prompt | 输入预处理 |
| PreCompact | 上下文压缩前 | 保存关键记忆 |
| Notification | 通知事件 | 外部通知集成 |

## Gotchas

- **Hook 返回 JSON 协议**：必须返回 `{"hookSpecificOutput": {"hookEventName": "...", "permissionDecision": "allow"|"deny"|"ask"}}`，不输出则走默认 ask 流程
- **PreToolUse 不能阻塞太久**：hook 脚本执行超时会影响用户体验，控制在 2 秒内
- **不要跳过 hook 链**：如果同时有多个 hook 匹配，全部都会执行，注意顺序
- **路径用绝对路径**：hook 脚本路径必须用绝对路径或 `${CLAUDE_PLUGIN_ROOT}` 变量
- **权限放行粒度要细**：避免 `Bash:*` 这种全部放行，至少精确到 `Bash:git status`

## 工作流

```text
Hook 创建进度：
- [ ] 步骤 1：明确需求和触发条件
- [ ] 步骤 2：选择事件类型
- [ ] 步骤 3：编写 hook 规则
- [ ] 步骤 4：测试 hook 行为
- [ ] 步骤 5：部署到 settings.json
```

### 步骤 1：明确需求

问用户：
- 要拦截/增强什么操作？
- 触发条件是什么（特定命令、文件模式、工具类型）？
- 预期行为（允许/拒绝/询问/记录）？

### 步骤 2：选择事件

- 在工具执行**前**检查 → PreToolUse
- 在工具执行**后**记录 → PostToolUse
- 会话级别事件 → SessionStart / SessionEnd / Stop
- 输入预处理 → UserPromptSubmit

### 步骤 3：编写规则

参考 `writing-hookify-rules` skill 的规则语法编写。

### 步骤 4：测试

先用 `dry_run` 模式验证匹配逻辑，确认无误后再启用。

### 步骤 5：部署

写入 `.claude/settings.json` 或 `.claude/settings.local.json`。

## 输出要求

- 完整的 hook 配置 JSON
- 说明部署到哪个 settings 文件（local / project / user）
- 给出验证命令

## 参考资料

- 规则语法：`writing-hookify-rules` skill
- Hook 开发指南：`hook-development` skill
