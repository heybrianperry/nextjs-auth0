---
version: 2
name: docs-assets-developers-not-use-lunr-primary-ee2a
description: "Lunr Search Index and Query Parser Adoption: Developers Not Use Lunr Primary Transactional"
metadata:
  actual:
    adr_id: ee2ab50e-d9c0-4f2a-aebc-734947a31ee4
    status: accepted
    candidate_group_id: 0c86c4c8-50ef-4b9e-b5d2-5a9c569fd2f1
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Index and Query Parser Adoption: Developers Not Use Lunr Primary Transactional

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-LNR-001** MUST_NOT: Developers MUST NOT use lunr as a primary transactional datastore for domain state or persistent records.

### Verify

```bash
# Discover and run the project test runner to execute unit and integration suites validating client search index generation.
# Discover and run the project static analysis and linting suite to verify compliance with query parser and lexer invocation standards.
```

**Accept when:**
- Search query execution returns expected ranked results without emitting pipeline or version mismatch warnings.
- All discovered automated test suites pass without regressions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>