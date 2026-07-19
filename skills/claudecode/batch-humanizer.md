---
name: batch-humanizer
description: Batch AI humanization for Chinese documents with multiple iteration rounds. Use when user needs to process large documents, apply multiple rounds of AI-trace removal, or batch-process multiple files.
---

# Batch Humanizer

对中文文档执行多轮去 AI 味处理，逐轮追踪改进量，保存中间结果。

## 设计模式

本 skill 采用 **Pipeline** 模式：
- 读取源文档（.docx / .md）
- 执行 3-5 轮 humanizer-zh 处理
- 每轮输出独立的中间文件 + 修改量统计
- 最终交付一份干净版本

## Gotchas

- **轮数不是越多越好**：3 轮通常最佳；超过 5 轮文本开始失真
- **每轮后必须统计**：追踪修改数量，如果连续两轮修改量 < 5 处，停止迭代
- **不要一上来就改**：先读全文理解风格和语境，再逐轮处理
- **保留专业术语**：技术名词、人名、地名不做 humanization
- **中间文件不要删**：用户可能需要回退到某一轮的结果

## 工作流

```text
处理进度：
- [ ] 步骤 1：读取源文档
- [ ] 步骤 2：确认轮数和参数
- [ ] 步骤 3：执行第 1 轮（模式移除）
- [ ] 步骤 4：执行第 2 轮（结构变化）
- [ ] 步骤 5：执行第 3 轮（最终润色）
- [ ] 步骤 6：汇总报告
```

### 步骤 1：读取

```bash
# .docx
python -c "from docx import Document; print(Document('file.docx').core_properties)"
# .md
wc -l file.md
```

### 步骤 2：确认参数

- **默认 3 轮**；用户可指定 1-5
- 目标字数范围（如有）
- 特殊保留词列表（专业术语、品牌名）

### 步骤 3-5：逐轮处理

每轮调用 humanizer-zh，保存中间文件：

| 轮次 | 重点 | 输出文件 |
|------|------|----------|
| Round 1 | 移除 AI 模板句（"首先其次最后""综上所述""值得注意的是"） | `file_r1.docx` |
| Round 2 | 变换句式结构、混合长短句、添加自然口语表达 | `file_r2.docx` |
| Round 3 | 检查节奏流畅度、验证真实性、确保可读性 | `file_r3.docx` |

每轮完成后统计：
```
Round 1: 修改 47 处 → file_r1.docx
Round 2: 修改 18 处 → file_r2.docx
Round 3: 修改 5 处 → file_r3.docx  (接近收敛)
```

如果连续两轮修改 < 5 处，自动停止后续轮次。

### 步骤 6：汇总

交付最终版本 + 修改统计摘要：
```
=== Batch Humanization 完成 ===
输入: thesis.docx (12,450 字)
输出: thesis_humanized.docx (12,380 字)
轮次: 3 轮
总修改: 70 处
中间文件: thesis_r1.docx / thesis_r2.docx / thesis_r3.docx
```

## 输出要求

- 最终 humanized 文件
- 每轮的中间文件（方便回退）
- 修改统计（每轮修改数 + 总修改数）
- 如某轮修改量过少，说明原因并建议停止

## 配合

本 skill 在每轮内部调用 `humanizer-zh` 做实际的文字修改。如需单次快速处理，直接用 `humanizer-zh`。
