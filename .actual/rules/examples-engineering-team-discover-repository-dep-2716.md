---
version: 2
name: examples-engineering-team-discover-repository-dep-2716
description: "Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Engineering Team Discover Repository Dependency Manifest"
metadata:
  actual:
    adr_id: 2716cf94-ac57-4270-9952-207b9b25af31
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

# Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Engineering Team Discover Repository Dependency Manifest

Scope: applies to `examples/with-passkeys/components/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for application route handlers, pages, and interactive UI components implementing authentication, passwordless login, passkey challenges, or identity verification.

### Rules

- **R-AUTH-001** MUST: The engineering team MUST discover the repository dependency manifest and resolution artifact to verify the exact resolved version of @auth0/nextjs-auth0 before invoking library APIs.

### Verify

```bash
# Discover and run project build, test, type checking, linting, and static analysis verification scripts from the project manifest
# Example discovery pattern:
# npm test
# npm run type-check
# npm run lint
```

**Accept when:**
- The project test suite passes with all authentication flow tests and error handling assertions succeeding.
- Static type analysis completes with zero errors across all modules importing @auth0/nextjs-auth0.
- Linting verification scripts validate that client and server authentication module boundaries are strictly preserved.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration static analysis checking import boundaries, automated test suites, and peer review are mandatory for all modifications touching identity utility modules or authentication handler routes.
</enforcement>