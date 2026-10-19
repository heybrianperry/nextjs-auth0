---
version: 2
name: server-before-integrating-updating-functionalit-c38e
description: "Next.js Server Modules next/headers and next/server: Before Integrating Updating Functionality Dependent These"
metadata:
  actual:
    adr_id: c38eb8a1-3735-4724-9021-5c75c018a3d1
    status: accepted
    candidate_group_id: b5f7f0c9-7911-4dae-a8d2-ba285f4925c3
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Modules next/headers and next/server: Before Integrating Updating Functionality Dependent These

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for server-side authentication client modules, domain extensions, server components, route handlers, and server actions requiring authentication state or token retrieval.

### Rules

- **R-NXT-001** MUST: Before integrating or updating functionality dependent on these server runtime modules, the consumer MUST inspect the repository lock artifact to determine the exact resolved framework version and verify compatibility of the accessed APIs against version-specific documentation.

### Verify

```bash
# Discover and run the project static analysis and linting scripts
# Discover and execute the project automated test suite
# Discover and execute the type-checking script
```

**Accept when:**
- All server authentication client modules import next/headers and next/server in alignment with architectural boundary constraints.
- Automated tests verify that cookie reads succeed in server contexts and that mutations in read-only rendering cycles emit diagnostic warnings without unhandled exceptions.
- Project static analysis, linting, and type verification suites pass with zero errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated static analysis checks, peer code review, and integration tests in continuous integration pipelines.
</enforcement>