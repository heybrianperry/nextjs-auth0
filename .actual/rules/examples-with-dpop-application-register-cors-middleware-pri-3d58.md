---
version: 2
name: examples-with-dpop-application-register-cors-middleware-pri-3d58
description: "cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Application Register Cors Middleware Primary Http"
metadata:
  actual:
    adr_id: 3d586632-7a31-483f-9d4a-f2f24b17c920
    status: accepted
    candidate_group_id: f5e0fe21-4661-4b6b-94c3-3f7dcfdab4c4
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Application Register Cors Middleware Primary Http

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for HTTP server applications exposing REST or JSON endpoints accessed by browser-based clients and services requiring origin filtering based on deployment environment configuration.

### Rules

- **R-CORS-001** MUST: The application MUST register cors middleware on the primary HTTP router before route definitions to restrict cross-origin request handling.

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