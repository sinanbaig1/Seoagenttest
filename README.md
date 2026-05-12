# Tuitional SEO Copywriter Agent

A constrained-prompt system for producing CMS-ready SEO pages for
[tuitionaledu.com](https://tuitionaledu.com), one page per session.

The system is **not** a multi-agent pipeline. It is one Claude session
following a 10-step workflow, backed by two Python tools:

* `tools/validate_page.py` — deterministic checks on the page YAML
  (word counts, em-dashes, banned words, FAQ rotation, URL inventory).
* `tools/build_page_xlsx.py` — converts the validated YAML to the
  CMS-ready xlsx the operations team uploads.

The "deterministic" part is the validator. Generation itself is
probabilistic; the validator either passes the output or sends it
back for regeneration.

---

## Repo layout

```
CLAUDE.md                     # Agent identity, voice, file dependencies, hard rules
skills.md                     # The 10-step workflow + every section spec
facts.md                      # Single source of truth for brand numbers and banned words
context.md                    # Narrative positioning (numbers reference facts.md)
memory.md                     # Process-mistake log (do not duplicate facts here)
humanizer.md                  # Anti-AI-detection rules; Stage-1 loaded; single-pass
subject-intelligence.md       # 13-subject lookup table (pain points, spec codes, LSI banks)
city-intelligence.md          # Location-page reference (schools, timezones, boards)
component-variance.md         # CMS component capabilities
page-differentiation.md       # Cross-page uniqueness rules (Batch Uniqueness Matrix)
tuitional_interlinking_agent.md  # Interlinking sub-agent + 362-page URL inventory

scaffolds/                    # YAML templates per page type (slot-constrained)
  cat_loc_page.yaml           #   Subject + Location (e.g. "Arabic Tutors in Jeddah")
  subject_page.yaml           #   Subject only (e.g. "IGCSE Chemistry Tutors")
  location_page.yaml          #   City landing (e.g. "Online Tutors in Dubai")
  category_page.yaml          #   Category landing (e.g. "Online IGCSE Tutoring")

tools/
  validate_page.py            # YAML validator (run in Step 8)
  build_page_xlsx.py          # YAML -> xlsx converter (run in Step 10)
  build_url_inventory.py      # Regenerate tools/urls.json from the markdown inventory
  run_tests.py                # Smoke tests for the validator
  urls.json                   # Auto-generated URL inventory (commit alongside the .md)

tests/
  golden_pass.yaml            # Reference page that must pass validation
  golden_fail.yaml            # Reference page that must fail every check

pages/                        # Working copies (gitignored or committed per workflow)
output/                       # Final xlsx files (one per page)
inputs/                       # External reference material (CMS Component Guide PDF)
cat-loc-template (1).xlsx     # The CMS template the build script targets
```

---

## Quickstart for the agent

1. **Read `CLAUDE.md`** and `skills.md`. The 10-step workflow is in
   skills.md; CLAUDE.md is identity + hard rules.
2. **Stage-1 load** (parallel, at session start):
   `skills.md`, `facts.md`, `context.md`, `memory.md`, `humanizer.md`,
   `subject-intelligence.md`.
3. **Read the output template** spreadsheet (which components, in what
   order).
4. **Parse the prompt** for primary keyword, page type. Generate the
   slug. Look up the subject row in `subject-intelligence.md`.
5. **Load** `page-differentiation.md` and `component-variance.md` at
   Step 3.5; load `city-intelligence.md` at Step 4.5 (location pages only).
6. **Fill the Batch Uniqueness Matrix**, then copy the right scaffold
   from `scaffolds/` to `pages/<slug>.yaml` and pre-write every H2.
7. **Write humanized copy in one pass** into the scaffold slots.
8. **Run the validator** until exit 0:
   ```
   py -3 tools/validate_page.py pages/<slug>.yaml
   ```
9. **Quality scoring** (Step 9 of skills.md).
10. **Build the xlsx**:
    ```
    py -3 tools/build_page_xlsx.py pages/<slug>.yaml
    ```

---

## Quickstart for an operator

```bash
# Install dependencies (Python 3.9+)
pip install pyyaml openpyxl

# Build the URL inventory JSON (re-run after editing tuitional_interlinking_agent.md)
py -3 tools/build_url_inventory.py

# Validate a page
py -3 tools/validate_page.py pages/<slug>.yaml

# Build the CMS xlsx
py -3 tools/build_page_xlsx.py pages/<slug>.yaml

# Run the validator's own smoke tests
py -3 tools/run_tests.py
```

The validator prints a sanity line on startup
(`[validator] Loaded N banned terms from facts.md.`). If you see
`WARNING: ... Using hardcoded fallback`, your `facts.md` Section 5
isn't being parsed correctly — fix the markdown before trusting the
banned-word check.

---

## What the validator checks

Every check runs against the body copy (paragraphs, FAQ answers, card
descriptions). Headers, alt text, button labels, and table cells are
out of scope unless noted.

| # | Check | Source rule |
|---|---|---|
| 1 | Word count per slot | skills.md slot specs |
| 2 | Sentence cap (no sentence > 30 words) | skills.md / humanizer Pass 2 |
| 3 | Primary keyword exact-match count <= 3 | skills.md Keyword Density |
| 4 | "Tuitional" total mentions <= 8 | skills.md Keyword Density |
| 4b | "Tuitional" per slot <= 3 | (new — prevents the 6x-in-one-paragraph case) |
| 5 | Tuitional opener percentage <= 30% | humanizer Architectural Rule 3 |
| 6 | Zero em/en dashes in body copy | humanizer Rule 11 |
| 7 | 3-word phrase repetition <= 2 occurrences | humanizer / general |
| 8 | LSI terms each appear >= 2 (body + tables) | skills.md LSI System |
| 9 | FAQ template rotation A/B/C/D no consecutive | humanizer FAQ Rotation |
| 10 | Dashboard mentioned -> all 5 features named | facts.md Section 2 |
| 11 | Hard-banned words (loaded from facts.md) | facts.md Section 5 |
| 12 | Card counts: tutor_program=6, tutor_program_1=3 | component-variance.md |
| 13 | Sentence variation: >=1 <12 words AND >=1 >22 (non-FAQ slots only) | humanizer Rule 4 |
| 14 | Contraction ratio >= 50% per slot | humanizer Rule 15 |
| 15 | Opener uniformity: no 3+ consecutive same opener class (non-FAQ slots) | humanizer Rule 16 |
| 16 | URL inventory: every link target must exist in `tools/urls.json`, no self-links, no duplicates | tuitional_interlinking_agent.md |

Checks 4b, 13, 14, 15, 16 were added on 2026-05-13. See `CHANGELOG.md`.

---

## What the validator does NOT check

These rules exist in the markdown but are not (yet) machine-enforced.
Step 7's manual eye-check covers them:

* Content purpose distinctness across repeated `why_igsce` instances.
* H2 searchability ("would someone type this into Google?").
* CTA placement (above-fold, after benefits, after process, at bottom).
* Tone / voice / pillar coverage.

---

## Conventions

* **Field spellings are template-driven.** The CMS uses `why_igsce`
  (typo retained). Always match the template — do not "correct" to
  `why_igcse`. The validator now defensively aliases both, but matching
  the template is still the policy.
* **Numbers come from `facts.md`.** If `context.md`, `humanizer.md`, or
  any scaffold contains a number that disagrees with `facts.md`, edit
  the offending file to point at `facts.md` rather than duplicate.
* **Canonical URL is no-www**: `https://tuitionaledu.com/online/<slug>`.
  This matches the live site; using `www.` produces a 301 redirect
  chain. All scaffolds and the URL inventory use no-www.

---

## Known issues / open decisions

See `CHANGELOG.md` for the full list. Open items:

* `facts.md` Section 5 bans the standalone word "Expert". The live site
  uses "expert tutors" in meta descriptions. Decision needed: either
  remove "Expert" from the hard ban (matching live), or rewrite live
  metadata to remove it (matching the ban).
* Inventory page count: the markdown header claims 376 pages; the
  parser finds 362. Recount and update the heading, or add the
  missing entries.

---

## Archived

The previous `README.md` was a chat transcript from the initial
authoring sessions. It is preserved as `README_chat_history.md` for
historical reference. It is not a guide — use this file instead.
