---
description: Enforce TDD workflow for Java with JUnit 5 and Mockito. Use for Java feature work.
---

# Java TDD Command

This command enforces test-driven development methodology for Java code using JUnit 5 and Mockito.

## What This Command Does

1. **Define Interfaces**: Scaffold class and method signatures
2. **Write Tests First**: Create failing JUnit tests (RED)
3. **Run Tests**: Verify failures are meaningful
4. **Implement Code**: Write minimal code to pass (GREEN)
5. **Refactor**: Improve code while keeping tests green
6. **Check Coverage**: Ensure meaningful coverage

## When to Use

Use `/java-test` when:
- Implementing new Java services
- Adding test coverage to existing code
- Fixing bugs (write failing test first)
- Building critical business logic

## TDD Cycle

```
RED     → Write failing test
GREEN   → Implement minimal code
REFACTOR → Improve design, keep tests green
REPEAT  → Next test case
```

## Example Session

```text
User: /java-test I need a validator for order IDs

Agent:
# TDD Session: Order ID Validator

## Step 1: Define Interface

public final class OrderIdValidator {
    public static boolean isValid(String orderId) {
        throw new UnsupportedOperationException("not implemented");
    }
}

## Step 2: Write Tests (RED)

class OrderIdValidatorTest {
    @Test
    void validOrderId() {
        assertTrue(OrderIdValidator.isValid("ORD-12345"));
    }

    @Test
    void invalidOrderId() {
        assertFalse(OrderIdValidator.isValid("bad"));
    }
}

## Step 3: Implement Minimal Code (GREEN)

public final class OrderIdValidator {
    public static boolean isValid(String orderId) {
        return orderId != null && orderId.matches("ORD-\\d+");
    }
}
```

## Related Skills

- `skills/springboot-tdd/`
- `skills/java-coding-standards/`
