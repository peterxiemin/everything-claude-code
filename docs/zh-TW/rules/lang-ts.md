# 語言規則：TypeScript/JavaScript

## 適用範圍

當存在 `package.json`，或編輯 `.ts/.tsx/.js/.jsx` 檔案時適用。

## 程式碼風格範例

### 不可變性

```typescript
// 錯誤：變異
function updateUser(user, name) {
  user.name = name
  return user
}

// 正確：不可變性
function updateUser(user, name) {
  return {
    ...user,
    name
  }
}
```

### 錯誤處理

```typescript
try {
  const result = await riskyOperation()
  return result
} catch (error) {
  console.error('Operation failed:', error)
  throw new Error('Detailed user-friendly message')
}
```

### 輸入驗證

```typescript
import { z } from 'zod'

const schema = z.object({
  email: z.string().email(),
  age: z.number().int().min(0).max(150)
})

const validated = schema.parse(input)
```

## 安全性範例

```typescript
// 絕不：寫死的密鑰
const apiKey = "sk-proj-xxxxx"

// 總是：環境變數
const apiKey = process.env.OPENAI_API_KEY

if (!apiKey) {
  throw new Error('OPENAI_API_KEY not configured')
}
```

## 模式

### API 回應格式

```typescript
interface ApiResponse<T> {
  success: boolean
  data?: T
  error?: string
  meta?: {
    total: number
    page: number
    limit: number
  }
}
```

### 自訂 Hooks 模式

```typescript
export function useDebounce<T>(value: T, delay: number): T {
  const [debouncedValue, setDebouncedValue] = useState<T>(value)

  useEffect(() => {
    const handler = setTimeout(() => setDebouncedValue(value), delay)
    return () => clearTimeout(handler)
  }, [value, delay])

  return debouncedValue
}
```

### Repository 模式

```typescript
interface Repository<T> {
  findAll(filters?: Filters): Promise<T[]>
  findById(id: string): Promise<T | null>
  create(data: CreateDto): Promise<T>
  update(id: string, data: UpdateDto): Promise<T>
  delete(id: string): Promise<void>
}
```
