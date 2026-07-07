# Toast & Confirm Dialogs Debug Notes

## What happened in this session
- The app had multiple frontend bundles: `app/static/app.js` for dashboard/settings and `app/static/transactions.js` for the transactions page.
- Replacing `alert()` in only the main bundle was insufficient; the transactions page kept using its own file.
- A custom popup introduced in one bundle did not work on another page until the same helper existed there too.
- `confirm()` calls remained visible because they are native browser dialogs; replacing them requires an explicit custom confirm modal, not just a toast helper.

## Durable lessons
- When users report missing notifications or dialogs, search **all page-specific bundles** in addition to the main bundle.
- Treat toast migration and confirm-dialog migration as separate tasks.
- Before declaring a UX migration done, scan for:
  - `alert(`
  - `confirm(`
  - page-specific JS entrypoints included by templates
- If the UX should be visible for both success and failure, add explicit success feedback too; error-only changes can feel like 'nothing happened'.

## Useful verification pattern
1. Search the frontend tree for `alert(` and `confirm(`.
2. Check each HTML template for the JS file it loads.
3. Apply the dialog helper to every loaded entrypoint.
4. Rebuild the relevant Docker environment.
5. Verify on the actual page, not just from a shared bundle assumption.
