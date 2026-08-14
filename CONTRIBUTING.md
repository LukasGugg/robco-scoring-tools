# Contributing

No build step — these are plain HTML/CSS/JS files. Open one directly in a browser to test it,
or run `python -m http.server` in this folder if you need `fetch` to reach the shared Apps Script
config endpoint (some browsers block that from a `file://` URL).

## Workflow

1. Branch off `main`: `git checkout -b feature/your-change` — never commit straight to `main`.
2. Make your change, test it in a browser.
3. Push the branch and open a PR. `main` is protected — it needs a PR to merge.

## Following the existing pattern

`index.html` (Concept) and `design-scorer.html` (Design) are structurally identical: header with
sender/HubSpot-deal-ID/project fields → Scorer/Learn tabs → a row-per-work-package grid (three-point
estimate + complexity multiplier) → Learn tab explaining the math → a `<script>` with `CONFIG`,
`state`, `computeStep`/`computeAll`, and render functions. If you're adding a new phase or reworking
a scorer, copy that structure rather than inventing a new one — it keeps every tool consistent for
whoever picks it up next. `execution-scorer.html` is the exception (per-criterion hour formulas
instead of PERT) because Execution's estimating method is genuinely different, not because the
pattern was abandoned.

## The backend

Config (weights, contingency %, correlation, hour-formula coefficients) lives in a Google Sheet's
Config tab, read through a shared Apps Script Web App. Submissions go through a Google Form per
phase into that same Sheet. None of that is in this repo — ask Lukas for access if you need to add
or change a Config key or entry ID.
