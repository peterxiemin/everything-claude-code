---
description: Comprehensive Java code review for security, correctness, and performance. Invokes the java-reviewer agent.
---

# Java Code Review

This command invokes the **java-reviewer** agent for comprehensive Java-specific code review.

## What This Command Does

1. **Identify Java Changes**: Find modified `.java` files via `git diff`
2. **Run Static Analysis**: Execute Checkstyle/SpotBugs/PMD if configured
3. **Security Scan**: Look for injection, deserialization, and TLS issues
4. **Concurrency Review**: Analyze thread safety and synchronization
5. **Quality Review**: Check error handling, resource usage, and performance
6. **Generate Report**: Categorize issues by severity

## When to Use

Use `/java-review` when:
- After writing or modifying Java code
- Before committing Java changes
- Reviewing pull requests with Java code
- Onboarding to a new Java codebase

## Automated Checks Run (if configured)

```bash
mvn -q -DskipTests checkstyle:check
mvn -q -DskipTests spotbugs:check
mvn -q -DskipTests pmd:check
```

## Related

- Agent: `agents/java-reviewer.md`
