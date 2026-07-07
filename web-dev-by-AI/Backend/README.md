# Backend Skills

Backend web development skills covering API design, database, security, DevOps, and Flask architecture.

## Skills

| Skill | Description |
|-------|-------------|
| `api-design-architecture` | REST API design, pagination, filtering, rate limiting, versioning, RFC 7807 error handling |
| `database-storage` | PostgreSQL, Redis caching, indexing strategies, connection pooling, ORM patterns |
| `backend-security-auth` | HTTPS/TLS, OWASP, CSP, CORS, rate limiting, authentication patterns |
| `devops-ci-cd` | Docker multi-stage, healthchecks, GitHub Actions, Nginx reverse proxy, CI/CD pipelines |
| `flask-blueprint-refactor` | Refactoring Flask apps into scalable Blueprint-based architecture |

## Quick Reference

### API Design
```python
# Cursor pagination
cursor = base64urlencode(next_cursor)
has_more = len(results) > limit
```

### Database Connection Pool
```python
# Sizing formula: (cores*2)+spindles
pool = ConnectionPool(size=9, ...)
```

### Redis Rate Limiter
```python
# Sliding window
timestamps = redis.lrange(key, 0, -1)
timestamps = [t for t in timestamps if t > window_start]
```

### Flask Blueprint
```python
from flask import Blueprint
bp = Blueprint('name', __name__, url_prefix='/path')
app.register_blueprint(bp)
```

### Docker Multi-Stage
```dockerfile
FROM node:alpine AS builder
COPY . /app && npm run build

FROM node:alpine
COPY --from=builder /app/dist /app
CMD ["node", "server.js"]
```

## Folder Structure

```
Backend/
├── api-design-architecture/
│   └── references/
├── database-storage/
│   └── references/
├── backend-security-auth/
│   └── references/
├── devops-ci-cd/
│   └── references/
├── flask-blueprint-refactor/
└── README.md
```

## Triggers

Use these skills when:
- Building or debugging REST APIs
- Working with databases (PostgreSQL, Redis)
- Implementing security (auth, rate limiting, headers)
- Setting up Docker or CI/CD pipelines
- Refactoring Flask applications