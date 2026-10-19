---
version: 2
name: examples-with-dpop-client-authentication-integrations-confi-e470
description: "oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Client Authentication Integrations Configured Demonstrating Proof"
metadata:
  actual:
    adr_id: e4702693-34b7-406f-81b2-9b2b49c4b5db
    status: accepted
    candidate_group_id: c1c1a0d0-6255-4ae6-aff0-e4c2f82dfbcc
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Client Authentication Integrations Configured Demonstrating Proof

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for all client authentication integrations, API server middleware, and route handlers configuring or validating Demonstrating Proof-of-Possession token bindings.

### Rules

- **R-POP-001** MUST: Client authentication integrations configured with Demonstrating Proof-of-Possession MUST supply a valid client key pair parameter to generate signed proof tokens bound to target audience endpoints.

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
Claude Code MUST NOT skip or defer verification. All pull requests lacking required token binding validation or test coverage must be blocked from merging.
</enforcement>