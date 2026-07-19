---
name: academic-essay
description: Specialized skill for writing Chinese or English academic essays with character count validation and direct docx output. Use when user asks to write academic papers, course essays, thesis chapters, or research reports. Built-in word count verification within ±10% tolerance.
---

# Academic Essay

中英文学术论文写作——内置字数验证、直接 .docx 输出、引用格式规范。

## 设计模式

本 skill 是 **Generator + Reviewer**：
- 收集用户需求（主题、字数、格式、引用风格）
- 生成结构化论文
- 验证字数（±10% 容差）
- 直接输出 .docx 文件

## Gotchas

- **写作前必须确认字数要求**：用户不说就问，不要假设。±10% 容差范围内
- **直接输出 .docx，不输出到 CLI**：大段文字不应占满对话窗口
- **引用必须验证来源有效性**：不确定的引用标注"待核实"
- **中文学术格式**：正文单倍行距 / 摘要 1.5 倍 / 参考文献双倍行距，三号 16pt 正文 / 小四 12pt 脚注
- **不要编造数据**：没有把握的数字和统计不写，宁可留白
- **保持中性语调**：用"本文""本研究"，不写"具有重要意义""完美""卓越"等 AI 套话

## 工作流

```text
写作进度：
- [ ] 步骤 1：确认需求（主题 / 字数 / 格式 / 引用风格）
- [ ] 步骤 2：构建大纲
- [ ] 步骤 3：逐节撰写
- [ ] 步骤 4：字数验证
- [ ] 步骤 5：引用检查
- [ ] 步骤 6：导出 .docx
```

### 步骤 1：确认需求

必须确认：
- 论文字数（±10%）
- 格式要求（APA / MLA / GB/T 7714 / 学校模板）
- 是否有参考范文或模板
- 是否需要图表 / 公式

### 步骤 2：构建大纲

先出大纲，让用户确认再开始写。大纲格式：
```
1. 引言（~500 字）
2. 文献综述（~1000 字）
3. 方法论（~800 字）
...
```

### 步骤 3-4：逐节撰写 + 字数验证

每写完一节检查字数，确保不超出分配范围。总字数 = 正文（不含摘要 + 参考文献）。

### 步骤 5：引用检查

- 每处引用验证格式正确
- URL 引用确认可访问
- 不确定来源标注"[待核实]"

### 步骤 6：导出 .docx

用 `docx` skill 直接生成 Word 文件，不输出正文到对话。

## 中文字号映射

| 字号 | 磅值 | 用途 |
|------|------|------|
| 三号 | 16pt | 正文 |
| 小四 | 12pt | 脚注 / 表格 |
| 四号 | 14pt | 标题 |
| 二号 | 22pt | 大标题 |
| 五号 | 10.5pt | 参考文献 |

## 行距规范

| 部分 | 行距 |
|------|------|
| 摘要 | 1.5 倍 |
| 正文 | 单倍 |
| 参考文献 | 双倍 |

## 输出要求

- `.docx` 文件（不是 CLI 输出）
- 文件名：`<论文标题>_V<版本号>.docx`
- 含目录（自动生成页码）
- 含参考文献列表

## 配合

- 生成 .docx：`docx` skill
- 去 AI 味：`humanizer-zh` / `batch-humanizer`
- 文献调研：`academic-researcher`
