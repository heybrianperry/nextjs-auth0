---
version: 2
name: cross-cutting-before-implementing-upgrading-applicatio-7796
description: "Next.js Application Framework Adoption: Before Implementing Upgrading Application Code Relying"
metadata:
  actual:
    adr_id: 77965e2f-cc0c-4cc5-80b5-0702c22737d8
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

# Next.js Application Framework Adoption: Before Implementing Upgrading Application Code Relying

Scope: applies to `e2e/test-app/pages/pages-router/server/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-mrrt/app/**`.

These rules are ALWAYS ACTIVE for all web application packages, frontend routing entrypoints, server-rendered view modules, layout components, and server-side request handlers.

### Rules

- **R-NJS-001** MUST: Before implementing or upgrading application code relying on Next.js, developers MUST inspect the repository dependency lock artifact to determine the exact resolved framework version and verify that all invoked framework interfaces exist in that version's official documentation.

### Verify

```bash
# Discover and run the project build script declared in the repository manifest
# Discover and run the repository automated test suite
```

**Accept when:**
- The project build script completes with exit code 0 and successfully generates all configured routes and layouts without compilation errors.
- All automated test suites for server-rendered endpoints and layout components pass successfully.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>