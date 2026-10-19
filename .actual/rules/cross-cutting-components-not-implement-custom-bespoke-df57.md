---
version: 2
name: cross-cutting-components-not-implement-custom-bespoke-df57
description: "Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Components Not Implement Custom Bespoke Http"
metadata:
  actual:
    adr_id: df579273-00bd-4845-aca1-9b868364797c
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

# Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Components Not Implement Custom Bespoke Http

Scope: applies to `examples/with-dpop/lib/**`, `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all server-side modules performing OAuth 2.0 or OpenID Connect token requests, token refreshes, and discovery operations, as well as client integration layers negotiating Demonstrating Proof-of-Possession.

### Rules

- **R-OAUTH-001** MUST_NOT: Components MUST_NOT implement custom, bespoke HTTP authorization request encoders or manual token exchange endpoints when equivalent routines exist within oauth4webapi.

### Verify

```bash
# Discover the repository build and validation scripts from the project manifest, and execute the static analysis suite to verify library import boundaries.
# Discover and run the project test automation suite to validate OAuth discovery caching and proof-of-possession retry flows.
```

**Accept when:**
- Static analysis validates that all server-side OAuth protocol exchanges route through oauth4webapi without unauthorized bespoke client wrappers.
- Automated test suites confirm successful authorization server discovery, key caching, and proof-of-possession retry handling under simulated nonce rotation.

<enforcement>
Claude Code MUST NOT skip or defer verification. All server-side OAuth protocol exchanges and token operations must be validated against the standard oauth4webapi library.
</enforcement>