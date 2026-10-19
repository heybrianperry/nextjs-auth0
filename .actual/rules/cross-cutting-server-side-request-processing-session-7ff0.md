---
version: 2
name: cross-cutting-server-side-request-processing-session-7ff0
description: "Next.js Server Module Integration for Request and Session Handling: Server Side Request Processing Session State"
metadata:
  actual:
    adr_id: 7ff0368d-b869-4c32-9a2b-c616d6f106d8
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

# Next.js Server Module Integration for Request and Session Handling: Server Side Request Processing Session State

Scope: applies to `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-NXT-001** MUST: Server-side request processing and session state management MUST interface through Next.js server module abstractions, encapsulating request inspection and cookie mutation mechanics within dedicated compatibility boundaries.

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