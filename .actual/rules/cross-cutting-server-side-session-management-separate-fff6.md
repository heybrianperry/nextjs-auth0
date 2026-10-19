---
version: 2
name: cross-cutting-server-side-session-management-separate-fff6
description: "Next.js Server Module Integration for Request and Session Handling: Server Side Session Management Separate Read"
metadata:
  actual:
    adr_id: fff6f816-f071-412b-805e-1234674487e2
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

# Next.js Server Module Integration for Request and Session Handling: Server Side Session Management Separate Read

Scope: applies to `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-SESSION-001** SHOULD: Server-side session management SHOULD separate read-only session inspection from stateful cookie modification routines across distinct execution contexts.
- **R-SESSION-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-SESSION-003** MANDATORY: Before writing code that uses a versioned library, execute the lock-version grounding steps in order (find manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for that exact version, confirm APIs exist, re-run per dependency at point of use).
- **R-SESSION-004** MANDATORY: Verify that request handling logic checks framework-specific prefetch headers before initiating stateful session operations.
- **R-SESSION-005** MANDATORY: Ensure server-side session writers differentiate between mutable response pipelines and read-only component rendering pipelines.

### Verify

```bash
# Discover and run the repository test execution script declared in the dependency manifest to validate server module compatibility.
# Discover and run the project type checker and linter scripts to verify compliance with server API contracts and boundary constraints.
```

**Accept when:**
- All automated test suites pass without framework compatibility or cookie manipulation errors.
- Static type analysis succeeds with zero type errors across server module entry points.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration test suites and peer code reviews enforce compliance, blocking pull requests that introduce direct cookie mutation in read-only component lifecycles.
</enforcement>