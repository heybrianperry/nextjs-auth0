---
version: 2
name: examples-auth0client-instance-configure-authoriza-9bc0
description: "Adopt @auth0/nextjs-auth0/server for Server-Side Authentication: Auth0client Instance Configure Authorizationparameters Including Audience"
metadata:
  actual:
    adr_id: 9bc066ec-0071-4f32-8bb2-21f9e3a51397
    status: accepted
    candidate_group_id: d7b8f89c-0b8b-4612-abbe-bf2681edc5b8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-cte/app/api/stt/**
      - examples/with-dpop/lib/**
      - examples/with-mrrt/lib/**
---

# Adopt @auth0/nextjs-auth0/server for Server-Side Authentication: Auth0client Instance Configure Authorizationparameters Including Audience

Scope: applies to `examples/with-cte/app/api/stt/**`, `examples/with-dpop/lib/**`, `examples/with-mrrt/lib/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST: The Auth0Client instance MUST configure authorizationParameters including audience and scope sourced from validated runtime environment configurations.

### Verify

```bash
# Discover project dependency manifests and verify the presence of the authentication library
npm ls @auth0/nextjs-auth0

# Run the repository test suite to confirm server authentication integration passes
npm test

# Run project static analysis checks
npm run lint
```

**Accept when:**
- All server-side authentication modules instantiate Auth0Client using centralized configuration parameters.
- Repository lock resolution confirms exact dependency versions prior to execution.
- Server route handlers validate authorization context via the centralized client without inline authentication logic.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>