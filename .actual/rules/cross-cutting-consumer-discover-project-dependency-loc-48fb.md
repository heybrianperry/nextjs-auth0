---
version: 2
name: cross-cutting-consumer-discover-project-dependency-loc-48fb
description: "Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Consumer Discover Project Dependency Lock Artifact"
metadata:
  actual:
    adr_id: 48fb0d13-68e0-4485-81a2-abff7bf716ca
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

# Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Consumer Discover Project Dependency Lock Artifact

Scope: applies to `e2e/test-app/app/app-router/client/**`, `examples/with-dpop/lib/**`.

These rules are ALWAYS ACTIVE for full-stack application routes, components, and server-side identity client initializations requiring user identity, session access, or authentication tokens.

### Rules

- **R-AUTH-001** MUST: The consumer MUST discover the project dependency lock artifact and resolve the exact locked version of @auth0/nextjs-auth0 before implementing or calling any authentication interfaces.

### Verify

```bash
# Discover the repository test execution script and run the automated test suite covering authentication routes and components.
# Discover the repository static analysis script and execute linting and type checking across client and server source files.
```

**Accept when:**
- Server-side authentication client initializes successfully using resolved environment variables and passes integration tests.
- Client components render user profile information from the useUser hook without runtime exceptions or type errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks and peer code reviews auditing imports of @auth0/nextjs-auth0 across server and client boundaries.
</enforcement>