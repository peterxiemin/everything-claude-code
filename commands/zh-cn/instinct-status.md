---
name: instinct-status
description: 显示所有已学习的直觉及其置信水平
command: true
---

# 直觉状态命令 (Instinct Status Command)

显示所有已学习的直觉及其置信得分，按领域分组。

## 用法

```
/instinct-status
/instinct-status --domain code-style
/instinct-status --low-confidence
```

## 执行步骤

1. 从 `~/.claude/homunculus/instincts/personal/` 读取所有个人直觉文件
2. 从 `~/.claude/homunculus/instincts/inherited/` 读取继承的直觉
3. 按领域分组显示，并带有置信度进度条

## 参数

- `--domain <name>`：按领域过滤 (code-style, testing, git 等)
- `--low-confidence`：仅显示置信度 < 0.5 的直觉
- `--high-confidence`：仅显示置信度 >= 0.7 的直觉
- `--source <type>`：按来源过滤 (session-observation, repo-analysis, inherited)
- `--json`：以 JSON 格式输出，供程序使用
