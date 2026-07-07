---
name: AI-frontend-developer
description: "AI-driven web development knowledge base — modern stack, best practices, frameworks, responsive design, a11y, performance. Auto-updates via cron job. No restrictions on learning scope."
version: 1.0.0
author: Rass (AI-driven autodidact)
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [web, frontend, html, css, javascript, nextjs, tailwind, astro, responsive, a11y, performance]
    related_skills: []
---

# AI Web Developer

> AI-driven web development knowledge base. This skill is managed via cron job and contains learned knowledge about modern web technologies.

## Overview

This skill serves as the central knowledge base for AI-driven web development learning. It covers:
- Modern HTML/CSS/JS
- Frontend frameworks (Next.js, Astro, Tailwind CSS)
- Backend integration
- Responsive design
- Accessibility (a11y)
- Performance optimization
- Deployment patterns

## Learning Path

Learning path will be defined through the autodidact cron job system.

## Reset Protocol

When the user asks for a fresh start, clear only the targeted subtree and rebuild from zero instead of carrying forward stale frontend notes.
- Remove stale frontend references and obsolete learning jobs.
- Keep the root skill as the single class-level umbrella.
- Recreate frontend knowledge only through the new curriculum.

See `references/frontend-reset-protocol.md` for the exact cleanup sequence used in this session.

## Quick Reference

Coming soon — content will be built through learning sessions.

## Best Practices

1. **Learn by doing**: Always experiment with code, not just reading.
2. **Apply to projects**: Transfer knowledge to real projects like Cashflow Journal.
3. **Document mistakes**: Note what doesn't work and why.
4. **Iterate**: Revisit and improve past understanding as skills grow.
5. **Use daily loops**: Break one phase into small micro-topics so every day produces a visible output.
6. **Reset cleanly when asked**: If the user asks for a from-zero restart, remove old frontend references, old cadence, and stale learning artifacts before rebuilding the curriculum.

## Autodidact Learning Loop

Frontend learning should follow a loop, not a one-way reading pipeline:
1. **Theory** — learn a focused micro-topic.
2. **Lab** — build a small standalone experiment.
3. **Application** — apply the lesson to a real project or a realistic slice.
4. **Audit** — review the result and record what needs to change.
5. **Next iteration** — refine the topic or move to the next micro-topic.

### Cadence
- Prefer **daily micro-topics** with a small deliverable each day.
- Group micro-topics into **weekly phases** instead of trying to cover a whole competence in one day.
- Ensure the user sees impact early; do not wait for a full cycle to produce useful output.

## Folder Structure
## Folder Structure

```
AI-web-developer/
├── SKILL.md           # Main skill entry point
├── references/        # Session-specific detailed notes
└── scripts/            # Reusable verification/generation scripts
```

## Frontend Curriculum (Rebuilt from Zero)

The frontend curriculum is organized into **4 phases**, each lasting ~1 week. Each phase groups related competencies, not one topic per day. Within each phase, learning happens in **daily micro-topics** to ensure consistent visible progress.

### Phase Structure

| Phase | Name | Duration | Key Competencies |
|-------|------|----------|------------------|
| 1 | The Bedrock | 1 week | HTML Expert, CSS Expert, JavaScript Expert |
| 2 | The Designer's Eye | 1 week | UI Designer, UX Reviewer, Accessibility Expert, Design System |
| 3 | The Engineer | 1 week | Component Architect, React Expert, API Integration |
| 4 | The Polisher | 1 week | Frontend Reviewer, Performance Expert, Frontend Mentor |

### Cadence Summary
- **Daily**: 1 micro-topic → 1 small deliverable → audit before moving on
- **Weekly**: complete one phase → review and adjust
- **Full cycle**: 4 weeks to go through all phases once

### Daily Update System
A cron job (`Frontend Daily Update 22:00`) delivers a short daily update in Indonesian to Discord channel `1523924526549958696` with:
1. Current phase
2. Today's micro-topic
3. Key learning / change
4. Experiment output
5. Next step

### Backfill / Manual Trigger Rule
If the user asks to cover a missed day (e.g. Monday replayed on Tuesday), treat it as a **manual trigger** and label the update clearly as a backfill for the missing day rather than pretending it happened on the current date.

See `references/frontend-reset-protocol.md` for the cleanup sequence and the cronjob/channel history used in this reset.

### Backfill / Manual Trigger Rule
If the user asks to cover a missed day (e.g. Monday replayed on Tuesday), treat it as a **manual trigger** and label the update clearly as a backfill for the missing day rather than pretending it happened on the current date.

See `references/frontend-reset-protocol.md` for the cleanup sequence and the cronjob/channel history used in this reset.

### Target Project for Application
Use the **Cashflow Journal** project (`~/Web-Projects/cash-flow-journal/`) as the main application target. Every learning loop should find a way to apply the new knowledge to this project's frontend templates.

- "frontend", "backend", "web development", "css", "javascript", "nextjs", "tailwind"
- "belajar frontend", "belajar web"
- "apa itu container queries", "apa itu server component"
- "reset frontend", "mulai dari nol", "bersihkan pembelajaran frontend"

## Version History

- 1.0.1 — Added frontend reset protocol and umbrella-skill guidance.
- 1.0.0 — Initial reset. Fresh start for AI-driven learning.