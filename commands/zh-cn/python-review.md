---
description: 对 PEP 8 合规性、类型提示、安全性和 Pythonic 惯用法进行全面的 Python 代码评审。调用 python-reviewer 代理。
---

# Python 代码评审 (Python Code Review)

此命令调用 **python-reviewer** 代理进行全面的 Python 特定代码评审。

## 此命令的作用

1. **识别 Python 更改**：通过 `git diff` 查找修改过的 `.py` 文件
2. **运行静态分析**：执行 `ruff`, `mypy`, `pylint`, `black --check`
3. **安全扫描**：检查 SQL 注入、命令注入、不安全的反序列化
4. **类型安全评审**：分析类型提示和 mypy 错误
5. **Pythonic 代码检查**：验证代码遵循 PEP 8 和 Python 最佳实践
6. **生成报告**：按严重程度对问题进行分类

## 评审类别

### 严重 (CRITICAL - 必须修复)
- SQL/命令注入漏洞
- 不安全的 eval/exec 使用
- Pickle 不安全反序列化
- 硬编码凭据
- 裸 except 子句隐藏错误

### 高 (HIGH - 应该修复)
- 公共函数缺失类型提示
- 可变默认参数 (Mutable default arguments)
- 静默吞掉异常
- 未对资源使用上下文管理器 (Context Managers)
- 使用 C 风格循环而非推导式 (Comprehensions)
- 使用 type() 而非 isinstance()
- 未经锁保护的竞态条件

### 中 (MEDIUM - 考虑改进)
- PEP 8 格式违规
- 公共函数缺失 Docstrings
- 使用 print 语句而非 logging
- 低效的字符串操作
- 无命名的魔法数字
- 未使用 f-strings 进行格式化
