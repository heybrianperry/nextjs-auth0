---
version: 2
name: cross-cutting-client-rendered-components-requiring-rea-6d5e
description: "Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Client Rendered Components Requiring Reactive Authentication"
metadata:
  actual:
    adr_id: 6d5e0ae8-a9f4-4312-8051-b5f6d8c77804
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

# Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Client Rendered Components Requiring Reactive Authentication

Scope: applies to `e2e/test-app/app/app-router/client/**`, `examples/with-dpop/lib/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-AUTH-001** MUST: Client-rendered components requiring reactive authentication context MUST obtain user identity via the useUser hook.

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