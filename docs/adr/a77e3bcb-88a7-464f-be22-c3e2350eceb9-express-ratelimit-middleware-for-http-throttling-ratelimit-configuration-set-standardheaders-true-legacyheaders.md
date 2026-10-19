---
version: 2
name: a77e3bcb-88a7-464f-be22-c3e2350eceb9-express-ratelimit-middleware-for-http-throttling-ratelimit-configuration-set-standardheaders-true-legacyheaders
description: "Express rateLimit Middleware for HTTP Throttling: Ratelimit Configuration Set Standardheaders True Legacyheaders"
metadata:
  actual:
    adr_id: a77e3bcb-88a7-464f-be22-c3e2350eceb9
    status: accepted
    candidate_group_id: 6c224766-e92a-4e60-96d6-678c2cffb625
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express rateLimit Middleware for HTTP Throttling: Ratelimit Configuration Set Standardheaders True Legacyheaders

Status: proposed
Date: 2025-02-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-dpop/**`

## Context

- Incoming HTTP endpoints require throttling mechanisms to prevent request exhaustion and protect upstream service resources from abusive traffic.
- The application pipeline incorporates middleware chaining to process inbound requests prior to routing execution.
- Public API routes must communicate rate limiting quotas to clients using standardized response headers rather than non-standard legacy headers.
- The current codebase configures IP-based windowed request quotas directly within the primary service routing initialization layer.

## Problem Statement

Unprotected HTTP API endpoints are vulnerable to request flooding and resource depletion from unconstrained clients. The service requires an explicit middleware-based throttling boundary that intercepts inbound requests, tracks per-client quota consumption across a defined time window, rejects excess traffic with standard error payloads, and exposes quota metadata via standardized HTTP response headers.

## Decision

1. MUST: The rateLimit configuration MUST set standardHeaders to true and legacyHeaders to false to emit standardized rate limit metadata headers in HTTP responses.

## Policy Block

- MUST The rateLimit configuration MUST set standardHeaders to true and legacyHeaders to false to emit standardized rate limit metadata headers in HTTP responses.

In scope:
- Inbound HTTP request routing pipelines exposing application endpoints.
- Public API routes subject to abuse prevention and client traffic throttling.

Out of scope:
- Background asynchronous worker processes and scheduled batch jobs.
- Direct inter-process communications over local UNIX sockets.

Exceptions:
- EXC-41-001: A dedicated upstream reverse proxy, API gateway, or cloud edge provider enforces equivalent or stricter rate limiting prior to routing requests to the application service.

## Rationale

- Configuring rateLimit directly in the express middleware pipeline establishes an immediate, code-level line of defense against excessive request volume.
- Enabling standardHeaders while disabling legacyHeaders conforms HTTP responses to modern rate limiting specifications, providing clear quota visibility to API consumers.
- Defining explicit windowMs and max thresholds prevents unbounded CPU and memory consumption by throttling burst traffic at the network edge of the application.

## Consequences

Positive:
- Prevents resource starvation and denial-of-service degradation on public HTTP routes by bounding inbound request throughput per client IP.
- Provides transparent quota tracking and reset indicators to API clients via standardized HTTP response headers.
- Operates as lightweight middleware within the existing request processing pipeline without requiring external infrastructure for single-instance deployments.

Negative:
- Default in-memory state tracking does not synchronize across horizontally scaled multi-instance deployments without a distributed storage adapter.
- IP-based throttling may inadvertently restrict multiple distinct users sharing a common corporate network gateway or proxy IP address.

## Alternatives

- Delegating all rate limiting exclusively to an external API gateway or cloud edge network. (rejected)
  Rejected because: Relying solely on external network infrastructure leaves standalone or locally tested service instances unprotected against traffic floods during development and direct-access deployment topologies.
  When valid: Valid when all service instances are strictly isolated within a private virtual network behind a managed enterprise gateway that handles all client ingress.
- Custom token-bucket middleware implemented with application-level timers and dictionaries. (rejected)
  Rejected because: Custom in-house rate limiting implementations incur maintenance overhead and risk edge-case concurrency defects compared to established middleware modules.
  When valid: Valid when specialized domain-specific throttling rules require custom business logic not supported by standard middleware options.

## Risks

- In-memory rate limit counters reset upon process restart and do not aggregate across multiple application replicas.
  Mitigation: Evaluate and configure an external distributed cache store adapter for rate limiting when scaling beyond a single application process.
  Owner: Platform Engineering
- Legitimate users behind shared network address translation gateways may experience unexpected 429 rejections during peak usage.
  Mitigation: Monitor quota consumption metrics and adjust max request limits or incorporate authenticated client identifiers for quota tracking.
  Owner: Application Engineering

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Mount the rateLimit middleware early in the express middleware execution chain prior to costly authentication, JSON body parsing, or database querying operations.
- Ensure proxy trust settings are appropriately configured on the express instance so client IP addresses are accurately extracted from proxy forwarding headers.

## Continuation Context


Verify commands:
- Discover the project test execution runner from the manifest and run automated integration test suites validating rate limit response codes and headers.
- Execute automated HTTP test scenarios that issue requests exceeding the configured max threshold within the windowMs interval and verify the returned status code matches client error throttling.

Accept when:
- HTTP requests exceeding the configured threshold return HTTP status 429 Too Many Requests along with standard rate limit headers.
- HTTP requests within the configured threshold succeed and include decreasing remaining quota counts in the standard response headers.

## Enforcement

- Verified by: Automated continuous integration pipeline executing route integration tests.
- Verified by: Peer code review verifying middleware ordering and rateLimit parameter configuration.
- Violation handling: Pull requests lacking rate limiting middleware on public API routes are blocked from merge until compliance is established.
- Exception process: Submit an architectural exception request documenting compensating rate limiting controls at upstream gateway layers, approved by the engineering security lead.