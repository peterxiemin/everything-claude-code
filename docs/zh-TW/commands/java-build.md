---
description: Fix Java build errors and Maven failures. Invokes the java-build-resolver agent.
---

# Java 建置與修復

此指令呼叫 **java-build-resolver** Agent，以最小變更增量修復 Java 建置錯誤。

## 此指令的功能

1. **執行診斷**：執行 Maven 建置與測試
2. **解析錯誤**：依檔案分組並依嚴重性排序
3. **增量修復**：一次一個錯誤
4. **驗證每次修復**：每次變更後重新執行建置
5. **報告摘要**：顯示已修復和剩餘的問題

## 何時使用

在以下情況使用 `/java-build`：
- `mvn -q -DskipTests package` 失敗並出現錯誤
- `mvn test` 失敗或有編譯錯誤
- 相依性解析失敗
- 拉取破壞建置的變更後

## 執行的診斷指令

```bash
# 主要建置檢查（跳過測試）
mvn -q -DskipTests package

# 測試
mvn test

# verify 生命週期（跳過測試）
mvn -q -DskipTests verify

# 相依性樹
mvn -q -DskipTests dependency:tree
```

## 相關

- Agent: `agents/java-build-resolver.md`
