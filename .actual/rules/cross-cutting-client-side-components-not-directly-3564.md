---
version: 2
name: cross-cutting-client-side-components-not-directly-3564
description: "Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Client Side Components Not Directly Instantiate"
metadata:
  actual:
    adr_id: 35646aec-a394-446f-b30e-36ff82074e65
    status: accepted
    candidate_group_id: 09fc163c-af7c-4dcc-877f-a2c758c104bd
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - e2e/test-app/app/app-router/client/**
      - examples/with-dpop/lib/**
---

# Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Client Side Components Not Directly Instantiate

Scope: applies to `e2e/test-app/app/app-router/client/**`, `examples/with-dpop/lib/**`.

These rules are ALWAYS ACTIVE for all-stack application routes and components requiring user identity, session access, or authentication tokens.

### Rules

- **R-AUTH-001** MUST_NOT: Client-side components MUST NOT directly instantiate Auth0Client or handle cryptographic signing keys reserved for server boundaries.

### Verify

```bash
# Discover the repository test execution script and run the automated test suite covering authentication routes and components.
# Discover the repository static analysis script and execute linting and type checking across client and server source files.
```

**Accept when:**
- Server-side authentication client initializes successfully using resolved environment variables and passes integration tests.
- Client components render user profile information from the useUser hook without runtime exceptions or type errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration checks and peer code reviews.
</enforcement>