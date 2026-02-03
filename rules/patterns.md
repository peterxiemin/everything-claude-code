# Common Patterns

## Scope

These patterns are cross-language. For language-specific examples, see `rules/lang-*.md`.

## API Response Format

Use a consistent response envelope across APIs:

```json
{
  "success": true,
  "data": {},
  "error": null,
  "meta": { "total": 0, "page": 1, "limit": 20 }
}
```

## Repository Pattern

Expose a stable CRUD surface, regardless of backing store:
- `findAll(filters)`
- `findById(id)`
- `create(data)`
- `update(id, data)`
- `delete(id)`

## Skeleton Projects

When implementing new functionality:
1. Search for battle-tested skeleton projects
2. Use parallel agents to evaluate options:
   - Security assessment
   - Extensibility analysis
   - Relevance scoring
   - Implementation planning
3. Clone best match as foundation
4. Iterate within proven structure
