---
version: 2
name: examples-with-dpop-before-implementing-updating-rate-limiti-7667
description: "Express rateLimit Middleware for HTTP Throttling: Before Implementing Updating Rate Limiting Middleware"
metadata:
  actual:
    adr_id: 7667947e-0d73-4855-9ee9-bb3117c869fa
    status: accepted
    candidate_group_id: 6c224766-e92a-4e60-96d6-678c2cffb625
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express rateLimit Middleware for HTTP Throttling: Before Implementing Updating Rate Limiting Middleware

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for inbound HTTP request routing pipelines and public API routes subject to abuse prevention and client traffic throttling.

### Rules

- **R-RL-001** MUST: Before implementing or updating the rate limiting middleware, the consumer MUST inspect the repository dependency resolution lock artifact to verify and ground against the exact resolved package version.

### Verify

```bash
# Discover the project test execution runner from the manifest and run automated integration test suites validating rate limit response codes and headers.
# Execute automated HTTP test scenarios that issue requests exceeding the configured max threshold within the windowMs interval and verify the returned status code matches client error throttling.
```

**Accept when:**
- HTTP requests exceeding the configured threshold return HTTP status 429 Too Many Requests along with standard rate limit headers.
- HTTP requests within the configured threshold succeed and include decreasing remaining quota counts in the standard response headers.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>