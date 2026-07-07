# API Design & Architecture — Reference

> Detail eksperimen Backend Sesi 8 (2026-06-29)

## Project Location
`~/hermes-lab/web/backend/src/api-design/`

## Stack
- Fastify 5.8.5
- Vitest 4.1.9 (test runner)
- Zero external dependencies for core logic

## Architecture Patterns Implemented

### Response Envelope (JSON:API-like)
```json
{
  "data": { ... } | [ ... ],
  "_links": { "self": {...}, "collection": {...} },
  "_meta": { "total": N, "count": N, "nextCursor": "..." }
}
```

### Error Envelope (RFC 7807)
```json
{
  "type": "https://httpstatuses.com/404",
  "title": "Not Found",
  "status": 404,
  "detail": "Resource not found",
  "instance": "/v1/articles/xyz",
  "requestId": "req-uuid",
  "timestamp": "2026-06-29T15:00:00Z"
}
```

### Cursor Pagination Flow
1. Client: `GET /v1/articles?limit=20`
2. Server: fetch `limit + 1` items from data
3. If extra item exists → set `nextCursor` in `_meta`
4. Client: `GET /v1/articles?limit=20&cursor=eyJuZX...MjB9`
5. Cursor decoded → `startIndex = nextIndex`

### API Version Detection Priority
1. Accept header: `application/vnd.api+json;version=2`
2. X-API-Version header: `2`
3. URL path: `/v2/articles`
4. Default: `1`

### Middleware Stack (Fastify hooks)
```
onRequest: CORS headers → Rate limit check → Version detection
onSend: Response transformation (v2 strips internal fields)
```

## Test Coverage (40 tests)
- Health check (1)
- HATEOAS discovery (2)
- CRUD operations (5)
- Cursor pagination (4)
- Filtering (4)
- Sorting (3)
- RFC 7807 errors (4)
- API versioning (3)
- CORS (2)
- Content negotiation (2)
- Nested resources (1)
- HTTP status codes (5)
- Rate limiting (2)
- Input validation (2)

## Common Pitfalls

### ⚠️ Map Spread Bug
```js
const map = new Map([['a', 1], ['b', 2]]);
[...map];           // [['a', 1], ['b', 2]] — WRONG!
[...map.values()];  // [1, 2] — CORRECT
```

### ⚠️ Fastify Error Handler
```js
// Fastify v5 uses err.statusCode, not err.status
app.setErrorHandler((err, req, reply) => {
  const status = err.statusCode || err.status || 500;
  reply.code(status).send(problem);
});
```

### ⚠️ pino-pretty in Tests
```js
// This fails if pino-pretty is not installed:
const app = Fastify({ logger: { transport: { target: 'pino-pretty' } } });

// Fix: use simple string level in test mode
const app = Fastify({ logger: 'silent' });
// or install: npm install -D pino-pretty
```

### ⚠️ Shared State in Tests
```js
// Module-level Map persists across test instances
// beforeEach creates new app but data survives
// Fix: use unique IDs per test, or create fresh data in beforeEach
```

## Resources
- [RFC 7807](https://tools.ietf.org/html/rfc7807) — Problem Details for HTTP APIs
- [JSON:API spec](https://jsonapi.org/) — Response format
- [HATEOAS RFC 5988](https://tools.ietf.org/html/rfc5988) — Link relations
