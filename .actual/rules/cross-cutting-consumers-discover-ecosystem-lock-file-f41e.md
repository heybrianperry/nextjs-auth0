---
version: 2
name: cross-cutting-consumers-discover-ecosystem-lock-file-f41e
description: "jose Adoption for Cryptographic Operations and Token Management: Consumers Discover Ecosystem Lock File Verify"
metadata:
  actual:
    adr_id: f41e7e00-b5a9-4df1-bfb2-c8952455a1d7
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

# jose Adoption for Cryptographic Operations and Token Management: Consumers Discover Ecosystem Lock File Verify

Scope: applies to `src/server/**`, `src/types/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CRYPTO-001** MUST: Consumers MUST discover the ecosystem lock file and verify the exact resolved version of the cryptographic library before implementing or modifying dependent features.

### Verify

```bash
echo "Discover and execute project test suite for cryptographic and session verification"
eecho "Discover and execute project linter and dependency checks for unauthorized cryptographic libraries"
```

**Accept when:**
- All cryptographic signing, encryption, decryption, and verification operations compile and pass automated test suites using the standardized token library.
- No unapproved third-party or platform-specific cryptographic token libraries are referenced in session or authentication workflows.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>