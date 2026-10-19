---
version: 2
name: examples-authentication-state-transitions-verific-43b4
description: "Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Authentication State Transitions Verification Callbacks Validate"
metadata:
  actual:
    adr_id: 43b43ccd-1b3d-41d1-a2cf-801a68e30cff
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

# Adoption of @auth0/nextjs-auth0 for Application Authentication and Error Handling: Authentication State Transitions Verification Callbacks Validate

Scope: applies to `examples/with-passkeys/components/**`, `examples/with-passwordless/app/server-passwordless/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** SHOULD: Authentication state transitions and verification callbacks SHOULD validate session tokens and payload authenticity prior to issuing redirects or committing cookie mutations.

### Verify

```bash
# Discover and run the project build, test, type checking, and linting scripts from the project manifest
# Example discovery flow:
# 1. Read package.json to find test, typecheck, and lint scripts
# 2. Execute the detected test suite for authentication flows
# 3. Execute type checking across authentication modules
# 4. Execute linter to verify boundary constraints
```

**Accept when:**
- The project test suite passes with all authentication flow tests and error handling assertions succeeding.
- Static type analysis completes with zero errors across all modules importing @auth0/nextjs-auth0.
- Linting verification scripts validate that client and server authentication module boundaries are strictly preserved.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>