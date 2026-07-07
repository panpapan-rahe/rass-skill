---
name: flask-blueprint-refactor
description: Refactoring Flask applications into scalable Blueprint-based architecture. Practical patterns from Cashflow Journal project.
category: web-development
platforms: [linux, macos, windows]
---

# Flask Blueprint Refactor

Step-by-step guide for refactoring a monolithic Flask app into a scalable Blueprint-based structure.

## Why Blueprints?

Blueprints allow you to:
- Organize routes into logical modules
- Register routes dynamically
- Separate concerns: auth, pages, API
- Make testing easier
- Scale without a single massive `app.py`

## Refactor Workflow

### Step 1: Identify Route Groups
Group routes by function:
- **Auth routes**: `/login`, `/register`, `/logout`, `/forgot-password`
- **Page routes**: `/`, `/dashboard`, `/transactions`, `/accounts`, `/settings`
- **API routes**: `/api/transactions`, `/api/accounts`, `/api/debts`

### Step 2: Create Blueprint Files
For each group, create a separate file:
```
routes/
├── __init__.py      # imports all blueprints
├── auth.py          # auth blueprint
├── pages.py         # page blueprints
└── api.py           # API blueprints
```

### Step 3: Convert Route-by-Route
1. Move routes in small, testable slices (auth/pages first, then API groups)
2. Convert each to Blueprint format:
   ```python
   from flask import Blueprint
   auth_bp = Blueprint('auth', __name__, url_prefix='/auth')
   
   @auth_bp.route('/login', methods=['GET', 'POST'])
   def login():
       ...
   ```

### Step 4: Register Blueprints
In your main `app.py` or factory:
```python
def create_app():
    app = Flask(__name__)
    from routes import auth_bp, pages_bp, api_bp
    
    app.register_blueprint(auth_bp)
    app.register_blueprint(pages_bp)
    app.register_blueprint(api_bp)
    return app
```

### Step 5: Extract Business Logic
After runtime boots cleanly:
1. Move complex logic into `services/` module
2. Keep route handlers thin — they should only:
   - Parse request
   - Call service
   - Render response

### Step 6: Verify Each Slice
After each slice refactor:
1. Start the app
2. Test key endpoints (`/login`, dashboard, API health)
3. Only commit after verification passes

## Key Principles

### URL Stability
- Keep template/static renames internal to Flask paths
- Browser URLs should stay stable unless intentionally changed
- This preserves bookmarked links and SEO

### Template Organization
- Group templates by Blueprint: `templates/auth/`, `templates/pages/`, `templates/api/`
- Use Jinja2 `{% extends %}` for shared layouts

### Static Files
- Organize by concern: `static/auth/`, `static/pages/`, `static/api/`
- Or keep a flat structure with namespaced folders

## Common Pitfalls

| Pitfall | Prevention |
|---------|------------|
| Circular imports | Use lazy imports in `__init__.py` |
| Broken URLs after refactor | Test all routes before committing |
| Blueprint registered twice | Check `app.register_blueprint()` called once |
| Lost static/template paths | Use `url_for('static', filename='...')` correctly |

## Real-World Reference

This pattern was used to refactor **Cashflow Journal**:
- Original: single `app.py` with all routes
- After: `auth_bp`, `pages_bp`, `api_bp` separated
- Result: cleaner code, easier testing, clearer ownership

## Triggers
- "flask", "blueprint", "refactor", "scale flask", "organize routes"