---
version: 2
name: f21ad8b7-e5fe-48bc-9a31-0d3de6f834f1-adoption-of-pathutils-internal-module-for-client-route-resolution-engineers-discover-project-dependency-manifest-lock
description: "Adoption of pathUtils Internal Module for Client Route Resolution: Engineers Discover Project Dependency Manifest Lock"
metadata:
  actual:
    adr_id: f21ad8b7-e5fe-48bc-9a31-0d3de6f834f1
    status: accepted
    candidate_group_id: a2b468be-d313-45f9-8c06-f88068ede2ec
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - src/client/**
---

# Adoption of pathUtils Internal Module for Client Route Resolution: Engineers Discover Project Dependency Manifest Lock

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `src/client/**`

## Context

- Client authentication features span multiple independent capabilities including session management, passkey registration and verification, passwordless authentication, enterprise federated login, and route protection.
- Each client authentication capability depends on dynamic endpoint paths supplied via client-side environment configurations for login, profile retrieval, session creation, and credential challenges.
- Inconsistent URL formatting, duplicate slashes, or missing leading slashes when concatenating base routes and relative endpoints introduce runtime boundary failures during authentication handshakes.
- The project routes all path normalization and URL construction in client authentication routines through the internal pathUtils module to maintain deterministic endpoint addressing across boundary calls.

## Problem Statement

Client-side authentication workflows require dynamic endpoint resolution based on environment configurations across disparate features such as passkey registration, passwordless authentication, profile retrieval, and route protection. Ad-hoc string concatenation across multiple client modules creates high risks of malformed request paths, inconsistent slash handling, and difficult-to-maintain API contracts, necessitating a single shared utility module to govern client-side route path resolution.

## Decision

1. MUST: Engineers MUST discover the project dependency manifest and lock artifact to verify locked versions of all external dependencies before integrating client module routines.

## Policy Block

- MUST Engineers MUST discover the project dependency manifest and lock artifact to verify locked versions of all external dependencies before integrating client module routines.

In scope:
- Client-side authentication modules, hooks, providers, and navigation helpers that interact with configured route endpoints
- Client network boundary calls that dispatch requests to configured server authentication paths

Out of scope:
- Server-side route handlers executing exclusively within backend execution runtimes
- External third-party redirects pointing to fully qualified external origins outside the local domain configuration

Exceptions:
- EX-20-001: Direct external fully-qualified absolute URLs are provided by external identity providers during federated domain handshakes

## Rationale

- Static analysis confirms eight client authentication files uniformly import and execute pathUtils functions to resolve runtime route configurations.
- Centralizing path resolution in pathUtils isolates edge-case handling for leading slashes, trailing slashes, and parameter serialization to a single tested module.
- Enforcing a single path resolution utility across authentication hooks, passkeys, and providers eliminates duplicate path-parsing logic and reduces bundle footprint.

## Consequences

Positive:
- Ensures uniform, deterministic URL and route formatting across all client-side authentication mechanisms.
- Eliminates duplicate path-handling logic and reduces regression risks when route configuration conventions change.
- Simplifies client-side testing by allowing mock verification of a single path resolution interface.

Negative:
- Couples all client-side authentication features to the internal pathUtils module API contract.
- Requires any updates to path normalization behavior to maintain backward compatibility across multiple calling client workflows.

## Alternatives

- Inline string concatenation within each individual client helper and hook (rejected)
  Rejected because: Causes widespread code duplication, inconsistent delimiter handling, and higher susceptibility to route mismatch defects across disparate authentication flows
  When valid: Single-file prototype implementations with fixed static routes
- Adopting an external third-party URL management library for client path resolution (rejected)
  Rejected because: Introduces unnecessary third-party dependency overhead and bundle weight for straightforward path formatting operations already fulfilled internally
  When valid: Complex routing environments requiring advanced URI template compilation and multi-domain route meshes

## Risks

- Breaking changes in the internal pathUtils module could simultaneously disrupt multiple client authentication workflows
  Mitigation: Maintain comprehensive unit test suites covering the utility module for all route formatting edge cases and verify consuming modules via integration suites
  Owner: Engineering Team
- Developers bypassing the utility module and using manual string interpolation in newly created client helpers
  Mitigation: Enforce automated static analysis and peer review checks that flag direct path string manipulation in client authentication files
  Owner: Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Consuming client modules must import the shared path resolution functions from the internal utility module and pass configured route tokens as input parameters.
- When adding support for new authentication endpoints, verify that the path utility correctly handles optional query parameters and anchor fragments without manual string splitting.

## Continuation Context


Verify commands:
- Discover and run the project's static analysis and linting scripts to verify compliance with internal module import conventions across client files.
- Discover and run the project's test execution script to validate that all path resolution unit tests and client integration tests pass.

Accept when:
- Static analysis passes with zero violations regarding path resolution utility usage in client modules.
- All unit and integration test suites covering client authentication flows execute successfully.

## Enforcement

- Verified by: Automated continuous integration pipeline execution checking code style, import boundaries, and test assertions
- Verified by: Peer review gating on pull requests modifying or adding client authentication logic
- Violation handling: Pull requests containing inline string concatenation for routes or failing verification scripts must be blocked from merging until corrected.
- Exception process: Exceptions must be submitted via an architecture review request detailing the specific technical rationale for bypassing the utility module, subject to lead architect approval.