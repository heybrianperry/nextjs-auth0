---
version: 2
name: examples-client-side-interactive-components-not-5e6a
description: "Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Client Side Interactive Components Not Invoke"
metadata:
  actual:
    adr_id: 5e6aab89-f322-4419-a57f-a539d5cd3957
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

# Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Client Side Interactive Components Not Invoke

Scope: applies to `examples/with-passkeys/components/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for all application route handlers, pages, and interactive UI components implementing authentication, passwordless login, passkey challenges, or identity verification.

### Rules

- **R-AUTH-001** MUST_NOT: Client-side interactive components MUST NOT invoke server-only authentication routines directly and MUST consume exported primitives from @auth0/nextjs-auth0/client.

### Verify

```bash
# Discover and execute the project build, test, type checking, and linting scripts from the manifest
npm test
npm run lint
npm run typecheck
```

**Accept when:**
- The project test suite passes with all authentication flow tests and error handling assertions succeeding.
- Static type analysis completes with zero errors across all modules importing @auth0/nextjs-auth0.
- Linting verification scripts validate that client and server authentication module boundaries are strictly preserved.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by continuous integration static analysis, automated test suites, and peer review.
</enforcement>