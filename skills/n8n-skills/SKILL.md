---
name: n8n-skills
description: n8n 工作流自动化全栈技能路由。14 个子技能覆盖：n8n-mcp 工具专家、表达式语法、工作流模式、验证专家、节点配置、JavaScript/Python 代码节点、错误处理、二进制数据、子工作流、AI Agent、多实例部署、自托管运维。当用户提到 n8n、工作流、自动化流程等关键词时自动路由。
---

# n8n Skills

n8n 工作流自动化的全栈技能集合，从节点配置到生产部署全覆盖。

## 设计模式

本 skill 是 **Meta-skill**，根据用户的具体任务路由到 14 个子技能之一。

## 子技能索引

| 子技能 | 职责 | 使用场景 |
|--------|------|----------|
| using-n8n-mcp-skills | 顶层路由 | 不确定用哪个子技能时 |
| n8n-mcp-tools-expert | MCP 工具深度使用 | search_nodes / get_node / validate_node |
| n8n-expression-syntax | n8n 表达式语法 | 写 `{{ }}` 表达式、数据转换 |
| n8n-workflow-patterns | 工作流设计模式 | 设计复杂流程、最佳实践 |
| n8n-validation-expert | 工作流验证 | 部署前检查、错误排查 |
| n8n-node-configuration | 节点参数配置 | 配置特定节点的 resource/operation |
| n8n-code-javascript | JavaScript 代码节点 | 写 JS 转换逻辑 |
| n8n-code-python | Python 代码节点 | 写 Python 转换逻辑 |
| n8n-error-handling | 错误处理策略 | 重试、fallback、告警 |
| n8n-binary-data | 二进制数据处理 | 文件上传下载、格式转换 |
| n8n-subworkflows | 子工作流 | 模块化复用、流程拆分 |
| n8n-agents | AI Agent 工作流 | LLM 驱动的自动化 |
| n8n-multi-instance | 多实例管理 | 队列模式、负载均衡 |
| n8n-self-hosting | 自托管运维 | Docker 部署、升级、备份 |

## Gotchas

- **必须先路由**：不要直接给用户答案，先确定场景 → 匹配子技能，然后加载子技能执行
- **n8n 版本差异**：节点参数在版本间可能变化，不确定时用 `get_node` 查最新 schema
- **表达式引号**：n8n 表达式内字符串用单引号 `'{{$json.name}}'`，双引号会破坏 JSON
- **Code 节点沙箱**：JavaScript 代码节点不能 `require`，只能用内置全局函数

## 工作流

```text
路由进度：
- [ ] 步骤 1：识别 n8n 任务类型
- [ ] 步骤 2：匹配子技能
- [ ] 步骤 3：加载并执行子技能
- [ ] 步骤 4：验证输出
```

### 步骤 1：识别任务

- 用户问 "怎么配 X 节点" → n8n-node-configuration
- 用户问 "表达式怎么写" → n8n-expression-syntax
- 用户问 "工作流报错" → n8n-error-handling 或 n8n-validation-expert
- 用户问 "部署/运维" → n8n-self-hosting 或 n8n-multi-instance
- 用户问 "AI Agent 自动化" → n8n-agents
- 不确定 → using-n8n-mcp-skills（顶层路由再判断）

### 步骤 2-4

加载子技能 → 按子技能工作流执行 → 验证结果。

## 输出要求

- 路由结果：说明匹配的子技能及原因
- 子技能执行结果：按子技能自身的输出规范

## 参考资料

- 所有子技能的 SKILL.md 在 `skills/n8n-*/` 目录下
- n8n 官方文档：https://docs.n8n.io
