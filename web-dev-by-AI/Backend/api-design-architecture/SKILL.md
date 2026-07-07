---
name: api-design-architecture
description: REST API design principles, server architecture patterns, and API governance for scalable backend systems.
category: web-development
platforms: [linux, macos, windows]
---

# API Design & Architecture

Covers the foundational patterns for designing, versioning, and operating production-grade REST APIs.

## Core Topics

### REST API Design Principles
- Resource-based routing (nouns, not verbs)
- Proper HTTP methods: GET, POST, PUT, PATCH, DELETE
- Status codes mapping (2xx success, 4xx client error, 5xx server error)
- HATEOAS for discoverability

### Pagination & Filtering
- **Cursor pagination**: opaque base64url token, `limit+1` trick for `hasMore`, O(1) performance
- **Filtering**: comma-separated tags (OR), partial search, `-prefix` for desc, multi-field sort
- **Sorting**: multi-field, stable ordering

### Error Handling
- **RFC 7807 Problem Details**: standardized envelope with `type`, `title`, `status`, `detail`, `instance`, `requestId`, `timestamp`
- Consistent error shape across all endpoints

### API Versioning
- URL path (primary): `/v1/`, `/v2/`
- Accept header: `application/vnd.myapi.v1+json`
- `X-API-Version` header
- Reject unsupported versions explicitly

### Rate Limiting
- Sliding window with timestamps array
- Headers: `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`
- Per-IP or per-user scopes

### Middleware Ordering (Critical)
```
CORS → Rate Limit → Version Detection → Logging → Handlers
```

### API Discovery
- Root endpoint returns HATEOAS links + supported versions
- Self-documenting entry point

## Key Implementation Notes

### Fastify 5 Reference Implementation
- Full CRUD with pagination, filtering, sorting
- Error handling per RFC 7807
- CORS + rate limiting + versioning middleware chain
- 40 tests (35 passed, 5 fixed during learning)

### Common Bugs to Avoid
- Spreading JS `Map` directly yields `[key, value]` pairs — use `[...map.values()]`
- Don't forget `OPTIONS` preflight → 204 for CORS
- Cursor tokens must be opaque; never expose internal IDs

## Related References
- `references/api-design-architecture.md` (detailed notes)
- `references/cron-jobs.md` (scheduling context)

## Triggers
- "api design", "rest api", "pagination", "rate limiting", "api versioning", "rfc 7807"