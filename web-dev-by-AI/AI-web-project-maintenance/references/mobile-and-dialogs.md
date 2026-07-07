# Cashflow UI debug notes (session reference)

- Page-specific bundles matter:
  - `app/templates/index.html` -> `app/static/app.js`
  - `app/templates/settings.html` -> `app/static/app.js`
  - `app/templates/transactions.html` -> `app/static/transactions.js`
- When migrating from native browser dialogs to custom dialogs, update **all entrypoints**; otherwise one page can keep using the old interaction.
- A custom confirm helper must not silently fall back to `window.confirm()` or the browser-native prompt will still appear (`... says:`). If the UX must be fully custom, create the overlay/modal unconditionally.
- If a popup works on one page but not another, verify the helper exists in that page bundle; do not assume shared helpers are globally loaded.
- Separate feedback types: success, warning, error, and confirm should be implemented and tested independently.
- For mobile responsiveness in this app, the highest-impact first fix is stacking the main layout (`flex-col` on mobile, `flex-row` on desktop) and making the sidebar full-width on small screens.
- After changing layout or dialogs, rebuild staging and validate the specific page bundle again.
