# Rass Skills

Collection of custom Hermes Agent skills maintained by Rahe. These skills are tailored for Rahe's workflows and home server environment.

---

## Skills

| Skill | Category | Description |
|-------|----------|-------------|
| `bible-study-with-rass` | note-taking | Create and maintain Bible study notes in `~/Hermes-Knowledge/inside-bible/` with exact filename conventions, content structure, and workflow. Merges former `bible-note-format`, `bible-study-template`, `inside-bible-format`, `inside-bible-notes`. |
| `file-management` | productivity | Comprehensive file organization and system navigation for structured file management and efficient system surfing. |
| `AI-frontend-developer` | web-dev-by-AI | Frontend learning skill built from zero with a weekly 4-phase loop: HTML/CSS/JS fundamentals, UI/UX/a11y/design system, component engineering, and review/performance. |
| `AI-backend-developer` | web-dev-by-AI | Backend learning skill reset from zero with a 4-level progression: Fundamental, Keamanan & Data, Skalabilitas, and Engineering. |

---

## Installation

These skills are designed to live in `~/.hermes/skills/rass-skill/`. To use them:

```bash
# Option 1: Clone directly into Hermes skills directory
git clone git@github.com:panpapan-rahe/rass-skill.git ~/.hermes/skills/rass-skill

# Option 2: If already cloned elsewhere, symlink
ln -s /path/to/rass-skill ~/.hermes/skills/rass-skill
```

Then in Hermes, load a skill with:

```text
skill_view(name="bible-study-with-rass")
skill_view(name="file-management")
skill_view(name="AI-frontend-developer")
skill_view(name="AI-backend-developer")
```

---

## Skill Details

### bible-study-with-rass

**Triggers:**
- "buat catatan alkitab" / "bible study" / "catat perikop"
- "Rass, aku baru membaca alkitab" (followed by passage sharing)

**Workflow:**
1. Observe existing notes in `~/Hermes-Knowledge/inside-bible/`
2. Look up pericope on LAI/SABDA for authoritative boundaries
3. Build filename: `YYMMDD_Kitab_UrutanPerikop_Pasal_Judul.md`
4. Draft content following the 7-section template with emoji headings
5. Mirror local house style exactly
6. Write file and auto-commit

**Filename Convention:**
```text
YYMMDD_Kitab_UrutanPerikop_Pasal_Judul.md
```

**Content Template:**
```markdown
# [Judul Perikop]
**[Kitab X:Y-Z]** | Terjemahan Baru (TB) LAI 1974

---

## 📋 Informasi Perikop
## 📖 Teks Ringkasan
## 🔍 Rincian Per Ayat
## 🔑 Poin Teologis
## 🌍 Konteks Historis & Lintas Kitab
## 💡 Refleksi & Aplikasi
## 📚 Catatan Tambahan
```

---

### file-management

General-purpose file organization and navigation skill. Use for:
- Structured folder creation
- Consistent naming conventions
- Efficient file search and retrieval
- System navigation enhancement

---

### AI-frontend-developer

Frontend learning skill reset from zero. It uses a daily loop with weekly phases:
- **Phase 1 — The Bedrock**: HTML Expert, CSS Expert, JavaScript Expert
- **Phase 2 — The Designer's Eye**: UI Designer, UX Reviewer, Accessibility Expert, Design System
- **Phase 3 — The Engineer**: Component Architect, React Expert, API Integration
- **Phase 4 — The Polisher**: Frontend Reviewer, Performance Expert, Frontend Mentor

**Daily rhythm:** theory → lab → application → audit → next iteration

---

### AI-backend-developer

Backend learning skill reset from zero. It uses a 4-level progression:
- **Level 1 — Fundamental**: API Architect, Business Logic, Database Architect, Validation
- **Level 2 — Keamanan & Data**: Authentication, Authorization, Security, File Storage
- **Level 3 — Skalabilitas**: Queue, Background Worker, Caching, Performance
- **Level 4 — Engineering**: Testing, Logging, Monitoring, Architecture, DevOps Integration, Backend Reviewer

**Daily rhythm:** one micro-topic, one experiment, one update

---

## Contributing

These are personal skills for Rahe's workflow. If you find them useful, feel free to fork and adapt.

---

## License

Personal use.
