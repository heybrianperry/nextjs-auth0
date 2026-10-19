---
version: 2
name: 33c5dcf0-e280-46cf-a596-1d4c7abfbf3f-dotenv-environment-variable-configuration-application-business-logic-client-initialization-routines
description: "dotenv Environment Variable Configuration: Application Business Logic Client Initialization Routines"
metadata:
  actual:
    adr_id: 33c5dcf0-e280-46cf-a596-1d4c7abfbf3f
    status: accepted
    candidate_group_id: 32228038-5c64-4715-8c2b-ad6a35e9f91b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# dotenv Environment Variable Configuration: Application Business Logic Client Initialization Routines

Status: proposed
Date: 2025-05-14
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `examples/with-dpop/**`

## Context

- External runtime configuration values such as host identifiers, authentication server domains, audience strings, and execution mode flags must be injected dynamically across runtime boundaries.
- The server runtime imports dotenv to load environment variables into the process execution context during startup initialization.
- Application modules across framework configuration, authentication clients, and HTTP services read configuration directly from process environment variables.
- Ad-hoc access to process environment properties without centralized validation introduces configuration drift and runtime failures when expected variables are missing.

## Problem Statement

Directly accessing runtime environment variables across disparate modules without centralized schema validation creates implicit coupling to the execution host, risks unhandled runtime crashes due to undefined variables, and scatters environment dependency contracts throughout the codebase.

## Decision

1. MUST_NOT: Application business logic and client initialization routines MUST_NOT access raw process environment variables directly across dispersed application layers without central configuration export.

## Policy Block

- MUST_NOT Application business logic and client initialization routines MUST_NOT access raw process environment variables directly across dispersed application layers without central configuration export.

In scope:
- Runtime environment configuration loading in server execution contexts.
- Process environment property consumption in application client initializers and framework configurations.

Out of scope:
- Static build-time constants that do not vary across deployment environments.
- Ephemeral in-memory cache states and transient session data.

Exceptions:
- EX-37-001: A third-party framework configuration module mandates direct top-level access to process environment properties during its initialization lifecycle.

## Rationale

- Initializing dotenv at service entry ensures all downstream middleware and service providers receive a populated execution environment before processing incoming requests.
- Centralizing environment property access prevents fragmented dependencies on external ambient environment states and enables unified schema validation.
- Inspecting locked dependency artifacts ensures deterministic runtime configuration behavior and guards against breaking changes across dependency updates.

## Consequences

Positive:
- Decouples deployment environment configuration from application source code across runtime boundaries.
- Establishes a predictable startup sequence where configuration is loaded prior to service initialization.
- Improves security posture by preventing accidental hardcoding of sensitive environment values in application code.

Negative:
- Introduces startup latency when parsing and loading configuration files in non-production environments.
- Requires strict operational coordination to ensure required environment variables are defined in each host environment.

## Alternatives

- Direct Host Environment Injection Without dotenv (rejected)
  Rejected because: Relies entirely on container or host process environment configuration, which complicates local development workflows and requires additional tooling for developers.
  When valid: Valid in containerized production environments where external secret managers inject variables directly into the process runtime.
- Centralized Configuration Management Service (deferred)
  Rejected because: Adds network overhead and infrastructure complexity that is disproportionate for lightweight service deployments.
  When valid: Valid in complex distributed microservice architectures requiring dynamic runtime configuration reloading without service restarts.

## Risks

- Missing or malformed environment variables cause runtime exceptions during execution when accessed by downstream consumers.
  Mitigation: Enforce startup schema validation that crashes immediately if any required environment variable is absent.
  Owner: engineering team
- Inadvertent exposure of environment files containing secrets through repository commits or public artifacts.
  Mitigation: Configure repository ignore rules and automated secret detection scanners in continuous integration pipelines.
  Owner: security team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Initialize configuration loading as the first executable statement in the service entry point before importing modules that depend on environment variables.
- Maintain a dedicated environment schema definition that maps raw environment strings to typed configuration objects consumed by application services.

## Continuation Context


Verify commands:
- Discover and run the repository test suite to verify that service components initialize correctly with expected configuration parameters.
- Discover and execute the repository configuration validation script to verify that required environment variables are parsed without errors.

Accept when:
- All configuration schema validations pass successfully with valid environment variables provided.
- Application bootstrap aborts with a descriptive error when any mandatory environment variable is absent.

## Enforcement

- Verified by: Automated static analysis checks in continuous integration pipelines verifying no raw process environment reads outside designated configuration modules.
- Verified by: Pull request code reviews ensuring environment variables are declared in the central schema.
- Violation handling: Pull requests with unvalidated environment variable access or missing schema entries are blocked from merging.
- Violation handling: Continuous integration builds fail if secret-bearing files or undeclared environment variables are detected.
- Exception process: Submit an architectural review request documenting the framework constraint requiring direct environment variable access, subject to lead engineer sign-off.