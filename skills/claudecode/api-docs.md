---
name: api-docs
description: Generate API documentation from source code with JSDoc and OpenAPI support. Use when user asks to generate API docs, document endpoints, or add JSDoc comments.
allowed-tools: Read, Write, Grep, Glob, Bash
---

# API Docs

从 TypeScript/JavaScript 源码自动生成 API 文档，含 JSDoc 注释补全和 OpenAPI 规范输出。

## 设计模式

本 skill 采用 **Generator** 模式：
- 扫描源码中的 public 导出（函数、类、接口、HTTP 端点）
- 解析已有的 JSDoc 注释（`@param`、`@returns`、`@throws`、`@example`）
- 为缺失文档的 API 自动补全 JSDoc
- 对 HTTP 端点生成 OpenAPI 3.0 规范

## Gotchas

- **不要改函数签名**：只补文档，不改逻辑和接口
- **推断类型要保守**：如果不能确定参数类型，用 `{unknown}` 而不是瞎猜
- **OpenAPI 路径要完整**：包含 base path 和版本前缀（如 `/api/v1/users`）
- **已有文档不覆盖**：如果 @param 已存在但描述不完整，只补充不替换
- **MCP dispatch 是可选的**：如果项目没有配置 MCP 工作流，直接操作文件

## 工作流

```text
生成进度：
- [ ] 步骤 1：扫描源码中的 public API
- [ ] 步骤 2：解析已有 JSDoc
- [ ] 步骤 3：补全缺失文档
- [ ] 步骤 4：生成 OpenAPI 规范（如有 HTTP 端点）
- [ ] 步骤 5：验证生成结果
```

### 步骤 1：扫描

```bash
# 找到所有 public 导出
grep -rn "export (function|class|interface|const|type)" src/ --include="*.ts"
```

或使用项目配置的 glob 模式。

### 步骤 2：解析

对每个 public API，检查是否有前导 JSDoc 注释块。提取已有标签。

### 步骤 3：补全

对缺失或不全的注释补全：

```typescript
/**
 * @brief 一句话描述函数功能
 * @param userId - 用户 ID
 * @returns 用户详情对象
 * @throws {NotFoundError} 用户不存在时抛出
 * @example
 * const user = await getUserById("123");
 */
export async function getUserById(userId: string): Promise<User> { ... }
```

### 步骤 4：OpenAPI

对于 HTTP 端点（Express/Fastify/Koa 路由），生成 OpenAPI 3.0 片段：

```yaml
/users/{id}:
  get:
    summary: 获取用户详情
    parameters:
      - name: id
        in: path
        required: true
        schema:
          type: string
    responses:
      '200':
        description: 用户详情
```

### 步骤 5：验证

用对应工具验证生成的文档格式正确（如 `swagger-cli validate`）。

## 输出要求

- 修改后的源文件（补全了 JSDoc）
- 如生成 OpenAPI：`openapi.json` 或 `openapi.yaml`
- 统计：补了多少个函数/参数的文档
