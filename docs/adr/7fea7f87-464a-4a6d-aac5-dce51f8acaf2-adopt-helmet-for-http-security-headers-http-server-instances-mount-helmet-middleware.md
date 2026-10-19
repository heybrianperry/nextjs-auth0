---
version: 2
name: 7fea7f87-464a-4a6d-aac5-dce51f8acaf2-adopt-helmet-for-http-security-headers-http-server-instances-mount-helmet-middleware
description: "Adopt Helmet for HTTP Security Headers: Http Server Instances Mount Helmet Middleware"
metadata:
  actual:
    adr_id: 7fea7f87-464a-4a6d-aac5-dce51f8acaf2
    status: accepted
    candidate_group_id: 06493b99-f9c8-438f-b320-b4939e124ca8
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Adopt Helmet for HTTP Security Headers: Http Server Instances Mount Helmet Middleware

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-dpop/**`

## Context

- HTTP servers lacking defensive headers remain exposed to common browser-targeted vulnerabilities such as clickjacking and MIME-type sniffing
- The application initialises an Express service that serves API endpoints requiring robust client-side protection
- Evidence demonstrates the use of Helmet middleware in the request processing pipeline alongside CORS and request parsers
- The pattern is currently isolated to a single example service without verified multi-file adoption across production modules

## Problem Statement

Deploying HTTP API services without standardized security headers leaves endpoints vulnerable to common browser-based attacks. Applications require an automated, minimal-configuration mechanism to apply secure HTTP response headers across all exposed endpoints.

## Decision

1. MUST: All HTTP API server instances MUST mount Helmet middleware in the request processing pipeline to enforce baseline HTTP security headers.

## Policy Block

- MUST All HTTP API server instances MUST mount Helmet middleware in the request processing pipeline to enforce baseline HTTP security headers.

In scope:
- All HTTP API server applications serving network requests
- Backend services handling authenticated web endpoints

Out of scope:
- Background batch workers and command-line execution tools
- Client-side browser applications

Exceptions:
- EXC-42-001: An upstream reverse proxy or gateway manages security headers uniformly for the service

## Rationale

- Applying Helmet middleware provides automated defense against well-known web security issues with zero custom header scripting
- Configuring security headers at the application level ensures defense-in-depth across both local development and remote deployments
- Evidence confirms compatibility with the existing middleware pipeline alongside CORS and request body parsers

## Consequences

Positive:
- Standardizes defense-in-depth across HTTP endpoints by delivering protective response headers automatically
- Mitigates common web vulnerabilities including clickjacking, MIME sniffing, and cross-site scripting by default
- Reduces repetitive boilerplate security configuration across service initialization logic

Negative:
- Default protective directives can block legitimate cross-origin requests or embedding unless explicitly reconfigured
- Adds minimal request-processing overhead to inject response headers on every HTTP transaction

## Alternatives

- Manual configuration of individual HTTP response headers via custom middleware (rejected)
  Rejected because: Manual header manipulation is prone to omissions, increases maintenance overhead, and fails to track evolving browser security standards
  When valid: Valid only in minimal runtime environments where external middleware dependencies cannot be installed
- Relying solely on external ingress proxies to inject security headers (rejected)
  Rejected because: Leaves internal service communications and local development environments unprotected against header-based vulnerabilities
  When valid: Valid when organizational policy mandates centralized gateway termination across every deployment stage

## Risks

- Strict Content-Security-Policy or cross-origin directives may interfere with valid client asset loading
  Mitigation: Specify necessary header exemptions in the middleware configuration and validate integration workflows in automated test suites
  Owner: Engineering Team
- Upstream library version updates may alter default header policies unexpectedly
  Mitigation: Follow lock-version grounding and run regression test suites before upgrading middleware dependencies
  Owner: Security and Infrastructure Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Mount Helmet middleware before application routers and handlers to guarantee all outbound responses carry protective headers
- Consult resolved documentation to configure specific header options when cross-origin resource sharing or embedding is needed

## Continuation Context


Verify commands:
- grep -rn "app.use(helmet" . || echo "Verify Helmet middleware registration in HTTP server setup"
- find . -maxdepth 3 -name "*test*" -o -name "*spec*" | head -n 1 && echo "Execute discovered test runner to validate response headers"

Accept when:
- HTTP server setup code contains Helmet middleware registration prior to route definitions
- Discovered test suite executes successfully and confirms security headers are present on HTTP responses

## Enforcement

- Verified by: Static analysis checks verifying the inclusion of Helmet middleware within HTTP server initialization sequences
- Verified by: Automated test runner suites inspecting HTTP response headers on exposed endpoints
- Verified by: Peer review during code integration to prevent omission of security middleware
- Violation handling: Continuous integration checks fail when an HTTP service exposes endpoints without mounting security header middleware
- Violation handling: Pull requests lacking required middleware are blocked from merging until remediation is complete
- Exception process: Submit an architecture exception request detailing why upstream infrastructure handles HTTP security headers uniformly
- Exception process: Obtain sign-off from the security review team prior to deploying services without application-level security headers