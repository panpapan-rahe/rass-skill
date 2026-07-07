# Flask Blueprint Refactor Notes

Session-derived workflow for refactoring a Flask app into a scalable layout without breaking runtime.

## Practical sequence used
1. **Rename templates/statics first** into a clearer tree.
2. **Update render paths** in the current entrypoint.
3. **Validate runtime** with a real restart and a few HTTP checks.
4. **Split routes into Blueprints** in slices:
   - auth + page routes first
   - transaction/debt/master-data routes next
5. **Create an app factory** in `app/__init__.py` and register blueprints there.
6. **Move shared logic into `services/`** after the route split is stable.
7. **Commit + push after each stable slice**.

## Pitfalls discovered
- Don’t delete the old route module until the new blueprint is registered and the app boots cleanly.
- Keep URL routes stable while changing internal template paths.
- When refactoring shared helpers, extract the helper first into `services/`, then replace inline logic in routes.
- For route modules, prefer thin handlers that validate input and call service functions.

## Verification pattern
- Start/restart the app/container.
- Check `/login` first.
- Then verify the protected page routes redirect as expected when not logged in.
- Confirm blueprint registration by importing `create_app()` and inspecting `app.blueprints.keys()`.

## Related skill pointers
- See the parent skill's section: **Flask/Blueprint Refactor Workflow**.
