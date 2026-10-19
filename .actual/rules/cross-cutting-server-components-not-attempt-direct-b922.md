---
version: 2
name: cross-cutting-server-components-not-attempt-direct-b922
description: "Next.js Server Module Integration for Request and Session Handling: Server Components Not Attempt Direct Cookie"
metadata:
  actual:
    adr_id: b922025c-9279-486d-b955-b7fe379be9ee
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

# Next.js Server Module Integration for Request and Session Handling: Server Components Not Attempt Direct Cookie

Scope: applies to `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for server-side request processing, session storage, and token synchronization code.

### Rules

- **R-NSM-001** MUST_NOT: Server Components MUST NOT attempt direct cookie mutation or token refresh persistence operations during render phase execution.

### Verify

```bash
# Discover and run the repository test execution script declared in the dependency manifest to validate server module compatibility.
# Discover and run the project type checker and linter scripts to verify compliance with server API contracts and boundary constraints.
```

**Accept when:**
- All automated test suites pass without framework compatibility or cookie manipulation errors.
- Static type analysis succeeds with zero type errors across server module entry points.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>