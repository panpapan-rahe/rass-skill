# Iterative Staged Debugging Pattern

When debugging a broken web app (Flask + JS frontend) with multiple simultaneous errors:

## Pattern
1. **Reset to last known good state** — `git reset --hard <stable-commit>` to eliminate all experimental changes and get a clean baseline.
2. **One error at a time.** Take all user-reported errors, but fix only ONE per iteration.
3. **Confirm with user after each fix.** Let them hard-refresh and report which errors remain and which are resolved.
4. **Re-patch on the clean base.** Don't accumulate speculative patches.
5. **Guard DOM listeners BEFORE fixing UI logic.** Null-guards (`if (el)`) prevent JS execution from stopping, enabling subsequent code to run even when some elements are missing.

## Symptoms from this session (Cashflow Web v1.5.0)
- `Uncaught TypeError: Cannot read properties of null (reading 'addEventListener')` at multiple lines (303, 364, 412, etc.) — resolved by guarding all `addEventListener` calls.
- Tab switching not working in settings — caused by CSS class selector mismatch: JS used `.settings-nav-item` / `.settings-panel`, HTML used `.settings-tab` / `.settings-content`.
- List rekening did not appear on first open — needed `loadAccountsSettings()` call in the `btnSettings.click` handler immediately, not just on tab-switch.
- Button "Hapus Akun" appeared in the wrong tab — check both HTML placement AND JS event listener target element ID.
- Category badges missing — added visual distinction with inline badge styling (`bg-emerald-100 text-emerald-700` / `bg-red-100 text-red-700`).

## Integration Notes
Always match the HTML layer structure with the JS event listener layer. Triple-check every `getElementById` and `querySelectorAll` call when classes or IDs change in templates.
