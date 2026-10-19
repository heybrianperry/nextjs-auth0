---
version: 2
name: examples-with-dpop-development-team-inspect-project-depende-259d
description: "cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Development Team Inspect Project Dependency Lock"
metadata:
  actual:
    adr_id: 259d6dcb-7534-4604-aae4-bffa142648b8
    status: accepted
    candidate_group_id: f5e0fe21-4661-4b6b-94c3-3f7dcfdab4c4
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Development Team Inspect Project Dependency Lock

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for HTTP server applications exposing REST or JSON endpoints accessed by browser-based clients and services requiring origin filtering based on deployment environment configuration.

### Rules

- **R-COR-001** MUST: The development team MUST inspect the project dependency lock artifact to verify the exact resolved version of the cross-origin sharing dependency before using its configuration APIs.

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