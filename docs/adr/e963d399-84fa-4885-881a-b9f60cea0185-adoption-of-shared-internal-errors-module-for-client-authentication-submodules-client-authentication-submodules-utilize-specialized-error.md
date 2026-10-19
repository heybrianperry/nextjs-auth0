---
version: 2
name: e963d399-84fa-4885-881a-b9f60cea0185-adoption-of-shared-internal-errors-module-for-client-authentication-submodules-client-authentication-submodules-utilize-specialized-error
description: "Adoption of Shared Internal Errors Module for Client Authentication Submodules: Client Authentication Submodules Utilize Specialized Error"
metadata:
  actual:
    adr_id: e963d399-84fa-4885-881a-b9f60cea0185
    status: accepted
    candidate_group_id: 62626e87-6d3f-40ac-af82-3a586d2993b7
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/client/**
---

# Adoption of Shared Internal Errors Module for Client Authentication Submodules: Client Authentication Submodules Utilize Specialized Error

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `src/client/**`

## Context

- Client authentication capabilities span multiple specialized protocols and mechanisms including passkeys, passwordless flows, multi-factor authentication, and token retrieval helpers.
- Each authentication submodule communicates with external endpoints and platform authenticator APIs that produce disparate transport, protocol, and lifecycle errors.
- Decentralized error handling across authentication submodules risks exposing inconsistent error payloads to consumers and complicates failure recovery.
- Static analysis of client authentication implementations reveals consistent dependencies on a shared internal errors module to normalize error types across submodules.

## Problem Statement

Client authentication routines encounter diverse failure conditions across distinct authentication mechanisms, including platform authenticator rejections, network transport errors, session expiration, and challenge invalidation. Without standardized error representations, client submodules risk leaking implementation details, producing inconsistent error structures, and hindering predictable error handling in consuming applications.

## Decision

1. SHOULD: Client authentication submodules SHOULD utilize specialized error types from the internal errors module to differentiate between interactive popup lifecycle aborts, network transport failures, and protocol challenge validation failures.

## Policy Block

- SHOULD Client authentication submodules SHOULD utilize specialized error types from the internal errors module to differentiate between interactive popup lifecycle aborts, network transport failures, and protocol challenge validation failures.

In scope:
- All client-side authentication submodules, challenge verification routines, and token acquisition helper functions.
- Error mapping logic converting transport or platform authenticator responses into consumer-facing errors.

Out of scope:
- Server-side authentication endpoints and backend service boundary error propagation.
- Standard language utility functions that do not interact with authentication workflows or external service boundaries.

Exceptions:
- EXC-001: An external runtime environment or platform credential API requires passing an unmapped native exception directly to the host platform.

## Rationale

- Centralizing error definitions in a dedicated internal errors module guarantees uniform error shapes, codes, and behaviors across disparate authentication mechanisms.
- Standardized error structures decouple consumer error handling logic from underlying network transport and platform credential implementations.
- Static intermediate representation evidence demonstrates high-confidence reuse of the internal errors module across passkey, passwordless, multi-factor, and helper submodules.

## Consequences

Positive:
- Consumers of client authentication modules receive predictable, structured error types with standardized failure classifications.
- Maintenance overhead decreases as error schemas and formatting logic reside in a single authoritative location.
- Platform credential and transport variations are isolated from consuming application logic.

Negative:
- Client submodules incur direct dependency coupling to the shared internal errors module.
- Introducing new error classifications requires coordinated updates within the shared error definitions.

## Alternatives

- Decentralized ad-hoc error throwing using native Error objects in each submodule (rejected)
  Rejected because: Produces inconsistent error structures, lacks unified error classification, and complicates recovery handling for consumers.
  When valid: In isolated scripts or rapid prototypes with no consumer integration contract.
- Adoption of a third-party external error modeling library (rejected)
  Rejected because: Introduces external runtime bundle overhead and additional dependency maintenance when internal domain-specific error structures satisfy all architectural requirements.
  When valid: When enterprise-wide cross-language error serialization frameworks are strictly mandated.

## Risks

- Tightly coupling all authentication submodules to a single internal errors module could cause circular dependencies if errors import domain types improperly.
  Mitigation: Ensure the internal errors module depends solely on foundational types and never imports higher-level client authentication submodules.
  Owner: SDK Engineering Team
- Unmapped external transport or platform errors could be missed during authentication flow additions.
  Mitigation: Enforce comprehensive boundary unit tests simulating transport and platform failures for every authentication workflow.
  Owner: Client Architecture Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Client authentication modules must centralize error mapping at the boundary where external transport or platform authenticator responses are received.
- Consumer applications should inspect standardized error codes exposed by the internal errors module to guide recovery flows and user interface messaging.

## Continuation Context


Verify commands:
- Discover the project test script from the repository dependency manifest and execute the test suite to validate error handling paths across all client authentication modules.
- Discover the project static analysis and linting scripts from the repository build configuration and execute them to verify that module imports adhere to internal module boundaries.
- Discover the project type checking script and execute type validation to confirm that error hierarchies conform to exported interfaces.

Accept when:
- All client authentication test suites execute and pass, confirming proper wrapping and propagation of internal errors.
- Static analysis and type checking complete with zero errors and no boundary violations.
- All thrown errors across client authentication submodules inherit from standard internal error abstractions.

## Enforcement

- Verified by: Automated test suite execution validating that all rejection paths yield instances of the shared internal error classes.
- Verified by: Static analysis import boundary rules verifying that client submodules only import standardized error definitions.
- Verified by: Peer code review during pull request evaluation confirming error propagation standards.
- Violation handling: Build and test pipelines fail if unmapped native errors or unauthorized import paths are introduced.
- Violation handling: Pull requests containing ad-hoc error literals or unhandled raw rejections are blocked until normalized against the internal errors module.
- Exception process: Developers submit an architecture variance request detailing why standard internal error types cannot represent the failure condition.
- Exception process: Variance requests must be reviewed and approved by client architecture maintainers prior to merging.