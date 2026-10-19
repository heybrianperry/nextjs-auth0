---
version: 2
name: cross-cutting-server-rendered-page-handlers-requiring-5614
description: "Next.js Application Framework Adoption: Server Rendered Page Handlers Requiring Side"
metadata:
  actual:
    adr_id: 5614c655-2aea-4ce1-b3ff-31dfa20d16e2
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

# Next.js Application Framework Adoption: Server Rendered Page Handlers Requiring Side

Scope: applies to `e2e/test-app/pages/pages-router/server/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-mrrt/app/**`.

These rules are ALWAYS ACTIVE for all web application packages, frontend routing entrypoints, server-rendered view modules, layout components, and server-side request handlers requiring framework lifecycle coordination.

### Rules

- **R-FRAMEWORK-001** MUST: Server-rendered page handlers requiring server-side context or dynamic request properties MUST utilize framework server-side data fetching interfaces such as getServerSideProps rather than client-side ad-hoc data orchestration.

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