---
name: writing-hookify-rules
description: Hookify 规则语法参考。配套 hookify skill，详细说明 hook 规则的结构（event、matcher、command、timeout）及编写示例。当用户要编写或修改 hookify 规则时使用。
---

# Writing Hookify Rules

Hookify 规则的语法手册。配合 `hookify` skill 使用——hookify 负责选事件类型和部署，本 skill 负责规则的具体写法。

## 设计模式

本 skill 是 **Documentation** 型：
- 提供规则语法模板
- 给出常见场景的示例
- 不生成代码时作为参考查阅

## 规则结构

每条规则包含以下字段：

```json
{
  "event": "PreToolUse",
  "matcher": "Bash:rm *",
  "command": "echo 'Blocked'",
  "timeout": 2000
}
```

| 字段 | 必需 | 说明 |
|------|------|------|
| event | 是 | 事件类型：PreToolUse / PostToolUse / Stop 等 |
| matcher | 是 | 匹配模式，支持 glob 和正则 |
| command | 是 | 匹配时执行的命令 |
| timeout | 否 | 命令超时（ms），默认 5000 |

## Matcher 语法

### Glob 模式（默认）

```
Bash:git push*         # 匹配 git push / git push origin main
Bash:rm *              # 匹配 rm -rf / rm file.txt
Bash:npm install*      # 匹配 npm install / npm install --save
```

### 正则模式（以 ~ 开头）

```
~Bash:rm\s+-rf\s+/     # 匹配 rm -rf / 开头的命令
~Write:.*\.env          # 匹配写入 .env 文件
```

## 常用示例

### 阻止危险命令

```json
{
  "event": "PreToolUse",
  "matcher": "Bash:rm -rf /*",
  "command": "echo 'Dangerous: rm -rf / blocked'",
  "timeout": 500
}
```

### 自动放行安全命令

```json
{
  "event": "PreToolUse",
  "matcher": "Bash:git status",
  "command": "echo 'auto-allowed'",
  "timeout": 500
}
```

### 操作后记录日志

```json
{
  "event": "PostToolUse",
  "matcher": "Write:*",
  "command": "echo \"[$(date)] File written: ${MATCH}\" >> ~/.claude/audit.log",
  "timeout": 1000
}
```

## Gotchas

- **Matcher 不支持空格分隔的多模式**：匹配多个文件类型用 `Write:*.{js,ts,py}` 不是 `Write:*.js *.ts`
- **PostToolUse 中 `${MATCH}` 是实际调用的工具名+参数**：不是 matcher 模式本身
- **Hook 脚本的 exit code**：非 0 = deny，0 = allow，无输出 = ask
- **规则顺序影响行为**：PreToolUse 的多条规则按顺序匹配，第一条匹配的生效
- **timeout 超时后走默认行为（ask）**：重要的 deny 规则 timeout 可以设短一点

## 工作流

```text
规则编写进度：
- [ ] 步骤 1：确定触发事件和条件
- [ ] 步骤 2：选择 matcher 类型（glob / regex）
- [ ] 步骤 3：编写匹配模式
- [ ] 步骤 4：编写处理命令
- [ ] 步骤 5：测试匹配逻辑
```

### 步骤 1-2

先确定：
- 在哪一步拦截？（Pre/Post）
- 精确匹配还是模糊匹配？
- 需要访问匹配内容吗？（需要则用正则捕获组）

### 步骤 3-4

- glob 模式写出来用具体例子验证
- 正则模式先在测试工具里验证
- 命令保持简短，复杂逻辑写到独立脚本

### 步骤 5：测试

- 先在 dry run 模式确认匹配
- 再用实际工具调用验证
- 检查 hook 输出是否符合 JSON 协议

## 输出要求

- 完整的规则 JSON
- 一段话说明这条规则做什么
- 部署位置（settings.json 的哪个 hooks 数组）

## 参考资料

- `hookify` skill：事件类型选择和整体部署
- Claude Code Hook 官方文档
