# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the App

```bash
# Install dependencies (in venv)
pip install -r requirements.txt

# Run dev server (port 5001)
python app.py
```

## Running Tests

```bash
pytest
# or a single test file
pytest tests/test_foo.py
```

## Architecture

**Stack:** Flask + Jinja2 + SQLite + plain CSS/JS. No frontend build step — all assets are served directly from `static/`.

**Entry point:** `app.py` — all routes live here. Renders templates from `templates/` using `render_template`.

**Templates:** `base.html` is the shared shell (navbar, footer, font imports, `style.css`, `main.js`). All other templates extend it via `{% extends "base.html" %}` and fill `{% block content %}` / `{% block scripts %}`.

**Styling:** A single file, `static/css/style.css`, uses CSS custom properties defined in `:root` (`--ink`, `--accent`, `--paper`, `--font-display`, etc.). All components reference these variables — do not hardcode colors or fonts.

**JavaScript:** `static/js/main.js` is loaded globally via `base.html`. Page-specific JS goes in `{% block scripts %}` in each template (see the video modal in `landing.html` for the pattern).

**Database:** `database/db.py` will expose `get_db()`, `init_db()`, and `seed_db()` using SQLite with `row_factory` and foreign keys enabled. Not yet implemented — placeholder stubs only.

## Project Structure Notes

- Several routes in `app.py` are intentional placeholders (logout, profile, add/edit/delete expense) returning plain strings — they are meant to be implemented in sequence.
- The `expected_design.png` / `generated_design.png` files in the root are design reference images, not application assets.
- `venv/` and `expense_tracker.db` are gitignored.
