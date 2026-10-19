---
version: 2
name: cross-cutting-system-standardize-jose-cryptographic-to-c2fe
description: "jose Adoption for Cryptographic Operations and Token Management: System Standardize Jose Cryptographic Token Operations"
metadata:
  actual:
    adr_id: c2fef9b4-e4c8-4aa7-ae7e-51d05de00c09
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

# jose Adoption for Cryptographic Operations and Token Management: System Standardize Jose Cryptographic Token Operations

Scope: applies to `src/server/**`, `src/types/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-JOSE-001** MUST: The system MUST standardize on jose for all cryptographic token operations, including signing, verification, encryption, decryption, and key set resolution across server session and authentication components.

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