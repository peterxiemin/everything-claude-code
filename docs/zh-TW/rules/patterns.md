# 常見模式

## 適用範圍

此檔案為跨語言模式。語言專屬範例請參考 `rules/lang-*.md`。

## API 回應格式

請在 API 中使用一致的回應格式：

```json
{
  "success": true,
  "data": {},
  "error": null,
  "meta": { "total": 0, "page": 1, "limit": 20 }
}
```

## Repository 模式

保持穩定的 CRUD 介面：
- `findAll(filters)`
- `findById(id)`
- `create(data)`
- `update(id, data)`
- `delete(id)`

## 骨架專案

實作新功能時：
1. 搜尋經過實戰驗證的骨架專案
2. 使用平行 agents 評估選項：
   - 安全性評估
   - 擴展性分析
   - 相關性評分
   - 實作規劃
3. 複製最佳匹配作為基礎
4. 在經過驗證的結構中迭代
