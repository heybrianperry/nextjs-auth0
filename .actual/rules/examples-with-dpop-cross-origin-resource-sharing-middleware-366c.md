---
version: 2
name: examples-with-dpop-cross-origin-resource-sharing-middleware-366c
description: "cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Cross Origin Resource Sharing Middleware Registered"
metadata:
  actual:
    adr_id: 366cff48-8b57-4daf-97e0-96bc4104af39
    status: accepted
    candidate_group_id: f5e0fe21-4661-4b6b-94c3-3f7dcfdab4c4
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Cross Origin Resource Sharing Middleware Registered

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for HTTP server applications exposing REST or JSON endpoints accessed by browser-based clients and services requiring origin filtering based on deployment environment configuration.

### Rules

- **R-CORS-001** SHOULD: Cross-origin resource sharing middleware SHOULD be registered early in the middleware pipeline alongside core security header handlers.
- **R-CORS-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository (DISCOVERY POLICY).
- **R-CORS-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect lock/resolution artifact for exact version, look up official documentation for that exact version, confirm every API/class/function exists in that exact version, and re-run per dependency at point of use (LOCK-VERSION GROUNDING).
- **R-CORS-004** MANDATORY: Ensure the cors middleware is mounted prior to application routes to intercept preflight OPTIONS requests before endpoint authorization logic.
- **R-CORS-005** MANDATORY: Validate the origin configuration parameter during runtime initialization to guarantee that empty or malformed origin variables fail fast.

### Verify

```bash
# Discover and execute the repository security linting suite to ensure cors middleware is registered with explicit origin constraints.
# Discover and execute the HTTP test suite verifying that cross-origin preflight requests evaluate the origin against configured environment values.
```

**Accept when:**
- Cross-origin preflight and standard HTTP requests validate that the Access-Control-Allow-Origin header strictly mirrors authorized configured origins.
- Requests originating from unauthorized origins do not receive permissive cross-origin response headers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated security linter rules checking middleware registration and integration test suites validating Access-Control-Allow-Origin response headers are mandatory.
</enforcement>