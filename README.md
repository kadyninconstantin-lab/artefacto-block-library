# artefacto-block-library

Static + Jinja2 HTML block library for the [`lp-generator`](https://github.com/kadyninconstantin-lab/lp-generator) project. Each block is a self-contained HTML fragment with inline `<style>` (Artefacto `.af-*` class prefix) that is composed by the assembler into a full landing page.

## Layout

- `blocks/*.html` — static blocks (BS4 content_overrides at assembly time).
- `blocks/*.html.j2` — Jinja2 repeater blocks (segments, FAQ, process steps, etc.) rendered with `items=...`.
- `blocks/_custom_placeholder.html` — sentinel for the `id="custom"` manifest entry; never rendered (Session E).
- `index.html` — block-library showcase / preview page.
- `js/gc-date-localizer.js` — client-side date localization snippet (Session A).

## Conventions

- Class prefix `.af-{block-id}` (e.g. `af-hero-split`, `af-testimonials-grid`).
- Inline `<style>` per block — preprocessor hoists into shared block at assembly time.
- Per-block CSS variables `--af-*` are stripped at preprocess (overridden by the LP-level `:root` token block).
- Jinja2 blocks declare `repeater_item_schema` in `manifest/manifest.json`; the assembler renders with `items=[...]`.

## Linkage

- Manifest catalogue: `lp-generator/manifest/manifest.json` enumerates all blocks with `editable_fields`, `singleton`, `template_engine`.
- Assembler: `lp-generator/lpgen/assembler.py` reads block files at build time.
- Path expectation: `block-library/` is a sibling of `lp-generator/` (relative path `../block-library/` from lpgen).
