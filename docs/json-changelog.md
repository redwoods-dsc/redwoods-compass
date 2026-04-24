# JSON Changelog

A plain log of changes made to any JSON file in the project.

---

**Date:** 2026-04-24  
**File:** `src/redwoods_compass_questions_v1.0.json`  
**Change:** Global update:
- Removed the `Infotip` property from all questions in the questionnaire.
- Replaced all single quotes used as quotation marks around words with escaped double quotes (`\"`) for consistency across Subcategories, Questions, and Descriptions.
- Formatted all Questions and Descriptions to ensure they start with a capital letter and all Descriptions end with terminal punctuation (a period, if missing).
**Change:** `Authority` → Detailed description of changes:
- Subhead description for "Is there a design critique culture in the organization?" changed from "What's being measured here is a gauge the willingness to share, collaborate, and have hard-discussions" to "Organizations with a design critique culture indicates one that has the hard-discussions and has a willingness to share, collaborate, and iterate together"
**Change:** `Resource Lifecycle` → Detailed description of changes:
- Subhead description for "Is there a documented process for intake that allows non-maintainers to propose or contribute changes?" changed from "This could include intake forms, contribution guidelines, or open office hours for proposals." to "This could include intake forms, contribution guidelines, or open office hours for proposals for individuals that don't directly work on the design system"
- Subhead description for "Are documentation updates tied to the release cadence of the code/design libraries?" changed from "Select 'Yes' if your documentation site automatically builds or versions alongside your code packages." to "Select 'Yes' if your documentation site automatically builds or versions alongside your code packages, even if its a manual process"
**Change:** `People` → Detailed description of changes:
- Subhead description for "Is there a defined group of intended users for the design system?" changed from "This question is looking to analyze clarity of scope. Ie. 'everyone at our company' is not a 'defined group'" to "Said differently, is the system built for certain internal groups and not others? \"Everyone\" is not a \"defined group\""
- Question text "Do we have the teammates internally that can successfully build the design system?" changed to "Does the organization have individuals with the skills needed to build a system internally?"
---

**Date:** 2026-04-03  
**File:** `src/redwoods_compass_questions_v1.0.json`  
**Change:** `Infrastructure` → Detailed description of changes:
- Removed redundant question: "Is the design system compatible with the primary languages and frameworks teams use?"
- Replaced question "For QA testing, do teams rely on human testing, automated testing, or a combination of the two?" with "Is your design system manually tested by a QA team?"
- Added new question under Subcategory "Distribution & Version Control": "Does your design system have its own release cadence?"
- **File Renamed:** Renamed the JSON questionnaire file from `v0.6.json` to `v1.0.json`.

---

**Date:** 2026-04-02  
**File:** `src/redwoods_compass_questions_v0.6.json`  
**Change:** `Infrastructure` → Detailed description of changes:
- Replaced question "Does the design system fully support the primary code language(s) used by product teams?" with two new questions:
  - "Are you able to use the design system in all applications in your company?"
  - "Is the design system compatible with the primary languages and frameworks teams use?"
- Added two new questions under Subcategory "Distribution & Version Control":
  - "Is the design system isolated in its own repo or colocated with the product?"
  - "Do you use a tool like a package manager to distribute the design system?"
- Added three new questions under Subcategory "Quality & Testing":
  - "Are there quality standards for your application for things like performance and accessibility?"
  - "Are there defined quality guidelines that your application is evaluated by?"
  - "For QA testing, do teams rely on human testing, automated testing, or a combination of the two?"

---

**Date:** 2026-04-01  
**File:** `src/redwoods_compass_questions_v0.6.json`  
**Change:** `Infrastructure` → Detailed description of changes:
- Added new conditional follow-up question: "Does it happen in a code generating tool or static artifacts tool?" (under `infra_prototyping`).

---

**Date:** 2026-03-28  
**File:** `src/redwoods_compass_questions_v0.6.json`  
**Change:** `Infrastructure` → Detailed overhaul of category questions:
- Replaced "Is the organization (or product) on a single code framework?" with "For your web applications are you using multiple frameworks?".
- Replaced "Is the organization (or product) on a single tech stack?" with a conditional tree (`id: infra_multiple_platforms`): "Does your organisation build on multiple platforms?" → If YES: "Are each of those platforms building in alignment with the same design system?" / If NO: "Is your platform built using your design system?".
- Added question: "Does the design system fully support the primary code language(s) used by product teams?".
- Added question: "Is there a standard practice for using a central communication platform at the organization?" (focusing on chat/email vs. documentation).
- Replaced old communication questions with a refined one: "In addition to communication platforms does your organization or team send out regular company updates from leadership?".
- Deleted 8 legacy questions under "Are all teams on the same design tooling?" and "Are all teams on the same engineering tooling?".
- Added and organized new questions at the bottom of the category:
  - "Are the designers using the same set of tools to do work?"
  - "Is prototyping happening in your company?"
  - "Are design resources distributed through the same tool?"

---

<!-- TEMPLATE (copy & paste for each change):
**File:** `src/redwoods_compass_questions_v0.6.json`  
**Change:** Category updates and global field additions:
- `People`: Replaced 1 generic split-time question (`id: people_split_time`) and its follow-ups with 2 separate role-based trees: Makers (`id: people_makers_split_time`) and Consumers (`id: people_consumers_split_time`) to measure organizational resilience and rotation practices.
- `Resource Lifecycle`: Complete replacement of questions to focus on Definition of Done parity, intake processes, documentation cadence, versioning/labeling, and deprecation/migration support. Updated `CategoryDescription` to reflect the focus on the operational reality of assets.
- `Global`: Added `"weight"` field (values: 1, 0.5, 0) to every question object to enable informational or partially-weighted items in scoring calculations.

---

<!-- TEMPLATE (copy & paste for each change):

**Date:** YYYY-MM-DD  
**File:** `path/to/file.json`  
**Change:** [Question / field name] changed from "[old text]" to "[new text]"

---
-->
