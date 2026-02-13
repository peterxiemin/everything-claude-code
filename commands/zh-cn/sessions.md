# 会话命令 (Sessions Command)

管理 Claude Code 会话历史 —— 列出、加载、设置别名及编辑存储在 `~/.claude/sessions/` 中的会话。

## 用法

`/sessions [list|load|alias|info|help] [options]`

## 操作

### 列出会话 (List Sessions)

显示所有会话及其元数据，支持过滤和分页。

```bash
/sessions                              # 列出所有会话 (默认)
/sessions list --limit 10              # 显示 10 个会话
/sessions list --date 2026-02-01       # 按日期过滤
```

### 加载会话 (Load Session)

加载并显示会话内容 (通过 ID 或别名)。

```bash
/sessions load <id|alias>             # 加载会话
/sessions load my-alias               # 通过别名加载
```

### 创建别名 (Create Alias)

为会话创建一个易于记忆的别名。

```bash
/sessions alias <id> <name>           # 创建别名
/sessions alias 2026-02-01 today-work # 创建名为 "today-work" 的别名
```

### 移除别名 (Remove Alias)

删除现有的别名。

```bash
/sessions unalias <name>               # 移除别名
```

### 会话信息 (Session Info)

显示关于会话的详细统计信息。

```bash
/sessions info <id|alias>              # 显示会话详情
```

## 参数说明

$ARGUMENTS:
- `list [options]` - 列出会话
- `load <id|alias>` - 加载会话内容
- `alias <id> <name>` - 为会话创建别名
- `unalias <name>` - 移除别名
- `info <id|alias>` - 显示会话统计信息
- `aliases` - 列出所有别名
- `help` - 显示此帮助信息
