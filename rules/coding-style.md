# Coding Style

## Scope

This file defines cross-language coding style rules. For language-specific examples and overrides, see `rules/lang-*.md`.

## Immutability (CRITICAL)

Prefer immutability and avoid in-place mutation of shared state. When mutation is necessary, keep it localized and explicit.

## File Organization

MANY SMALL FILES > FEW LARGE FILES:
- High cohesion, low coupling
- 200-400 lines typical, 800 max
- Extract utilities from large components
- Organize by feature/domain, not by type

## Error Handling

ALWAYS handle errors comprehensively:
- Add context to errors
- Don’t swallow exceptions
- Use structured logging when available

## Input Validation

ALWAYS validate user input using language-appropriate validators or schemas.

## Code Quality Checklist

Before marking work complete:
- [ ] Code is readable and well-named
- [ ] Functions are small (<50 lines)
- [ ] Files are focused (<800 lines)
- [ ] No deep nesting (>4 levels)
- [ ] Proper error handling
- [ ] No debug prints (console/System.out)
- [ ] No hardcoded values
- [ ] No mutation (immutable patterns used)
