---
version: 2
name: 7e3567a9-1f8f-4816-9330-584702aba008-oauth4webapi-for-demonstrating-proof-of-possession-token-binding-protected-endpoints-validating-demonstrating-proof-possession
description: "oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Protected Endpoints Validating Demonstrating Proof Possession"
metadata:
  actual:
    adr_id: 7e3567a9-1f8f-4816-9330-584702aba008
    status: accepted
    candidate_group_id: c1c1a0d0-6255-4ae6-aff0-e4c2f82dfbcc
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# oauth4webapi for Demonstrating Proof-of-Possession Token Binding: Protected Endpoints Validating Demonstrating Proof Possession

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-dpop/**`

## Context

- Traditional bearer tokens permit any party in possession of the credential string to access protected application programming interfaces without proving ownership of the client entity.
- Sender-constrained security architectures mitigate credential interception by binding access tokens cryptographically to client-managed asymmetric cryptographic keys.
- The oauth4webapi library provides protocol compliance and validation primitives for sender-constrained token flows, specifically Demonstrating Proof-of-Possession mechanisms.
- Heterogeneous endpoint environments necessitate distinguishing between bound tokens bearing cryptographic confirmation claims and standard bearer tokens during phased security transitions.

## Problem Statement

API endpoints serving sensitive application resources face security risks when relying solely on bearer token authorization, as exfiltrated or intercepted credentials can be replayed by unauthorized actors without detection. The architecture requires a reliable mechanism to bind access tokens cryptographically to client key pairs using Demonstrating Proof-of-Possession specifications, verify confirmation claims upon token presentation, and isolate legacy bearer token consumers from sender-constrained enforcement.

## Decision

1. MUST: Protected endpoints validating Demonstrating Proof-of-Possession tokens MUST verify the cryptographic confirmation claim within token claims and reject requests where token binding validation fails.

## Policy Block

- MUST Protected endpoints validating Demonstrating Proof-of-Possession tokens MUST verify the cryptographic confirmation claim within token claims and reject requests where token binding validation fails.

In scope:
- Client authentication client modules requesting sender-constrained tokens
- API server middleware and route handlers validating inbound access tokens

Out of scope:
- Public unauthenticated endpoints not requiring access token verification
- Legacy endpoints explicitly designated for backward-compatible bearer token authorization

Exceptions:
- EXC-43-001: Legacy client applications cannot generate cryptographic proof key pairs

## Rationale

- Adopting oauth4webapi establishes standardized Demonstrating Proof-of-Possession validation, eliminating custom cryptographic implementations and ensuring RFC-compliant confirmation claim verification.
- Sender-constrained tokens mitigate token theft and replay vulnerabilities by requiring proof-of-possession signatures matching the embedded confirmation claim.
- Structured diagnostic recording of token binding attributes enables transparent auditing and monitoring of proof validation across service boundaries.

## Consequences

Positive:
- Substantially reduces token exfiltration and replay attack vectors through cryptographic sender constraints.
- Standardizes token confirmation claim verification across client authentication and server endpoints via oauth4webapi.
- Provides structured request-level diagnostic instrumentation for token binding validation and confirmation status.

Negative:
- Increases computational latency on inbound requests due to cryptographic proof validation and signature verification.
- Requires key pair generation and management on client platforms interacting with protected endpoints.
- Introduces architectural complexity in maintaining dual-path support for legacy bearer and sender-constrained consumers.

## Alternatives

- Standard Bearer Tokens without Sender Constraints (rejected)
  Rejected because: Bearer tokens are susceptible to theft and replay across network hops and client environments without cryptographic sender verification.
  When valid: Valid only for low-risk non-sensitive APIs where cryptographic overhead is unacceptable and tokens have short expiration windows.
- Mutual TLS Client Certificate-Bound Access Tokens (rejected)
  Rejected because: Mutual TLS token binding requires complex transport layer certificate infrastructure and is often unsupported in browser or serverless runtimes.
  When valid: Valid in strictly controlled enterprise service-to-service backhaul networks with established public key infrastructure.

## Risks

- Misconfiguration of client key pairs or clock skew leading to false-positive proof validation rejections
  Mitigation: Implement clock skew tolerance in token proof verification and provide structured diagnostic error reporting on validation failures
  Owner: Security Engineering
- Performance degradation under high throughput due to asymmetric cryptographic signature verification
  Mitigation: Cache verified public keys and authorization server metadata while isolating rate limiting controls prior to token validation
  Owner: Platform Engineering

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Configure token validation middleware to attach confirmation claim diagnostics to the incoming request object prior to reaching business route handlers.
- Ensure fallback configurations are available when authorization server metadata discovery fails, while emitting appropriate diagnostic warnings.

## Continuation Context


Verify commands:
- # Discover and run the project test suite verifying proof-of-possession token validation
- # Discover and run repository static analysis for secrets handling and token binding compliance

Accept when:
- Token validation test suite successfully confirms valid DPoP proof tokens and confirmation claims
- Requests with invalid, expired, or missing proof signatures are rejected with appropriate error diagnostics
- No unauthorized token fallback or bypassed confirmation checks are detected during automated verification

## Enforcement

- Verified by: Continuous integration test pipelines executing automated token validation suites
- Verified by: Static analysis checks identifying token handling and cryptographic claim validation patterns
- Verified by: Architecture review for any modifications to authentication middleware and route handlers
- Violation handling: Pull requests lacking required token binding validation or test coverage must be blocked from merging
- Violation handling: Non-compliant endpoints deployed without sender-constraint enforcement will trigger security alerts and rollback
- Exception process: Submit an architectural exception request detailing technical barriers to sender-constrained token implementation
- Exception process: Secure formal approval from the Security Architecture Team and record exception expiration date in the central registry