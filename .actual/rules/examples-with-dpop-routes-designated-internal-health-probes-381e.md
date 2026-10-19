---
version: 2
name: examples-with-dpop-routes-designated-internal-health-probes-381e
description: "Express rateLimit Middleware for HTTP Throttling: Routes Designated Internal Health Probes Private"
metadata:
  actual:
    adr_id: 381e4135-a294-47ed-9a14-323a4c648060
    status: accepted
    candidate_group_id: 6c224766-e92a-4e60-96d6-678c2cffb625
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express rateLimit Middleware for HTTP Throttling: Routes Designated Internal Health Probes Private

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for inbound HTTP request routing pipelines exposing application endpoints and public API routes subject to abuse prevention and client traffic throttling.

### Rules

- **R-EX-001** MAY: Routes designated as internal health probes or private administrative endpoints MAY be exempted from client IP rate limiting middleware.

### Verify

```bash
# Discover the project test execution runner from the manifest and run automated integration test suites validating rate limit response codes and headers.
# Execute automated HTTP test scenarios that issue requests exceeding the configured max threshold within the windowMs interval and verify the returned status code matches client error throttling.
```

**Accept when:**
- HTTP requests exceeding the configured threshold return HTTP status 429 Too Many Requests along with standard rate limit headers.
- HTTP requests within the configured threshold succeed and include decreasing remaining quota counts in the standard response headers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>