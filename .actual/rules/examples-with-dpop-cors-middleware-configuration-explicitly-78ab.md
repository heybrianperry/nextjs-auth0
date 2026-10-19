---
version: 2
name: examples-with-dpop-cors-middleware-configuration-explicitly-78ab
description: "cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Cors Middleware Configuration Explicitly Specify Origin"
metadata:
  actual:
    adr_id: 78ab492b-9cd7-41b3-8029-ce9ba88d4359
    status: accepted
    candidate_group_id: f5e0fe21-4661-4b6b-94c3-3f7dcfdab4c4
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Cors Middleware Configuration Explicitly Specify Origin

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for HTTP server applications exposing REST or JSON endpoints accessed by browser-based clients and services requiring origin filtering based on deployment environment configuration.

### Rules

- **R-CORS-001** MUST: The cors middleware configuration MUST explicitly specify the origin option bound to an environment-configured base address rather than allowing wildcard origin access.

### Verify

```bash
# Discover and execute the repository security linting suite to ensure cors middleware is registered with explicit origin constraints.
# Discover and execute the HTTP test suite verifying that cross-origin preflight requests evaluate the origin against configured environment values.
```

**Accept when:**
- Cross-origin preflight and standard HTTP requests validate that the Access-Control-Allow-Origin header strictly mirrors authorized configured origins.
- Requests originating from unauthorized origins do not receive permissive cross-origin response headers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>