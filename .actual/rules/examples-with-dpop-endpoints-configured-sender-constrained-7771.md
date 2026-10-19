---
version: 2
name: examples-with-dpop-endpoints-configured-sender-constrained-7771
description: "oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Endpoints Configured Sender Constrained Token Binding"
metadata:
  actual:
    adr_id: 77717b46-287c-489c-9b82-1958f82391be
    status: accepted
    candidate_group_id: c1c1a0d0-6255-4ae6-aff0-e4c2f82dfbcc
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Endpoints Configured Sender Constrained Token Binding

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DPOP-001** MUST_NOT: Endpoints configured for sender-constrained token binding MUST_NOT accept standard bearer tokens without cryptographic proof unless explicitly isolated on dedicated legacy compatibility routes.

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
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>