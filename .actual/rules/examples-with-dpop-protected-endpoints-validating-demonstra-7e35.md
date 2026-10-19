---
version: 2
name: examples-with-dpop-protected-endpoints-validating-demonstra-7e35
description: "oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Protected Endpoints Validating Demonstrating Proof Possession"
metadata:
  actual:
    adr_id: 7e3567a9-1f8f-4816-9330-584702aba008
    status: accepted
    candidate_group_id: c1c1a0d0-6255-4ae6-aff0-e4c2f82dfbcc
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Protected Endpoints Validating Demonstrating Proof Possession

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DPOP-001** MUST: Protected endpoints validating Demonstrating Proof-of-Possession tokens MUST verify the cryptographic confirmation claim within token claims and reject requests where token binding validation fails.

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
Claude Code MUST NOT skip or defer verification.
</enforcement>