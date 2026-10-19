---
version: 2
name: cross-cutting-components-within-scope-session-manageme-f130
description: "jose Adoption for Cryptographic Operations and Token Management: Components Within Scope Session Management Authentication"
metadata:
  actual:
    adr_id: f1309c1d-023f-43bf-8b32-e0be0ff560c8
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

# jose Adoption for Cryptographic Operations and Token Management: Components Within Scope Session Management Authentication

Scope: applies to `src/server/**`, `src/types/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-JOSE-001** MUST_NOT: Components within the scope of session management and authentication MUST NOT introduce alternative cryptographic token libraries for operations supported by the primary library.
- **R-JOSE-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-JOSE-003** MANDATORY: Before writing code that uses a versioned library, execute in order the lock-version grounding steps: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps per dependency at point of use.

### Verify

```bash
echo "Discover and execute project test suite for cryptographic and session verification"
echo "Discover and execute project linter and dependency checks for unauthorized cryptographic libraries"
```

**Accept when:**
- All cryptographic signing, encryption, decryption, and verification operations compile and pass automated test suites using the standardized token library.
- No unapproved third-party or platform-specific cryptographic token libraries are referenced in session or authentication workflows.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated code quality and dependency compliance checks in continuous integration pipelines enforce these requirements.
</enforcement>