---
version: 2
name: docs-assets-serialized-search-indexes-validate-schem-2465
description: "Lunr Search Index and Query Parser Adoption: Serialized Search Indexes Validate Schema Consistency"
metadata:
  actual:
    adr_id: 2465d8f2-8810-4359-b166-96e4b2e642f5
    status: accepted
    candidate_group_id: 0c86c4c8-50ef-4b9e-b5d2-5a9c569fd2f1
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Index and Query Parser Adoption: Serialized Search Indexes Validate Schema Consistency

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for static documentation search interfaces requiring client-side index querying and in-memory token-based text search evaluation using lunr QueryParser.

### Rules

- **R-LUNR-001** SHOULD: Serialized search indexes validate schema consistency using JSON deserialization and cache lookups before executing query dispatch.

### Verify

```bash
# Discover and run the project test runner to execute unit and integration suites validating client search index generation.
# Discover and run the project static analysis and linting suite to verify compliance with query parser and lexer invocation standards.
```

**Accept when:**
- Search query execution returns expected ranked results without emitting pipeline or version mismatch warnings.
- All discovered automated test suites pass without regressions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>