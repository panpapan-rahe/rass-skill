---
name: AI-web-project-maintenance
description: Prosedur pemeliharaan aplikasi web (Flask/Docker) dengan fokus pada environment staging/live.
---
# web-project-maintenance

## Overview
Prosedur untuk mengelola dan memelihara proyek web, khususnya aplikasi Flask dengan Docker (lingkungan multi-environment seperti live/staging).

## Best Practices
- **Environment Verification FIRST:** Sebelum melakukan perubahan apa pun, SELALU verifikasi branch git aktif, port yang sedang diakses, dan nama container untuk memastikan Anda berada di environment yang benar (staging vs live). User sangat sensitif terhadap campur tangan langsung di live tanpa testing di staging.
- **Staging-First Workflow:** Selalu kerjakan perbaikan bug dan fitur baru di branch `staging` (atau branch fitur terpisah), verifikasi secara menyeluruh di container staging, dan HANYA setelah user memberikan persetujuan eksplisit baru merge ke `master` untuk deployment live.
- **Environment Separation:** Selalu pastikan environment (`staging` vs `live`) terisolasi dengan data yang terpisah. Jangan biarkan production dan staging memakai folder data host yang sama; idealnya database berada di direktori shared khusus di luar folder runtime kedua environment.
- **External Data Root Pattern:** Jika repo harus tetap satu, pindahkan data ke folder di luar repo, misalnya `.../cashflow-data/prod` dan `.../cashflow-data/staging`, lalu mount masing-masing environment ke path tersebut.
- **Repo/Backup Boundary:** Untuk backup atau pemulihan, bedakan dengan tegas antara folder kode repo (`cash-flow-journal`) dan folder data eksternal (`cashflow-data`). Jangan gunakan istilah “staging cleanup” untuk menghapus root repo; itu berisiko menghapus production code saat yang dimaksud hanya environment-side files.
- **Data Synchronization Protocol:** Ketika diperlukan untuk menyalin data antar environment, salin dari root data eksternal ke target yang benar (bukan dari folder runtime/container mount yang sedang aktif), lalu rebuild/restart environment target.
- **Selective Cleanup Rule:** Before deleting anything with `rm -rf`, confirm whether the user wants only the environment-specific config/data or the entire repository checkout. Never assume “staging cleanup” means deleting the main project folder.
- **Runtime Verification Before Cleanup:** Always run `docker ps` and `docker inspect <container>` to confirm which container is running and which host paths are mounted before removing folders or moving databases.
- **GitHub Push/Delete Branch Auth:** If `git push` or remote branch deletion fails because GitHub asks for credentials, first verify whether the repo remote is HTTPS or SSH. If HTTPS keeps prompting, switching the remote to SSH and validating with `ssh -T git@github.com` is a clean fix when an SSH key is available.
- **Remote Branch Hygiene:** After deleting a branch on GitHub, run `git fetch --prune` locally to remove stale `origin/<branch>` references.

    - **DOM Guards:** Gunakan pengecekan keberadaan elemen (`if (el) { ... }`) sebelum menambahkan event listener untuk menghindari `TypeError: Cannot read properties of null`.
    - **Source Integrity:** Jangan mencampur file CSS dan JS. Jangan memuat file CSS sebagai `<script src="...">`.
- **Container Management:** Setelah perubahan kode atau compose file, selalu rebuild dan restart container yang sesuai (`docker compose -f [file].yml up -d --build`). Perhatikan peringatan tentang orphan containers.
- **Consistency:** Pastikan sinkronisasi data antar environment dilakukan secara eksplisit dengan persetujuan user sebelum melakukan tindakan destruktif (seperti `rm -rf`).
- **Legacy Script Cleanup:** Secara berkala cari dan hapus kode dinamis yang tidak digunakan (orphaned script tags, file sumber daya dengan ekstensi yang salah) untuk mencegah kesalahan runtime dan menjaga aplikasi tetap ringkas.

## Pitfalls
- **Live-First Mistake:** Menghapus atau mengubah fitur di live sebelum testing di staging adalah kesalahan kritis yang dapat merusak pengalaman pengguna. Selalu verifikasi bahwa Anda berada di environment yang benar sebelum melakukan perubahan.
- **Mismatched Data:** Jangan berasumsi staging memiliki data yang sama dengan live tanpa melakukan sinkronisasi eksplisit.
- **Orphan Containers:** Perhatikan peringatan Docker tentang container yang tidak terdaftar di compose file saat rebuild.
- **Sync Issues:** Selalu verifikasi status branch git dan container yang sedang berjalan (`docker ps`) sebelum melakukan tindakan perbaikan.
- **Environment Confusion:** Menganggap bahwa perubahan di satu environment otomatis tersinkron ke environment lain tanpa tindakan eksplisit.
- **Unguarded DOM Access:** Mengakses properti atau menambahkan event listener ke elemen yang mungkin tidak ada tanpa pengecekan null akan menyebabkan runtime error yang dapat menghentikan eksekusi JavaScript selanjutnya.
- **Mixed Asset Types:** Memuat file CSS sebagai JavaScript atau sebaliknya akan menyebabkan syntax error yang mencegah aplikasi berjalan dengan benar.
- **Legacy Script Accumulation:** Tidak menghapus script HTML yang tidak digunakan yang menyebabkan error inisiasi saat halaman dimuat.
- **Unverified Container Cleanup:** Menghapus container atau volume tanpa verifikasi yang tepat dapat menyebabkan hilangnya data.
- **Overreliance on Staging:** Percaya bahwa staging sepenuhnya mencerminkan produksi dapat menyebabkan masalah selain integrasi.
- **Form Button Default Action:** Tombol di dalam `<form>` default ke `type="submit"`; tombol aksi seperti hapus harus selalu diberi `type="button"` agar tidak memicu submit diam-diam.
- **Template Literal Scope Confusion:** Saat merender tombol dari `.map()`, pastikan variabel interpolasi tetap berada di template literal (`${acc.id}`), jangan tertulis literal `acc.id` di HTML.
- **Event Binding Reliability:** Jika tombol yang dirender inline tidak merespons, prefer `data-*` + event delegation pada container atau `document` agar listener tetap aman saat DOM dirender ulang.
- **Toast Migration Completeness:** Saat mengganti `alert()` ke toast, cari dan ganti seluruh panggilan yang relevan dalam satu sweep; sebagian yang tertinggal akan membuat UX terasa setengah jadi.

## Technical Patterns
### DOM Guard Pattern
```javascript
const element = document.getElementById('element-id');
if (element) {
    element.addEventListener('event', handler);
    // atau
    element.value = 'some value';
}
```

### Environment Verification Steps
1. `git branch --show-current` - verify branch (should be staging for development)
2. `docker ps` - verify which containers are running and on which ports
3. Confirm URL/port matches intended environment (localhost:9101 for staging, localhost:9102 for live in this project)
4. Get explicit user confirmation before making changes to live environment

### Data Sync Procedure (with user consent)
```bash
# From project root
rm -rf data-staging/*          # Clear staging data (WARNING: data loss!)
cp -a data/* data-staging/     # Copy live data to staging
docker compose -f docker-compose.staging.yml up -d --build  # Rebuild and restart staging
```

## Workflow Example
1. User requests feature/bug fix
2. Developer verifies they are on staging branch (`git branch --show-current` returns `staging`)
3. Developer makes changes in feature branch or directly on staging
4. Developer tests changes in staging container (`http://localhost:9101`)
5. User reviews and approves changes in staging
6. Developer merges to master branch
7. User approves deployment to live
8. Deployment to live environment occurs

### Pitfall: Settings Tab Sync
If the list rekening doesn't appear immediately upon opening the Settings modal, verify:
- Initial render call in the `btnSettings` click handler
- That `loadAccountsSettings()` is correctly linked and panel visibility is toggled (e.g., `document.getElementById('content-accounts').style.display = 'block'`)
- Ensure the active class is set on the tab before the fetch completes
- **Auto-Load Logic:** If Settings is a separate page (not a modal), ensure `loadAccountsSettings()` and `loadCategoriesSettings()` are triggered on `DOMContentLoaded` or through a dedicated initial check.

### Pitfall: DOMContentLoaded Race Condition
When using separate pages for settings and other dashboards, ensure initial data loads (like account/category lists) are triggered after `checkAuth()` or inside `DOMContentLoaded` using a guard to check if the specific element (`accounts-settings-body`) exists on that page to avoid errors.

## Pitfall: Button Scope
Be careful when moving buttons between HTML panels (`accounts` tab vs `extra` tab). Ensure the JavaScript event listener `getElementById` targeting the button IDs is matched with the HTML ID and the button is only moved, not duplicated in the DOM. Use guards: `if (buttonElement) { ... }`.

### Pitfall: HTML Form Element Default Action
When placing buttons inside an HTML `<form>` (like in a modal), remember that buttons without an explicit `type` attribute default to `type="submit"`. This can cause forms to submit and reload the page when you intended for the button to trigger a JavaScript function (e.g., `onclick="deleteAccount(id)"`).
**Always explicitly set `type="button"` for non-submit buttons in forms.**

### Pitfall: Responsive Grid Layout for Summary Cards
When implementing a multi-column layout for summary cards (like Balance and Debt), ensure they are placed within a single container grid (e.g., `grid grid-cols-1 md:grid-cols-2`) rather than nesting containers that inadvertently break the grid. Ensure each card is an independent child element of the grid container.
**Use `grid-cols-1 md:grid-cols-2` and verify that each card is a direct child to prevent layout nesting issues.**

## Recent Improvements to Cashflow Web App
### Summary Cards Fix
The `updateSummaryCards()` function in `app.js` was causing inconsistent dashboard displays. The problem was that it used multiple separate fetches (for account balances and debts) that could complete in any order, leading to race conditions.

**Solution:** Use a single API call to `/api/summary` which contains both total balance and total debt in one consistent response.

### DOM Guard Pattern Implementation
Fixed multiple `TypeError: Cannot read properties of null (reading 'addEventListener')` errors by adding null checks before adding event listeners:
- `btnSettings` guard in settings modal
- `payModal` and `payForm` guards in debt payment functionality

### Asset Type Consistency
## Recent Improvements to Cashflow Web App
### Summary Cards Fix
The `updateSummaryCards()` function in `app.js` was causing inconsistent dashboard displays. The problem was that it used multiple separate fetches (for account balances and debts) that could complete in any order, leading to race conditions.

**Solution:** Use a single API call to `/api/summary` which contains both total balance and total debt in one consistent response.

### Button System Standardization
Implemented comprehensive button system across all modals to ensure consistent styling, spacing, and behavior.

**Components:**
- **Primary Actions:** `btn-primary` - Main submit/save buttons
- **Secondary Actions:** `btn-secondary` - Cancel/close buttons  
- **Danger Actions:** `btn-danger` - Delete/remove buttons
- **Warning Actions:** `btn-warning` - Secondary warning buttons
- **Outline Buttons:** `btn-outline` - Tertiary action buttons
- **Link Buttons:** `btn-link` - Navigation/secondary actions

**Applied to:** Debt modal, Pay Debt modal, Settings modals, all forms

### Form Field Standardization
Standardized form input styling across all pages:
- Consistent borders, padding, and focus states
- Unified input backgrounds and text styling
- Standardized label alignment and spacing
- Consistent form action button layouts

### HTML Form Element Pitfall
**Always explicitly set `type="button"` for non-submit buttons in forms.** Form buttons without explicit `type` default to `type="submit"` which can trigger form submission when unintended.

### Modal Layout Pitfall
Ensure summary cards are placed within a single grid container:
**Use `grid grid-cols-1 md:grid-cols-2` and verify that each card is a direct child to prevent layout nesting issues.**

## Recent Improvements to Cashflow Web App
### Modal Structure Standardization
**Fixed inconsistent modal structures** - Standardized all modals to use a single container instead of duplicate nested containers.

**Before:**
```html
<section class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
    <div class="card-1">...</div>
</section>
<section class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">  <!-- Duplicate! -->
    <div class="card-1">...</div>
    <div class="card-2">...</div>
</section>
```

**After:**
```html
<section class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
    <div class="card-1">...</div>
    <div class="card-2">...</div>
</section>
```

### Asset Type Fix
Fixed CSS loader issue where CSS was being loaded as JavaScript in settings page:
- Replaced incorrect `<script src="...">` reference
- Removed redundant circular dependency in settings.js
