---
version: 2
name: docs-assets-developers-not-load-serialized-indexes-eb8a
description: "Lunr Search Index and Query Parser Adoption: Developers Not Load Serialized Indexes That"
metadata:
  actual:
    adr_id: eb8ae83e-b354-48a0-9156-958dd12f0022
    status: accepted
    candidate_group_id: 0c86c4c8-50ef-4b9e-b5d2-5a9c569fd2f1
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Index and Query Parser Adoption: Developers Not Load Serialized Indexes That

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for static documentation search interfaces requiring client-side index querying and in-memory token-based text search evaluation using lunr QueryParser.

### Rules

- **R-LUNR-001** MUST_NOT: Developers MUST NOT load serialized indexes that mismatch the active lunr library version without pipeline re-registration.

### Verify

```bash
# Discover and run the project test runner to execute unit and integration suites validating client search index generation.
# Discover and run the project static analysis and linting suite to verify compliance with query parser and lexer invocation standards.
```

**Accept when:**
- Search query execution returns expected ranked results without emitting pipeline or version mismatch warnings.
- All discovered automated test suites pass without regressions.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests that misconfigure query execution or violate serialization constraints must be blocked until resolved.
</enforcement>