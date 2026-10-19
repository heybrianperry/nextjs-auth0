---
version: 2
name: docs-assets-lexical-event-handlers-not-register-de6f
description: "Lunr Search Integration: Lexical Event Handlers Not Register Unhandled"
metadata:
  actual:
    adr_id: de6fee76-d9c7-462e-b13f-7d0b90c47c77
    status: accepted
    candidate_group_id: 114ecd47-c00c-419f-94d4-752c22fe63aa
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Search Integration: Lexical Event Handlers Not Register Unhandled

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for client-side search integration components that parse and execute text queries against serialized indices, and runtime modules interacting with query lexer event emissions and query parser instances.

### Rules

- **R-LUNR-001** SHOULD: Lexical event handlers SHOULD NOT register unhandled token types outside the supported lexer event boundary.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute the test runner to validate search integration suites.
# Discover and run the project build and static analysis commands to ensure lexer event integration conforms to type definitions.
```

**Accept when:**
- All client search unit and integration tests pass without unhandled lexer event warnings.
- Index loading verifies schema compatibility without version mismatch diagnostic warnings.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration test suites and peer code review checking adherence to event lexer boundaries and lock artifact version verification.
</enforcement>