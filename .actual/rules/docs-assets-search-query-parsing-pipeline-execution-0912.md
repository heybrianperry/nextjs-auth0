---
version: 2
name: docs-assets-search-query-parsing-pipeline-execution-0912
description: "Lunr Diagnostic Logging and Search Index Warning Handling: Search Query Parsing Pipeline Execution Routines"
metadata:
  actual:
    adr_id: 0912553c-430f-4a7d-8480-9ee3af0436a7
    status: accepted
    candidate_group_id: 0c01218e-3ef5-4031-9d6d-7ab5e4b5d884
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - docs/assets/**
---

# Lunr Diagnostic Logging and Search Index Warning Handling: Search Query Parsing Pipeline Execution Routines

Scope: applies to `docs/assets/**`.

These rules are ALWAYS ACTIVE for client-side search index loading and query processing modules, and pipeline registration and tokenization workflows using Lunr.

### Rules

- **R-LUNR-001** MUST_NOT: Search query parsing and pipeline execution routines MUST NOT suppress or discard diagnostic warnings emitted during index loading or query tokenization.
- **R-LUNR-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-LUNR-003** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: (1) Find dependency manifest, (2) Identify build tool, (3) Inspect repository lock/resolution artifact for exact version, (4) Look up official documentation/changelog, (5) Confirm every API/class/function exists in that exact version, (6) Re-run per dependency at point of use.

### Verify

```bash
# Discover and run static analysis and linting suites for logging checks
# Discover and execute test runner to verify warning emission during deserialization and registration
```

**Accept when:**
- Search initialization and query execution complete without unhandled exceptions across all supported document sets.
- Diagnostic warnings are emitted to console utilities when intentional version mismatches or unregistered pipeline functions are evaluated.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>