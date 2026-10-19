---
version: 2
name: examples-with-dpop-ratelimit-middleware-define-positive-int-0e7f
description: "Express rateLimit Middleware for HTTP Throttling: Ratelimit Middleware Define Positive Integer Values"
metadata:
  actual:
    adr_id: 0e7f3f25-eb90-49a3-af43-e65254d22a23
    status: accepted
    candidate_group_id: 6c224766-e92a-4e60-96d6-678c2cffb625
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express rateLimit Middleware for HTTP Throttling: Ratelimit Middleware Define Positive Integer Values

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for inbound HTTP request routing pipelines and public API routes subject to abuse prevention and client traffic throttling.

### Rules

- **R-RL-001** MUST: The rateLimit middleware MUST define positive integer values for windowMs and max options to establish an explicit sliding or fixed time window and quota ceiling per client identifier.

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