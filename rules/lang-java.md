# Language Rules: Java

## Scope

Apply when `pom.xml` is present or when editing `.java` files.

## Coding Style Examples

### Immutability

Prefer immutable objects, defensive copies, and `final` fields.

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

### Error Handling

```java
try {
    return service.process(request);
} catch (IOException ex) {
    logger.error("Failed to process request {}", requestId, ex);
    throw new IllegalStateException("Processing failed", ex);
}
```

### Input Validation

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

## Security Example

```java
String apiKey = System.getenv("OPENAI_API_KEY");
if (apiKey == null || apiKey.isBlank()) {
    throw new IllegalStateException("OPENAI_API_KEY not configured");
}
```

## Patterns

### API Response Envelope

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

### Repository Pattern (Spring Data)

```java
public interface UserRepository extends JpaRepository<UserEntity, Long> {
    Optional<UserEntity> findByEmail(String email);
}
```
