# Redwoods Compass

A self-assessment questionnaire for evaluating design-system maturity across six pillars (Authority, Alignment, Resource Lifecycle, People, Investment, Infrastructure), with a results visualization page that renders a spider chart from one or more exported responses.

The app is a fully client-side static site — vanilla HTML, CSS, and JavaScript. Tailwind and Chart.js are loaded from CDN. No build step, no server, no database. All in-progress answers are kept in browser `localStorage` and exported as CSV.

## Project structure

```
index.html          Questionnaire UI (entry point)
visualization.html  Results page — drop in CSVs, renders spider chart
script.js           Questionnaire logic, state, CSV export
tokens.css          Semantic design tokens
src/
  redwoods_compass_questions_v1.0.json   Question data (active version)
  tokens/                                 Foundation + semantic token sources
resources/          SVG assets (logo, trees icon)
docs/
  json-changelog.md                       Log of question/data edits
REDWOODS_COMPASS_SCHEMA.md                Question JSON schema reference
```

The active questionnaire file path is hard-coded in `script.js` as `QUESTIONS_FILE_URL`. When the questionnaire is bumped to a new version, that constant moves with it — see the `sync-questionnaire` skill under `.claude/skills/`.

## Running locally

Because `script.js` loads the questionnaire JSON over `fetch`, opening `index.html` directly via `file://` will fail CORS. Serve the directory over HTTP. With Node installed:

```bash
npx serve .
# then open the URL it prints (defaults to http://localhost:3000)
```

Any static Node-based server works (`npx http-server`, `npx live-server`, etc.) — there is nothing to install for the app itself.

## Editing the questionnaire

1. Edit (or replace) `src/redwoods_compass_questions_v1.0.json`. The schema is documented in `REDWOODS_COMPASS_SCHEMA.md`.
2. Append an entry to `docs/json-changelog.md` describing the change.
3. If the filename or version changes, also update `QUESTIONS_FILE_URL` at the top of `script.js`. The `sync-questionnaire` skill automates this.

## Using the app

1. Open the questionnaire and answer questions across the six categories. Progress autosaves to `localStorage` (key: `compassState`) — closing and reopening the tab restores state.
2. When a category is complete, the export button appears. Export downloads a timestamped CSV.
3. Open `visualization.html` and drop one or more exported CSVs onto the upload area. Each file becomes a dataset on the spider chart for side-by-side comparison.

## Deployment

Production is hosted on **Cloudflare Pages** at <https://redwoods-compass.pages.dev>. Pushes to `main` auto-deploy; PRs get preview URLs.

A Vercel deployment is also still connected to `main` in parallel during the consolidation onto Cloudflare. It will be torn down in a later cleanup pass.

There is no build command and no environment configuration — Cloudflare Pages serves the repository root as-is.
