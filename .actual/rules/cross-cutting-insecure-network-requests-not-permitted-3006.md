---
version: 2
name: cross-cutting-insecure-network-requests-not-permitted-3006
description: "Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Insecure Network Requests Not Permitted Outside"
metadata:
  actual:
    adr_id: 30061bce-a98b-42d9-b22a-2d40d166d053
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

# Adoption of @auth0/nextjs-auth0 for Client and Server Authentication: Insecure Network Requests Not Permitted Outside

Scope: applies to `e2e/test-app/app/app-router/client/**`, `examples/with-dpop/lib/**`.

These rules are ALWAYS ACTIVE for all full-stack application routes, components, and server-side identity clients requiring user identity, session access, or authentication tokens.

### Rules

- **R-AUTH-001** SHOULD: Insecure network requests SHOULD NOT be permitted outside development environments.
- **R-AUTH-002** MANDATORY: Configure server-side Auth0Client within an isolated server-only module to prevent accidental bundling into client artifacts.
- **R-AUTH-003** MANDATORY: Wrap client components requiring access to the useUser hook with the appropriate identity context provider higher in the component hierarchy.
- **R-AUTH-004** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: 1. Find the dependency manifest in the repo. 2. Identify the build tool from the manifest. 3. Inspect the repository lock or resolution artifact to determine the exact resolved version. 4. Look up official documentation/changelog/API reference for that exact version. 5. Confirm every API, class, or function used exists in that version's documentation. 6. Re-run steps 3-5 per dependency at point of use for version-sensitive behavior.

### Verify

```bash
# Discover the repository test execution script and run the automated test suite covering authentication routes and components.
# Discover the repository static analysis script and execute linting and type checking across client and server source files.
```

**Accept when:**
- Server-side authentication client initializes successfully using resolved environment variables and passes integration tests.
- Client components render user profile information from the useUser hook without runtime exceptions or type errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks and peer code reviews auditing imports of @auth0/nextjs-auth0 across boundaries.
</enforcement>