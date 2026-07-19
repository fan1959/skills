---
name: skill-install
description: Install Claude Code skills with automatic fallback methods for network failures. Use when user wants to install a skill from GitHub, npm, or skills.sh registry, especially behind firewalls or network restrictions.
---

# Skill Install

安装 Agent Skill 到本地 Claude Code，含网络失败的自动备用方案。

## 设计模式

本 skill 采用 **Tool Wrapper** 模式：
- 接收 skill 名称或仓库 URL
- 按优先级尝试多种安装方式
- 一种失败自动切换到下一种
- 报告哪种方式成功了

## 安装方式优先级

| 优先级 | 方式 | 命令 |
|--------|------|------|
| 1 | `npx skills add` | `npx skills add <owner/repo> -g` |
| 2 | Git 克隆 | `git clone <url> ~/.claude/skills/<name>/` |
| 3 | npm/npx 包 | `npm install -g <package>` |
| 4 | WebFetch + 手动 | 下载 → 解压 → 放到 skills 目录 |
| 5 | 镜像/代理备选 | ghproxy / gitee 镜像 |

## Gotchas

- **安装前先查连通性**：不要连试 4 种都失败才发现 GitHub 被墙了
- **Skill 名称用 Title Case**：如 `Hook Development` 不是 `hook-development`
- **全局 vs 项目级**：`-g` 装到用户级 `~/.claude/skills/`，不加 `-g` 装到项目 `.claude/skills/`
- **重复安装检测**：装之前检查目标目录是否已存在，避免覆盖用户修改
- **安装后要验证**：读一下 SKILL.md 确认文件完整，不是 0 字节空文件

## 工作流

```text
安装进度：
- [ ] 步骤 1：预检连通性
- [ ] 步骤 2：尝试主安装方式
- [ ] 步骤 3：失败则切换备用方案
- [ ] 步骤 4：验证安装完整性
- [ ] 步骤 5：报告结果
```

### 步骤 1：预检

```bash
curl -s --connect-timeout 5 https://github.com -o /dev/null && echo "GitHub: OK" || echo "GitHub: BLOCKED"
curl -s --connect-timeout 5 https://registry.npmjs.org -o /dev/null && echo "npm: OK" || echo "npm: BLOCKED"
```

被墙时自动启用：
- `https://ghproxy.com/https://github.com/...`（GitHub 代理）
- `https://gitee.com/...`（Gitee 镜像）

### 步骤 2-3：尝试安装

每种方式失败时输出原因，然后自动尝试下一种：

```
[x] npx skills add → 网络超时
[x] git clone → GitHub 无响应
[✓] WebFetch → 下载成功，已放置到 ~/.claude/skills/xxx/
```

### 步骤 4：验证

```bash
ls -la ~/.claude/skills/<name>/SKILL.md  # 检查文件存在且非空
head -5 ~/.claude/skills/<name>/SKILL.md  # 检查 frontmatter 格式
```

### 步骤 5：报告

```
✅ Skill "humanizer-zh" 安装成功
   方式: WebFetch + 手动
   位置: ~/.claude/skills/humanizer-zh/
   协议: CC BY-NC-SA 4.0
```

## 网络备用方案详情

### 方案 A：ghproxy（GitHub 被墙时）

```bash
git clone https://ghproxy.com/https://github.com/owner/repo.git
```

### 方案 B：Gitee 镜像

搜索 gitee.com 上是否有同名仓库。

### 方案 C：WebFetch

用 WebFetch 工具直接下载原始文件的 raw URL，跳过 git 协议：

```
WebFetch: https://raw.githubusercontent.com/owner/repo/main/SKILL.md
```

然后 Write 到本地 `~/.claude/skills/<name>/SKILL.md`。

## 输出要求

- 安装成功：skill 名称 + 安装方式 + 本地路径
- 安装失败：每种方式的失败原因 + 建议用户手动操作
- 不擅自改 skill 内容（除非是格式转换需要）
