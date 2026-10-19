---
version: 2
name: cross-cutting-server-side-request-fetchers-wrap-80f0
description: "Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Server Side Request Fetchers Wrap Standard"
metadata:
  actual:
    adr_id: 80f00949-794c-4822-9627-087415e81192
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

# Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Server Side Request Fetchers Wrap Standard

Scope: applies to `examples/with-dpop/lib/**`, `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-OAUTH-001** SHOULD: Server-side request fetchers SHOULD wrap standard HTTP abstractions and propagate response header validations in conformity with oauth4webapi response processing expectations.
- **R-OAUTH-002** MANDATORY: The consumer MUST derive tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-OAUTH-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version's documentation, and re-run steps 3-5 per dependency at point of use.

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