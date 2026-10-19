---
version: 2
name: cross-cutting-oauth-authorization-server-metadata-cryp-cbf5
description: "Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Oauth Authorization Server Metadata Cryptographic Key"
metadata:
  actual:
    adr_id: cbf5c1ee-6a4f-461a-b1bd-946b93b2c83b
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

# Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Oauth Authorization Server Metadata Cryptographic Key

Scope: applies to `examples/with-dpop/lib/**`, `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all server-side modules performing OAuth 2.0 or OpenID Connect token requests, token refreshes, discovery operations, and client integration layers that negotiate Demonstrating Proof-of-Possession.

### Rules

- **R-OAUTH-001** MUST: OAuth authorization server metadata and cryptographic key sets MUST be resolved through cached discovery routines that coordinate in-flight requests and prevent redundant network round-trips.

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