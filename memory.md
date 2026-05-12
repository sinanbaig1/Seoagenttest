# memory.md — Agent Memory: Process Mistakes Only

This file logs **process mistakes** the agent has made in past sessions — the kind of error that recurs unless the agent is reminded.

It does NOT duplicate brand facts. Every "the dashboard has 5 features" or "matching is under 10 minutes" reference points to `facts.md`, the single source. If `facts.md` changes, this file does not need to.

The agent reads this at Step 1 to avoid repeating these specific errors.

**Update format:** add new entries at the top, most recent first. Date in YYYY-MM-DD. Be specific.

---

## Section 1 — Known Mistakes to Avoid

*Log errors the agent has made in previous outputs. Be specific — vague entries will not prevent recurrence.*

| # | Date | Page / Context | Mistake | Where the correct fact lives |
|---|---|---|---|---|
| 6 | 2026-05-07 | Workflow timing | Spent ~18 minutes on the Arabic Tutors in Sharjah page. Most of the time went to manual word-counting in `<thinking>` blocks ("Sharjah(1) English(2) School(3)..."), drafting paragraphs in thinking before writing the file, and a two-pass write (Step 6 draft → Step 8 humanize) that produced three drafts of every paragraph. The agent's own self-counted Tuitional total (7) was wrong — the validator found 10. | Use `tools/validate_page.py` for all numeric checks. `humanizer.md` is now Stage-1 loaded, so Step 6 writes humanized copy directly. Subject lookups live in `subject-intelligence.md`. See `claude.md` Hard rules 1–4 and 7. |
| 1 | 2026-04-02 | All pages | Generated content for the hardcoded header form fields (form heading, Select Grade / Curriculum / Subject dropdowns). These fields are hardcoded in the CMS and cannot be changed via content entry. | `component-variance.md` — the `with_form` block accepts only header / paragraph / imageAltText. The form dropdowns are not writable. |
| 2 | 2026-04-02 | All pages — Progress Tracking bullet + FAQ answers | Described the parent dashboard as showing only session activity, tutor notes, and grade trajectory. Reduced the dashboard to grade tracking alone. | `facts.md` Section 2 — all five dashboard features must be named when the dashboard is mentioned. |
| 3 | 2026-04-02 | All pages — FAQ 6 / onboarding speed answers | Stated tutor matching takes 24 to 48 hours. | `facts.md` Section 1 — matching is under 10 minutes. Use the verbatim phrasing in `facts.md`. |
| 4 | 2026-05-06 | Arabic tutors Jeddah/Sharjah session | Wrote a Python xlsx generator from scratch in-session. Hit non-ASCII syntax errors. Rewrote the script three times. | The committed generator is `tools/build_page_xlsx.py`. Never write Python ad-hoc — use that one and pass it the page YAML. |
| 5 | 2026-05-06 | All pages | Loaded all reference files at session start, including `humanizer.md` and `component-variance.md`. Caused 30+ minute mid-write constraint loops. | **Updated 2026-05-07:** `humanizer.md` is now Stage 1 by design (paired with single-pass writing in Step 6 + the validator script). The loop happened because the agent did *two-pass* writing while humanizer was in context. Stage discipline is still real for `component-variance.md`, `page-differentiation.md`, and `city-intelligence.md` — see `claude.md` File Dependencies for the current staging. |

---

**Example entry format (do not delete this — use as reference):**

| 1 | 2026-04-01 | IGCSE Service Page | Intro paragraph exceeded 40-word limit (written at 67 words) | Trimmed to 38 words, removed two filler phrases |
| 2 | 2026-04-01 | IGCSE Service Page | Used the word "expert" in tutor profile copy | Replaced with "Cambridge-certified" and "15,000+ tutoring hours" |

---

## Section 2 — Approved Iterations

*Log content that was revised and approved. This builds a reference library of what "good" looks like for Tuitional.*

### Approved Intro Paragraphs

*Add approved H1 intros here once confirmed by the team.*

```
[Page name]:
[Approved copy]
[Word count: X]
[Date approved: ]
```

---

### Approved FAQ Answers

*Log FAQ Q&A pairs that have been approved and can serve as tone/style reference.*

```
Q: [Question]
A: [Approved answer — under 35 words]
[Date approved: ]
```

---

### Approved CTA Language

*Log CTA button labels and supporting microcopy that have been approved.*

```
[CTA text] — approved [date]
```

---

## Section 3 — Workflow Updates

*Log any changes to the standard workflow defined in skills.md. If the process changes, document it here before updating skills.md.*

| # | Date | Change Description | Reason | Updated in skills.md? |
|---|---|---|---|---|
| — | — | — | No updates yet. | — |

---

## Section 4 — Content Rule Updates

*Log any changes to word count rules, banned words, or AEO guidelines.*

| # | Date | Rule Changed | Old Rule | New Rule | Reason |
|---|---|---|---|---|---|
| — | — | — | — | — | No updates yet. |

---

## Section 5 — CMS Component Notes

*Log any observations about specific CMS components that affect how content should be written or structured — e.g. character limits discovered in practice, rendering issues, label constraints.*

| # | Date | Component Name | Observation | Action Taken |
|---|---|---|---|---|
| — | — | — | — | No entries yet. |

---

## Section 6 — Page-Specific Notes

*Log page-level decisions and exceptions that shouldn't be in the general guidelines.*

### IGCSE Tutors Page (`/online/igcse-tutors`)
- No entries yet.

### [Next page — add when worked on]
- No entries yet.

---

## How to Add Entries

Anyone updating this file (agent or human reviewer) should follow this format:

1. **Always add to the top** of the relevant section table
2. **Always include a date** in YYYY-MM-DD format
3. **Be specific** — "the intro was too long" is not useful; "intro was 67 words vs 40-word limit" is
4. **Close the loop** — If a mistake was fixed, log what the fix was, not just that a fix was needed