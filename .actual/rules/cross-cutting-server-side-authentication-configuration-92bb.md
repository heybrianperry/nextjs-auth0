---
version: 2
name: cross-cutting-server-side-authentication-configuration-92bb
description: "Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Server Side Authentication Configurations Instantiate Auth0client"
metadata:
  actual:
    adr_id: 92bb8901-c369-446c-a315-0bded0044afe
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

# Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Server Side Authentication Configurations Instantiate Auth0client

Scope: applies to `e2e/test-app/app/app-router/client/**`, `examples/with-dpop/lib/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST: Server-side authentication configurations MUST instantiate Auth0Client with explicit authorization parameters and runtime environment configuration.

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