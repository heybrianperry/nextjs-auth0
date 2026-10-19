---
version: 2
name: 80f00949-794c-4822-9627-087415e81192-adopt-oauth4webapi-for-oauth-2-0-and-dpop-client-protocol-management-server-side-request-fetchers-wrap-standard
description: "Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Server Side Request Fetchers Wrap Standard"
metadata:
  actual:
    adr_id: 80f00949-794c-4822-9627-087415e81192
    status: accepted
    candidate_group_id: 918731ad-5f52-4610-aa8b-fdb972929680
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/lib/**
      - src/server/**
      - src/utils/**
---

# Adopt oauth4webapi for OAuth 2.0 and DPoP Client Protocol Management: Server Side Request Fetchers Wrap Standard

Status: proposed
Date: 2025-02-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-dpop/lib/**`
- `src/server/**`
- `src/utils/**`

## Context

- Authentication and authorization subsystems require standards-compliant client interactions with OAuth 2.0 and OpenID Connect authorization servers.
- Hardening token security necessitates cryptographic proof-of-possession mechanisms to mitigate token interception and replay threats.
- Consistent caching of authorization server discovery documents and cryptographic key sets prevents latency spikes and avoids rate-limiting during high request volumes.
- Disparate, bespoke HTTP client implementations for token exchanges introduce security risks and maintenance overhead across server modules.

## Problem Statement

Managing OAuth 2.0 and OpenID Connect token lifecycles across distributed server components without a unified, standards-compliant client library leads to duplicated protocol logic, improper validation of cryptographic tokens, and inconsistent implementations of security extensions such as Demonstrating Proof-of-Possession. A centralized architectural standard is necessary to govern authorization client operations, metadata discovery caching, and secure token requests.

## Decision

1. SHOULD: Server-side request fetchers SHOULD wrap standard HTTP abstractions and propagate response header validations in conformity with oauth4webapi response processing expectations.

## Policy Block

- SHOULD Server-side request fetchers SHOULD wrap standard HTTP abstractions and propagate response header validations in conformity with oauth4webapi response processing expectations.

In scope:
- All server-side modules performing OAuth 2.0 or OpenID Connect token requests, token refreshes, and discovery operations.
- Client integration layers that negotiate Demonstrating Proof-of-Possession with compliant authorization servers and resource servers.

Out of scope:
- Direct browser-only authentication flows that do not traverse server-side token handling boundaries.
- Internal microservice-to-microservice mutual TLS communication channels that do not utilize OAuth bearer or proof-of-possession tokens.

Exceptions:
- EXC-20-001: A third-party upstream identity provider requires non-standard legacy protocol extensions unsupported by standards-compliant client libraries.

## Rationale

- Evidence across server fetching, retry handling, and discovery caches demonstrates consistent reliance on oauth4webapi for protocol compliance.
- Standardizing on a web-standards-compliant client library ensures compatibility with modern Fetch and Headers interfaces while enforcing strict protocol validations.
- Encapsulating Demonstrating Proof-of-Possession and discovery caching within disciplined module boundaries minimizes protocol vulnerabilities and prevents token replay attacks.

## Consequences

Positive:
- Provides rigorous adherence to OAuth 2.0, OpenID Connect, and cryptographic proof-of-possession standards.
- Eliminates redundant HTTP implementations for token exchange and discovery handling.
- Reduces latency and upstream load through synchronized caching of authorization server metadata.

Negative:
- Requires developers to adhere strictly to standards-based protocol semantics rather than ad-hoc HTTP configurations.
- Increases operational complexity when handling cryptographic key pairs and nonce rotation retries for proof-of-possession tokens.

## Alternatives

- Implement custom HTTP client functions for token exchange and discovery parsing. (rejected)
  Rejected because: Bespoke protocol implementations increase vulnerability to security regressions, signature verification oversights, and maintenance debt.
  When valid: Only when interacting with legacy proprietary systems that violate standard specifications.
- Adopt monolithic identity provider SDKs tightly coupled to specific vendor endpoints across all modules. (rejected)
  Rejected because: Tightly couples server-side architecture to single-vendor abstractions, reducing portability across diverse OAuth providers.
  When valid: When an application strictly relies on an exclusive proprietary identity platform with no multi-provider requirements.

## Risks

- Failure to properly handle authorization server nonce rotation during proof-of-possession requests may cause dropped authentication requests.
  Mitigation: Enforce automated retry routines that capture server-provided challenge nonces and regenerate proof tokens seamlessly.
  Owner: Security engineering team
- Stale or uncoordinated discovery caching could lead to authentication failures during authorization server key rotations.
  Mitigation: Implement cache eviction strategies and in-flight request deduplication on discovery endpoints.
  Owner: Backend platform team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Ensure server-side fetch wrappers properly instantiate standard Headers collections and adhere to HTTP status expectations when passing responses to oauth4webapi parsers.
- Maintain discovery metadata and cryptographic key set caches with time-to-live expiration and concurrent request coalescing to protect upstream identity endpoints.

## Continuation Context


Verify commands:
- Discover the repository build and validation scripts from the project manifest, and execute the static analysis suite to verify library import boundaries.
- Discover and run the project test automation suite to validate OAuth discovery caching and proof-of-possession retry flows.

Accept when:
- Static analysis validates that all server-side OAuth protocol exchanges route through oauth4webapi without unauthorized bespoke client wrappers.
- Automated test suites confirm successful authorization server discovery, key caching, and proof-of-possession retry handling under simulated nonce rotation.

## Enforcement

- Verified by: Automated continuous integration checks inspecting dependency imports and protocol handler implementations.
- Verified by: Peer code reviews conducted by security and platform engineers on authentication modules.
- Violation handling: Pull requests introducing manual OAuth token requests or bypassing discovery caching will be blocked until refactored to use standard library abstractions.
- Exception process: Exceptions must be submitted via an architecture review request detailing provider non-compliance and reviewed by the security team.