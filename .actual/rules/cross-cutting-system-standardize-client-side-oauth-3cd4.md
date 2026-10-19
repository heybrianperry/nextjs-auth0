---
version: 2
name: cross-cutting-system-standardize-client-side-oauth-3cd4
description: "Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: System Standardize Client Side Oauth Openid"
metadata:
  actual:
    adr_id: 3cd44062-deb8-4f82-bce5-8c1396cae3e9
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

# Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: System Standardize Client Side Oauth Openid

Scope: applies to `examples/with-dpop/lib/**`, `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all server-side modules performing OAuth 2.0 or OpenID Connect token requests, token refreshes, discovery operations, and client integration layers negotiating Demonstrating Proof-of-Possession.

### Rules

- **R-OAUTH-001** MUST: Standardize all client-side OAuth 2.0 and OpenID Connect protocol exchanges, authorization server discovery operations, and Demonstrating Proof-of-Possession mechanisms on oauth4webapi.

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