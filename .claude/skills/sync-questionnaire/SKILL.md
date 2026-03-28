Sync the Redwoods Compass questionnaire JSON across the entire project.

Run this skill whenever:
- A new questionnaire JSON file has been provided or created (e.g., upgrading from v0.6 to v0.7)
- Questions have been added, removed, or renamed inside the existing JSON
- The JSON file has been renamed

## Step 1 — Identify the new JSON file

Use `Glob` with the pattern `src/redwoods_compass_questions_*.json` to list all questionnaire files in `src/`.

- If exactly one file exists and no rename is happening, that is the active file.
- If multiple files exist, ask the user which one is the new canonical version, then delete or archive the old one.
- Determine the **old filename** (previously referenced in `script.js` via `QUESTIONS_FILE_URL`) and the **new filename**.
- Extract the **version string** from the new filename (e.g., `v0.7` from `redwoods_compass_questions_v0.7.json`).

## Step 2 — Read and parse the new JSON

Read the full content of the new JSON file. It is a JSON array of category objects shaped like:

```json
[
  {
    "Category": "...",
    "CategoryDescription": "...",
    "Questions": [
      { "Question": "...", "weight": 1, "showIf": { ... } },
      ...
    ]
  }
]
```

Extract:
- **All question texts** — every `Question` value across all categories and subcategories, including conditional follow-ups (those with a `showIf` field). Collect them as a flat, deduplicated list.
- **All category names** — the unique `Category` values in order.

## Step 3 — Update `script.js`

In `script.js`, find the line:
```js
const QUESTIONS_FILE_URL = './src/redwoods_compass_questions_....json';
```
Replace the filename with the new one. If the filename has not changed, skip this step.

## Step 4 — Rebuild `VALID_QUESTIONS` in `visualization.html`

Find the block in `visualization.html` that starts with:
```js
// ── Authoritative question list (from redwoods_compass_questions_
```
and ends just before:
```js
// ── Palette ─
```

Replace the entire block with a freshly generated one using the question list from Step 2.
Format it exactly like this, grouping questions under `// CategoryName` comments:

```js
// ── Authoritative question list (from FILENAME) ──
// All questions across all categories, including conditional follow-ups.
// Used to validate that an uploaded CSV belongs to this questionnaire version.
const VALID_QUESTIONS = new Set([
    // Category Name
    "Question text here?",
    "Another question?",
    // Next Category
    "...",
]);
```

Use the exact question text strings from the JSON — do not paraphrase or trim.

## Step 5 — Update `REDWOODS_COMPASS_SCHEMA.md`

In `REDWOODS_COMPASS_SCHEMA.md`:
- Replace every occurrence of the old filename with the new filename.
- Update the `Version:` line at the top to match the new version string.

## Step 6 — Update `.agent/workflows/update-json-changelog.md`

In `.agent/workflows/update-json-changelog.md`, replace any occurrence of the old filename with the new filename.

## Step 7 — Log the change in `docs/json-changelog.md`

Follow the existing workflow in `.agent/workflows/update-json-changelog.md`:

- Check for an existing entry for today's date.
- If none exists, prepend a new date block at the top of the log (below the `---` header separator).
- If one already exists, append to it.

The entry must describe what changed:
- If this is a version rename: note the old and new filename.
- If questions were added/removed/renamed: list each one specifically (old text → new text, or "added", or "removed").
- If both: cover both.

Use this format:
```md
**Date:** YYYY-MM-DD
**File:** `src/NEW_FILENAME.json`
**Change:** [Summary of what changed]:
- [Specific item 1]
- [Specific item 2]

---
```

## Step 8 — Report

After all edits are complete, output a concise summary:
- New filename and version
- How many questions are now in `VALID_QUESTIONS`
- Which files were modified and what changed in each
- Any questions added or removed compared to the previous version (if determinable from context)
