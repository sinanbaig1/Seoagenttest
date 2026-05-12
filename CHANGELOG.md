# CHANGELOG

## 2026-05-13 — Audit and patch pass

This pass addresses bugs and gaps surfaced by reading the full repo
end-to-end. Each item below explains what changed, why, and where to
verify.

### Critical fixes

1. **Canonical URL: www. → no www.**
   The live site canonical is `https://tuitionaledu.com/online/...`
   (verified by fetching the live page). The repo's scaffolds wrote
   `https://www.tuitionaledu.com/online/...` for canonicalTag and ogUrl,
   which produces a 301-redirect chain on the self-canonical of every
   generated page. The URL inventory in
   `tuitional_interlinking_agent.md` and city-intelligence.md already
   uses no-www. Scaffolds and skills.md now match.

   Files changed:
   - `scaffolds/cat_loc_page.yaml`
   - `scaffolds/subject_page.yaml`
   - `scaffolds/location_page.yaml`
   - `scaffolds/category_page.yaml`
   - `skills.md` (Step 3 URL slug generation rule)

2. **Validator silent-pass when `why_igcse` is used.**
   The CMS field is spelled `why_igsce` (typo retained). The validator's
   `SLOT_RANGES` was keyed on `why_igsce` only. If anyone wrote
   `why_igcse` (the "correct" spelling, which appears throughout
   `skills.md` and `component-variance.md` prose), the validator
   silently skipped every word-count check.

   Verified before the fix:
   ```
   $ python3 tools/validate_page.py pages/test_spelling.yaml
   === test-spelling: PASS ===
   TOTAL: 0 violations
   ```
   With a 1-character paragraph in a `why_igcse` block.

   After the fix:
   ```
   [FAIL] why_igcse.paragraph: word_count | 1 words (range 20-50)
   TOTAL: 1 violation(s) - FAIL
   ```

   `tools/validate_page.py` now registers both spellings in
   `SLOT_RANGES` and adds a defensive alias in `slot_range()`.
   `skills.md` Step 2 instructions updated to use only the
   template-canonical `why_igsce` spelling and explicitly forbid
   "correcting" the typo.

3. **Number drift across `context.md` / `humanizer.md` / `subject-intelligence.md`.**
   `facts.md` is declared the single source of truth. Several files had
   contradicting numbers:

   - `context.md` line 86: "less than 10 Minutes" (mixed case)
   - `context.md` line 101: "94–97% per featured tutor"
     (`facts.md` says 87–97.2%)
   - `context.md` line 141: "tutor match in under 5 Minutes"
     (`facts.md` says 10 minutes)
   - `humanizer.md` line 281 (example): "average success rate of 94–97%"
   - `humanizer.md` line 486 (Rule 18 example): "within 24–48 hours"
     — explicitly banned phrasing in `memory.md` mistake #3
   - `humanizer.md` line 513 (FAQ Template D example): same 24–48 hours
     ban-violating phrasing
   - `humanizer.md` line 121: "94–97% success rate" in Do-Not-Touch list

   All reconciled to `facts.md` values. Examples that referenced banned
   numbers now use the canonical phrasing.

### Validator improvements

4. **Banned-word loader is no longer silent on fallback.**
   `load_banned_words()` previously fell back to a 2026-05-06 hardcoded
   list if it couldn't parse `facts.md`, with no signal to the operator.
   Now prints `[validator] Loaded N banned terms from facts.md.` on
   success, and a stderr WARNING on every fallback path.

5. **New: per-paragraph "Tuitional" density cap (3 per slot).**
   The previous page-total cap (8) didn't catch the most common failure
   mode: a single paragraph using "Tuitional" 4–6 times. New check
   fires per body slot.

6. **New: contraction ratio per slot.**
   `humanizer.md` Rule 15 requires >=50% of eligible contractable forms
   to be contracted. The validator now counts uncontracted/contracted
   pairs for 28 common forms (`do not / don't`, `it is / it's`, etc.)
   and fails any slot with eligible >= 2 and contraction ratio < 50%.

7. **New: sentence-initial uniformity check.**
   `humanizer.md` Rule 16 forbids 3+ consecutive sentences with the
   same opener class. The validator classifies each sentence opener
   into one of: `noun`, `verb_imp`, `subord`, `question`, `participial`,
   `pp`, `conj`. Flags any run of 3+ same-class openers within a slot.
   Skipped for FAQ answers and slots with fewer than 3 sentences.

8. **Sentence-length variation rule tightened.**
   The old check was `range >= 5 words` across sentences in a slot.
   The humanizer's stated rule is stricter: "at least one sentence
   under 12 words AND at least one over 22 words." Now enforced for
   paragraph slots. Skipped for FAQ answers (15-42 word range cannot
   naturally fit a 22+ word sentence with three sentences) and for
   card descriptions (20-30 word cap).

9. **LSI presence now scans table cells too.**
   `skills.md` says LSI terms must appear "in body copy or table
   content". The previous validator counted only body copy.
   `collect_table_text()` now pulls cell strings from common table
   shapes (`rows`, `table`, `table_rows`, `data`).

10. **Card-count check now fails on missing/empty cards.**
    Previously `if cards and len(cards) != 6` — meaning a `tutor_program`
    with `cards: []` or no `cards` key silently passed. Now fails.

11. **CI-friendly summary line.**
    Validator final line is now either
    `TOTAL: 0 violations - PASS` or
    `TOTAL: N violation(s) - FAIL`.

### New tooling

12. **`tools/build_url_inventory.py`** — parses
    `tuitional_interlinking_agent.md`'s "COMPLETE PAGE INVENTORY"
    section into a structured `tools/urls.json` (362 pages, categorised).
    Both the validator and the interlinking sub-agent should consume
    this JSON instead of re-parsing the markdown each time.

13. **Validator URL-inventory check (optional).**
    If `tools/urls.json` exists, the validator now checks every link
    target in `link_list`, `popular_subjects`, and similar components:
    * Must exist in the inventory (`url_not_in_inventory`).
    * Must not equal the current page URL (`self_link`).
    * Must not appear more than once on the page (`duplicate_link`).
    Falls through silently if the JSON is absent.

14. **`tools/run_tests.py`** — smoke tests for the validator:
    * `tests/golden_pass.yaml` must exit 0.
    * `tests/golden_fail.yaml` must fire every expected check.
    * `why_igcse` 1-word paragraph must fail (regression test for the
      silent-pass bug).
    * `tools/urls.json` must have >= 300 entries.

15. **`README.md`** rewritten. The previous README was a 1,077-line
    chat transcript from the authoring sessions. Preserved as
    `README_chat_history.md`. New README explains the system, the
    workflow, the validator's checks, and what the validator does NOT
    enforce.

### Notes on changes I did not make

16. **"Expert" hard-ban kept as-is.**
    `facts.md` Section 5 bans "Expert". The live site uses "expert
    tutors" in meta descriptions (verified). This is a content/brand
    decision, not a code decision. I did not silently remove "Expert"
    from the ban. Either:
    - Decide the ban is correct → update the live meta descriptions
      and any existing copy that uses it.
    - Decide the ban is too aggressive → remove "Expert" from
      `facts.md` Section 5 and re-run the validator on all existing
      pages.
    Until decided, the validator continues to flag it.

17. **`component-variance.md` `why_igcse` references kept.**
    The file uses `why_igcse` in prose to refer to the logical
    component name, with an explicit note (line 30) that the CMS uses
    `why_igsce`. The intent is documented; the validator now handles
    both. Sweeping this file would lose the documentation of the
    discrepancy.

18. **Inventory count: header says 376, parser finds 362.**
    14-entry gap. Likely the header is out of date or a few entries
    aren't in the standard `- Name → URL` format. I did not audit
    each missing entry. If it matters, run a diff against a sitemap
    export.

19. **Dashboard CLAUDE.md mention preserved.**
    `CLAUDE.md` line 49-51 tells the agent to ignore a separate
    dashboard `CLAUDE.md` not present in this repo. No such file was
    uploaded; the instruction is preserved in case it's referenced
    via another mechanism.

---

## Verification

Run the test suite from the repo root:

```
$ python3 tools/run_tests.py
[OK]   golden_pass: validator exit 0
[OK]   golden_fail: validator exit 1, all expected checks fired
[OK]   alias: why_igcse 1-word paragraph correctly flagged
[OK]   url inventory: 362 entries loaded

PASS: 4/4 tests passed
```

Regenerate the URL inventory after any edit to
`tuitional_interlinking_agent.md`:

```
$ python3 tools/build_url_inventory.py
Wrote 362 pages to /path/to/tools/urls.json
```
