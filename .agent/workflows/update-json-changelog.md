---
description: Update and consolidate the JSON changelog whenever a JSON file is modified
---

Every time any JSON file in this project is modified (e.g., `src/redwoods_compass_questions_v0.6.json` or `resources/tokens.json`), you MUST update `docs/json-changelog.md` as part of the same change.

## Steps

1. Make the change to the JSON file.

2. Check `docs/json-changelog.md` for an entry with today's date (**YYYY-MM-DD**).

3. **Consolidate by Date:**
    - If the date **does not exist**, prepend a new entry at the top of the log (below the header) using the template below.
    - If the date **already exists**, append the new change as a bullet point or sub-section within the existing date block to keep all changes for the same day grouped together.

4. **Maintain Detail:** Preserve specific details (old vs. new text, subcategory updates, IDs) even when consolidated. Be specific: quote the exact old and new text so the log is useful at a glance.

## Template (Daily Block)

```md
**Date:** YYYY-MM-DD  
**File:** `path/to/file.json`  
**Change:** [Category/Section] → Detailed description of changes:
- [Item 1] changed from "[old value]" to "[new value]"
- [Item 2] added/removed [details]

---
```
