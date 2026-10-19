---
version: 2
name: 7585d7f2-511f-4c02-b95f-06d15ab5a90b-abstract-session-store-internal-module-consumers-inspect-repository-dependency-manifest-lock
description: "abstract-session-store Internal Module: Consumers Inspect Repository Dependency Manifest Lock"
metadata:
  actual:
    adr_id: 7585d7f2-511f-4c02-b95f-06d15ab5a90b
    status: accepted
    candidate_group_id: c6c0b49c-264f-4527-9db3-63e25d949e1e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/server/session/**
---

# abstract-session-store Internal Module: Consumers Inspect Repository Dependency Manifest Lock

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `src/server/session/**`

## Context

- Server session management requires consistent handling of session rolling, cookie lifecycle management, and session payload normalization across varied deployment environments.
- Storage demands diverge between stateless encrypted token persistence in client cookies and stateful persistence backed by an external data store.
- Cookie-based stateless storage introduces header size overflow risks when token payloads expand, necessitating threshold detection and fallback guidance.
- The codebase establishes an abstract session store hierarchy to standardize lifecycle hooks such as session rolling while supporting pluggable concrete persistence implementations.

## Problem Statement

Session management mechanisms often diverge when supporting both stateless cookie-based sessions and stateful server-backed sessions, leading to fragmented lifecycle handling, inconsistent rolling logic, and unmonitored cookie growth that causes header size overflow errors on upstream proxies and content delivery networks.

## Decision

1. MUST: Consumers MUST inspect the repository dependency manifest and lock resolution artifacts to lock the exact version of any external cryptographic or server dependencies prior to implementation.

## Policy Block

- MUST Consumers MUST inspect the repository dependency manifest and lock resolution artifacts to lock the exact version of any external cryptographic or server dependencies prior to implementation.

In scope:
- All server-side session management implementations, including stateless encrypted cookie adapters and stateful data store adapters.
- Authentication middleware and request handlers managing session lifecycle, rolling, or cookie dispatch.

Out of scope:
- Client-side state management that does not interact with server session cookies or tokens.
- Static assets or public endpoints that do not process session authentication state.

## Rationale

- Centralizing session lifecycle logic in the abstract-session-store module ensures that security-critical behaviors like session rolling hooks and session normalization remain consistent across all persistence mechanisms.
- Separating the abstract store interface from stateless and stateful implementations allows applications to switch or support both storage strategies without altering authentication consumers.
- Incorporating payload size threshold checks into stateless session handling directly addresses upstream proxy and gateway header limits, preventing unexpected request failures.

## Consequences

Positive:
- Standardized session lifecycle and rolling behavior across diverse session storage implementations.
- Decoupled storage backend logic that permits independent migration between stateless cookies and stateful databases.
- Early detection of session cookie payload bloat prior to triggering header overflow errors in network infrastructure.

Negative:
- Additional abstraction overhead requiring all concrete stores to conform to the base lifecycle interface.
- Dual implementation maintenance requiring parallel testing for both stateless encryption and stateful database storage.

## Alternatives

- Direct unabstracted session handlers per storage type (rejected)
  Rejected because: Leads to fragmented session rolling logic, inconsistent cookie configuration, and duplicate normalization code across storage strategies.
  When valid: Only viable in single-strategy prototypes with no requirement for session rolling or cookie size governance.
- Mandatory stateful session storage exclusively (rejected)
  Rejected because: Requires all deployment environments to provision and maintain a centralized session database, eliminating lightweight stateless deployment options.
  When valid: Applicable when architectural requirements strictly forbid sensitive tokens on the client.

## Risks

- Stateless session cookie payload exceeds network gateway header limits causing request drops.
  Mitigation: Enforce cookie size calculation and automated warning logs recommending token claim reduction or migration to stateful storage.
  Owner: engineering team
- Failure in beforeSessionRolled lifecycle hook blocking valid user requests.
  Mitigation: Enforce fallback behavior in the abstract session store to proceed with session rolling upon hook failure while logging a warning.
  Owner: engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- When extending the abstract session store for stateless operation, configure encrypted cookie serialization and verify that total header size stays safely beneath network proxy limits.
- When extending the abstract session store for stateful operation, map store operations to a persistent cache or database while maintaining session identifier cookies.

## Continuation Context


Verify commands:
- Discover and run the project test suite verifying session store implementations against the abstract session store contract.
- Discover and run the lint and type-check scripts across server session modules to confirm compliance with session interface definitions.

Accept when:
- All unit and integration tests for stateless and stateful session stores pass without errors.
- Session rolling hooks execute correctly and default to rolling upon hook failure.
- Cookie size threshold warnings trigger when session payloads exceed configured byte limits.

## Enforcement

- Verified by: Automated continuous integration test suites covering session store lifecycle scenarios.
- Verified by: Peer code review verifying adherence to the abstract session store contract.
- Violation handling: Pull requests containing unabstracted session access or direct cookie manipulation will be rejected during review.
- Violation handling: Static analysis and test failures in session modules will block deployment pipelines.
- Exception process: Exceptions require documented architectural review and sign-off by the platform engineering team.