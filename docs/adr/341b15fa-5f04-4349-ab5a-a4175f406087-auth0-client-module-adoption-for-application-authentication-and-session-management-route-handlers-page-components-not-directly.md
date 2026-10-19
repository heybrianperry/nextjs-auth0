---
version: 2
name: 341b15fa-5f04-4349-ab5a-a4175f406087-auth0-client-module-adoption-for-application-authentication-and-session-management-route-handlers-page-components-not-directly
description: "Auth0 Client Module Adoption for Application Authentication and Session Management: Route Handlers Page Components Not Directly"
metadata:
  actual:
    adr_id: 341b15fa-5f04-4349-ab5a-a4175f406087
    status: accepted
    candidate_group_id: c31ceea8-7373-423a-b207-4ff7f2a56177
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-cte/app/**
      - examples/with-enterprise-connect/app/**
      - examples/with-ipsie-session-expiry/app/**
      - examples/with-next-intl/app/**
      - examples/with-passkeys/app/**
      - examples/with-passwordless-db/app/**
      - examples/with-passwordless/app/**
---

# Auth0 Client Module Adoption for Application Authentication and Session Management: Route Handlers Page Components Not Directly

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-cte/app/**`
- `examples/with-enterprise-connect/app/**`
- `examples/with-ipsie-session-expiry/app/**`
- `examples/with-next-intl/app/**`
- `examples/with-passkeys/app/**`
- `examples/with-passwordless-db/app/**`
- `examples/with-passwordless/app/**`

## Context

- Application features require secure authentication, session verification, and token exchange across diverse user flows.
- Decentralized instantiation of identity SDK clients across individual route handlers introduces configuration drift and inconsistent session validation.
- Consolidating identity operations into a dedicated Auth0 client module establishes a uniform interface for server components and route handlers.
- Application routes coordinate authentication checks with navigation utilities to control access to protected views.

## Problem Statement

Scattering authentication SDK client configurations, credential bindings, and session validation logic across disparate application route handlers introduces maintenance overhead and risks inconsistent security enforcement. Without a unified module boundary, application routes risk divergent session handling, fragmented error logging, and duplicate credential parsing across different authentication methods.

## Decision

1. MUST_NOT: Route handlers and page components MUST NOT directly handle raw authentication credentials or bypass the centralized Auth0 client module when validating session state.

## Policy Block

- MUST_NOT Route handlers and page components MUST NOT directly handle raw authentication credentials or bypass the centralized Auth0 client module when validating session state.

In scope:
- All application routes, server components, and handlers requiring user authentication, token exchange, or session state inspection.
- Workflows integrating passwordless, enterprise connection, passkey, or credential-based identity validation.

Out of scope:
- Public static informational routes that do not inspect user identity or maintain authenticated state.
- Independent external microservices operating outside this application codebase.

Exceptions:
- EXC-001: A third-party webhook requires standalone signature verification independent of application user sessions.

## Rationale

- Centralizing authentication through a dedicated Auth0 client module establishes a single source of truth for identity configuration and session lifecycle management across all routes.
- Static evidence across seventeen files demonstrates consistent consumption of the centralized Auth0 module alongside navigation utilities across varied authentication flows.
- Standardizing client module access simplifies security auditing, centralizes secret management, and prevents fragmentation of error handling logic.

## Consequences

Positive:
- Provides a single point of control for tenant configuration, credential handling, and session state verification.
- Enforces consistent error handling and user redirection across all protected application entry points.
- Eliminates boilerplate and prevents duplicate SDK client instantiations across route handlers.

Negative:
- Creates architectural coupling between application routes and the centralized Auth0 client module interface.
- Modifications to the centralized client module interface require coordinated verification across all dependent route handlers.

## Alternatives

- Ad-hoc inline instantiation of identity SDK clients within each individual page and route handler (rejected)
  Rejected because: Causes widespread configuration duplication, credential exposure risk, and inconsistent session validation behavior.
  When valid: Single-file prototype applications with no protected routes or shared state.
- Generic custom session token management without a dedicated third-party identity module (rejected)
  Rejected because: Significantly increases development complexity, security surface area, and maintenance burden for modern authentication protocols.
  When valid: Air-gapped environments where external identity providers cannot be reached.

## Risks

- Breaking API changes in upstream identity libraries could impact the centralized client module and disrupt application authentication.
  Mitigation: Lock exact dependency versions in repository resolution artifacts and validate all API surfaces against resolved documentation before upgrades.
  Owner: Security and Platform Engineering Team
- Misconfiguration of the centralized module could propagate authentication failures across all dependent application routes.
  Mitigation: Maintain automated test suites covering the centralized client module and mandate integration tests for authentication flows.
  Owner: Application Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Centralize configuration parameters, callback URLs, and tenant credentials in environment configurations consumed exclusively by the Auth0 client module.
- Structure route guards to evaluate session context from the centralized module prior to rendering protected page layouts or handling mutation actions.

## Continuation Context


Verify commands:
- Discover the project test runner and static analysis scripts from the dependency manifest and execute the test suite validating authentication flows.
- Discover the project linting and module import boundary verification scripts to confirm that all authentication references originate from the centralized Auth0 client module.
- Discover and execute the type-checking task to confirm that all invocations of Auth0 client APIs conform to the resolved library type signatures.

Accept when:
- All automated test suites covering authentication and session validation pass without errors.
- Static analysis and architectural lint checks confirm zero unauthorized direct imports of external authentication SDKs outside the centralized client module.
- Type checking succeeds with all Auth0 API calls matching the resolved library interfaces.

## Enforcement

- Verified by: Continuous integration checks enforcing static module boundary rules and running automated test suites.
- Verified by: Peer code review verifying that all authentication interactions consume the centralized Auth0 client module.
- Violation handling: Pull requests containing direct external identity SDK instantiations outside the designated client module are blocked from merging.
- Violation handling: Architectural lint violations trigger build failures that require remediation before deployment.
- Exception process: Submit an architectural review request detailing why the centralized module cannot fulfill the specific requirement, requiring approval from the security lead.