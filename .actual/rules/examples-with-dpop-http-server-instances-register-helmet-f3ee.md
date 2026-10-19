---
version: 2
name: examples-with-dpop-http-server-instances-register-helmet-f3ee
description: "Adopt Helmet for HTTP Security Headers: Http Server Instances Register Helmet Prior"
metadata:
  actual:
    adr_id: f3ee6a95-703e-4fa0-8c16-a5b729858d89
    status: accepted
    candidate_group_id: 06493b99-f9c8-438f-b320-b4939e124ca8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Adopt Helmet for HTTP Security Headers: Http Server Instances Register Helmet Prior

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-HLMT-001** MUST: HTTP server instances MUST register Helmet prior to mounting routing and payload-handling middleware.

### Verify

```bash
grep -rn "app.use(helmet" . || echo "Verify Helmet middleware registration in HTTP server setup"
find . -maxdepth 3 -name "*test*" -o -name "*spec*" | head -n 1 && echo "Execute discovered test runner to validate response headers"
```

**Accept when:**
- HTTP server setup code contains Helmet middleware registration prior to route definitions
- Discovered test suite executes successfully and confirms security headers are present on HTTP responses

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>