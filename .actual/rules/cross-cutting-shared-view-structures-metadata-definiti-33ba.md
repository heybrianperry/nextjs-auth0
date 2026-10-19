---
version: 2
name: cross-cutting-shared-view-structures-metadata-definiti-33ba
description: "Next.js Application Framework Adoption: Shared View Structures Metadata Definitions Defined"
metadata:
  actual:
    adr_id: 33ba791f-6275-46e6-908b-b11bb6fb0744
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

# Next.js Application Framework Adoption: Shared View Structures Metadata Definitions Defined

Scope: applies to `e2e/test-app/pages/pages-router/server/**`, `examples/with-ipsie-session-expiry/app/**`, `examples/with-mrrt/app/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-NXT-001** SHOULD: Shared view structures and metadata definitions SHOULD be defined in root and nested layout modules to preserve cross-route presentation consistency.

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