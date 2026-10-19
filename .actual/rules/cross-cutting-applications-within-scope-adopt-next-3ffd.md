---
version: 2
name: cross-cutting-applications-within-scope-adopt-next-3ffd
description: "Next.js Application Framework Adoption: Applications Within Scope Adopt Next Core"
metadata:
  actual:
    adr_id: 3ffd5816-5c6f-4462-9fb1-cf860292285c
    status: accepted
    candidate_group_id: cf525615-6f42-4da5-82c9-6e313038bd53
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/pages/pages-router/server/**
      - examples/with-ipsie-session-expiry/app/**
      - examples/with-mrrt/app/**
---

# Next.js Application Framework Adoption: Applications Within Scope Adopt Next Core

Scope: applies to `e2e/test-app/pages/pages-router/server/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-mrrt/app/**`.

These rules are ALWAYS ACTIVE for all web application packages, frontend routing entrypoints, server-rendered view modules, layout components, and server-side request handlers within scope.

### Rules

- **R-FRAMEWORK-001** MUST: Applications within scope MUST adopt Next.js as the core web application framework for managing application routing, layout structures, and server-side page execution.

### Verify

```bash
# Discover and run the project build script declared in the repository manifest
# Discover and run the repository automated test suite
```

**Accept when:**
- The project build script completes with exit code 0 and successfully generates all configured routes and layouts without compilation errors.
- All automated test suites for server-rendered endpoints and layout components pass successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>