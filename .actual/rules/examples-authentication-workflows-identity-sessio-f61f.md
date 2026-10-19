---
version: 2
name: examples-authentication-workflows-identity-sessio-f61f
description: "Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Authentication Workflows Identity Session Management Integrate"
metadata:
  actual:
    adr_id: f61ffcd5-2525-49a2-ad41-71def08cd74e
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

# Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Authentication Workflows Identity Session Management Integrate

Scope: applies to `examples/with-passkeys/components/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST: All authentication workflows and identity session management MUST integrate through @auth0/nextjs-auth0 modules to maintain consistent authentication boundaries across server and client boundaries.
- **R-AUTH-002** MUST: Encapsulate authentication configuration inside internal module boundaries to insulate application handlers from identity provider API changes.
- **R-AUTH-003** MUST: Ensure that all authentication errors are caught, sanitized against information leakage, and routed through standardized logging pipelines.

### Verify

```bash
# Discover the repository build and test verification scripts from the project manifest and execute the test suite.
# Discover and run the project type checking and static analysis verification scripts across all authentication modules.
# Execute the repository linting verification scripts to ensure imports conform to boundary constraints.
```

**Accept when:**
- The project test suite passes with all authentication flow tests and error handling assertions succeeding.
- Static type analysis completes with zero errors across all modules importing @auth0/nextjs-auth0.
- Linting verification scripts validate that client and server authentication module boundaries are strictly preserved.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>