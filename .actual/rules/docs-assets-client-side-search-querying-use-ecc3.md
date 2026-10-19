---
version: 2
name: docs-assets-client-side-search-querying-use-ecc3
description: "Lunr Search Index and Query Parser Adoption: Client Side Search Querying Use Lunr"
metadata:
  actual:
    adr_id: ecc371e9-f942-4891-b562-55aeea585fc4
    status: accepted
    candidate_group_id: 0c86c4c8-50ef-4b9e-b5d2-5a9c569fd2f1
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Index and Query Parser Adoption: Client Side Search Querying Use Lunr

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for static documentation search interfaces requiring client-side index querying and in-memory token-based text search evaluation using lunr QueryParser.

### Rules

- **R-LUNR-001** MUST: Client-side search querying MUST use the lunr query execution interface via QueryParser and QueryLexer token pipelines to evaluate search criteria against the serialized index.
- **R-LUNR-002** MANDATORY: Execute lock-version grounding before writing code that uses a versioned library (find dependency manifest, identify build tool, inspect repository lock/resolution artifact, lookup official documentation for exact version, confirm every API/class/function exists, and re-run per dependency at point of use).
- **R-LUNR-003** MANDATORY: Query tokenization pipelines MUST configure lexer tokens for fields, terms, and edit distance to maintain consistent relevance scoring.
- **R-LUNR-004** MANDATORY: Custom pipeline functions MUST be registered prior to index serialization to avoid deserialization warnings during runtime execution.

### Verify

```bash
# Discover and run the project test runner to execute unit and integration suites validating client search index generation
# Discover and run the project static analysis and linting suite to verify compliance with query parser and lexer invocation standards
```

**Accept when:**
- Search query execution returns expected ranked results without emitting pipeline or version mismatch warnings.
- All discovered automated test suites pass without regressions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration build checks and peer code review.
</enforcement>