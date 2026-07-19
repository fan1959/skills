---
name: pptx-manipulation
description: 编辑已有 .pptx 文件。用 python-pptx 操作幻灯片、形状、文本框架、版式、图片、表格、图表。适用场景：批量替换文本、插入/删除幻灯片、替换 Logo/图片、调整版式、提取文本内容。不需要创建新 PPT——创建用 ppt-master 或 gomoku-defense-ppt。
---

# PPTX Manipulation

用 Python 程序化编辑 PowerPoint 文件，精确控制每个元素。

## 设计模式

本 skill 是 **Tool Wrapper**（python-pptx）：
- 接收用户的编辑指令
- 翻译为 python-pptx API 调用
- 输出修改后的 .pptx

## Gotchas

- **幻灯片索引从 0 开始**：用户说"第 3 页"对应 `prs.slides[2]`
- **删页必须倒序**：`for i in sorted(pages_to_delete, reverse=True): del prs.slides._sldIdLst[i]`
- **文本框架有层级**：`shape.text_frame.paragraphs[0].runs[0].text`，空框架没有 runs
- **中文字体名**：python-pptx 设置中文字体需要同时设 `font.name` 和 `font._element.rPr` 的东亚字体属性
- **图片替换不改尺寸**：替换图片后 shape 尺寸不变，如果新图比例不同需要手动调整
- **不要反复保存**：一次编辑完成后再 `prs.save()`，中间修改全部在内存中

## 常用操作

### 替换文本

```python
for slide in prs.slides:
    for shape in slide.shapes:
        if shape.has_text_frame:
            for para in shape.text_frame.paragraphs:
                for run in para.runs:
                    if "{{old}}" in run.text:
                        run.text = run.text.replace("{{old}}", "new")
```

### 删除幻灯片

```python
slide_ids = [3, 7, 12]  # 1-based from user
for i in sorted(slide_ids, reverse=True):
    rId = prs.slides._sldIdLst[i-1].get('r:id')
    prs.part.drop_rel(rId)
    del prs.slides._sldIdLst[i-1]
```

### 插入图片

```python
from pptx.util import Inches
slide.shapes.add_picture("image.png", Inches(1), Inches(2), Inches(4), Inches(3))
```

## 工作流

```text
编辑进度：
- [ ] 步骤 1：打开源文件
- [ ] 步骤 2：确认编辑目标（第几页、哪个 shape）
- [ ] 步骤 3：执行编辑
- [ ] 步骤 4：保存并验证
```

### 步骤 1：打开

```python
from pptx import Presentation
prs = Presentation("source.pptx")
print(f"Slides: {len(prs.slides)}, Width: {prs.slide_width}, Height: {prs.slide_height}")
```

### 步骤 2：确认目标

如用户说"改第 3 页的标题"：
1. 列出第 3 页所有 text_frame 内容
2. 让用户确认要改哪一个
3. 确认新内容

### 步骤 3：执行

用 python-pptx API 精确修改，不碰其他元素。

### 步骤 4：保存验证

- 保存为新文件（保留原文件）
- 用 python-pptx 重新打开验证修改生效
- 报告修改了什么

## 输出要求

- 输出新 .pptx 文件路径
- 说明修改了哪些页、哪些元素
- 如有无法完成的操作，明确说明原因

## 参考资料

- python-pptx 文档：https://python-pptx.readthedocs.io
- 常用操作参考：本 skill 的"常用操作"章节
