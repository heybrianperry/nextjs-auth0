---
version: 2
name: examples-server-side-route-handlers-encapsulate-5516
description: "Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Server Side Route Handlers Encapsulate Authentication"
metadata:
  actual:
    adr_id: 5516e618-10e5-4a93-950e-576b4a6fddf6
    status: accepted
    candidate_group_id: 7805364d-7d73-4bc5-bb37-3587755b89bf
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-passkeys/components/**
      - examples/with-passwordless/app/server-passwordless/**
---

# Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Server Side Route Handlers Encapsulate Authentication

Scope: applies to `examples/with-passkeys/components/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for application route handlers, pages, and interactive UI components implementing authentication, passwordless login, passkey challenges, or identity verification.

### Rules

- **R-AUTH-001** SHOULD: Server-side route handlers SHOULD encapsulate authentication configuration and client initialization within an internal identity utility module rather than instantiating ad-hoc client configurations.

### Verify

```bash
# Discover and execute project test suite, type checking, and linting scripts from project manifest
# Example discovery flow:
# 1. Inspect package.json for test, typecheck/lint scripts
# 2. Run test suite
# 3. Run type checking
# 4. Run linter
npm test
npm run typecheck
npm run lint
```

**Accept when:**
- The project test suite passes with all authentication flow tests and error handling assertions succeeding.
- Static type analysis completes with zero errors across all modules importing @auth0/nextjs-auth0.
- Linting verification scripts validate that client and server authentication module boundaries are strictly preserved.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration static analysis, automated test suites, and peer review enforce client/server import boundaries and standardized error handling.
</enforcement>