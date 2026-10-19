---
version: 2
name: cross-cutting-discovery-key-caching-modules-utilize-2df2
description: "jose Adoption for Cryptographic Operations and Token Management: Discovery Key Caching Modules Utilize Standardized"
metadata:
  actual:
    adr_id: 2df21a6b-d70c-46af-82bb-bf684d9a4b26
    status: accepted
    candidate_group_id: b93acc58-b784-4e2f-ad35-c3ca460b1a5e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
      - src/types/**
      - src/utils/**
---

# jose Adoption for Cryptographic Operations and Token Management: Discovery Key Caching Modules Utilize Standardized

Scope: applies to `src/server/**`, `src/types/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ADR-001** SHOULD: Discovery and key caching modules utilize standardized key retrieval utilities from the adopted cryptographic library rather than custom key format parsers.

### Verify

```bash
echo "Discover and execute project test suite for cryptographic and session verification"
echo "Discover and execute project linter and dependency checks for unauthorized cryptographic libraries"
```

**Accept when:**
- All cryptographic signing, encryption, decryption, and verification operations compile and pass automated test suites using the standardized token library.
- No unapproved third-party or platform-specific cryptographic token libraries are referenced in session or authentication workflows.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>