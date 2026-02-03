---
description: Fix Java build errors and Maven failures. Invokes the java-build-resolver agent.
---

# Java Build and Fix

This command invokes the **java-build-resolver** agent to incrementally fix Java build errors with minimal changes.

## What This Command Does

1. **Run Diagnostics**: Execute Maven build and tests
2. **Parse Errors**: Group by file and sort by severity
3. **Fix Incrementally**: One error at a time
4. **Verify Each Fix**: Re-run build after each change
5. **Report Summary**: Show what was fixed and what remains

## When to Use

Use `/java-build` when:
- `mvn -q -DskipTests package` fails with errors
- `mvn test` fails with compilation or test errors
- Dependency resolution breaks
- After pulling changes that break Maven builds

## Diagnostic Commands Run

```bash
# Primary build check (skip tests)
mvn -q -DskipTests package

# Test run
mvn test

# Verify lifecycle (skip tests)
mvn -q -DskipTests verify

# Dependency tree
mvn -q -DskipTests dependency:tree
```

## Fix Strategy

1. **Compilation errors first** - Code must compile
2. **Test failures second** - Fix failing tests or minimal code
3. **Dependency issues third** - Resolve version conflicts
4. **One fix at a time** - Verify after each change
5. **Minimal changes** - Avoid refactors

## Related

- Agent: `agents/java-build-resolver.md`
