---
version: 2
name: cross-cutting-request-inspection-utilities-identify-ro-2286
description: "Next.js Server Module Integration for Request and Session Handling: Request Inspection Utilities Identify Router Prefetch"
metadata:
  actual:
    adr_id: 2286bd8f-7b35-432d-8f80-257c887a7060
    status: accepted
    candidate_group_id: 13bc1b43-d3a4-4ae2-b129-f923d42b27b8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
      - src/utils/**
---

# Next.js Server Module Integration for Request and Session Handling: Request Inspection Utilities Identify Router Prefetch

Scope: applies to `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-REQ-001** MUST: Request inspection utilities MUST identify router prefetch requests using standard framework prefetch headers before executing expensive session reconciliation operations.

### Verify

```bash
# Discover and run the repository test execution script declared in the dependency manifest
# Discover and run the project type checker and linter scripts
```

**Accept when:**
- All automated test suites pass without framework compatibility or cookie manipulation errors.
- Static type analysis succeeds with zero type errors across server module entry points.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>