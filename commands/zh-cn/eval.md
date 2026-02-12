# Eval 命令

管理评测驱动开发 (Eval-driven development) 的工作流。

## 用法

`/eval [define|check|report|list] [feature-name]`

## 定义评测 (Define Evals)

`/eval define feature-name`

创建一个新的评测定义：

1. 创建 `.claude/evals/feature-name.md`，使用以下模板：

```markdown
## 评测：feature-name
创建日期：$(date)

### 能力评测 (Capability Evals)
- [ ] [能力 1 的描述]
- [ ] [能力 2 的描述]

### 回归评测 (Regression Evals)
- [ ] [现有行为 1 仍然正常]
- [ ] [现有行为 2 仍然正常]

### 成功标准
- 能力评测 pass@3 > 90%
- 回归评测 pass^3 = 100%
```

2. 提示用户填写具体的标准

## 检查评测 (Check Evals)

`/eval check feature-name`

为某项功能运行评测：

1. 从 `.claude/evals/feature-name.md` 读取评测定义
2. 针对每项能力评测：
   - 尝试验证标准
   - 记录通过/失败 (PASS/FAIL)
   - 在 `.claude/evals/feature-name.log` 中记录尝试
3. 针对每项回归评测：
   - 运行相关测试
   - 与基准进行对比
   - 记录通过/失败
4. 报告当前状态：

```
评测检查：feature-name
========================
能力：X/Y 通过
回归：X/Y 通过
状态：进行中 / 就绪
```

## 报告评测 (Report Evals)

`/eval report feature-name`

生成详细的评测报告：

```
评测报告：feature-name
=========================
生成日期：$(date)

能力评测 (CAPABILITY EVALS)
----------------
[eval-1]: 通过 (pass@1)
[eval-2]: 通过 (pass@2) - 经过重试
[eval-3]: 失败 - 详见备注

回归评测 (REGRESSION EVALS)
----------------
[test-1]: 通过
...

推荐建议
--------------
[可发布 / 仍需改进 / 阻断]
```

## 列出评测 (List Evals)

`/eval list`

显示所有评测定义：

```
评测定义列表
================
feature-auth      [3/5 通过] 进行中
feature-search    [5/5 通过] 就绪
```

## 参数说明

$ARGUMENTS:
- `define <name>` - 创建新的评测定义
- `check <name>` - 运行并检查评测
- `report <name>` - 生成完整报告
- `list` - 显示所有评测
- `clean` - 移除旧的评测日志 (保留最近 10 次运行)
