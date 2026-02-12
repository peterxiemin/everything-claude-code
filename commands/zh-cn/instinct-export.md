---
name: instinct-export
description: 导出“直觉”(instincts) 以与队友或其他项目共享
command: /instinct-export
---

# 直觉导出命令 (Instinct Export Command)

将直觉导出为可共享的格式。非常适用于：
- 与队友共享
- 转移到新机器
- 为项目约定做贡献

## 用法

```
/instinct-export                           # 导出所有个人直觉
/instinct-export --domain testing          # 仅导出测试领域的直觉
/instinct-export --min-confidence 0.7      # 仅导出高置信度的直觉
/instinct-export --output team-instincts.yaml
```

## 执行步骤

1. 从 `~/.claude/homunculus/instincts/personal/` 读取直觉
2. 根据参数进行过滤
3. 剥离敏感信息：
   - 移除会话 ID
   - 移除文件路径 (仅保留模式)
   - 移除“上周”之前的时间戳
4. 生成导出文件

## 隐私考虑

导出内容包含：
- ✅ 触发模式
- ✅ 动作
- ✅ 置信度得分
- ✅ 领域
- ✅ 观察次数

导出内容 **不** 包含：
- ❌ 实际代码片段
- ❌ 文件路径
- ❌ 会话转录
- ❌ 个人标识符
