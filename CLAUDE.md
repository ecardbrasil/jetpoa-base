# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This is the GitBook-synced documentation source for **Jetpoa Beach Club** (a beach club/venue on the Rio Jacuí, Porto Alegre). It contains no application code — only Markdown content that GitBook renders and syncs with. All content is in Brazilian Portuguese.

## Structure

- `.gitbook.yaml` — GitBook config; sets `docs/` as root, with `README.md` as the landing page and `SUMMARY.md` as the table of contents.
- `docs/SUMMARY.md` — defines the site's navigation tree. **Any new page must be added here** or it won't appear in GitBook's sidebar.
- `docs/README.md` — the site's landing/home page.
- `docs/informacoes-gerais/`, `docs/reservas/`, `docs/regras-da-casa/` — top-level content sections (general info, reservations, house rules). Subfolders with their own `README.md` represent a section landing page with nested sub-pages (e.g. `docs/reservas/nossos-espacos-ambientes/`).
- `docs/.gitbook/includes/` — reusable Markdown snippets (e.g. `endereco.md`, `contato.md`, `horario-de-funcionamento.md`) injected into pages via GitBook's `{% include "..." %}` block. Edit the include file once to update the value everywhere it's referenced, rather than editing every page that includes it.
- `docs/.gitbook/assets/` — images/media referenced by pages.

## Working conventions

- This repo has no build, lint, or test tooling — it is pushed straight to GitBook via git sync. There is nothing to run before committing.
- When adding a new page: create the `.md` file in the appropriate section folder, then add an entry to `docs/SUMMARY.md` at the correct nesting level.
- Prefer editing/adding an include in `docs/.gitbook/includes/` over duplicating repeated content (hours, address, pricing, contact info) across multiple pages.
- GitBook-specific syntax used throughout (preserve these when editing):
  - `{% include "path.md" %}` — embed a reusable snippet
  - `{% content-ref url="..." %}...{% endcontent-ref %}` — styled link card to another page
  - `{% hint style="info" %}...{% endhint %}` — callout box
  - `{% embed url="..." %}` — embedded external media (e.g. YouTube)

## graphify

This project has a knowledge graph at graphify-out/ with god nodes, community structure, and cross-file relationships.

Rules:
- For codebase questions, first run `graphify query "<question>"` when graphify-out/graph.json exists. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. These return a scoped subgraph, usually much smaller than GRAPH_REPORT.md or raw grep output.
- If graphify-out/wiki/index.md exists, use it for broad navigation instead of raw source browsing.
- Read graphify-out/GRAPH_REPORT.md only for broad architecture review or when query/path/explain do not surface enough context.
- After modifying code, run `graphify update .` to keep the graph current (AST-only, no API cost).
