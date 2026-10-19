---
version: 2
name: docs-assets-before-integrating-updating-client-side-9947
description: "Lunr Diagnostic Logging and Search Index Warning Handling: Before Integrating Updating Client Side Search"
metadata:
  actual:
    adr_id: 994771fd-1ecb-4835-aa73-8745d2dd1562
    status: accepted
    candidate_group_id: 0c01218e-3ef5-4031-9d6d-7ab5e4b5d884
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Diagnostic Logging and Search Index Warning Handling: Before Integrating Updating Client Side Search

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for all client-side search index loading, query processing modules, pipeline registration, and tokenization workflows using Lunr.

### Rules

- **R-LUN-001** MUST: Before integrating or updating client-side search components, the consumer MUST inspect the project dependency manifest and lock artifact to resolve the authoritative version of the search runtime.
- **R-LUN-002** MANDATORY: Execute the lock-version grounding process (discover manifest, identify build tool, inspect lock artifact for resolved version, consult official docs for that exact version, and confirm every API/class/function exists).
- **R-LUN-003** MUST: Verify that custom pipeline functions are registered before triggering index loading or serialization routines.
- **R-LUN-004** MUST: Inspect runtime console output during client search initialization to detect version drift between precomputed indices and the search library.

### Verify

```bash
# Discover and run the project static analysis and linting suites to ensure logging calls follow architectural constraints.
# Discover and execute the test runner to verify warning emission during index deserialization and pipeline registration.
```

**Accept when:**
- Search initialization and query execution complete without unhandled exceptions across all supported document sets.
- Diagnostic warnings are emitted to console utilities when intentional version mismatches or unregistered pipeline functions are evaluated.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>