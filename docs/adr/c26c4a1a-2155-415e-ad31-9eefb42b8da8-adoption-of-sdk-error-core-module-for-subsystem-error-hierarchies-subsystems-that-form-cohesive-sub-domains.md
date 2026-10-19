---
version: 2
name: c26c4a1a-2155-415e-ad31-9eefb42b8da8-adoption-of-sdk-error-core-module-for-subsystem-error-hierarchies-subsystems-that-form-cohesive-sub-domains
description: "Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Subsystems That Form Cohesive Sub Domains"
metadata:
  actual:
    adr_id: c26c4a1a-2155-415e-ad31-9eefb42b8da8
    status: accepted
    candidate_group_id: 33495c33-7d8f-4435-9cd6-09c297f16d44
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/errors/**
---

# Adoption of sdk-error Core Module for Subsystem Error Hierarchies: Subsystems That Form Cohesive Sub Domains

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `src/errors/**`

## Context

- Multiple functional subsystems within the SDK require domain-specific error classifications to represent distinct protocol and operational failure states.
- Without a shared foundation, independent error classes risk inconsistent metadata structures, incompatible serialization formats, and fragmented consumer catch blocks.
- Static analysis identifies consistent specialization of the sdk-error core module across eleven discrete subsystem error modules.

## Problem Statement

The SDK encompasses multiple functional domains, each requiring specialized error reporting for authentication, session management, and cryptographic workflows. Without a standardized base error module, subsystems risk defining fragmented error structures that force consuming applications to implement disparate error handling logic, breaking architectural consistency across the SDK boundary.

## Decision

1. MAY: Subsystems that form cohesive sub-domains MAY establish intermediate error abstractions between their domain errors and the sdk-error module.

## Policy Block

- MAY Subsystems that form cohesive sub-domains MAY establish intermediate error abstractions between their domain errors and the sdk-error module.

In scope:
- All error definitions and exception classes across SDK functional domains and protocol subsystems.
- New subsystem modules introducing failure classifications or diagnostic error payloads.

Out of scope:
- Third-party library integration wrappers that do not surface exceptions across the SDK public interface.
- Development-time assertions and internal invariant checks that never escape to consumers.

## Rationale

- The sdk-error core module establishes a uniform interface contract for diagnostic metadata, error codes, and serialization across the SDK.
- Specializing domain errors from a central base module enables external consumers to catch a single root error type while discriminating specific failure conditions.
- Modular domain-level error declarations preserve subsystem encapsulation while maintaining ecosystem-wide consistency.

## Consequences

Positive:
- External SDK consumers can rely on a consistent error hierarchy and unified error catching semantics.
- Subsystem domain errors maintain semantic isolation while sharing common contextual fields and serialization logic.
- Static analysis can reliably trace and audit error dispatching across all functional domains.

Negative:
- All domain error modules retain a direct architectural dependency on the sdk-error core module.
- Changes to the foundational error class contract require coordinated testing across all dependent subsystems.

## Alternatives

- Standalone native error classes per subsystem without a shared core module (rejected)
  Rejected because: Creating disconnected root errors prevents client applications from catching all SDK-generated exceptions under a unified hierarchy, complicating error handling and telemetry.
  When valid: Valid only in decoupled polyglot microservices where each service maintains an independent runtime contract.
- Single monolithic error enumeration module defining all error codes and messages (rejected)
  Rejected because: Centralizing all subsystem error definitions into a single module degrades modularity and increases merge contention across feature teams.
  When valid: Valid in minimal utilities with a small and static set of failure conditions.

## Risks

- Tight coupling to the base error module interface could make foundational changes breaking across all subsystems.
  Mitigation: Keep the base error interface minimal, stable, and focused on universal diagnostic attributes.
  Owner: SDK Core Team
- Subsystem developers might introduce intermediate error layers that obscure root causes.
  Mitigation: Provide clear documentation and test fixtures demonstrating compliant error derivation.
  Owner: SDK Core Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Domain error classes should pass domain-specific identifiers and descriptive messages up to the superclass constructor defined in the sdk-error module.
- Ensure that custom error properties preserve standard error stack traces and support structured serialization.

## Continuation Context


Verify commands:
- Discover the project test execution script from the repository manifest and run the test suite to verify error inheritance compliance.
- Discover and run the project static analysis and linting verification scripts to ensure all domain error definitions import from the sdk-error module without cycles.

Accept when:
- All domain error modules specialize the base error types exported by the sdk-error module.
- The discovered verification test suite passes with zero uncaught or unclassified error exceptions across all subsystems.

## Enforcement

- Verified by: Continuous integration automated test pipeline runs
- Verified by: Peer code review during pull request evaluation
- Verified by: Automated static analysis rules enforcing import boundaries
- Violation handling: Pull requests introducing root error classes that bypass the sdk-error module are blocked from merging.
- Violation handling: Non-compliant error instantiations must be refactored to extend the sdk-error base hierarchy.
- Exception process: Exceptions require formal architectural review and approval by the principal engineering team.
- Exception process: Approved deviations must document why the sdk-error module cannot accommodate the domain failure mode.