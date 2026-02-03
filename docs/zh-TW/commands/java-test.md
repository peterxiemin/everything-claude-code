---
description: Enforce TDD workflow for Java with JUnit 5 and Mockito. Use for Java feature work.
---

# Java TDD 指令

此指令以 JUnit 5 與 Mockito 執行 Java 的測試驅動開發流程。

## 此指令的功能

1. **定義介面**：先建立類別與方法簽名
2. **先寫測試**：建立會失敗的 JUnit 測試（RED）
3. **執行測試**：確認失敗原因正確
4. **實作程式**：寫最小可行程式碼通過測試（GREEN）
5. **重構**：保持測試綠燈下改善程式碼
6. **檢查覆蓋率**：確保合理覆蓋率

## 何時使用

在以下情況使用 `/java-test`：
- 開發新的 Java 功能
- 為既有程式碼補測試
- 修 bug（先寫失敗測試）
- 建立關鍵商業邏輯

## TDD 週期

```
RED     → 寫失敗測試
GREEN   → 寫最小實作
REFACTOR → 重構保持綠燈
REPEAT  → 下一個測試案例
```

## 相關技能

- `skills/springboot-tdd/`
- `skills/java-coding-standards/`
