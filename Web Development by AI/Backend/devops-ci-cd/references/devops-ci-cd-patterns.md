# DevOps & CI/CD — Patterns & Templates (2025-2026)

> Referensi dari sesi autodidak Backend Kamis, 2026-07-02.
> Artefak eksperimen di `~/Web-Projects/devops-ci-cd/`.

## Lingkungan Server

Home server dengan Docker 29.5.3 + Docker Compose v5.1.4.
9 container aktif — lihat `docker ps` untuk status terkini.

### Jaringan Eksternal (`docker_network`)

Semua service inti (Nginx, AdGuardHome, JellyFin) terhubung ke `docker_network`:
- Subnet: `172.23.0.0/16`
- Driver: bridge
- Eksternal (`external: true`), dibuat manual sebelum compose up
- Pola: service yang perlu reverse-proxy di Nginx harus join network ini

```yaml
networks:
  docker_network:
    external: true  # Jangan recreate — shared antar compose files
```

### Infrastruktur Terpetakan

| Service | Container | Port | Image |
|---------|-----------|------|-------|
| Nginx Proxy Manager | Nginx | 443, 8080, 9998 | jc21/nginx-proxy-manager |
| AdGuardHome | AdGuardHome | 53, 9999, 8001 | adguard/adguardhome |
| JellyFin | JellyFin | 9001 | jellyfin/jellyfin |
| Cashflow (live) | cashflow-web | 9102 | custom (Flask) |
| Cashflow (staging) | cashflow-staging | 9101 | custom (Flask) |
| 9router | 9router | 20128 | decolua/9router |
| Recap Hardware | recap-hardware-scrt-app | 9103 | custom (FastAPI) |
| CamouFox | CamoFox | 9377 | camoufox |
| ExcaliDraw | ExcaliDraw | 9003 | excalidraw |

## Docker Multi-stage Build (Python Web App)

### Pola Builder + Runtime

```dockerfile
# Stage 1: Builder — install dependencies into venv
FROM python:3.11-slim AS builder
WORKDIR /build
RUN apt-get update && apt-get install -y --no-install-recommends gcc \
    && rm -rf /var/lib/apt/lists/*
RUN python -m venv /build/venv
ENV PATH="/build/venv/bin:$PATH"
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Stage 2: Runtime — minimal image, non-root user
FROM python:3.11-slim AS runtime
RUN apt-get update && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/*
COPY --from=builder /build/venv /venv
ENV PATH="/venv/bin:$PATH"
RUN groupadd -r app && useradd -r -g app -d /app -s /sbin/nologin app
WORKDIR /app
COPY app/ ./app/
USER app
HEALTHCHECK --interval=30s --timeout=5s --start-period=15s --retries=3 \
    CMD curl --fail http://localhost:8000/health || exit 1
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "--workers", "2", "app.main:app"]
```

### Key Points
- **Dependency caching**: Copy `requirements.txt` sebelum `COPY .` agar layer cache bekerja
- **`--no-cache-dir`**: Kecilkan image dengan tidak menyimpan cache pip
- **Non-root user**: `groupadd` + `useradd` + `USER app` — mitigasi container breakout
- **`curl` di runtime**: Hanya untuk healthcheck, bukan untuk aplikasi
- **`HEALTHCHECK`**: Docker built-in, bukan di level aplikasi — lebih reliable

## Docker Compose — Best Practices

### Healthcheck + Resource Limits + Networks

```yaml
services:
  app:
    build: .
    restart: unless-stopped
    ports:
      - "9102:8000"
    environment:
      - APP_LOG_LEVEL=${APP_LOG_LEVEL:-info}
    volumes:
      - app_data:/app/data
    healthcheck:
      test: ["CMD", "curl", "--fail", "http://localhost:8000/health"]
      interval: 30s
      timeout: 5s
      retries: 3
      start_period: 15s
    deploy:
      resources:
        limits:
          cpus: "0.5"
          memory: "256M"
        reservations:
          cpus: "0.1"
          memory: "64M"
    networks:
      - app_net
      - docker_network  # external shared network

volumes:
  app_data:
    driver: local

networks:
  app_net:
    driver: bridge
  docker_network:
    external: true
```

### Pola Profil (Optional Services)

Gunakan `profiles` untuk service opsional yang tidak perlu start setiap kali:

```yaml
  redis:
    image: redis:7-alpine
    profiles: ["full"]  # Hanya start dengan `--profile full`
```

## GitHub Actions CI/CD Pipeline

### Job Structure (Modern 2025-2026)

```
test (matrix: 3.11 + 3.12)
  ↓
build (Docker image build + GHA cache)
  ↓
deploy-staging (if branch=staging) ──┐
  ↓                                   ├→ notify (Discord)
deploy-production (if branch=main)  ──┘
```

### Key Patterns
- **Concurrency group**: `${{ github.workflow }}-${{ github.ref }}` — cancel-in-progress
- **Matrix testing**: `fail-fast: false` — jangan batalkan semua jika satu gagal
- **Service containers**: PostgreSQL container langsung di runner untuk integ test
- **Docker layer caching**: `type=gha` (GitHub Actions cache) — shared across runs
- **Environment protection**: GitHub Environments dengan required reviewers untuk prod
- **SSH deploy**: `appleboy/ssh-action` — langsung `docker compose up -d` di server
- **Post-deploy verification**: `curl --fail http://localhost:8000/health`
- **Discord notification**: Webhook dengan status deploy

### Template Lengkap

Lihat `~/Web-Projects/devops-ci-cd/scripts/ci-cd-pipeline.yml` untuk contoh pipeline lengkap dengan:
- Checkout → Setup Python → Cache pip → Ruff lint → Pytest coverage
- Docker meta (tag semver, SHA, branch) → Buildx → Login GHCR → Build + push
- Deploy staging via SSH → Deploy production via SSH
- Discord notifikasi

## Nginx Reverse Proxy

Lihat `~/Web-Projects/devops-ci-cd/nginx/cashflow-reverse-proxy.conf` untuk konfigurasi lengkap.

### Fitur yang Diimplementasikan

| Fitur | Detail |
|-------|--------|
| TLS 1.2 + 1.3 | Cipher modern, OCSP stapling |
| HSTS | `max-age=63072000; includeSubDomains; preload` |
| Security Headers | X-Content-Type-Options, X-Frame-Options, Permissions-Policy |
| CSP | Tight policy dengan fallback untuk inline scripts |
| Rate Limiting | `limit_req_zone` (30r/s) + `limit_conn_zone` (10 connection/IP) |
| JSON Structured Logging | Log format untuk aggregator (Grafana Loki, ELK) |
| Static File Caching | `Cache-Control: public, immutable`, expires 7d |
| Upstream Keepalive | 32 persistent connections ke backend |
| Health Check Endpoint | Exempt dari rate limiting |
| Sensitive Path Blocking | `.git`, `.env`, `.venv` → 404 |

## Monitoring Checklist

### Health Check Endpoint Pattern (Flask/FastAPI)

```python
@app.route('/health')
def health():
    return {
        "status": "ok",
        "timestamp": datetime.utcnow().isoformat(),
        "version": os.environ.get("APP_VERSION", "dev"),
        "uptime": time.time() - START_TIME,
    }
```

### Commands Cepat

```bash
# Cek semua container
docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Status}}\t{{.Ports}}"

# Cek jaringan
docker network ls && docker network inspect docker_network --format '{{.IPAM.Config}}'

# Cek healthcheck status
docker inspect --format='{{json .State.Health}}' <container>

# Cek log error Nginx
docker exec Nginx cat /data/logs/error.log | tail -20

# Prune unused
docker system prune -af --volumes
```
