# Rass Skills

Collection of custom Hermes Agent skills maintained by Rahe. These skills are tailored for Rahe's workflows and home server environment.

---

## Skills

| Skill | Category | Description |
|-------|----------|-------------|
| `bible-study-with-rass` | note-taking | Create and maintain Bible study notes in `~/Hermes-Knowledge/inside-bible/` with exact filename conventions, content structure, and workflow. Merges former `bible-note-format`, `bible-study-template`, `inside-bible-format`, `inside-bible-notes`. |
| `file-management` | productivity | Comprehensive file organization and system navigation for structured file management and efficient system surfing. |

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
```
skill_view(name="bible-study-with-rass")
# or
skill_view(name="file-management")
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
```
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
## �
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

## Contributing

These are personal skills for Rahe's workflow. If you find them useful, feel free to fork and adapt.

---

## License

Personal use.