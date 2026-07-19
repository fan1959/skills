---
name: ppt-template-creator
description: 从 PPT 模板创建可复用 Skill。读取 .pptx 模板 → 分析版式/占位符/设计意图 → 输出 SKILL.md + assets/template.pptx。它是一个 meta-skill——产物是 Skill，不是直接的 .pptx 文件。用此 skill 把 SCU 答辩模板、企业 PPT 模板等封装为可重复调用的生成器。
---

# PPT Template Creator

把 PowerPoint 模板封装成可复用的 Claude Code Skill，让 AI 能按模板批量生成 PPT。

## 设计模式

本 skill 是 **Meta-skill（Generator）**：
- 输入：一个 .pptx 模板文件
- 分析：版式布局、占位符、颜色方案、设计意图
- 输出：SKILL.md（描述 + 工作流 + Gotchas）+ assets/template.pptx

## Gotchas

- **产物是 Skill，不是 .pptx**：如果用户要做 PPT，用 `ppt-master` 或 `gomoku-defense-ppt`，不要用本 skill
- **「空白」版式陷阱**：很多模板用空白 layout + 手绘 shape，分析时要正确识别文本框架和非文本装饰
- **占位符识别要保守**：宁可漏清也别误删模板装饰元素——"模板中的所有颜色板式..."这类说明是设计意图
- **输出目录结构**：`skills/<name>/SKILL.md` + `skills/<name>/assets/template.pptx`

## 工作流

```text
创建进度：
- [ ] 步骤 1：加载模板并分析版式
- [ ] 步骤 2：识别占位符和填充规则
- [ ] 步骤 3：提取设计约束（颜色/字体/间距）
- [ ] 步骤 4：编写 SKILL.md
- [ ] 步骤 5：复制模板到 assets/
- [ ] 步骤 6：验证 Skill 可用
```

### 步骤 1：分析版式

用 `python-pptx` 打开模板：
```python
from pptx import Presentation
prs = Presentation("template.pptx")
for i, slide in enumerate(prs.slides):
    for shape in slide.shapes:
        if shape.has_text_frame:
            print(f"Slide {i}: {shape.text_frame.text[:50]}")
```

记录：总页数、每页版式类型、文本框架位置、图片占位符、颜色方案。

### 步骤 2：识别占位符

区分三类内容：
- **可替换文本**：标题、姓名、日期、技术栈等（做成参数）
- **固定文本**：设计说明、颜色板式、版权信息（保留）
- **装饰元素**：背景图、Logo、分隔线（不修改）

### 步骤 3：提取设计约束

- 字体：中英文分别用什么字体？字号范围？
- 颜色：主题色、强调色、文字色
- 间距：段落间距、页边距
- 图片：尺寸、位置、是否需要占位图

### 步骤 4：编写 SKILL.md

按 chujianyun/skills 标准格式：
1. YAML frontmatter（name + description）
2. 设计模式
3. Gotchas（模板特有的坑）
4. 工作流（分步骤、带 checklist）
5. 输出要求
6. 参考资料

### 步骤 5：复制模板

将原始 .pptx 复制到 `skills/<name>/assets/template.pptx`。

### 步骤 6：验证

- SKILL.md 格式正确（YAML 可解析）
- 模板文件存在且可被 python-pptx 打开
- 用 Skill 跑一次空跑（dry run）确认流程走通

## 输出要求

- 目录结构：`skills/<name>/` 下有 SKILL.md + assets/template.pptx
- SKILL.md 500-3000 行（取决于模板复杂度）
- Gotchas 至少 3 条模板特定的注意事项

## 参考资料

- python-pptx 文档：https://python-pptx.readthedocs.io
- Skill 格式标准：参照 `skills/prompt-optimizer/SKILL.md`
