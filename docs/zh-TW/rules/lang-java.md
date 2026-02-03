# 語言規則：Java

## 適用範圍

當存在 `pom.xml`，或編輯 `.java` 檔案時適用。

## 程式碼風格範例

### 不可變性

偏好不可變物件、保護性複製與 `final` 欄位。

```java
public final class User {
    private final String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public User withName(String nextName) {
        return new User(nextName);
    }
}
```

### 錯誤處理

```java
try {
    return service.process(request);
} catch (IOException ex) {
    logger.error("Failed to process request {}", requestId, ex);
    throw new IllegalStateException("Processing failed", ex);
}
```

### 輸入驗證

```java
public record CreateUserRequest(
    @NotBlank String email,
    @Min(0) @Max(150) int age
) {}

@PostMapping("/users")
public ResponseEntity<User> createUser(@Valid @RequestBody CreateUserRequest request) {
    return ResponseEntity.ok(service.create(request));
}
```

## 安全性範例

```java
String apiKey = System.getenv("OPENAI_API_KEY");
if (apiKey == null || apiKey.isBlank()) {
    throw new IllegalStateException("OPENAI_API_KEY not configured");
}
```

## 模式

### API 回應封裝

```java
public record ApiResponse<T>(
    boolean success,
    T data,
    String error,
    Meta meta
) {
    public record Meta(int total, int page, int limit) {}
}
```

### Repository 模式（Spring Data）

```java
public interface UserRepository extends JpaRepository<UserEntity, Long> {
    Optional<UserEntity> findByEmail(String email);
}
```
