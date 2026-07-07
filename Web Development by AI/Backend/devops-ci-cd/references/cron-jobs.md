# Web Dev Autodidak — Cron Job Reference

## Active Cron Jobs (2026-06-28)

### Backend — `128f67360c16`
- **Name**: "Web Dev Learning — Backend (23:00-23:30)"
- **Schedule**: `0 23 * * *` (daily at 23:00, but effectively Tue/Thu/Sat)
- **Deliver**: `discord:1520473323362849021`
- **Skill**: `web-development`
- **Last run**: 2026-06-28 07:40 (UTC) — status ok
- **History**: Testing & Quality (06-27), Auth & Framework Benchmark (06-28)

### Frontend — `f2fba12dfb68`
- **Name**: "Web Dev Learning — Frontend (23:30-00:00)"
- **Schedule**: `30 23 * * *` (daily at 23:30, but effectively Wed/Sun)
- **Deliver**: `discord:1520473323362849021`
- **Skill**: `web-development`
- **Last run**: never (first run triggered manually on 2026-06-28 ~15:41 WIB)
- **Status**: first-run pending result

## Delivery Discord
- Channel ID: `1520473323362849021`
- Format: Markdown report with sections (� topic, � eksperimen, 📝 update)

## Triggering Manually
```json
{"action": "run", "job_id": "128f67360c16"}  // backend
{"action": "run", "job_id": "f2fba12dfb68"}  // frontend
```

## Common Issues
- `job not found` = ID changed after recreate. Always list first to verify.
- Frontend previously had wrong ID `620077d9-90f5-4030-a572-81adaf0d6017` (deleted/recreated).
