---
description: Comprehensive Java code review for security, correctness, and performance. Invokes the java-reviewer agent.
---

# Java 程式碼審查

此指令呼叫 **java-reviewer** Agent 進行 Java 專屬程式碼審查。

## 此指令的功能

1. **找出 Java 變更**：透過 `git diff` 找出修改的 `.java` 檔案
2. **執行靜態分析**：若專案已配置，執行 Checkstyle/SpotBugs/PMD
3. **安全檢查**：注入、反序列化、TLS 等問題
4. **並行審查**：執行緒安全與同步
5. **品質審查**：錯誤處理、資源使用、效能
6. **產出報告**：按嚴重性分類問題

## 何時使用

在以下情況使用 `/java-review`：
- 修改 Java 程式碼後
- 提交 Java 變更之前
- 審查含 Java 的 PR
- 上手新的 Java 程式碼庫

## 執行的檢查（若已配置）

```bash
mvn -q -DskipTests checkstyle:check
mvn -q -DskipTests spotbugs:check
mvn -q -DskipTests pmd:check
```

## 相關

- Agent: `agents/java-reviewer.md`
