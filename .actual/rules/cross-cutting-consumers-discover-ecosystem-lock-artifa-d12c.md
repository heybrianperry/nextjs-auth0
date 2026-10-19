---
version: 2
name: cross-cutting-consumers-discover-ecosystem-lock-artifa-d12c
description: "Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Consumers Discover Ecosystem Lock Artifact Resolve"
metadata:
  actual:
    adr_id: d12caddb-9d2f-4c25-88a9-c0649917879f
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

# Adoption of @auth0/nextjs-auth0/types for Shared Authentication Type Contracts: Consumers Discover Ecosystem Lock Artifact Resolve

Scope: applies to `e2e/test-app/pages/api/pages-router/get-session/**`, `examples/with-cte/app/api/cte/**`, `examples/with-passkeys/**`, `examples/with-passwordless-db/components/**`.

These rules are ALWAYS ACTIVE for modules handling authentication requests, session retrieval, passkey challenges, or identity data structures across client and server boundaries.

### Rules

- **R-AUTH-001** MUST: Consumers MUST discover the ecosystem lock artifact and resolve the exact locked version of the identity library before implementing or altering type references.

### Verify

```bash
# Discover and run the project type checker script defined in the dependency manifest
# Discover and execute the repository static analysis and linting scripts
```

**Accept when:**
- All imports from @auth0/nextjs-auth0/types pass static type validation without errors across client and server boundaries.
- No circular dependencies or leaked server-side runtime code are detected in client bundles during verification builds.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>