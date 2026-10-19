---
version: 2
name: server-server-side-authentication-operations-th-b0fe
description: "Next.js Server Modules next/headers and next/server: Server Side Authentication Operations That Read"
metadata:
  actual:
    adr_id: b0fe4324-8be4-45fe-9e99-71afdf031e94
    status: accepted
    candidate_group_id: b5f7f0c9-7911-4dae-a8d2-ba285f4925c3
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Modules next/headers and next/server: Server Side Authentication Operations That Read

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for server-side authentication client modules and domain extensions managing session tokens, request headers, or cookies, including server components, route handlers, and server actions requiring authentication state or token retrieval.

### Rules

- **R-AUTH-001** MUST: Server-side authentication operations that read cookies MUST invoke the cookies function from next/headers within supported execution contexts.

### Verify

```bash
# Discover and run project static analysis, type-checking, and linting scripts
# Discover and execute project automated test suite to confirm session handling and cookie interactions
```

**Accept when:**
- All server authentication client modules import next/headers and next/server in alignment with architectural boundary constraints.
- Automated tests verify that cookie reads succeed in server contexts and that mutations in read-only rendering cycles emit diagnostic warnings without unhandled exceptions.
- Project static analysis, linting, and type verification suites pass with zero errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. All server authentication client modules must adhere strictly to framework-native header and cookie integration standards.
</enforcement>