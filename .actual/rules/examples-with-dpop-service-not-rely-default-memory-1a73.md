---
version: 2
name: examples-with-dpop-service-not-rely-default-memory-1a73
description: "Express rateLimit Middleware for HTTP Throttling: Service Not Rely Default Memory Rate"
metadata:
  actual:
    adr_id: 1a7332ac-97b9-44ba-91da-7a840e167204
    status: accepted
    candidate_group_id: 6c224766-e92a-4e60-96d6-678c2cffb625
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express rateLimit Middleware for HTTP Throttling: Service Not Rely Default Memory Rate

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for inbound HTTP request routing pipelines and public API routes subject to abuse prevention and client traffic throttling.

### Rules

- **R-RL-001** SHOULD_NOT: The service SHOULD NOT rely on default in-memory rate limiting stores when deployed across horizontally scaled multi-process or multi-container application clusters.

### Verify

```bash
# Discover the project test execution runner from the manifest and run automated integration test suites validating rate limit response codes and headers.
# Execute automated HTTP test scenarios that issue requests exceeding the configured max threshold within the windowMs interval and verify the returned status code matches client error throttling.
```

**Accept when:**
- HTTP requests exceeding the configured threshold return HTTP status 429 Too Many Requests along with standard rate limit headers.
- HTTP requests within the configured threshold succeed and include decreasing remaining quota counts in the standard response headers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline executing route integration tests and peer code review verifying middleware ordering and rateLimit parameter configuration.
</enforcement>