---
version: 2
name: 16930089-f8d9-461e-b743-bbf68fbacb64-express-http-middleware-pipeline-architecture-middleware-registrations-express-application-instance-precede
description: "Express HTTP Middleware Pipeline Architecture: Middleware Registrations Express Application Instance Precede"
metadata:
  actual:
    adr_id: 16930089-f8d9-461e-b743-bbf68fbacb64
    status: accepted
    candidate_group_id: 9bb84435-f3dc-4714-8a47-97e99459c951
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express HTTP Middleware Pipeline Architecture: Middleware Registrations Express Application Instance Precede

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-dpop/**`

## Context

- The codebase contains HTTP service ingress endpoints requiring standardized boundary handling for incoming requests.
- Security headers, cross-origin resource sharing, request body parsing, and telemetry need centralized execution before business route dispatch.
- The evidence demonstrates Express middleware chaining via app.use within an isolated example boundary.

## Problem Statement

Without a unified HTTP boundary middleware architecture, incoming network requests risk bypassing critical security headers, payload parsing, and logging controls, leading to inconsistent security enforcement and duplicated boundary handling across routes.

## Decision

1. MUST: Middleware registrations on the Express application instance MUST precede all route definitions to guarantee uniform inspection of incoming requests.

## Policy Block

- MUST Middleware registrations on the Express application instance MUST precede all route definitions to guarantee uniform inspection of incoming requests.

In scope:
- HTTP API service ingress definitions using Express.
- Boundary middleware registration pipelines.

Out of scope:
- Non-HTTP background workers and queue consumers.
- Internal utility functions operating outside request dispatch lifecycles.

## Rationale

- Sequential middleware registration through app.use establishes a predictable order of execution for ingress request filtering and enrichment.
- Centralizing cross-cutting policies at the boundary level isolates domain route handlers from transport and security concerns.
- Direct integration of standard Express middleware primitives provides lightweight boundary enforcement without custom interception layers.

## Consequences

Positive:
- Guarantees consistent execution of security headers, cross-origin resource sharing policies, and request parsing across downstream routes.
- Decouples transport-level hygiene and observation logic from individual route controllers.
- Provides a standard lifecycle hook for attaching request diagnostics and authentication metadata.

Negative:
- Introduces strict execution order sensitivity where incorrect registration sequence can cause unparsed bodies or bypassed security controls.
- Applies global middleware processing overhead across every request hitting the application instance.

## Alternatives

- Per-Route Middleware Declaration (rejected)
  Rejected because: Declaring middleware individually per route leads to configuration drift, duplicated declarations, and risk of omitting boundary security controls.
  When valid: Valid when specific endpoints require bespoke, non-standard authorization policies distinct from common service boundaries.
- Reverse Proxy Boundary Delegation (rejected)
  Rejected because: Delegating security headers and payload filtering entirely to an upstream reverse proxy obscures application-level diagnostics and complicates standalone execution.
  When valid: Valid in environments where edge infrastructure standardizes all ingress security headers centrally across multi-service deployments.

## Risks

- Misconfigured middleware execution order can cause silent failures or unhandled request bodies.
  Mitigation: Establish standardized middleware initialization sequences validated by automated integration test suites.
  Owner: Backend Engineering Team
- Scope is observed in only a single example file, creating risk of over-specifying architecture from non-production code.
  Mitigation: Treat this record as proposed with low confidence until adopted across primary production service boundaries.
  Owner: Architecture Review Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Register telemetry and logging middleware immediately after instantiating the Express application to capture full request latency.
- Ensure body parsing middleware precedes any route handler or custom middleware that inspects request payload data.

## Continuation Context


Verify commands:
- Discover and run the repository build validation and lint scripts to verify middleware chaining syntax.
- Execute the project automated integration test suite to verify that middleware handles boundary ingress correctly.

Accept when:
- All HTTP ingress routes process requests through the registered middleware pipeline without uncaught exceptions.
- Automated test suites confirm that security headers and cross-origin resource sharing headers are present on HTTP responses.

## Enforcement

- Verified by: Continuous integration test execution and automated boundary route verification.
- Verified by: Peer code review verifying middleware registration ordering.
- Violation handling: Pull requests registering routes prior to required security middleware will be blocked.
- Violation handling: Unvalidated middleware configurations must be corrected before deployment.
- Exception process: Submit an architectural review request with justification for route-specific middleware deviations.