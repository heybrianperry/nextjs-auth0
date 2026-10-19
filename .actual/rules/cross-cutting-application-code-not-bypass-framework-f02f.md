---
version: 2
name: cross-cutting-application-code-not-bypass-framework-f02f
description: "Next.js Application Framework Adoption: Application Code Not Bypass Framework Routing"
metadata:
  actual:
    adr_id: f02f08f6-639d-4c11-9f99-6126275223cb
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

# Next.js Application Framework Adoption: Application Code Not Bypass Framework Routing

Scope: applies to `e2e/test-app/pages/pages-router/server/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-mrrt/app/**`.

These rules are ALWAYS ACTIVE for all web application packages, frontend routing entrypoints, and server-rendered view modules within the repository.

### Rules

- **R-FRAMEWORK-001** MUST_NOT: Application code MUST NOT bypass the framework routing and rendering architecture by introducing competing presentation servers or uncoordinated routing handlers.

### Verify

```bash
# Discover and run the project build script declared in the repository manifest to verify route compilation and static page generation.
# Discover and run the repository automated test suite to validate page rendering, layout composition, and server-side fetching behavior.
```

**Accept when:**
- The project build script completes with exit code 0 and successfully generates all configured routes and layouts without compilation errors.
- All automated test suites for server-rendered endpoints and layout components pass successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>