---
version: 2
name: examples-with-dpop-http-services-not-return-permissive-89be
description: "cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Http Services Not Return Permissive Wildcard"
metadata:
  actual:
    adr_id: 89be473e-e26e-4440-895e-1db424aa8f6c
    status: accepted
    candidate_group_id: f5e0fe21-4661-4b6b-94c3-3f7dcfdab4c4
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Http Services Not Return Permissive Wildcard

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all HTTP server applications exposing REST or JSON endpoints accessed by browser-based clients.

### Rules

- **R-CORS-001** MUST_NOT: HTTP API services MUST NOT return permissive wildcard access control headers for endpoints requiring credentialed or token-bound authorization.

### Verify

```bash
# Discover and execute the repository security linting suite to ensure cors middleware is registered with explicit origin constraints.
# Discover and execute the HTTP test suite verifying that cross-origin preflight requests evaluate the origin against configured environment values.
```

**Accept when:**
- Cross-origin preflight and standard HTTP requests validate that the Access-Control-Allow-Origin header strictly mirrors authorized configured origins.
- Requests originating from unauthorized origins do not receive permissive cross-origin response headers.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>