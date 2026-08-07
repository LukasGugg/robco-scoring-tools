# Scoring Tools

Three standalone HTML tools, each usable on its own by opening the file (or its
hosted URL) in a browser — no build step, no server required:

- **`index.html`** — Concept complexity scorer (Concept phase)
- **`admin.html`** — Admin panel
- **`phase-scorer.html`** — Design/Execution scorer (phase dropdown built in)

All three point at the same shared Apps Script backend for config and
submissions, so scores entered in any of them land in the same place.

## Making changes

1. Edit the relevant `.html` file directly — each one is self-contained
   (markup, styles, and script in a single file).
2. Commit and push:
   ```bash
   git add <file>
   git commit -m "describe the change"
   git push
   ```
3. Wherever the file is hosted or embedded, the new version shows up as soon
   as that host picks up the latest commit (immediately if it's an iframe
   pointed at a live URL; otherwise whenever the file is next re-uploaded/
   re-deployed).

## Embedding in Notion / ClickUp

Point Notion's `/embed` block or ClickUp's Dashboard "Embed" widget at
wherever the tool is served from. Since these just iframe a live URL, updates
pushed to that URL show up immediately with nothing else to touch.

## Backend config

Weights, bands, and submission targets are read from the Apps Script Web App
referenced near the top of each file's `<script>` block (`WEBAPP_URL`,
`FORM_ACTION_URL`, `FORM_ENTRY_IDS`). Update those constants if the backend
changes.
