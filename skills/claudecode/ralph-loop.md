---
name: ralph-loop
description: Automated agent-driven development loop. Define features as user stories with testable acceptance criteria, then run AI agents in a loop until all stories pass. Use when setting up autonomous coding workflows or CI-driven development pipelines.
---

# Ralph Loop

自动化 Agent 驱动的开发循环：用 User Story + Acceptance Criteria 驱动迭代开发。

## 设计模式

本 skill 采用 **Pipeline** 模式：
- 将功能需求拆解为 JSON 格式的 User Story（含验收条件）
- Agent 读取 Story → 实现 → 验证 → 标记完成
- 循环直到所有 Story 通过

## Gotchas

- **验收条件必须可测试**：不能用"界面好看"这类主观描述，要写"按钮点击后 200ms 内弹出对话框"
- **一个 Story 只做一件事**：不要在一个 Story 里塞"实现登录 + 注册 + 忘记密码"
- **Agent 循环需要明确的退出条件**：最大轮数、超时时间、全部 Story 通过
- **不要跳过验证步骤**：每个 Story 完成后必须跑对应测试，不能假设"应该没问题"
- **日志要完整**：每轮 Agent 的输出都记录到日志文件，出问题时能回溯

## 工作流

```text
循环进度：
- [ ] 步骤 1：编写 User Stories（JSON 格式）
- [ ] 步骤 2：配置 Agent 循环参数
- [ ] 步骤 3：启动循环
- [ ] 步骤 4：监控每轮输出
- [ ] 步骤 5：汇总结果
```

### 步骤 1：编写 User Stories

```json
{
  "story_id": "US-001",
  "title": "用户登录",
  "description": "用户输入邮箱和密码，点击登录按钮后进入主页",
  "acceptance_criteria": [
    "输入正确的邮箱密码 → 200ms 内跳转到 /home",
    "输入错误的密码 → 显示红色错误提示 '密码错误'",
    "连续 3 次错误 → 锁定账户 15 分钟"
  ],
  "status": "pending"
}
```

### 步骤 2：配置循环

- **Agent 类型**：编码 Agent（如 Claude Code）
- **最大轮数**：建议 20 轮（防止死循环）
- **超时**：每轮 300 秒
- **通过条件**：所有 acceptance_criteria 的测试 PASS

### 步骤 3：启动

```
Agent:
1. 读取 US-001 (status: pending)
2. 搜索代码库，理解现有登录逻辑
3. 实现登录功能
4. 写测试覆盖 3 条 acceptance criteria
5. 跑测试，全部 PASS 后标记 US-001 为 done
6. 写日志到 ralph_loop.log
7. 读取下一个 pending Story，重复
```

### 步骤 4：监控

```
=== Ralph Loop Round 3 ===
Agent: 正在处理 US-003 "用户头像上传"
测试: 4/4 PASS
本轮耗时: 45s
累计: US-001 ✅ / US-002 ✅ / US-003 ✅
```

### 步骤 5：汇总

```
=== Ralph Loop 完成 ===
总轮次: 5
处理 Story: 6/6 PASS
总耗时: 8 分 32 秒
日志: ralph_loop.log
```

## 输出要求

- 每个 Story 的 PASS/FAIL 状态
- 每轮的耗时和日志摘要
- 已完成的代码改动列表（文件 + 行数）
- 失败的 Story 附失败原因

## 参考资料

- User Stories 模板：`examples/user-stories-template.json`
- Ralph Loop 配置：`ralph.config.json`
