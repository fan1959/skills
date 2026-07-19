---
name: playwright
description: Playwright end-to-end testing best practices for web applications, covering test design, locator strategies, and assertion patterns. Use when writing, reviewing, or debugging Playwright E2E tests.
allowed-tools: Read, Write, Bash
---

# Playwright

Playwright E2E 测试最佳实践——test 设计、locator 策略、断言模式。

## 设计模式

本 skill 是 **Best Practice**：
- 提供 Playwright 测试的惯用写法和反模式
- 代码审查时对照检查
- 不替代 Playwright 官方文档，而是补充实战经验

## Gotchas

- **用 `page.waitForSelector` 不如用 `expect(locator).toBeVisible()`**：后者自带超时和重试，失败时输出更友好
- **不要用 CSS class 做 locator**：class 会变。用 `getByRole` / `getByLabel` / `getByTestId` 优先级从高到低
- **`page.evaluate` 是 escape hatch**：能用 locator API 就不用 evaluate，后者脱离 Playwright 的自动等待
- **不要串行写长测试**：一个 test 只测一个用户行为。10 个 5 行的 test >> 1 个 50 行的 test
- **CI 超时默认不够**：headless CI 比本地慢，`expect` timeout 至少 10s，test timeout 至少 30s

## Locator 优先级

| 优先级 | API | 示例 |
|--------|-----|------|
| 1 (最佳) | `getByRole` | `page.getByRole('button', { name: '提交' })` |
| 2 | `getByLabel` | `page.getByLabel('邮箱')` |
| 3 | `getByPlaceholder` | `page.getByPlaceholder('请输入')` |
| 4 | `getByText` | `page.getByText('确认删除')` |
| 5 | `getByTestId` | `page.getByTestId('submit-btn')` |
| 6 (最后) | CSS/XPath | `page.locator('.btn-primary')` |

## 工作流

```text
测试编写进度：
- [ ] 步骤 1：确认用户行为（不是实现细节）
- [ ] 步骤 2：选 locator 策略
- [ ] 步骤 3：写 arrange → act → assert
- [ ] 步骤 4：跑测试验证稳定性（3 次全过）
```

### 步骤 1：确认行为

测试描述应该是用户视角：
- ✅ "用户可以输入邮箱和密码登录"
- ❌ "点击第 3 个 div 里的第 2 个 button"

### 步骤 2：选 locator

从上表优先级 1→6 选择。如果没有任何语义化选择器可用，加 `data-testid` 属性。

### 步骤 3：AAA 模式

```typescript
test('用户可以用邮箱和密码登录', async ({ page }) => {
  // Arrange
  await page.goto('/login');

  // Act
  await page.getByLabel('邮箱').fill('test@example.com');
  await page.getByLabel('密码').fill('password123');
  await page.getByRole('button', { name: '登录' }).click();

  // Assert
  await expect(page.getByText('欢迎回来')).toBeVisible();
});
```

### 步骤 4：验证稳定性

同一个 test 连续跑 3 次，全部通过才算稳定。有 flaky 立即修。

## 常见反模式

| 反模式 | 正确写法 |
|--------|----------|
| `page.waitForTimeout(3000)` | `await expect(locator).toBeVisible()` |
| `page.locator('.btn')` | `page.getByRole('button')` |
| `page.evaluate(() => document.title)` | `await expect(page).toHaveTitle('...')` |
| 一个 test 测 5 个功能 | 拆成 5 个独立 test |
| `page.click({ force: true })` | 检查是否有 overlay 遮挡，修代码而非 force |

## 输出要求

- 可运行的 `.spec.ts` 文件
- 使用 AAA 模式
- locator 优先语义化
- 3 次连续跑全通过
