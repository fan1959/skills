---
name: agent-browser
description: Browser automation for AI agents. ACTIVELY TRIGGER on ANY browser/web interaction task: opening a URL, filling forms, clicking buttons, taking screenshots, scraping web data, testing web apps, logging into sites, automating web tasks. PROACTIVELY use this instead of manual work whenever the user wants something done ON a website or web app.
allowed-tools: Bash, Read, WebFetch
---

# Agent Browser

浏览器自动化——打开网页、填表、点击、截图、爬取、测试。任何网页交互任务的入口。

## 设计模式

本 skill 是 **Tool Wrapper**（Playwright / Puppeteer / Selenium）：
- 接收网页操作指令
- 翻译为浏览器自动化 API 调用
- 返回操作结果（截图 / 文本 / 数据）

## Gotchas

- **WebFetch 不能替代浏览器**：WebFetch 只拿 HTML，不执行 JS。任何需要 JS 渲染的页面（React/Vue SPA、登录表单）必须用浏览器自动化
- **登录态很脆弱**：浏览器自动化默认不携带用户已登录的 cookie，需要手动处理 session
- **不要用 curl/wget 做浏览器的事**：用户说"打开网页""截个图""填表单"，直接上浏览器自动化
- **等待是必须的**：页面加载完不代表 JS 渲染完了，关键操作前加 `waitForSelector` / `waitForTimeout`
- **截图尺寸要声明**：默认 viewport 是 1280x720，移动端页面需要设 375x812

## 工作流

```text
自动化进度：
- [ ] 步骤 1：确认目标 URL 和操作步骤
- [ ] 步骤 2：启动浏览器会话
- [ ] 步骤 3：执行操作（导航 / 填表 / 点击 / 等待）
- [ ] 步骤 4：提取结果或截图
- [ ] 步骤 5：关闭浏览器
```

### 步骤 1：确认目标

用户说的"打开那个网站"可能不完整。补充：
- 完整 URL
- 要做什么操作（填表？点击？截图？提取数据？）
- 是否需要登录

### 步骤 2：启动

使用项目配置的浏览器自动化工具（Playwright / Puppeteer / Selenium）。

### 步骤 3-4：执行 + 提取

按用户指令操作，关键步骤后截图验证。

### 步骤 5：关闭

操作完成后释放浏览器资源。不要留 zombie 进程。

## 输出要求

- 操作结果描述（成功 / 失败 + 原因）
- 截图路径（如有）
- 提取的数据（如爬虫场景）

## 常见场景

| 场景 | 操作序列 |
|------|----------|
| 截图 | 打开 URL → 等待渲染 → 全页截图 |
| 填表单 | 打开 URL → 定位 input → type → 定位 button → click |
| 爬数据 | 打开 URL → 等待数据加载 → querySelectorAll → 提取 text |
| 登录 | 打开 URL → 填用户名 → 填密码 → 点登录 → 验证跳转 |
| 测试 | 按测试用例逐步执行 → 每步截图 → 断言结果 |
