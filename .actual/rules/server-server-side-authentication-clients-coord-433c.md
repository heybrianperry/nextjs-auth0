---
version: 2
name: server-server-side-authentication-clients-coord-433c
description: "Next.js Server Modules next/headers and next/server: Server Side Authentication Clients Coordinate Session"
metadata:
  actual:
    adr_id: 433cfb62-25bd-4e90-a843-b2d9fece53a7
    status: accepted
    candidate_group_id: b5f7f0c9-7911-4dae-a8d2-ba285f4925c3
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Modules next/headers and next/server: Server Side Authentication Clients Coordinate Session

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for server-side authentication client modules, domain extensions, server components, route handlers, and server actions requiring authentication state or token retrieval.

### Rules

- **R-AUTH-001** MUST: Server-side authentication clients MUST coordinate session and header operations through the adopted Next.js server runtime modules next/headers and next/server rather than interacting directly with transport-layer HTTP abstractions.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify import boundaries
npm run lint

# Discover and execute type-checking script for server runtime module imports
npm run typecheck

# Discover and execute the automated test suite to confirm session handling and cookie interactions
npm test
```

**Accept when:**
- All server authentication client modules import next/headers and next/server in alignment with architectural boundary constraints.
- Automated tests verify that cookie reads succeed in server contexts and that mutations in read-only rendering cycles emit diagnostic warnings without unhandled exceptions.
- Project static analysis, linting, and type verification suites pass with zero errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via static analysis, peer review, and integration tests, with builds failing upon unauthorized transport layer imports.
</enforcement>