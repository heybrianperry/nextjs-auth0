---
version: 2
name: cross-cutting-third-party-provider-integrations-state-b3ec
description: "Next.js Application Framework Adoption: Third Party Provider Integrations State Boundaries"
metadata:
  actual:
    adr_id: b3ec023c-ee6f-4fe4-9743-1536985435e7
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

# Next.js Application Framework Adoption: Third Party Provider Integrations State Boundaries

Scope: applies to `e2e/test-app/pages/pages-router/server/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-mrrt/app/**`.

These rules are ALWAYS ACTIVE for web application packages, frontend routing entrypoints, server-rendered view modules, layout components, and server-side request handlers requiring framework lifecycle coordination.

### Rules

- **R-NXT-001** SHOULD: Third-party provider integrations and state boundaries SHOULD be wrapped at layout or designated boundary components to minimize duplicate instantiation across route transitions.

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