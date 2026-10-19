---
version: 2
name: server-specialized-authentication-domain-client-d127
description: "Next.js Server Modules next/headers and next/server: Specialized Authentication Domain Clients Including Passkey"
metadata:
  actual:
    adr_id: d127e168-7343-4731-8e51-052611fbc2bb
    status: accepted
    candidate_group_id: b5f7f0c9-7911-4dae-a8d2-ba285f4925c3
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
---

# Next.js Server Modules next/headers and next/server: Specialized Authentication Domain Clients Including Passkey

Scope: applies to `src/server/**`.

These rules are ALWAYS ACTIVE for server-side authentication client modules, domain extensions, server components, route handlers, and server actions requiring authentication state or token retrieval.

### Rules

- **R-AUTH-001** SHOULD: Specialized authentication domain clients, including passkey, multi-factor authentication, and passwordless modules, delegate client lifecycle and provider initialization through the shared server authentication client provider infrastructure.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance with server module import boundaries.
# Discover and execute the project automated test suite to confirm session handling and cookie interactions pass across server execution scenarios.
# Discover and execute the type-checking script to ensure compatibility of all server runtime module imports against resolved framework declarations.
```

**Accept when:**
- All server authentication client modules import next/headers and next/server in alignment with architectural boundary constraints.
- Automated tests verify that cookie reads succeed in server contexts and that mutations in read-only rendering cycles emit diagnostic warnings without unhandled exceptions.
- Project static analysis, linting, and type verification suites pass with zero errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via static analysis, peer code review, and integration tests, with builds failing upon unauthorized transport layer imports.
</enforcement>