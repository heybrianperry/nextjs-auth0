---
version: 2
name: docs-assets-consumers-handle-serialized-index-versio-6c2b
description: "Lunr Search Integration: Consumers Handle Serialized Index Version Discrepancies"
metadata:
  actual:
    adr_id: 6c2bf115-fa8a-419d-b4a5-7fe8cda6061b
    status: accepted
    candidate_group_id: 114ecd47-c00c-419f-94d4-752c22fe63aa
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Integration: Consumers Handle Serialized Index Version Discrepancies

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for client-side search integration components that parse and execute text queries against serialized indices, and runtime modules interacting with query lexer event emissions and query parser instances.

### Rules

- **R-LUNR-001** MUST: Consumers MUST handle serialized index version discrepancies by issuing warning diagnostics prior to initiating index deserialization.

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