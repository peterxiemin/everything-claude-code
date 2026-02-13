---
name: instinct-import
description: 从队友、Skill Creator 或其他来源导入直觉
command: true
---

# 直觉导入命令 (Instinct Import Command)

## 用法

从以下来源导入直觉：
- 队友的导出文件
- Skill Creator (代码库分析)
- 社区集合
- 以前机器的备份

```bash
/instinct-import team-instincts.yaml
/instinct-import https://github.com/org/repo/instincts.yaml
/instinct-import --from-skill-creator acme/webapp
```

## 合并策略

### 针对重复项
当导入的直觉与现有直觉匹配时：
- **高置信度胜出**：保留置信度较高的一个
- **合并证据**：合并观察次数
- **更新时间戳**：标记为最近已验证

### 针对冲突项
当导入的直觉与现有直觉矛盾时：
- **默认跳过**：不导入冲突的直觉
- **标记待评审**：将两者均标记为需要注意
- **手动解决**：由用户决定保留哪一个

## 来源追踪

导入的直觉会标记有：
```yaml
source: "inherited"
imported_from: "team-instincts.yaml"
imported_at: "2025-01-22T10:30:00Z"
```

## 参数

- `--dry-run`：预览而不导入
- `--force`：即使存在冲突也强制导入
- `--merge-strategy <higher|local|import>`：如何处理重复项
- `--from-skill-creator <owner/repo>`：从 Skill Creator 分析结果中导入
- `--min-confidence <n>`：仅导入超过阈值的直觉
