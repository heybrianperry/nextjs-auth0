---
version: 2
name: examples-with-dpop-application-architecture-adopt-oauth4web-e79c
description: "oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Application Architecture Adopt Oauth4webapi Perform Demonstrating"
metadata:
  actual:
    adr_id: e79c85bd-c9c8-4931-a5f7-dec76549f8c6
    status: accepted
    candidate_group_id: c1c1a0d0-6255-4ae6-aff0-e4c2f82dfbcc
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Application Architecture Adopt Oauth4webapi Perform Demonstrating

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-OAUTH-001** MUST: Adopt oauth4webapi to perform Demonstrating Proof-of-Possession token binding verification and validate sender-constrained cryptographic proof claims on protected resources.

### Verify

```bash
# Discover and run the project test suite verifying proof-of-possession token validation
# Discover and run repository static analysis for secrets handling and token binding compliance
```

**Accept when:**
- Token validation test suite successfully confirms valid DPoP proof tokens and confirmation claims
- Requests with invalid, expired, or missing proof signatures are rejected with appropriate error diagnostics
- No unauthorized token fallback or bypassed confirmation checks are detected during automated verification

<enforcement>
Claude Code MUST NOT skip or defer verification. All token binding validation implementations and modifications to authentication middleware must be fully verified by the test suite and static analysis checks.
</enforcement>