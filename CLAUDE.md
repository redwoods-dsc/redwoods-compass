# CLAUDE.md

Notes for Claude Code working in this repo. Read `README.md` first for the user-facing overview; this file covers things that aren't obvious from the code.

## Shape of the project

Pure static site. **There is no `package.json`, no bundler, no build step, and no server runtime.** Do not suggest adding Webpack, Vite, Next.js, or a Node toolchain unless the user explicitly asks for it — the simplicity is the design.

- Tailwind CSS and Chart.js are loaded from CDN (`cdn.tailwindcss.com`, `cdn.jsdelivr.net`). Tailwind config is inline in `index.html` via `tailwind.config = { ... }`. Don't reach for a `tailwind.config.js`.
- Two pages, no router: `index.html` (questionnaire) and `visualization.html` (results). Navigation is a plain `<a>` link.
- All app logic for the questionnaire lives in a single file: `script.js`. The visualization page has its logic embedded inline in `visualization.html`.

## Where the questionnaire data lives

- Active file: `src/redwoods_compass_questions_v1.0.json`.
- Path is hard-coded at the top of `script.js` as `QUESTIONS_FILE_URL` (line 2). If you rename or version-bump the JSON, update that constant.
- Schema reference: `REDWOODS_COMPASS_SCHEMA.md`.
- Whenever you change the JSON's content or filename, **append an entry to `docs/json-changelog.md`** — the team uses it as the single record of question history. Use the template at the bottom of that file.
- A `sync-questionnaire` skill exists at `.claude/skills/sync-questionnaire/` that automates the version-bump workflow (rename file, update `QUESTIONS_FILE_URL`, update schema doc, write changelog entry). Use it when the user provides a new questionnaire version.

## Runtime behaviour worth knowing

- State is persisted to `localStorage` under the key `compassState` — shape: `{ answers, skippedCats, showSub }`. If you're debugging "why didn't my change show up," it's often stale state; clear that key.
- The questionnaire supports `showIf` conditional questions (see schema doc). `visibleQuestions` and `animatedFollowUps` in `script.js` track which conditional follow-ups are currently shown and which have already played their reveal animation.
- The export → visualize flow is a CSV round-trip: `exportCSV()` in `script.js` writes a CSV with columns `Category, Subcategory, Question, Weight, Answer`; `visualization.html` parses that exact shape. If you change the export columns, the parser must change too.
- Opening `index.html` over `file://` will fail because of the `fetch` for the JSON — local dev needs a static server. Use a Node-based one (`npx serve .`); the team prefers Node tooling over Python. The error UI in `script.js` already calls this out.

## Deployment

- Production: **Cloudflare Pages** (`redwoods-compass.pages.dev`), Git-integrated, auto-deploys from `main`. No build command. Output directory is the repo root.
- A Vercel deployment is still connected to `main` in parallel during the migration to Cloudflare. Both deploy on every push. Teardown of Vercel is deferred — don't propose deleting it without checking with the user.
- No `vercel.json`, no `wrangler.toml`, no `.github/workflows/`. Both platforms are configured entirely from their dashboards.

## What's not here

No test suite, no linter, no formatter config, no CI. Don't fabricate `npm test` instructions. If you're asked to verify a change, manual smoke-test in the browser is the only path: serve locally, walk the questionnaire, export, drop into the visualization page.
