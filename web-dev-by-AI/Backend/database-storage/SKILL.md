---
name: database-storage
description: PostgreSQL, SQLite, Redis caching patterns, indexing strategies, and database architecture for scalable backend systems.
category: web-development
platforms: [linux, macos, windows]
---

# Database & Storage

Comprehensive coverage of relational databases, caching, and storage patterns for production backends.

## Core Topics

### PostgreSQL

#### Connection Pooling
- **Sizing formula**: `(cores*2)+spindles`
- **PgBouncer** config for high-traffic scenarios
- Connection lifecycle management

#### Indexing Strategies
- **B-tree**: default, range queries
- **Partial**: subset of rows
- **Covering** (INCLUDE): include non-index columns
- **GIN**: JSONB, Full-Text Search
- **GiST**: ranges, geometric data
- **Expression**: functional indexes
- **Unique partial**: constraints on subsets

#### Monitoring & Optimization
- `pg_stat_activity`: active connections
- `pg_stat_statements`: query performance
- Unused index detection queries
- Query execution plan analysis (EXPLAIN ANALYZE)

### Redis

#### Caching Patterns
- **Cache-aside**: read-through, lazy loading
- **Write-through**: sync DB + cache
- **Write-behind**: async cache write
- **TTL management**: expiration strategies

#### Redis Commands
- `SCAN` vs `KEYS` (KEYS is O(n), avoid in production)
- Key naming convention: `domain:resource:identifier`

#### Advanced Patterns
- **Sliding window rate limiter**: timestamp arrays
- **Distributed lock**: `SET NX PX` + Lua release script

### ORM Comparison
- **Drizzle**: SQL-like, full control, zero runtime
- **Prisma**: schema-first, auto-generated types, DX-focused

### PostgreSQL Specifics
- ACID compliance
- Transactions and isolation levels
- JSON/JSONB usage
- Foreign keys and referential integrity

## Implementation Notes

### Tests Coverage (from learning session)
- 36 tests covering pool config
- 9 index types demonstrated
- Cache patterns (cache-aside, write-through)
- Rate limiter with sliding window
- Distributed lock pattern

### Best Practices
- Always use parameterized queries (prevents SQL injection)
- Monitor slow queries (log_min_duration_statement)
- Index foreign keys
- Use connection pooling in production
- Separate read replicas for read-heavy workloads

## Triggers
- "database", "postgres", "redis", "caching", "indexing", "connection pool", "orm"