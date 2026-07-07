# Toast and Alert Rollback Notes for Cashflow Web

Session learnings:
- Toasts were added in `app/static/app.js`, but transaction-page actions still used `app/static/transactions.js`.
- User reported toast not visible after hard refresh; simplest reliable fix was to rollback to `alert()` popups.
- Future migrations should sweep all page-specific bundles and verify with `search_files` for both `alert(` and `showToast(`.

Practical sequence:
1. Search all JS for `alert(` and `showToast(`.
2. Patch both `app.js` and page-specific bundles (`transactions.js`, etc.).
3. Rebuild staging (`docker compose -f docker-compose.staging.yml up -d --build`).
4. If UX still fails in practice, revert to alert for reliability.