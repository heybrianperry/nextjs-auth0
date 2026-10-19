---
version: 2
name: 3d586632-7a31-483f-9d4a-f2f24b17c920-cors-middleware-adoption-for-origin-restricted-http-endpoints-application-register-cors-middleware-primary-http
description: "cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Application Register Cors Middleware Primary Http"
metadata:
  actual:
    adr_id: 3d586632-7a31-483f-9d4a-f2f24b17c920
    status: accepted
    candidate_group_id: f5e0fe21-4661-4b6b-94c3-3f7dcfdab4c4
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# cors Middleware Adoption for Origin-Restricted HTTP Endpoints: Application Register Cors Middleware Primary Http

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-dpop/**`

## Context

- The HTTP service handles authenticated API transactions requiring protection against unauthorized cross-origin browser interactions.
- The codebase employs dedicated middleware to intercept cross-origin requests and enforce origin matching.
- Base URL configuration from environment sources defines the permissible origin for cross-origin resource requests.

## Problem Statement

Unrestricted cross-origin resource sharing exposes HTTP endpoints to cross-site request abuse and unauthorized data access from untrusted browser contexts. The application requires a consistent, standards-compliant mechanism to restrict cross-origin requests to explicit, configured origins.

## Decision

1. MUST: The application MUST register cors middleware on the primary HTTP router before route definitions to restrict cross-origin request handling.

## Policy Block

- MUST The application MUST register cors middleware on the primary HTTP router before route definitions to restrict cross-origin request handling.

In scope:
- HTTP server applications exposing REST or JSON endpoints accessed by browser-based clients.
- Services requiring origin filtering based on deployment environment configuration.

Out of scope:
- Internal server-to-server RPC endpoints that do not handle browser-initiated cross-origin requests.
- Static asset servers that do not process authenticated application traffic.

## Rationale

- Adopting cors middleware provides established compliance with Cross-Origin Resource Sharing specifications, avoiding custom header parsing errors.
- Restricting the origin parameter to an environment-configured base address ensures that only approved client applications can read response data.
- Positioning cors in the shared middleware pipeline guarantees uniform origin policy application across all exposed HTTP routes.

## Consequences

Positive:
- Prevents unauthorized browser origins from reading sensitive API responses.
- Standardizes CORS handling across endpoints using vetted middleware rather than ad-hoc header manipulation.
- Facilitates environment-specific origin configuration without requiring source code modifications.

Negative:
- Requires exact alignment between client origin domains and server environment configuration.
- Adds dependency coupling to an external CORS middleware package.
- Misconfigurations in the configured origin string can block legitimate client requests during deployment transitions.

## Alternatives

- Custom HTTP middleware setting manual Access-Control response headers (rejected)
  Rejected because: Manual header manipulation increases maintenance overhead and introduces risk of specification non-compliance or header injection vulnerabilities.
  When valid: When operating in constrained runtimes where third-party middleware packages cannot be introduced.
- Wildcard origin configuration across all routes (rejected)
  Rejected because: Permissive wildcard origins expose authenticated API resources to unauthorized browser domains, violating the principle of least privilege.
  When valid: When exposing strictly public, unauthenticated read-only resources intended for universal web consumption.
- Reverse-proxy or API-gateway-level CORS enforcement (deferred)
  Rejected because: Delegating CORS upstream shifts boundary validation away from the application runtime without an established requirement for dedicated gateway infrastructure.
  When valid: When all external traffic is routed through a centralized managed API gateway layer.

## Risks

- Misconfigured origin environment variables may reject legitimate frontend clients or default unexpectedly.
  Mitigation: Enforce startup-time validation of configured origin strings and assert expected origins in automated test suites.
  Owner: engineering team
- Origin matching logic may fail for dynamic subdomains or multi-tenant deployments.
  Mitigation: Support dynamic origin evaluation functions within cors configuration when multi-origin tenancy is required.
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
- Ensure the cors middleware is mounted prior to application routes to intercept preflight OPTIONS requests before endpoint authorization logic.
- Validate the origin configuration parameter during runtime initialization to guarantee that empty or malformed origin variables fail fast.

## Continuation Context


Verify commands:
- Discover and execute the repository security linting suite to ensure cors middleware is registered with explicit origin constraints.
- Discover and execute the HTTP test suite verifying that cross-origin preflight requests evaluate the origin against configured environment values.

Accept when:
- Cross-origin preflight and standard HTTP requests validate that the Access-Control-Allow-Origin header strictly mirrors authorized configured origins.
- Requests originating from unauthorized origins do not receive permissive cross-origin response headers.

## Enforcement

- Verified by: Automated security linter rules checking middleware registration.
- Verified by: Integration test suites validating Access-Control-Allow-Origin response headers.
- Verified by: Peer code review for any modifications to HTTP router middleware stacks.
- Violation handling: Pull requests lacking explicit origin restrictions in cors middleware are blocked by automated review checks.
- Violation handling: Deployments failing integration origin verification are halted.
- Exception process: Architectural and security review approval is required for any wildcard or unconstrained CORS configuration.