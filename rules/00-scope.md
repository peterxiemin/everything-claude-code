# Rule Scope And Precedence

## Intent

Rules are always-on, so language-specific guidance must be scoped to avoid conflicts.

## Precedence

1. **Language rules override core rules** when there is a conflict.
2. **Core rules apply to all languages** unless a language rule says otherwise.

## How To Detect Language Scope

Use any of the following signals:
- **Java**: `pom.xml` present or `.java` files modified
- **TypeScript/JavaScript**: `package.json` present or `.ts/.tsx/.js/.jsx` files modified
- **Go**: `go.mod` present or `.go` files modified

When in doubt, prefer the rule file that matches the modified file types.
