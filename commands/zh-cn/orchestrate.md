# 编排命令 (Orchestrate Command)

针对复杂任务的顺序代理工作流。

## 用法

`/orchestrate [workflow-type] [task-description]`

## 工作流类型

### feature (功能开发)
完整的功能实现工作流：
```
planner -> tdd-guide -> code-reviewer -> security-reviewer
```

### bugfix (Bug 修复)
Bug 调查与修复工作流：
```
explorer -> tdd-guide -> code-reviewer
```

### refactor (代码重构)
安全的重构工作流：
```
architect -> code-reviewer -> tdd-guide
```

### security (安全评审)
侧重安全的评审：
```
security-reviewer -> code-reviewer -> architect
```

## 执行模式

针对工作流中的每个代理：

1. 使用前一个代理提供的上下文**调用代理**
2. **收集输出**作为结构化的交接文档 (handoff document)
3. **传递给链条中的下一个代理**
4. 将所有结果**汇总到最终报告**中

## 示例：功能开发工作流

```
/orchestrate feature "添加用户身份验证"
```

执行过程：
1. **Planner 代理**：分析需求，创建实施方案。
2. **TDD Guide 代理**：读取方案，先写测试，实现代码使测试通过。
3. **Code Reviewer 代理**：评审实现，检查问题，建议改进。
4. **Security Reviewer 代理**：进行安全审计，漏洞检查，最终批准。

## 参数说明

$ARGUMENTS:
- `feature <description>` - 完整的功能开发工作流
- `bugfix <description>` - Bug 修复工作流
- `refactor <description>` - 重构工作流
- `security <description>` - 安全评审工作流
- `custom <agents> <description>` - 自定义代理序列
