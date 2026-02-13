---
description: 在 Go 中强制执行 TDD 工作流。先编写表驱动测试，然后进行实现。通过 go test -cover 验证 80% 以上的覆盖率。
---

# Go TDD 命令

此命令使用地道的 Go 测试模式强制执行 Go 代码的测试驱动开发方法论。

## 此命令的作用

1. **定义类型/接口**：先搭建函数签名
2. **编写表驱动测试**：创建全面的测试用例 (RED)
3. **运行测试**：验证测试是否因正确的原因失败
4. **实现代码**：编写能使测试通过的最简代码 (GREEN)
5. **重构**：在保持测试通过的同时改进代码
6. **检查覆盖率**：确保 80% 以上的覆盖率

## TDD 循环

```
RED     → 编写失败的表驱动测试
GREEN   → 编写最简代码使测试通过
REFACTOR → 改进代码，保持测试通过
REPEAT  → 下一个测试用例
```

## 测试模式

### 表驱动测试 (Table-Driven Tests)
```go
tests := []struct {
    name     string
    input    InputType
    want     OutputType
    wantErr  bool
}{
    {"用例 1", input1, want1, false},
    {"用例 2", input2, want2, true},
}

for _, tt := range tests {
    t.Run(tt.name, func(t *testing.T) {
        got, err := Function(tt.input)
        // 断言
    })
}
```

## 覆盖率目标

| 代码类型 | 目标 |
|----------|------|
| 关键业务逻辑 | 100% |
| 公共 API | 90%+ |
| 通用代码 | 80%+ |
| 生成的代码 | 排除 |
