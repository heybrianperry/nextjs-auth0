---
version: 2
name: docs-assets-before-implementing-updating-any-search-1f75
description: "Lunr Search Integration: Before Implementing Updating Any Search Integration"
metadata:
  actual:
    adr_id: 1f75c9d2-4218-4266-9bba-1f4e3f65cb65
    status: accepted
    candidate_group_id: 114ecd47-c00c-419f-94d4-752c22fe63aa
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Integration: Before Implementing Updating Any Search Integration

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-LUNR-001** MUST: Before implementing or updating any search integration code, consumers MUST inspect the repository lock or resolution artifact to confirm the exact resolved version of the search dependency matches the serialized search index schema.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute the test runner to validate search integration suites.
# Discover and run the project build and static analysis commands to ensure lexer event integration conforms to type definitions.
```

**Accept when:**
- All client search unit and integration tests pass without unhandled lexer event warnings.
- Index loading verifies schema compatibility without version mismatch diagnostic warnings.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>