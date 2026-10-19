---
version: 2
name: examples-with-dpop-service-enforce-inbound-request-rate-b410
description: "Express rateLimit Middleware for HTTP Throttling: Service Enforce Inbound Request Rate Limiting"
metadata:
  actual:
    adr_id: b41006c8-2274-4cd4-b957-ee3556c6de3e
    status: accepted
    candidate_group_id: 6c224766-e92a-4e60-96d6-678c2cffb625
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - examples/with-dpop/**
---

# Express rateLimit Middleware for HTTP Throttling: Service Enforce Inbound Request Rate Limiting

Scope: applies to `examples/with-dpop/**`.

These rules are ALWAYS ACTIVE for inbound HTTP request routing pipelines exposing application endpoints and public API routes subject to abuse prevention and client traffic throttling.

### Rules

- **R-RATE-001** MUST: The service MUST enforce inbound request rate limiting on public HTTP routes using rateLimit middleware integrated into the express application pipeline.

### Verify

```bash
# Discover the project test execution runner from the manifest and run automated integration test suites validating rate limit response codes and headers.
# Execute automated HTTP test scenarios that issue requests exceeding the configured max threshold within the windowMs interval and verify the returned status code matches client error throttling.
```

**Accept when:**
- HTTP requests exceeding the configured threshold return HTTP status 429 Too Many Requests along with standard rate limit headers.
- HTTP requests within the configured threshold succeed and include decreasing remaining quota counts in the standard response headers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Compliance is enforced via automated continuous integration pipeline executing route integration tests and peer code reviews.
</enforcement>