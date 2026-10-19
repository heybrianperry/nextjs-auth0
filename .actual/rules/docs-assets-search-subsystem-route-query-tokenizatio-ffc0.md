---
version: 2
name: docs-assets-search-subsystem-route-query-tokenizatio-ffc0
description: "Lunr Search Integration: Search Subsystem Route Query Tokenization Through"
metadata:
  actual:
    adr_id: ffc0ab83-8306-48ca-9f06-1db591360633
    status: accepted
    candidate_group_id: 114ecd47-c00c-419f-94d4-752c22fe63aa
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Integration: Search Subsystem Route Query Tokenization Through

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for client-side search integration components that parse and execute text queries against serialized indices, and runtime modules interacting with query lexer event emissions and query parser instances.

### Rules

- **R-LUNR-001** MUST: The search subsystem MUST route search query tokenization through the QueryLexer event emission pipeline to decouple lexical token streaming from index evaluation.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute test runner/build/static analysis commands
```

**Accept when:**
- All client search unit and integration tests pass without unhandled lexer event warnings.
- Index loading verifies schema compatibility without version mismatch diagnostic warnings.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>