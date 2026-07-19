---
name: system-doctor
description: 系统性能诊断工具。分析 CPU 占用、内存使用、磁盘空间、进程列表，输出诊断报告和优化建议。当用户说电脑卡、系统慢、CPU高、内存不够、查看进程时自动触发。
---

# System Doctor

快速诊断 Windows 系统性能问题，找到资源瓶颈并给出可操作的优化建议。

## 设计模式

本 skill 是 **Tool Wrapper**（诊断脚本）：
- 运行系统命令采集性能数据
- 分析瓶颈
- 输出诊断报告 + 优化建议

## 检查项目

| 检查项 | 命令 | 关注指标 |
|--------|------|----------|
| CPU | `wmic cpu get loadpercentage` | >80% 持续 |
| 内存 | `wmic os get TotalVisibleMemorySize,FreePhysicalMemory` | 可用 <10% |
| 磁盘 | `df -h`（Git Bash） | 使用率 >90% |
| 进程 | `tasklist /FO CSV` | 内存/CPU Top 10 |
| 启动项 | `wmic startup list brief` | 不必要的自启动 |

## Gotchas

- **Windows 命令在 Git Bash 中可能被错解析**：以 `/` 开头的参数被当 Unix 路径处理，用 `cmd /c` 包装
- **`df -h` 不走网络盘**：Git Bash 的 `df` 不显示网络映射盘，用 `wmic logicaldisk` 补充
- **单位换算**：`FreePhysicalMemory` 单位是 KB，转换为 GB 需要除以 1024^2
- **瞬时 CPU 不准**：取 3 次间隔 2 秒的平均值
- **不要直接建议杀进程**：先列出 Top 10，让用户判断哪些可以关

## 工作流

```text
诊断进度：
- [ ] 步骤 1：快速体检（CPU + 内存 + 磁盘）
- [ ] 步骤 2：深度分析（如有异常）
- [ ] 步骤 3：输出报告
- [ ] 步骤 4：给出优化建议
```

### 步骤 1：快速体检

一次性采集 CPU、内存、磁盘三项核心指标。约 5 秒。

如果三项全部正常 → 告诉用户"系统状态健康"并结束。
如果有异常 → 进入步骤 2。

### 步骤 2：深度分析

针对异常指标深入调查：

- **CPU 高**：列出 CPU Top 5 进程，检查是否有死循环/挖矿
- **内存不足**：列出内存 Top 5 进程，检查是否有内存泄漏
- **磁盘满**：`du -sh /c/* /d/* | sort -rh | head -15` 找大目录

### 步骤 3：输出报告

```
=== 系统诊断报告 ===
CPU:     [████████░░] 82% (异常)
内存:    [██████░░░░] 63% (正常)
C 盘:    [█████████░] 94% (警告)
D 盘:    [████░░░░░░] 38% (正常)

Top CPU:  1. chrome.exe (32%)  2. node.exe (18%) ...
Top Mem:  1. chrome.exe (2.1G) 2. Code.exe (890M) ...
大目录:   C:/Users/Fanyu/.claude/projects/ (12G)
```

### 步骤 4：优化建议

每条建议必须是具体可操作的：
- "清理 C:/Users/Fanyu/.claude/projects/ 的旧会话文件（可释放 ~5G）"
- "关闭不需要的 Chrome 标签页（当前占用 2.1G）"

## 输出要求

- ASCII 进度条展示三项指标
- 异常项目高亮标记
- 每条建议一行，具体到路径/进程名
- 不推荐第三方清理工具

## 参考资料

- Windows WMIC 文档
- Git Bash `df`/`du` 命令
