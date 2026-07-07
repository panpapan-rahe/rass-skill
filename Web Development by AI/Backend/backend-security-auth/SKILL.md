---
name: backend-security-auth
description: Backend security, authentication, TLS, CSP, CORS, rate limiting, and OWASP-oriented hardening practices.
category: web-development
platforms: [linux, macos, windows]
---

# Server Security & Auth

Security-first backend practices for hardening web applications and protecting user data.

## Core Topics

### OWASP Mindset
- Treat security as layered defense, not one feature
- Focus on prevention + detection + response
- Common classes: injection, broken access control, security misconfiguration

### HTTPS / TLS
- Encrypt data in transit
- Basic certificate and reverse proxy TLS setup
- Prefer modern ciphers and strong protocol versions

### Input Validation
- Validate all request payloads
- Sanitize and normalize before storage/use
- Defensive coding against XSS/SQLi/path traversal

### CSP & CORS
- **CSP** baseline: `default-src 'self'`, `object-src 'none'`, `base-uri 'self'`, `frame-ancestors 'none'`
- Use nonce/hash for inline scripts only when needed
- **CORS**: never use wildcard `*` for sensitive APIs; reflect origin selectively

### Rate Limiting
- Sliding window rate limiting for bursty traffic
- Apply per-IP or per-account as appropriate
- Expose useful rate limit headers

### Auth Patterns
- Session-based auth vs token-based auth trade-offs
- Authorization checks must be server-side, always
- Protect sensitive routes with explicit access control

## Implementation Notes

### Experiments / Reference
- Security middleware experiments created during learning sessions
- Flask security patterns and backend auth hardening are part of the knowledge base

### Best Practices
- Use secure cookies where possible
- Set `HttpOnly`, `Secure`, and `SameSite`
- Log auth failures for observability (without leaking secrets)
- Rotate secrets and avoid hardcoding credentials

## Triggers
- "security", "auth", "jwt", "csp", "cors", "tls", "rate limiting", "owasp"