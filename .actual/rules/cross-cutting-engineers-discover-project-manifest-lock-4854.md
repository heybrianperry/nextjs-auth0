---
version: 2
name: cross-cutting-engineers-discover-project-manifest-lock-4854
description: "Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Engineers Discover Project Manifest Lock Artifact"
metadata:
  actual:
    adr_id: 4854b1b5-8bd9-4221-a92d-fb5668db4fae
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

# Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Engineers Discover Project Manifest Lock Artifact

Scope: applies to `examples/with-dpop/lib/**`, `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all server-side modules performing OAuth 2.0 or OpenID Connect token requests, token refreshes, discovery operations, and DPoP client integration layers.

### Rules

- **R-OAUTH-001** MUST: Engineers MUST discover the project manifest and lock artifact to resolve the exact dependency version before integrating or updating oauth4webapi calls.

### Verify

```bash
# Discover the project manifest and run static analysis/test suites
# (Commands to be derived from repository configuration)
```

**Accept when:**
- Static analysis validates that all server-side OAuth protocol exchanges route through oauth4webapi without unauthorized bespoke client wrappers.
- Automated test suites confirm successful authorization server discovery, key caching, and proof-of-possession retry handling under simulated nonce rotation.

<enforcement>
Claude Code MUST NOT skip or defer verification. All server-side OAuth protocol exchanges must be verified against dependency manifests, locks, and static analysis suites.
</enforcement>