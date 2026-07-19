---
name: ui-design
description: Use this to design a nice UI in single HTML as inspiration & UI exploration. Generate distinctive, production-grade frontend interfaces with high design quality. Avoid generic AI aesthetics.
allowed-tools: Read, Write, Bash
---

# UI Design

用纯 HTML/CSS 快速产出高质量 UI 设计稿，做界面探索和灵感验证。

## 设计模式

本 skill 是 **Generator**：
- 根据用户需求生成单文件 HTML（内嵌 CSS + 可选 JS）
- 直接在浏览器中预览
- 可反复迭代修改直到满意

## Gotchas

- **不要生成"AI 味"UI**：避免蓝紫渐变 + 圆角卡片 + Inter/Roboto 字体 + 白色背景的千篇一律组合
- **风格要差异化**：根据用户描述判断风格——杂志排版？瑞士简约？Brutalist？玻璃态？暗色 OLED？
- **单文件限制**：所有 CSS/JS 必须内嵌或用 CDN，不能依赖本地文件
- **配色要有意图**：不要默认 #3B82F6 蓝色系——先选一个调色板，再开始写代码
- **字体选择影响风格**：衬线体 = 编辑/杂志感；等宽 = 终端/工具感；无衬线 = 工具/仪表盘感
- **先做结构再做细节**：不要上来就调 padding 和 box-shadow——先把布局骨架搭好

## 工作流

```text
设计进度：
- [ ] 步骤 1：确认设计方向和参考
- [ ] 步骤 2：选配色和字体
- [ ] 步骤 3：搭建布局骨架
- [ ] 步骤 4：填充内容和细节
- [ ] 步骤 5：视觉微调
- [ ] 步骤 6：输出并预览
```

### 步骤 1：确认方向

如果用户描述模糊（"做个好看的页面"），先问：
- 什么类型的页面？（landing / dashboard / blog / portfolio / 表单）
- 偏好的风格？（极简 / 杂志 / 瑞士 / 暗色 / 玻璃态...）
- 有没有参考图/网站？

### 步骤 2：选配色 + 字体

- **配色**：2-3 主色 + 中性色（白/灰/黑），避免超过 4 种颜色
- **字体**：Google Fonts CDN 或系统字体栈（`system-ui, -apple-system, sans-serif`）

### 步骤 3：布局骨架

CSS Grid 做大布局，Flexbox 做组件内排列。

### 步骤 4-5：填充 + 微调

- 用真实文案而非 lorem ipsum
- 间距和字号成比例（4px 或 8px 基准网格）
- hover/focus/active 状态完整

### 步骤 6：输出

单个 `.html` 文件，用户双击在浏览器打开即可预览。

## 输出要求

- 单个 .html 文件（内嵌 CSS + JS）
- 可直接浏览器打开预览
- 响应式适配（桌面 + 移动端基本可用）
- 不使用外部 CSS 框架（除非用户指定）

## 风格速查

| 风格 | 配色 | 字体 | 特征 |
|------|------|------|------|
| 瑞士国际 | IKB / 柠檬黄 / 黑 / 白 | 无衬线 (Helvetica/Monospace) | 网格、不对称、大字报 |
| 杂志编辑 | 暖白 / 深棕 / 暗红 | 衬线 (Georgia/Tiempos) | 大标题、留白、段落排版 |
| 暗色 OLED | #000 / 低饱和主色 | 无衬线 | 深黑背景、霓虹描边、低对比 |
| 玻璃态 | 半透明白 / 模糊背景 | 无衬线 | backdrop-filter、层叠、柔和阴影 |
| Brutalist | 黑白 / 醒目单色 | 等宽或粗无衬线 | 无圆角、粗边框、raw 感 |
