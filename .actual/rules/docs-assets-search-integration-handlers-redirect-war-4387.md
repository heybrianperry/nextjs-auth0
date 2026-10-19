---
version: 2
name: docs-assets-search-integration-handlers-redirect-war-4387
description: "Lunr Diagnostic Logging and Search Index Warning Handling: Search Integration Handlers Redirect Warning Utility"
metadata:
  actual:
    adr_id: 43879976-80a2-43fa-8120-15e4dcc06a33
    status: accepted
    candidate_group_id: 0c01218e-3ef5-4031-9d6d-7ab5e4b5d884
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Diagnostic Logging and Search Index Warning Handling: Search Integration Handlers Redirect Warning Utility

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for all client-side search index loading, query processing, and pipeline registration workflows using Lunr.

### Rules

- **R-LUNR-001** MAY: Search integration handlers MAY redirect warning utility streams to central telemetry sinks when observability collection is active in the host environment.
- **R-LUNR-002** MANDATORY: The consumer MUST discover dependency manifests, build tools, lock files, and exact resolved versions before writing code that uses a versioned library, ensuring API existence and version compatibility.
- **R-LUNR-003** MANDATORY: Verify that custom pipeline functions are registered before triggering index loading or serialization routines, and inspect runtime console output during client search initialization to detect version drift.

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