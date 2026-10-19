---
version: 2
name: examples-with-dpop-engineers-discover-repository-dependency-3328
description: "Adopt Helmet for HTTP Security Headers: Engineers Discover Repository Dependency Lock Artifact"
metadata:
  actual:
    adr_id: 3328715f-e43f-4a29-b99b-c7d6e37d1e72
    status: accepted
    candidate_group_id: 06493b99-f9c8-438f-b320-b4939e124ca8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Adopt Helmet for HTTP Security Headers: Engineers Discover Repository Dependency Lock Artifact

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-HLMT-001** MUST: Engineers MUST discover the repository dependency lock artifact and verify the exact resolved version of Helmet before applying or modifying security header configurations.
- **R-HLMT-002** MUST: Mount Helmet middleware before application routers and handlers to guarantee all outbound responses carry protective headers.

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