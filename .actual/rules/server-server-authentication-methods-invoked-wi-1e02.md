---
version: 2
name: server-server-authentication-methods-invoked-wi-1e02
description: "Next.js Server Modules next/headers and next/server: Server Authentication Methods Invoked Within Read"
metadata:
  actual:
    adr_id: 1e021893-c626-4447-b834-ef996f0a5be9
    status: accepted
    candidate_group_id: b5f7f0c9-7911-4dae-a8d2-ba285f4925c3
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Modules next/headers and next/server: Server Authentication Methods Invoked Within Read

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for server-side authentication client modules, domain extensions, server components, route handlers, and server actions requiring authentication state or token retrieval.

### Rules

- **R-AUTH-001** MUST_NOT: Server authentication methods invoked within read-only server contexts MUST NOT attempt mutating cookie writes, and MUST raise appropriate runtime warnings or errors when token refreshes cannot persist cookies.

### Verify

```bash
# Discover and run static analysis and linting scripts
# Discover and execute automated test suite
# Discover and execute type-checking script
```

**Accept when:**
- All server authentication client modules import next/headers and next/server in alignment with architectural boundary constraints.
- Automated tests verify that cookie reads succeed in server contexts and that mutations in read-only rendering cycles emit diagnostic warnings without unhandled exceptions.
- Project static analysis, linting, and type verification suites pass with zero errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>