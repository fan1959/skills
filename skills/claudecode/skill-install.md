---
name: skill-install
description: Install Claude Code skills with automatic fallback methods for network failures
---

# Skill Installer with Fallbacks

Install skills using multiple methods with automatic fallback when network issues occur.

## Installation Priority Order

1. **claude mcp add** - For MCP-based skills
2. **git clone** - Direct clone from repository
3. **npm/npx** - Package-based installation
4. **WebFetch + manual placement** - Download and extract manually
5. **Search alternative sources** - Find mirrors or alternative URLs

## Network Resilience

For Chinese users, GitHub is often blocked. Use these fallbacks:

- **ghproxy**: `https://ghproxy.com/https://github.com/...`
- **gitee mirrors**: Search for gitee.com equivalents
- **WebFetch**: Download via API tools

## Pre-flight Check

Before installing, always check connectivity:

```bash
curl -s --connect-timeout 5 https://github.com -o /dev/null && echo "GitHub: OK" || echo "GitHub: BLOCKED"
```

## Usage

```
/skill-install <skill-name> <repo-url>
```

## Examples

- GitHub direct: `/skill-install humanizer-zh https://github.com/example/humanizer-zh`
- NPM package: `/skill-install docx`
- Unknown source: `/skill-install my-tool` (will search)

## Error Handling

If primary method fails:
1. Try mirror/proxy
2. Try WebFetch download
3. Try npm registry
4. Search for alternatives
5. Report what worked and what didn't

## Auto-Detection

If no repo URL provided, attempt to:
1. Search npm registry
2. Search GitHub
3. Ask user for source
