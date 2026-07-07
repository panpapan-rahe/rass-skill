# Table Alignment & Consistency Pattern

## Overview
Pattern for creating aligned tables across Cashflow web pages, ensuring headers and body cells use identical spacing and alignment.

## Core Guidelines

### Padding Consistency
- All header cells (`<th>`) must use `py-3 px-3`
- All body cells (`<td>`) must use `py-3 px-3`
- Mixed padding (e.g., `pb-4 pt-2` mixed with `py-3`) breaks visual alignment

### Alignment Strategy
- Text columns: `text-left`
- Numeric columns: `text-right`
- Headers use same text alignment as body cells

### Examples Across the App

#### Dashboard Tables
- **5 Transaksi Terakhir**: Separation of `text-left` and `text-right` columns
- **Hutang**: Separate columns for "Bayar" and "Hapus" actions

#### Settings Tables
- **Rekening (Accounts)**: JS body has 8 columns — HTML must match
- **Kategori (Categories)**: Grid layout (not table) with consistent card styling

## Pitfalls to Avoid

### Column Count Mismatch
If JavaScript generates more `<td>` elements than the HTML `<th>` list, alignment breaks. Ensure HTML header matches the exact number of columns JS outputs, including empty state `colspan`.

### Settings Page Structure
Never stack multiple `patch` operations on a settings page; they can silently corrupt nested `<div>` closure. Prefer writing the complete file content when restructuring.

### Button Location
- "Hapus Akun" (Delete Account) belongs in **Extra** tab (danger zone)
- DO NOT move it to **Rekening** tab without updating JavaScript logic

## Quick Reference

### Header Cell (`<th>`)
```html
<th class="py-3 px-3 font-medium text-left">Text Column</th>
<th class="py-3 px-3 font-medium text-right">Numeric Column</th>
```

### Body Cell (`<td>`)
```html
<td class="py-3 px-3 text-sm text-left">Content</td>
<td class="py-3 px-3 text-sm text-right">123.456</td>
```

### CSS Button Styles
```css
.btn-circle {
    width: 32px;
    height: 32px;
    border-radius: 9999px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    transition: all 0.15s;
}

.btn-circle-success { background: #dcfce7; color: #16a34a; }
.btn-circle-success:hover { background: #bbf7d0; }

.btn-circle-danger { background: #fee2e2; color: #dc2626; }
.btn-circle-danger:hover { background: #fecaca; }
```

## Application Examples

### 1. Dashboard Debt Table
- Columns: Kebutuhan, Dari Rekening, Total, Dibayar, Sisa, Pelunasan, **Bayar**, **Hapus**
- Each action gets its own `<td text-right>` with `.btn-circle` buttons

### 2. Settings Account Table (HTML → JS)
- HTML header: 8 `<th>` elements matching JS body columns
- JS generates 8 `<td>` elements
- Empty state: `<td colspan="8">` matches total columns

### 3. Category Grid (Non-Table Layout)
- Uses CSS grid: `grid grid-cols-2 md:grid-cols-4 gap-3`
- Cards: `border border-warm-100 rounded-lg bg-warm-50 p-3`
- Split into separate income/expense grids

## Recent Fixes Applied

### Debt Actions
- Split single "debt-actions" `<td>` into separate columns for "Bayar" (left) and "Hapus" (right)
- Each column uses `text-right` for alignment

### Category Badges
- Removed redundant type badges from category cards (income/expense)
- Cards now focus on name + Hapus button

### Account Table Header
- Added missing columns: "Mutasi Keluar" and "Mutasi Masuk" to match JS body
- Updated `colspan` from 6 to 8 in empty state

## Maintenance Notes

### Patching an Individual Page
When only one page needs updating (e.g., only Debt table):
1. Write complete HTML for the entire page (not stacked patches)
2. Ensure JS function for that page also has updated column count

### Verify After Changes
After any table/patch update:
1. Check HTML header matches JS column count
2. Verify empty-state `colspan` matches total columns
3. Run `git diff HEAD~` to see changes vs previous commit
4. Rebuild (`docker compose -f docker-compose.staging.yml up -d --build`) and test hard refresh

## References
- `references/iterative-debugging-pattern.md`
- `references/table-alignment-pattern.md`

## Quick Checklist
- [ ] Headers use `py-3 px-3` with matching alignment
- [ ] Body uses `py-3 px-3` with matching alignment
- [ ] Column counts match between HTML and JS
- [ ] Empty-state `colspan` matches total columns
- [ ] Buttons have separate `<td>` cells where needed