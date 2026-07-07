---
name: bible-study-with-rass
description: Create and maintain Bible study notes in the user's inside-bible vault with the exact filename and markdown structure used in the Hermes-Knowledge archive. Merges bible-note-format, bible-study-template, inside-bible-format, and inside-bible-notes into a single comprehensive workflow.
category: note-taking
platforms: [linux, macos, windows]
---

# Bible Study with Rass

**Single authoritative skill for creating Bible study notes in `~/Hermes-Knowledge/inside-bible/`.**

This skill consolidates all previous Bible note skills into one complete workflow: filename conventions, content structure, style rules, and step-by-step execution process.

---

## Core Principle

**Mirror the local house style.** Before drafting anything, inspect 1–3 adjacent notes in the target folder and replicate their exact structure, tone, emoji usage, and naming pattern. The existing files are the source of truth—not memory, not generic templates.

---

## 1. FILENAME CONVENTION (Identity)

### Pattern
```
YYMMDD_Kitab_UrutanPerikop_Pasal_Judul.md
```

### Fields
| Field | Format | Example |
|-------|--------|---------|
| `YYMMDD` | Date of note creation (today) | `240807` |
| `Kitab` | Bible book name, Indonesian, capitalized | `Kejadian` |
| `UrutanPerikop` | 3-digit running pericope order within the book | `015` |
| `Pasal` | 3-digit chapter number of the passage | `001` |
| `Judul` | Pericope title in Indonesian, words separated by underscores | `Kunjungan_Ananias_Dan_Safir` |

### Rules
- **Authority for pericope boundaries & titles:** LAI/SABDA passage pages. Do not invent splits from memory.
- **Internal numbering:** `UrutanPerikop` = running order within the book/folder sequence. `Pasal` = biblical chapter number. Keep them distinct.
- **Inspection required:** Always read the latest files in the folder first to determine the next `UrutanPerikop`. Do not guess or shift numbering unless explicitly asked.
- **Separators:** Underscore `_` only. No spaces in filename.

---

## 2. CONTENT TEMPLATE (Architecture)

Every note **must** contain these sections in this exact order, with these exact emoji headings:

```markdown
# [Judul Perikop]
**[Kitab X:Y-Z]** | Terjemahan Baru (TB) LAI 1974

---

## 📋 Informasi Perikop
- **Kitab:** [Nama Kitab] ([bahasa asli] / [transliterasi])
- **Perikop:** [Nama Perikop]
- **Ayat:** [Ayat]
- **Penulis:** [Penulis] (tradisi)
- **Konteks:** [1-2 kalimat konteks]

---

## 📖 Teks Ringkasan
> *\"[Kutipan ayat kunci]\"* ([Ayat])

[Ringkasan naratif 1-3 paragraf]

---

## 🔍 Rincian Per Ayat
### Ayat X-Y — [Judul bagian]
- Penjelasan per ayat dengan format bullet

---

## 🔑 Poin Teologis

### 1. [Judul poin]
- Penjelasan

### 2. [Judul poin]
- Penjelasan

---

## 🌍 Konteks Historis & Lintas Kitab

### Perbandingan (jika relevan)
| Aspek | Kejadian | Mitologi Lazim |
|-------|----------|----------------|

### Kutipan Lintas Kitab
- **[Kitab:Ayat]** — kaitan

---

## 💡 Refleksi & Aplikasi
1. [Refleksi 1]
2. [Refleksi 2]

---

## 📚 Catatan Tambahan
- [Catatan teknis, terjemahan, dsb]
```

### Style Rules
- **Language:** Indonesian primary, technical terms in English/Hebrew/Greek when needed.
- **Verse quotes:** Use blockquote `>` for the key verse in Teks Ringkasan.
- **Emphasis:** `**bold**` for key terms, `*italic*` for foreign terms and titles.
- **Headings:** `##` for sections (never `#` — reserved for title).
- **Bullets:** Single-level bullets for detail sections; numbered lists for Refleksi.
- **Tables:** Use markdown tables for historical comparisons when relevant.
- **Tone:** Devotional-academic — structured, scannable, reflective but not chatty.
- **Cross-references:** Minimum 1 lintaskitab citation in Konteks Historis section.

---

## 3. EXECUTION WORKFLOW (Process)

Follow these steps **in order** for every new note:

### Step 1: Target & Observe
1. Navigate to `~/Hermes-Knowledge/inside-bible/`
2. List directory contents (`search_files target=files pattern=**/inside-bible/*`)
3. Read 1–3 adjacent notes (same book, recent dates) to extract:
   - Title line style
   - Reference line format
   - Emoji usage (confirm all 7 emojis match)
   - Bullet depth and prose density
   - Any folder-specific quirks

### Step 2: Pericope Data (LAI/SABDA)
1. Look up the target passage on LAI/SABDA to get:
   - Exact pericope title
   - Verse boundaries
   - Confirm "TB LAI 1974" as translation label
2. Determine:
   - Book name (Indonesian)
   - Next `UrutanPerikop` (3-digit, zero-padded)
   - `Pasal` (3-digit chapter)
   - Clean title for filename (underscores, Indonesian)

### Step 3: Build Filename
Construct: `YYMMDD_Kitab_UrutanPerikop_Pasal_Judul.md`
Verify against existing files — no duplicates, correct sequence.

### Step 4: Draft Content
Write the full note following the **Content Template** above.
- Fill every section (minimum 1-2 sentences per section).
- Use blockquote for exactly one key verse in Teks Ringkasan.
- Include at least 1 lintaskitab reference in Konteks Historis.
- Match the observed tone and bullet style from Step 1.

### Step 5: Mirror & Verify
Before saving:
- [ ] Filename matches convention exactly
- [ ] All 7 emoji headings present and in order
- [ ] Reference line format matches local pattern
- [ ] Bullet depth matches surrounding notes
- [ ] No missing required sections
- [ ] Tone matches "devotional-academic" house style

### Step 6: Write & Commit
1. `write_file` to `~/Hermes-Knowledge/inside-bible/<filename>`
2. Auto git commit (if repo initialized)

---

## COMMON PITFALLS

| Pitfall | Prevention |
|---------|------------|
| Guessing `UrutanPerikop` instead of inspecting folder | Always list + read latest files first |
| Confusing `UrutanPerikop` with `Pasal` | Remember: running order vs biblical chapter |
| Using generic template instead of local pattern | Step 1 (Observe) is mandatory |
| Skipping "Informasi Perikop" section | It's required — provides context |
| Inventing pericope boundaries from memory | Use LAI/SABDA as authority |
| Wrong emoji or heading level | Copy exactly from observed notes |
| Over-expanding into academic speculation | Keep it devotional-academic, scannable |

---

## SUPPORT FILES

Reference files in this skill's directory:
- `references/inside-bible-pericope-map.md` — Kejadian 1–9 pericope map & naming examples
- `references/kejadian-1-9-pericopes.md` — Detailed pericope list for Kejadian 1–9

Consult these when working on Kejadian passages to align with established numbering.

---

## TRIGGERS

Use this skill when user says:
- "buat catatan alkitab" / "bible study" / "catat perikop"
- "Rass, aku baru membaca alkitab" (followed by passage sharing)
- Any request to create/standardize a file in `inside-bible/`