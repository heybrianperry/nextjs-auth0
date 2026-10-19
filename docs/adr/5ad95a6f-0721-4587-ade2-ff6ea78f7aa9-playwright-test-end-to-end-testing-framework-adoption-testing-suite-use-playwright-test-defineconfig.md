---
version: 2
name: 5ad95a6f-0721-4587-ade2-ff6ea78f7aa9-playwright-test-end-to-end-testing-framework-adoption-testing-suite-use-playwright-test-defineconfig
description: "`@playwright/test` End-to-End Testing Framework Adoption: Testing Suite Use Playwright Test Defineconfig"
metadata:
  actual:
    adr_id: 5ad95a6f-0721-4587-ade2-ff6ea78f7aa9
    status: accepted
    candidate_group_id: 403ff59f-0ebc-49a7-89f5-39b4c2e9d5ce
    evidence:
      source: deep
  scope:
    root: .
---

# `@playwright/test` End-to-End Testing Framework Adoption: Testing Suite Use Playwright Test Defineconfig

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `**/*` (whole repository)

## Context

- The application requires automated end-to-end functional verification across realistic browser environments and multiple viewport profiles.
- Test suites must adapt execution parameters such as port allocation and execution environment behavior between local development and automated pipeline environments.
- Configuration must rely on standard framework conventions to ensure consistent multi-device simulation and maintainable test declarations.

## Problem Statement

End-to-end browser testing requires a consistent, multi-device configuration harness that adapts cleanly between local developer workflows and automated continuous integration pipelines without hardcoding runtime parameters.

## Decision

1. MUST: The testing suite MUST use `@playwright/test` and `defineConfig` as the primary configuration mechanism for end-to-end browser testing.

## Policy Block

- MUST The testing suite MUST use `@playwright/test` and `defineConfig` as the primary configuration mechanism for end-to-end browser testing.

In scope:
- All end-to-end browser test suites and configuration definitions within the repository.
- Automated integration and end-to-end test execution stages in continuous integration workflows.

Out of scope:
- Unit test suites verifying isolated functions, algorithmic components, or state stores.
- Component-level isolation tests that do not require full multi-page browser lifecycle verification.

## Rationale

- Adopting `@playwright/test` with `defineConfig` establishes a declarative, strongly-typed foundation for end-to-end testing across the codebase.
- Leveraging `devices` presets avoids manual maintenance of browser dimensions, user-agent strings, and device capabilities.
- Parameterizing configuration via environment variables ensures seamless portability across local development and continuous integration environments.

## Consequences

Positive:
- Provides unified configuration for browser-level end-to-end test execution across multiple device profiles.
- Enables dynamic adaptation between local development environments and continuous integration pipelines through runtime environment bindings.
- Standardizes test harness setup using official framework configuration helpers rather than custom harness wrappers.

Negative:
- Requires maintaining browser automation dependencies and managing browser engine downloads across execution environments.
- Introduces operational complexity in managing environment variables and port bindings between local workstations and continuous integration systems.

## Alternatives

- Unit and component test mocking without real browser automation (rejected)
  Rejected because: Fails to validate real browser rendering engines, client-side routing, DOM event lifecycles, and actual end-to-end user workflows.
  When valid: When testing pure business logic functions or isolated presentation components with no browser-specific behaviors.
- Unstructured custom browser automation scripts using low-level browser drivers (rejected)
  Rejected because: Increases maintenance overhead by lacking unified test harness configuration, device descriptor abstractions, and standardized runner features.
  When valid: When performing one-off synthetic monitoring or low-level protocol experimentation decoupled from application testing suites.

## Risks

- Discrepancies in environment variable configuration leading to port conflicts or unintended test execution modes across environments.
  Mitigation: Centralize environment variable reading and establish deterministic local fallback values for server port and execution mode flags.
  Owner: engineering team
- Flaky test outcomes caused by timing variations or resource contention across different continuous integration runner environments.
  Mitigation: Utilize framework-provided auto-waiting assertions and configure environment-appropriate timeout thresholds for continuous integration runners.
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
- Configure device simulation parameters using framework-supplied device presets to ensure tests accurately represent targeted runtime viewports.
- Ensure all dynamic runtime values fall back to sensible local defaults when optional continuous integration environment variables are not supplied.

## Continuation Context


Verify commands:
- Discover and execute the project's test verification script as defined in the repository manifest to validate test configuration validity.
- Execute the project's static analysis and type checking scripts to ensure end-to-end configuration definitions adhere to repository conventions.

Accept when:
- The project verification scripts execute the end-to-end test suite cleanly across configured device profiles without runtime syntax or configuration errors.
- Environment-dependent configuration bindings for execution mode and network port resolve correctly across local and pipeline environments.

## Enforcement

- Verified by: Automated continuous integration pipeline checks validating test configuration and test execution results.
- Verified by: Pull request code review confirming new end-to-end test specifications adhere to framework conventions.
- Violation handling: Pull requests introducing non-standard browser testing harnesses or hardcoded environment configurations will be blocked from merging.
- Violation handling: Violating test declarations must be refactored to use the standardized configuration pattern.
- Exception process: Submit an architectural variance request with technical justification detailing why a specific test suite cannot use the standard end-to-end framework.
- Exception process: Obtain written approval from the quality engineering lead and document the temporary waiver with an expiration milestone.