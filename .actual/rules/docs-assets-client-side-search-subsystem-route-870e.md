---
version: 2
name: docs-assets-client-side-search-subsystem-route-870e
description: "Lunr Diagnostic Logging and Search Index Warning Handling: Client Side Search Subsystem Route Pipeline"
metadata:
  actual:
    adr_id: 870e197c-d9cc-48cc-8631-a9c61cab6e7d
    status: accepted
    candidate_group_id: 0c01218e-3ef5-4031-9d6d-7ab5e4b5d884
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Diagnostic Logging and Search Index Warning Handling: Client Side Search Subsystem Route Pipeline

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-LUNR-001** MUST: The client-side search subsystem MUST route all search pipeline errors, unregistered function detections, and index version mismatches through Lunr warning utility handlers and structured diagnostic logging.

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