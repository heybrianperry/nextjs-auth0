---
version: 2
name: examples-authentication-failures-occurring-server-f5fa
description: "Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Authentication Failures Occurring Server Route Handlers"
metadata:
  actual:
    adr_id: f5fa2500-7e3b-4c35-9877-c2adc38593ff
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

# Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Authentication Failures Occurring Server Route Handlers

Scope: applies to `examples/with-passkeys/components/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for application route handlers, pages, and interactive UI components implementing authentication, passwordless login, passkey challenges, or identity verification.

### Rules

- **R-AUTH-001** MUST: Authentication failures occurring in server route handlers and client components MUST be trapped and normalized using the @auth0/nextjs-auth0/errors module.

### Verify

```bash
# Discover and execute repository test, type-checking, and lint scripts from the project manifest
# Example discovery loop:
# 1. Read package.json scripts
# 2. Run test suite
# 3. Run type check / static analysis
# 4. Run linting verification
```

**Accept when:**
- The project test suite passes with all authentication flow tests and error handling assertions succeeding.
- Static type analysis completes with zero errors across all modules importing @auth0/nextjs-auth0.
- Linting verification scripts validate that client and server authentication module boundaries are strictly preserved.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration static analysis checking import boundaries, automated test suites, and peer review enforce these rules, and unapproved libraries or bypassed error handling modules will be blocked.
</enforcement>