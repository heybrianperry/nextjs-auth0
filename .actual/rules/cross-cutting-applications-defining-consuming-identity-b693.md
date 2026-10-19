---
version: 2
name: cross-cutting-applications-defining-consuming-identity-b693
description: "Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Applications Defining Consuming Identity Data Contracts"
metadata:
  actual:
    adr_id: b693450d-d160-44dc-a21e-fb191e7f4786
    status: accepted
    candidate_group_id: 38f5d321-324d-4414-965e-59757a28e09c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/pages/api/pages-router/get-session/**
      - examples/with-cte/app/api/cte/**
      - examples/with-passkeys/**
      - examples/with-passwordless-db/components/**
---

# Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Applications Defining Consuming Identity Data Contracts

Scope: applies to `e2e/test-app/pages/api/pages-router/get-session/**`, `examples/with-cte/app/api/cte/**`, `examples/with-passkeys/**`, `examples/with-passwordless-db/components/**`.

These rules are ALWAYS ACTIVE for modules handling authentication requests, session retrieval, passkey challenges, or identity data structures across client and server boundaries.

### Rules

- **R-AUTH-001** MUST: Applications defining or consuming identity data contracts MUST import shared identity types directly from the @auth0/nextjs-auth0/types module.

### Verify

```bash
# Discover and run the project type checker script defined in the dependency manifest
# Discover and execute the repository static analysis and linting scripts
```

**Accept when:**
- All imports from @auth0/nextjs-auth0/types pass static type validation without errors across client and server boundaries.
- No circular dependencies or leaked server-side runtime code are detected in client bundles during verification builds.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>