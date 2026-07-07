---
name: devops-ci-cd
description: Docker, health checks, non-root containers, GitHub Actions, Nginx reverse proxy, and deployment workflows for web backends.
category: web-development
platforms: [linux, macos, windows]
---

# DevOps & CI/CD

Practical backend DevOps patterns for building, testing, and deploying web applications safely.

## Core Topics

### Docker Production Hardening
- Multi-stage builds: builder/runtime separation
- Slim base images
- Non-root user inside containers
- Healthcheck integration
- Environment variable configuration

### CI/CD
- GitHub Actions pipeline setup
- Matrix testing
- Service containers (e.g. Postgres)
- Cache usage for dependency speedups
- SSH-based deployment patterns
- Concurrency controls to avoid duplicate deploys

### Reverse Proxy / Nginx
- TLS 1.3
- Rate limiting per IP
- Security headers
- Structured logs
- Proxy pass and upstream management

### Networking
- Shared network patterns across containers
- External Docker network for isolated services
- Avoid exposing unnecessary ports to host

## Implementation Notes

### Reference Artifacts
- Dockerfile templates
- docker-compose patterns
- GitHub Actions workflows
- Nginx configs

### Best Practices
- Prefer immutable builds
- Keep runtime images minimal
- Add healthchecks before routing traffic
- Use least privilege across containers

## Triggers
- "docker", "ci/cd", "github actions", "nginx", "reverse proxy", "healthcheck", "deployment"