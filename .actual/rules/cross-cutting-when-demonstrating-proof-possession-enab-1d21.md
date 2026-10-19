---
version: 2
name: cross-cutting-when-demonstrating-proof-possession-enab-1d21
description: "Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: When Demonstrating Proof Possession Enabled Endpoint"
metadata:
  actual:
    adr_id: 1d21afc1-e264-487a-b387-a4ea5fd454f7
    status: accepted
    candidate_group_id: 918731ad-5f52-4610-aa8b-fdb972929680
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/lib/**
      - src/server/**
      - src/utils/**
---

# Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: When Demonstrating Proof Possession Enabled Endpoint

Scope: applies to `examples/with-dpop/lib/**`, `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-OAUTH-001** MUST: When Demonstrating Proof-of-Possession is enabled for an endpoint or client, requests MUST generate and attach the appropriate proof headers, and retry logic MUST handle nonce rotation challenges returned by the authorization server.

### Verify

```bash
# Discover the repository build and validation scripts from the project manifest, and execute the static analysis suite to verify library import boundaries.
# Discover and run the project test automation suite to validate OAuth discovery caching and proof-of-possession retry flows.
```

**Accept when:**
- Static analysis validates that all server-side OAuth protocol exchanges route through oauth4webapi without unauthorized bespoke client wrappers.
- Automated test suites confirm successful authorization server discovery, key caching, and proof-of-possession retry handling under simulated nonce rotation.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>