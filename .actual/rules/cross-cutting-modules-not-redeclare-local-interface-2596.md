---
version: 2
name: cross-cutting-modules-not-redeclare-local-interface-2596
description: "Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Modules Not Redeclare Local Interface Duplicates"
metadata:
  actual:
    adr_id: 2596d496-2038-48ac-8761-07226b499316
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

# Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Modules Not Redeclare Local Interface Duplicates

Scope: applies to `e2e/test-app/pages/api/pages-router/get-session/**`, `examples/with-cte/app/api/cte/**`, `examples/with-passkeys/**`, `examples/with-passwordless-db/components/**`.

These rules are ALWAYS ACTIVE for modules handling authentication requests, session retrieval, passkey challenges, or identity data structures across client and server boundaries.

### Rules

- **R-AUTH-001** MUST_NOT: Modules MUST NOT redeclare local interface duplicates of authentication session structures or challenge parameters provided by @auth0/nextjs-auth0/types.
- **R-AUTH-002** MUST: Use explicit type-only import syntax when referencing contracts from the identity types module to guarantee full removal during compilation.
- **R-AUTH-003** MUST: Maintain clear boundary separation by defining application-specific server actions or API responses that compose upstream identity contracts rather than mutating upstream types directly.

### Verify

```bash
# Discover and run the project type checker script defined in the dependency manifest to verify that all authentication type references resolve cleanly.
npm run typecheck

# Discover and execute the repository static analysis and linting scripts to verify that identity type imports comply with module boundary rules.
npm run lint
```

**Accept when:**
- All imports from @auth0/nextjs-auth0/types pass static type validation without errors across client and server boundaries.
- No circular dependencies or leaked server-side runtime code are detected in client bundles during verification builds.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline executing repository verification and type validation scripts, and by peer code review auditing authentication contract usage and import paths.
</enforcement>