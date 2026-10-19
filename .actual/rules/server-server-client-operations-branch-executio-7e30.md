---
version: 2
name: server-server-client-operations-branch-executio-7e30
description: "Next.js Server Modules next/headers and next/server: Server Client Operations Branch Execution Handling"
metadata:
  actual:
    adr_id: 7e308357-fab5-43ed-9057-305f213949d3
    status: accepted
    candidate_group_id: b5f7f0c9-7911-4dae-a8d2-ba285f4925c3
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Modules next/headers and next/server: Server Client Operations Branch Execution Handling

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ADR-001** MAY: Server client operations MAY branch execution handling to support alternative request and response structures when operating outside standard server component contexts.

### Verify

```bash
# Discover and run static analysis, linting, type-checking, and tests via the repository's package manager/build scripts
```

**Accept when:**
- All server authentication client modules import next/headers and next/server in alignment with architectural boundary constraints.
- Automated tests verify that cookie reads succeed in server contexts and that mutations in read-only rendering cycles emit diagnostic warnings without unhandled exceptions.
- Project static analysis, linting, and type verification suites pass with zero errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration builds fail upon detection of unauthorized transport layer imports in server client modules.
</enforcement>