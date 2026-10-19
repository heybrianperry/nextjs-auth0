---
version: 2
name: examples-with-dpop-http-server-instances-mount-helmet-7fea
description: "Adopt Helmet for HTTP Security Headers: Http Server Instances Mount Helmet Middleware"
metadata:
  actual:
    adr_id: 7fea7f87-464a-4a6d-aac5-dce51f8acaf2
    status: accepted
    candidate_group_id: 06493b99-f9c8-438f-b320-b4939e124ca8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Adopt Helmet for HTTP Security Headers: Http Server Instances Mount Helmet Middleware

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-HLMT-001** MUST: All HTTP API server instances MUST mount Helmet middleware in the request processing pipeline to enforce baseline HTTP security headers.
- **R-HLMT-002** MUST: Mount Helmet middleware before application routers and handlers to guarantee all outbound responses carry protective headers.
- **R-HLMT-003** MUST: Execute lock-version grounding before writing code that uses a versioned library, inspecting the dependency manifest, build tool, authoritative lock file, and official documentation.

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