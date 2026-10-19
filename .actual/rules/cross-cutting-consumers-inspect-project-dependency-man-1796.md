---
version: 2
name: cross-cutting-consumers-inspect-project-dependency-man-1796
description: "Next.js Server Module Integration for Request and Session Handling: Consumers Inspect Project Dependency Manifest Authoritative"
metadata:
  actual:
    adr_id: 1796ae50-aec3-4833-bd43-e25b26127644
    status: accepted
    candidate_group_id: 13bc1b43-d3a4-4ae2-b129-f923d42b27b8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/**
      - src/utils/**
---

# Next.js Server Module Integration for Request and Session Handling: Consumers Inspect Project Dependency Manifest Authoritative

Scope: applies to `src/server/**`, `src/utils/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-NSM-001** MUST: Consumers MUST inspect the project dependency manifest and authoritative lock artifact to resolve the exact locked version of the framework prior to utilizing server module capabilities.

### Verify

```bash
# Discover and run repository test execution script declared in dependency manifest
# Discover and run project type checker and linter scripts
```

**Accept when:**
- All automated test suites pass without framework compatibility or cookie manipulation errors.
- Static type analysis succeeds with zero type errors across server module entry points.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>