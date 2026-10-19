---
version: 2
name: cross-cutting-server-actions-routes-extend-exported-ebac
description: "Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Server Actions Routes Extend Exported Contracts"
metadata:
  actual:
    adr_id: ebac26ac-f4bd-4f6d-94ab-c5a0e728f306
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

# Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Server Actions Routes Extend Exported Contracts

Scope: applies to `e2e/test-app/pages/api/pages-router/get-session/**`, `examples/with-cte/app/api/cte/**`, `examples/with-passkeys/**`, `examples/with-passwordless-db/components/**`.

These rules are ALWAYS ACTIVE for modules handling authentication requests, session retrieval, passkey challenges, or identity data structures across client and server boundaries.

### Rules

- **R-AUTH-001** MAY: Server actions and API routes MAY extend exported contracts from @auth0/nextjs-auth0/types when adding application-specific authentication metadata.

### Verify

```bash
# Run the project type checker script defined in the dependency manifest
# Discover and execute the repository static analysis and linting scripts
```

**Accept when:**
- All imports from @auth0/nextjs-auth0/types pass static type validation without errors across client and server boundaries.
- No circular dependencies or leaked server-side runtime code are detected in client bundles during verification builds.

<enforcement>
Claude Code MUST NOT skip or defer verification. All authentication type references must resolve cleanly and comply with module boundary rules.
</enforcement>