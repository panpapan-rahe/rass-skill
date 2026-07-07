---
name: AI-backend-developer
description: "AI-driven backend development knowledge base — structured in 4 progressive levels: Fundamental, Keamanan & Data, Skalabilitas, and Engineering. Auto-updates via cron job."
version: 1.0.0
author: Rass (AI-driven autodidact)
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [backend, api, database, security, devops, performance, architecture]
    related_skills: []
---

# AI Backend Developer

> AI-driven backend development knowledge base. This skill is managed via cron job and contains learned knowledge about backend technologies, structured in 4 progressive levels.

## Learning Levels

This skill follows a 4-level progression to build robust backend expertise:

### Level 1 — Fundamental
- **API Architect**: REST API design, HTTP methods, status codes, versioning, pagination
- **Business Logic**: Service layer patterns, clean architecture, domain modeling
- **Database Architect**: Schema design, relationships, migrations
- **Validation**: Input validation, sanitization, error handling

### Level 2 — Keamanan & Data
- **Authentication**: JWT, sessions, OAuth, tokens
- **Authorization**: RBAC, permissions, scopes
- **Security**: OWASP, encryption, rate limiting, CSP
- **File Storage**: Local vs cloud, multipart uploads, CDN

### Level 3 — Skalabilitas
- **Queue**: Message brokers, task queues, async processing
- **Background Worker**: Job processing, schedulers, cron
- **Caching**: Redis, Memcached, cache strategies
- **Performance**: Profiling, optimization, connection pooling

### Level 4 — Engineering
- **Testing**: Unit tests, integration tests, mocking
- **Logging**: Structured logs, log levels, aggregation
- **Monitoring**: Health checks, metrics, alerting
- **Architecture**: Microservices, patterns, clean code
- **DevOps Integration**: Docker, CI/CD, deployment
- **Backend Reviewer**: Code review, best practices

## Learning Path

Learning path will be defined through the autodidact cron job system, following the level progression above.

## Daily Update System
A cron job (`Backend Daily Update 22:30`) delivers a short daily update in Indonesian to Discord channel `1523924571491926126` with:
1. Current level
2. Today's micro-topic
3. Key learning / change
4. Experiment output
5. Next step

### Backfill / Manual Trigger Rule
If the user asks to cover a missed day, treat it as a manual trigger and label the update clearly as a backfill for the missing day rather than pretending it happened on the current date.

See `references/backend-reset-protocol.md` for the cleanup sequence and the cronjob/channel history used in this reset.

## Quick Reference

Coming soon — content will be built through learning sessions.

## Best Practices

1. **Learn by doing**: Always experiment with code, not just reading.
2. **Apply to projects**: Transfer knowledge to real projects like Cashflow Journal.
3. **Document mistakes**: Note what doesn't work and why.
4. **Iterate**: Revisit and improve past understanding as skills grow.

## Folder Structure

```
AI-backend-developer/
├── SKILL.md
└── references/
    └── (reference files will be added over time)
```

## Triggers

- "backend", "api", "database", "security", "authentication", "devops"
- "belajar backend", "belajar api"
- "apa itu rest api", "apa itu jwt"

## Version History

- 1.0.0 — Initial reset with 4-level structure.