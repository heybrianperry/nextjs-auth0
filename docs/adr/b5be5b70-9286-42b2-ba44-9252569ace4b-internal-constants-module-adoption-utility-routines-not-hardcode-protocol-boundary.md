---
version: 2
name: b5be5b70-9286-42b2-ba44-9252569ace4b-internal-constants-module-adoption-utility-routines-not-hardcode-protocol-boundary
description: "Internal Constants Module Adoption: Utility Routines Not Hardcode Protocol Boundary"
metadata:
  actual:
    adr_id: b5be5b70-9286-42b2-ba44-9252569ace4b
    status: accepted
    candidate_group_id: b7d058aa-d221-4496-8376-bc96a764140f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/utils/**
---

# Internal Constants Module Adoption: Utility Routines Not Hardcode Protocol Boundary

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `src/utils/**`

## Context

- Multiple utility helper modules across the codebase require standardized operational thresholds, protocol tolerances, and error definitions.
- Scattering configuration constants and protocol boundaries across discrete utility files creates drift risk and undermines security guarantees.
- Centralizing shared operational definitions into a dedicated internal constants module establishes a single source of truth for runtime boundaries and fallback behaviors.

## Problem Statement

Inconsistent declaration of operational thresholds and protocol boundaries across disparate utility modules introduces maintenance overhead, risks configuration drift, and complicates security audits. Without a centralized constants module, runtime validation limits and fallback behaviors become fragmented across independent helper implementations.

## Decision

1. MUST_NOT: Utility routines MUST NOT hardcode protocol boundary values, timeout durations, or security limits within local module scopes.

## Policy Block

- MUST_NOT Utility routines MUST NOT hardcode protocol boundary values, timeout durations, or security limits within local module scopes.

In scope:
- Utility helper modules defining operational parameters, security thresholds, and configuration defaults.
- Authentication and protocol verification routines requiring standardized boundary values.

Out of scope:
- Dynamic user-configured runtime values retrieved from remote management services.
- Test mock fixtures and synthetic test assertions requiring arbitrary boundary values.

## Rationale

- Evidence demonstrates that utility helpers across the repository consistently import from a shared internal constants module alongside domain-specific error and type definitions.
- Centralizing boundary thresholds ensures uniform enforcement of security parameters across runtime environments.
- Maintaining constants in a dedicated internal module decouples operational thresholds from functional execution logic, simplifying reviews and updates.

## Consequences

Positive:
- Guarantees consistent operational thresholds and protocol tolerances across all utility modules.
- Eliminates duplicate magic literals and simplifies codebase-wide threshold tuning.
- Centralizes validation logic for runtime overrides and security boundary enforcement.

Negative:
- Creates a centralized internal module dependency that requires disciplined maintenance to prevent circular references.
- Modifications to shared constant definitions require regression verification across all consuming utility modules.

## Alternatives

- Decentralized inline literal values in individual utility modules (rejected)
  Rejected because: Leads to drift in security thresholds, duplicated magic values, and divergent protocol behavior across helper routines.
  When valid: One-off prototype scripts with no shared architectural lifecycle.
- External dynamic configuration service for all operational constants (rejected)
  Rejected because: Introduces unnecessary network latency and availability dependencies for static algorithmic and protocol boundary thresholds.
  When valid: Frequently modified feature flags and runtime tenant settings managed outside deployment cycles.

## Risks

- Central constants module may become a high-churn bottleneck as multiple utility domains expand.
  Mitigation: Group constants by functional domain within the module and enforce strict code review standards for boundary modifications.
  Owner: Core Engineering Team
- Permissive runtime environment overrides could inadvertently exceed recommended security thresholds.
  Mitigation: Implement programmatic clamping and warning logs when parsed environment overrides exceed maximum safe bounds.
  Owner: Security Architecture Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Organize internal constant declarations into cohesive domain groupings, ensuring export interfaces remain immutable.
- Pair threshold constants with validation helper functions to ensure runtime environment overrides never silently exceed safe boundaries.

## Continuation Context


Verify commands:
- Discover the project verification script from the root configuration manifest and execute the test suite to validate utility module compliance.
- Execute the repository linter script identified in the build configuration to check for prohibited literal constants and enforce centralized imports.
- Inspect the project lock resolution artifact to confirm all external dependencies match the expected resolved versions.

Accept when:
- All utility helper modules source operational thresholds and parameters exclusively from the designated constants module with zero unresolved literal violations.
- Automated test suites pass across all supported runtime environments, confirming proper fallback behavior when cryptographic capabilities are restricted.
- Static analysis checks confirm no hardcoded boundary values exist across utility implementations.

## Enforcement

- Verified by: Automated static analysis validating that utility modules import constants from the centralized module.
- Verified by: Continuous integration test pipelines executing protocol verification suites across supported runtime environments.
- Verified by: Peer code review for pull requests modifying shared constant definitions or security thresholds.
- Violation handling: Pull requests containing inline magic literals or unapproved constant declarations are rejected during continuous integration.
- Violation handling: Violations identified during code review require refactoring to import from the centralized constants module prior to approval.
- Exception process: Submit an architectural review request with justification detailing why a specific literal cannot be shared through the centralized constants module.
- Exception process: Obtain explicit approval from the security architecture team before merging localized threshold overrides.