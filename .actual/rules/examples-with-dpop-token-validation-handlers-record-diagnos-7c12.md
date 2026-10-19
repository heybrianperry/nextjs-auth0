---
version: 2
name: examples-with-dpop-token-validation-handlers-record-diagnos-7c12
description: "oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Token Validation Handlers Record Diagnostic Metadata"
metadata:
  actual:
    adr_id: 7c12e63a-6b12-4910-9f54-267892c07ac0
    status: accepted
    candidate_group_id: c1c1a0d0-6255-4ae6-aff0-e4c2f82dfbcc
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Token Validation Handlers Record Diagnostic Metadata

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for client authentication modules and API server middleware validating inbound access tokens.

### Rules

- **R-DPOP-001** SHOULD: Token validation handlers SHOULD record diagnostic metadata including confirmation claim presence, validation status, and verification method on the request context for downstream auditing.

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
Claude Code MUST NOT skip or defer verification. Continuous integration test pipelines and static analysis checks must enforce token binding validation.
</enforcement>