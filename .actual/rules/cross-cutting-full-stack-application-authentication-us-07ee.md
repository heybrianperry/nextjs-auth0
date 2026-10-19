---
version: 2
name: cross-cutting-full-stack-application-authentication-us-07ee
description: "Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Full Stack Application Authentication Use Auth0"
metadata:
  actual:
    adr_id: 07ee043b-c299-4bc8-8e0b-1fa063baec27
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

# Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Full Stack Application Authentication Use Auth0

Scope: applies to `e2e/test-app/app/app-router/client/**`, `examples/with-dpop/lib/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST: Full-stack application authentication MUST use @auth0/nextjs-auth0 as the standardized identity provider SDK across both server-side token handling and client-side session access.

### Verify

```bash
# Discover the repository test execution script and run the automated test suite covering authentication routes and components.
# Discover the repository static analysis script and execute linting and type checking across client and server source files.
```

**Accept when:**
- Server-side authentication client initializes successfully using resolved environment variables and passes integration tests.
- Client components render user profile information from the useUser hook without runtime exceptions or type errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>