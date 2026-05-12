# skills.md — SEO Copywriter Workflow & Content Writing Guidelines

---

## Overview

This file defines the exact step-by-step process the agent must follow every time it creates a new service page. It also contains the content writing rules, word count specifications, format standards, keyword strategy, SEO rules, and AEO/GEO optimisation criteria for every CMS component type.

All identity, voice, tone, content pillars, and banned language rules live in `claude.md`. This file does not repeat or override them.

Do not skip steps. Do not reorder steps. Follow this workflow exactly.

---

## Step-by-Step Page Creation Workflow

### STEP 1 — Load Stage 1 Reference Files

Before touching any content, load the Stage 1 files in parallel. The previous staged-load model (humanizer at 7.5, etc.) was retired on 2026-05-07 because the validator script now catches what the staging used to prevent — and staging caused two-pass writing that cost ~10 minutes per page.

**Load now (Stage 1, all in one batch):**
- `skills.md` (this file)
- `facts.md` — brand facts, banned words, ICPs, approved CTAs
- `context.md` — narrative positioning (numbers reference `facts.md`)
- `memory.md` — process mistakes
- `humanizer.md` — humanizer rules (loaded early so Step 6 writes humanized copy directly)
- `subject-intelligence.md` — subject lookup table (pain points, spec codes, LSI banks, card titles, university refs)

(`claude.md` loads automatically.)

**Load at Step 3.5 (when scaffold + matrix work begins):**
- `page-differentiation.md`
- `component-variance.md`

**Load at Step 4.5 (location pages only):**
- `city-intelligence.md`

If any Stage 1 file is missing, stop and request it before proceeding. Per-session inputs (output template spreadsheet, prompt) are read at Step 2 and parsed at Step 3.

---

### STEP 2 — Read the Output Template

Read the spreadsheet output template provided for this session. The template defines the exact component sequence — which components appear and in what order.

For each component in the template:
1. Note the exact component key as it appears in the template (e.g. `why_igsce`, `why_igsce_1`, `why_igsce_2`). NOTE: the CMS field is spelled `why_igsce` (a retained typo). Always use that exact spelling — the scaffolds, the validator, and the live CMS all expect `why_igsce`. Do not "correct" it to `why_igcse`.
2. Strip the numeric suffix to identify the base component type (e.g. `why_igsce_2` → base type is `why_igsce`)
3. Cross-reference the base type in `component-variance.md` to understand what fields and content it supports
4. Note which components are toggle-only (no content to write) and which require text

**Component instance naming:** When a component type appears more than once, the CMS appends a suffix — `_1`, `_2`, `_3`, etc. The first instance keeps the base name. All instances share the same fields. Always use the exact suffixed key from the template in your outline and output — never the base name when a suffix exists.

The template sequence IS the page sequence. Do not reorder components.

---

### STEP 3 — Parse the Prompt, Derive Keywords, and Generate URL

Extract the page information from the prompt provided at session start.

**What the prompt provides:**
- **Page name** — This IS the primary keyword (e.g. "psychology tutors in abu dhabi")
- **Page type** — Service Page or Blog Page

**Hardcoded intent and ICP by page type:**

| Page Type | Intent | Target ICP |
|---|---|---|
| Service Page | Transactional | Parents & Students |
| Blog Page | Provided in the prompt | Provided in the prompt |

**URL slug generation (service pages):**

All service pages live under the prefix `tuitionaledu.com/online/` (no `www.` — the live canonical drops it; using `www.` produces a 301 redirect chain). The agent must generate the slug automatically from the page name:

1. Take the page name (e.g. "psychology tutors in abu dhabi")
2. Convert to lowercase
3. Replace spaces with hyphens
4. Remove any special characters
5. Result: `psychology-tutors-in-abu-dhabi`
6. Full URL: `https://tuitionaledu.com/online/psychology-tutors-in-abu-dhabi`

Record the pageName (title-cased page name) and pageSlug before proceeding. These will appear as the first two rows of the section sheet output in Step 10.

**Secondary keyword derivation:**

The agent derives secondary keywords from the primary keyword. The amount of variance depends on the primary keyword length:

- **Primary keyword ≤ 3 words** (e.g. "Biology Tutors") — Generic keyword. More variance is possible. Derive 4–6 secondary keywords by adding modifiers: curriculum prefixes ("IGCSE Biology Tutors"), delivery mode ("Biology Tutors Online"), format ("Individual Biology Tutors"), and combined variations ("IGCSE Biology Tutors Online").

- **Primary keyword ≥ 3 words** (e.g. "IGCSE Biology Tutors in Abu Dhabi") — Targeted keyword. Less variance available. Derive 2–3 secondary keywords using minor variations: dropping the location ("IGCSE Biology Tutors"), swapping delivery mode ("IGCSE Biology Tutors Online"), or adjusting the curriculum prefix ("Cambridge Biology Tutors in Abu Dhabi").

Record the primary keyword and all derived secondary keywords before proceeding.

**Subject lookup (subject + location pages and subject-only pages):**

Open `subject-intelligence.md` and find the row for this subject in each table. Copy these values forward — do not re-derive them in Step 4 or Step 6:

- Suggested angle (Master Subject Table)
- Lead stat (Master Subject Table)
- Pain point opener (Master Subject Table) — goes verbatim into the `why_igsce_1` paragraph notes
- Specification codes (Specification Codes table) — go into the `why_igsce_4` paragraph notes
- LSI bank — pick 6–8 terms; these go into the page YAML's `_validation.lsi_terms` block
- Card title set (Card Title Sets table) — goes into `tutor_program.cards[*].title`
- University / career reference (University / Career References table) — goes into the `why_igsce_5` paragraph notes

The subject lookup eliminates ~3 minutes of mid-write derivation that previously bounced between `component-variance.md` and `page-differentiation.md`.

---

### STEP 3.5 — Load `component-variance.md` and `page-differentiation.md`

Now load both files. Step 4 needs `component-variance.md` to know which components have H2 fields and what content each holds. It needs `page-differentiation.md` to pick angles, frameworks, and lead stats — and to fill the **Batch Uniqueness Matrix** at the top of that file before any writing begins.

Loading either file earlier wasted tokens; loading later forces a return trip mid-Step-4.

Do not load `city-intelligence.md` or `humanizer.md` yet.

---

### STEP 4 — Fill the Batch Uniqueness Matrix, Then Pre-Write Final H2 Headings

This is the most important step for preventing mid-writing thrash. The agent has previously lost significant time reassigning heading frameworks during Step 6. To prevent this, lock the cross-page differentiators **and** the actual final H2 strings here.

**Step 4a — Fill the Batch Uniqueness Matrix**

Open `page-differentiation.md` and fill the **Batch Uniqueness Matrix** at the top of the file (single-page run = row 1 only). Every cross-page uniqueness rule in this file is satisfied by completing the matrix correctly. Do not start Step 4b until the matrix is filled and verified — same value in two rows of any column means change one before proceeding.

**Step 4b — Copy the scaffold and pre-write the H2s into it**

For each page in the batch:
1. Pick the scaffold that matches the page type:
   - `scaffolds/cat_loc_page.yaml` — Subject + Location (e.g. "Arabic Tutors in Jeddah")
   - `scaffolds/subject_page.yaml` — Subject only (e.g. "IGCSE Chemistry Tutors")
   - `scaffolds/location_page.yaml` — City landing (e.g. "Online Tutors in Dubai")
   - `scaffolds/category_page.yaml` — Category landing (e.g. "Online IGCSE Tutoring")
2. Copy it to `pages/<page-slug>.yaml`.
3. Fill the **PAGE VARIABLES** block from the matrix row.
4. Fill every `header:` slot with the actual final H2 string — under 10 words, including the city or subject keyword where natural. Note the framework name in the inline comment for that slot.

**For every writable component that has an H2 field (tutor_program, every why_igsce instance, tutor_section, tutor_program_1, what_our_student_says, link_list, Faqs):**

1. Look up the framework options in `page-differentiation.md` (Question, Outcome-first, Challenge-first, Curriculum-specific, Stat-led, Subject insight).
2. Pick a framework type for that component based on the content purpose stated in the scaffold's inline comment.
3. **Write the actual H2 string now, in full** — under 10 words, including the city or subject keyword where natural.
4. Note the chosen framework type next to the slot.

**Rules for variety:**
- Use at least 3 different framework types across all H2s on the page.
- No two adjacent H2s use the same framework type.
- This is decided once. Step 6 does not revisit it.

The angle, lead stat, opening structure, pain point, university reference, card title set, testimonial detail, and anchor phrasing are already locked in the matrix. Do not re-derive them in Step 6.

**Output of this step (example):**

```
PAGE VARIABLES — Arabic Tutors in Dubai
Angle: L1 — School Fit
Lead stat: 4.7 on Trustpilot
Opening structure: CL1 (school-led)

H2 HEADINGS (final — do not revisit in Step 6):
- tutor_program: "Arabic Tutoring in Dubai for Every Level and Goal" [Outcome-first]
- why_igsce: "Which Arabic Curriculum Do Dubai's International Schools Follow?" [Question]
- why_igsce_1: "Why Students Lose Marks on Arabic Composition" [Challenge-first]
- why_igsce_2: "How the Parent Dashboard Shows Arabic Progress" [Subject insight]
- tutor_section: "Featured Arabic Tutors in Dubai" [fixed format]
- why_igsce_3: "Online Arabic Tutoring Without the Commute" [Outcome-first]
- why_igsce_4: "Cambridge IGCSE Arabic 0508 and 0544 Explained" [Curriculum-specific]
- why_igsce_5: "Can Adults in Dubai Start Arabic with a Tuitional Tutor?" [Question]
- why_igsce_6: "4.7 on Trustpilot: How Dubai Families Rate Tuitional" [Stat-led]
- tutor_program_1: "Start Arabic Tutoring in Dubai in Three Steps" [Outcome-first]
- what_our_student_says: "What Our Arabic Students in Dubai Say" [fixed format]
- Faqs: "Arabic Tutoring in Dubai: Common Questions Answered" [fixed format]
```

After this step, the H2s are locked. In Step 6, the agent writes body content under each pre-written heading. It does not change, refine, or second-guess the headings.

---

### STEP 4.5 — Load `city-intelligence.md` (location pages only)

If the page is a service+location page, load `city-intelligence.md` now. Step 5 (outline) and Step 6 (writing) need school names, board distributions, timezones, and city-specific context.

If the page is a non-location page (e.g. a blog post or generic subject page), skip this load.

Do not load `humanizer.md` yet.

---

### STEP 5 — Build Content Outline Mapped to Template

Build a content outline using the component sequence from Step 2. For each writable component in the template:

1. Use the exact component key from the template (including any suffix — e.g. `why_igsce_2`, not just `why_igsce`)
2. Assign a content purpose based on the base type's capabilities in `component-variance.md`
3. Ensure each instance of the same component type has a different content purpose — e.g. `why_igsce` might be "tutor expertise," `why_igsce_1` might be "school landscape," `why_igsce_2` might be "online advantage"
4. Note what heading framework to use (from `page-differentiation.md`)
5. Note the word count range for that component type
6. Note how many paragraphs, bullets, or table rows are needed
7. Note which keyword (primary or secondary) will appear in that section

The outline must follow the template's component order exactly. Every writable component in the template must have an entry in the outline.

---

### STEP 6 — Write Humanized Copy Directly (single pass)

> **CRITICAL: write the final, humanized copy in one pass. Do not draft first and humanize later.**
>
> The previous two-pass model (Step 6 draft → Step 8 humanize) cost ~10 minutes per page and produced three drafts of every paragraph (thinking-draft → file draft → humanized rewrite). Now `humanizer.md` is Stage-1 loaded, so its rules are available from the first sentence. Apply them while writing, not after.

Open the page YAML you copied from a scaffold in Step 4b. Fill each `<<< ... >>>` placeholder. The inline comments above each slot are the spec.

**Do not draft paragraphs in `<thinking>` blocks before writing them to the file.** Pick the angle, framework, and lookup data in thinking. Write the prose directly to the YAML. Thinking is for selection, not composition.

**Do not count words manually.** The validator (`tools/validate_page.py`) runs in Step 8 and reports every violation. Aim within the slot range; the validator confirms.

**Apply during writing (already in Stage 1):**

1. Word-count range for the section type.
2. Component fits its purpose per `component-variance.md`.
3. Hard-banned words from `facts.md` Section 5 — none.
4. Primary keyword in H1 and hero paragraph.
5. Em/en dashes — zero. Replace with commas, periods, or two sentences.
6. Contractions where natural ("doesn't", "it's", "we've").
7. Tuitional opener percentage — at most ~30% of body paragraphs start with "Tuitional".
8. FAQ template rotation A/B/C/D — declare each in `# Template <X>` comments next to the FAQ item, ensure no two consecutive same template.
9. All five dashboard features named whenever the dashboard is referenced (`facts.md` Section 2).
10. LSI terms from `subject-intelligence.md` — each appears at least twice in body copy.

**Forbidden during writing (caught by validator):**

- Reassigning H2 frameworks (locked in Step 4).
- Rewriting H2 headings (locked in Step 4).
- Manual word/keyword/Tuitional/LSI counting in thinking blocks.
- Drafting prose in thinking before writing to file.

**Populate the `_validation` block** at the top of the page YAML before you stop. It powers the validator's lookup-driven checks:

```yaml
_validation:
  primary_keyword: "Arabic tutors in Sharjah"
  lsi_terms:
    - "Modern Standard Arabic"
    - "Fusha"
    - "0508"
    - "0544"
    - "Arabic composition"
    - "oral expression"
    - "reading comprehension"
    - "A Level Arabic"
  faq_templates: ["A", "B", "C", "D", "A", "B"]
```

Write naturally, in one pass, with humanizer rules applied from the first sentence. Move to Step 7 when every slot is filled.

---

### STEP 7 — Manual Eye Check (everything numeric is in Step 8)

This step is now five judgement calls. Every numeric and structural rule moved to the validator. Walk these by eye:

- [ ] Each instance of a repeated component type has a distinct content purpose (no two `why_igsce` instances saying the same thing — the validator can't judge content overlap).
- [ ] Content reflects at least one of the five content pillars from `claude.md`.
- [ ] CTA placement covers above-fold, after benefits, after process, and at bottom.
- [ ] Every H2 passes the searchability test: would someone type this into Google? (The validator cannot judge searchability.)
- [ ] No H2 is just "[Subject] + generic tutoring phrase".

Do not enumerate this list verbatim in thinking text. Read it, scan the YAML, fix what needs fixing, move to Step 8.

---

### STEP 8 — Run the validator and fix

```
py -3 tools/validate_page.py pages/<page-slug>.yaml
```

Exit 0 = pass. Exit 1 = at least one violation, surfaced as a table of `slot | check | detail`. Read the output, fix each violation in the YAML, re-run.

**The validator runs every numeric and structural check that used to live in Step 7 and the humanizer's Triple-Pass Audit:**

- Word counts per slot (hero 25–50, body 20–50, FAQ answers 15–42, card descriptions 20–30).
- Sentence cap (no sentence over 30 words).
- Primary keyword exact-match count ≤ 3 across page.
- Tuitional total mentions ≤ 8 across page (including meta).
- Tuitional opener percentage ≤ 30% of body paragraphs.
- Em/en dash scan — zero in body copy.
- 3+ word phrase repetition — no phrase exceeds 2 occurrences (skipping high-stopword phrases).
- LSI presence — each term ≥ 2 occurrences in body copy.
- FAQ template rotation — no two consecutive same template.
- All five dashboard features named whenever "dashboard" appears.
- Hard-banned words from `facts.md` Section 5 — zero.
- Card counts (`tutor_program` = 6, `tutor_program_1` = 3).
- Sentence-length variation per body slot (range ≥ 5 words when > 2 sentences).

**If a violation forces a paragraph rewrite**, write the replacement once, then re-run the validator on the whole file. Do not recount manually after every revision.

When the validator exits 0, move to Step 9.

---

### STEP 9 — Content Review Process (Quality Scoring)

This is a quality scoring pass — separate from the completeness checklist in Step 7. Step 7 checks whether the work was done. This step evaluates how well it was done.

Run this after Step 8.

#### Phase 1 — Strategic Intent Audit
- Confirm the content targets the right query with the right intent
- Confirm the format matches the intent (a mismatch will fail regardless of quality)
- Review AI Overview eligibility against the Citation Eligibility Criteria below

#### Phase 2 — E-E-A-T Audit
- Confirm experience signals are present: real exam marking references, past paper specifics, tutor credential details (see E-E-A-T Signals section below for the full requirements)
- Confirm at least 2 authority signals from the approved list appear in the body
- Confirm all claims have a number or a named credential — no vague claims remain
- For blog content only: confirm clear authorship, verified bio, and first-hand knowledge signals
- For sensitive topics: check for credible sources, accurate claims, proper disclosures

#### Phase 3 — Content Depth and Semantic Coverage
- Check if the topic is fully covered or just lightly mentioned
- Confirm the content offers something original: a data point, a specific insight, or a unique angle
- Verify all LSI terms are present and used naturally

#### Phase 4 — Engagement and Featured Snippet Audit
- The opening must confirm relevance immediately
- Page must be easy to scan: clean formatting, logical structure
- Check readability score targets Grade 5–7
- Confirm CTA placement: above fold, after benefits, after process, and at bottom
- At least one paragraph opens with a 40-word-or-fewer direct factual statement (paragraph snippet target)
- At least one list on the page is formatted for list snippet eligibility
- At least one table on the page is formatted for table snippet eligibility

#### Phase 5 — Human-Written Content Review
Read the content as a real person would. Check for:
- Natural variation in sentence length — AI output tends to be too smooth and even
- A hook or context in the first few lines — not generic openers
- Real details: specific numbers, tutor credentials, actual outcomes
- Uneven emphasis — humans focus more on what matters, AI gives all topics equal space
- The content must feel real, trustworthy, and written by a person

#### Phase 6 — AEO/GEO Audit
- Every paragraph opens with a declarative sentence naming the subject and board
- All entity names include specification codes where applicable
- All paragraphs are self-contained and make sense out of context
- FAQ questions map to real People Also Ask queries
- FAQ answers collectively reference Tuitional (3–4 of 6), the subject (all 6), and the curriculum (at least 4)

#### Phase 7 — Scoring and Action Prioritisation
Assign a score across all phases (1–10 per phase). Use the total to prioritise what needs fixing before the content goes live.

| Phase | Score (1–10) | Priority Action |
|---|---|---|
| 1. Strategic Intent | | |
| 2. E-E-A-T | | |
| 3. Content Depth | | |
| 4. Engagement & Snippets | | |
| 5. Human Review | | |
| 6. AEO/GEO | | |
| **Total** | **/60** | |

Any phase scoring below 7 must be revised before the content is approved for CMS entry.

**Scaffold-aware baseline:** if the scaffold from Step 4b was filled correctly and the Triple-Pass Audit cleared, expected total is **≥54/60** (every phase 9+). A score below 54 means a slot constraint was violated during writing — investigate which slot, fix the page YAML, and re-run from Step 8. Do not patch by re-scoring.

---

### STEP 10 — Save the Page YAML and Run the xlsx Generator

The content is already in the page YAML you filled in Steps 4b–6. There is no separate markdown-sheet step.

**Step 10a — Save the YAML**

The file is at `pages/<page-slug>.yaml`. Confirm:
- Every `<<< ... >>>` placeholder has been replaced with real content.
- The `pageName`, `pageSlug`, and `variant: new` header fields are set.
- Every `header:` slot has its framework name retained as a comment for traceability (the comment is stripped at generation time).
- The BUDGET block at the top reflects the final state — no negative values.

**Step 10b — Run the generator**

```
py -3 tools/build_page_xlsx.py pages/<page-slug>.yaml
```

The script wraps `tutor_program` cards in the mandated HTML/CSS automatically (Format A for 6 cards, Format B for 3). It expands `Faqs.items[]` and `link_list.items[]` into the indexed CMS field names (`faqs[0].question`, `subjects[0].link`, etc.). It writes the xlsx to `output/<page-slug>.xlsx`.

For batches:
- One YAML file per page, OR
- A single YAML with a top-level `pages:` list — the generator produces one sheet per page in one xlsx.

**Step 10c — Smoke check**

Open the resulting xlsx and confirm:
- Sheet name matches the page slug (truncated to 31 chars).
- Header rows: `pageName` / `pageSlug` / `variant` / `---`.
- Every component in the page YAML appears in template order with all expected fields.
- `tutor_program.paragraph` contains the `<style>` block followed by `<section class="tuitional-program-section">`.
- Toggle-only components (`school_logos`, `book_demo_cta`, `what_we_offer`, `get_started`) appear as `componentKey | isShow | true`.

The xlsx is the deliverable. Do not produce a separate markdown sheet — the YAML serves both as the working draft and as the canonical source for the xlsx.

---

## Search Intent — Service Page Rules

Every subject page on tuitionaledu.com/online/[subject]-tutors is a **transactional service page**. The primary intent of a visitor is:

- **Informational overlay:** "Is this platform credible? Do these tutors actually know my specific exam board?"
- **Transactional:** "I want to book a tutor. What do I do next?"

**Content must serve both.** The page must establish credibility through curriculum-specific depth AND create a clear pathway to booking. It should never read like an educational blog post.

**Practical rules:**
- Every section must either prove expertise OR move the reader toward a decision
- Do not include generic topic explanations that could appear in a Wikipedia article
- All subject knowledge references must link to tutor capability, not general education
- The page answers the question: "Why should I choose Tuitional for this specific subject at this level?"

**Intent flow across the page:**
The spreadsheet template defines the component sequence. Regardless of which specific components are used, the page must follow this intent progression:
- **Top of page** (first 2–3 components): Establish credibility fast — within 20 seconds of landing
- **Middle of page** (body content components): Deepen expertise and proof — support the decision
- **Lower page** (social proof, related links): Confirmation and exploration
- **Bottom of page** (CTAs, FAQs): Conversion — remove final objections

---

## Readability Standards

Every piece of written content on every page must be readable at Grade 5–7 level. This is the reading level of an average 10–13 year old — it does not mean dumbed down, it means clear.

**How to write at Grade 5–7:**

| Write this | Not this |
|---|---|
| "Our tutors know the mark scheme" | "Our pedagogical practitioners demonstrate comprehensive familiarity with assessment criteria" |
| "Sessions start within 6 hours" | "The onboarding process is expedited to commence within a 6-hour timeframe" |
| "Most Chemistry marks are lost on method, not knowledge" | "The predominant locus of mark attrition in Chemistry assessments pertains to methodological execution" |
| "You can cancel any time" | "Our service operates on a non-contractual, flexible commitment structure" |

**Rules:**
- Sentences: 15–20 words on average. Some shorter. Some slightly longer. Never over 30 words.
- Words: Use the simplest word that is accurate. "Use" not "utilise". "Show" not "demonstrate". "Start" not "commence".
- Jargon: Only subject-specific jargon (stoichiometry, titration, equilibrium). No business or marketing jargon.
- Contractions: Acceptable and encouraged — "you'll", "it's", "we've" — they reduce reading age without reducing credibility.

**How to write paragraphs within word count ranges:**
- One idea per paragraph. If a paragraph contains two ideas, split it into two.
- Cut filler openings ("It is worth noting that...", "As mentioned above...", "In addition to this...")
- Replace multi-word phrases with single words: "due to the fact that" becomes "because", "in order to" becomes "to"
- State the fact, then stop. Do not add a qualification sentence unless it adds a new fact.
- Count the words in every paragraph you write. Do not estimate. Count them.

---

## Format Selection Guide

Before writing any section, choose the right format for the content:

| If you are writing... | Use |
|---|---|
| An explanation, argument, or proof point | Paragraphs (within the word count range for that section type) |
| A list of features, steps, or items with no hierarchy | Bullet points (6 max, 45 words total, summary sentence required) |
| A comparison, coverage overview, or structured data | Table (3–7 rows, 2–4 columns, summary + follow-on required) |
| A step-by-step process | Numbered list (same word count rules as bullets) |
| A card grid or sign-up steps (tutor_program) | HTML card grid — follow Format A or Format B in `component-variance.md` |

Never mix formats in the same component unless the component explicitly requires it.

---

## Content Writing Guidelines by Section Type

These are the specifications for every content block type. Apply them in Step 6.

---

### H1 — Page Title
- One per page — no exceptions
- Must contain the primary keyword exactly as derived in Step 3
- Lead with the exact or close-match primary keyword
- Frame around the user's outcome, not just the service name
- Under 60 characters / 10 words maximum
- Use question-based phrasing where possible
- 1 line only — do not write a subtitle within the H1

---

### Hero / Intro Paragraph (Below H1)
- **Word count range: 25–50 words**
- Must open with a declarative, factual statement about Tuitional's offering
- Must reference the primary keyword or its close variant naturally
- No filler phrases ("experience the joy of," "we are proud to offer")
- Must give the reader one clear reason to keep reading

---

### Service Description Block (Main Body Section)
- **Word count range: 20–50 words per paragraph**
- One focused idea per paragraph — do not combine multiple points
- Each paragraph should be independently citable (AI engines pull paragraph-level content)
- No vague language — every sentence should contain a verifiable fact or clear benefit
- Write in second person throughout (you, your, you'll)
- Maximum 2–3 lines per paragraph
- Benefits first, features second — always
- Speak to the pain point before offering the solution
- Weave in trust signals: success rates, tutoring hours, Trustpilot rating, tutor credentials

---

### Sub-Section Headers (H2 / H3 / H4)

**H2 — Section Anchors**
- Must contain a secondary keyword where relevant and natural
- Each one must serve a specific purpose. Standard H2 jobs:
  - What the service is and who it's for
  - Core benefits (not features — benefits)
  - How it works / the process
  - Why choose Tuitional over competitors
  - Social proof / results
  - Service area or subjects served
  - Final CTA section
- Include secondary and LSI keywords naturally
- If it sounds off when read aloud, rewrite it

**H3 — Sub-Section Breakdowns**
- Break down H2 content into individual benefits, process steps, sub-services, or tutor credentials
- Punchy and scannable — a user browsing H2s and H3s alone should understand the full offer
- Keep under 10 words

**H4 — Deep Breakdowns (Rare)**
- Only when absolutely necessary for complex sections
- Most service pages will never need them

**General heading rules:**
- Never use generic headers like "More Information" or "About This"
- Question-based phrasing where possible
- All headings under 10 words

---

### Bullet Feature List
- **Maximum: 6 bullet points**
- **Bold Term** at the start of each bullet (does not count toward word limit)
- **All bullet descriptions combined must not exceed 45 words total**
- Each individual bullet description: 1 sentence, focused, specific
- Do not add a 7th bullet to fit more content — prioritise the 6 most impactful features
- 1 summary sentence (under 40 words) before the bullet list

---

### Tables
- **Row count: 3–7 rows** (header row does not count toward this limit, sweet spot: 5–7)
- **Column count: 2–4 columns maximum** (5+ columns break on mobile)
- **Per cell: 5–15 words maximum** (cells are labels and short phrases, not sentences)
- **Entire table: 50–150 words total** (excluding header row)
- **Summary sentence above the table: 30–40 words** — states what the table shows and why it is relevant
- **Follow-on below the table: 1–2 sentences** — interprets or extends the data

If a cell needs more than 15 words, the table is the wrong format. Use paragraphs instead.

---

### FAQ Accordion
- **Exactly 6 questions per FAQ section**
- Each answer: **word count range: 15–42 words**
- Answer the question directly and immediately — no preamble
- Bold **Q:** and **A:** labels on every entry (labels do not count toward the word limit)
- Questions must reflect real search queries parents or students ask — map to real People Also Ask boxes
- Answers must be factually specific to Tuitional — not templated or generic
- Naturally include keywords in both the question and the answer
- Across the 6 FAQ answers collectively: name Tuitional in 3–4 of them, the subject in all 6, and the curriculum/board in at least 4. Use "our tutors," "the platform," or "your Academic Consultant" as variants in the rest. This keeps total Tuitional mentions across the page within the 8-cap.
- End with a specific fact or outcome — not a soft CTA

---

### Tutor Profile Cards (If Applicable)
- 1–2 sentences per tutor bio preview (as shown on listing pages)
- Must reference: subject, years of experience or teaching hours, and one standout credential
- Do not use the word "Expert" — use specific qualifiers ("Cambridge-certified," "15,000+ tutoring hours")

---

### CTA Buttons and Labels
- 3–5 words maximum
- Action-oriented but not aggressive
- Be specific — "Book a Free Demo" over "Contact Us"
- Reduce friction — tell the user what happens after they click
- Repeat across the page, tied directly to a form or phone number
- Approved and banned CTA language is defined in `claude.md`

---

### Social Proof Section
- Include star ratings, client logos, testimonials, or results snippets
- Place near the bottom of main content, before the final CTA
- Real numbers beat vague claims — "97% student success rate" over "great outcomes"

---

### Meta Title
- Format: Primary keyword + value prop + brand name
- Under 60 characters total

---

### Meta Description
- Under 155 characters
- Must include: a CTA, a secondary keyword, and a trust signal
- **Format priority:**
  1. Question + Answer + CTA (preferred)
  2. Question + CTA
  3. Question + Answer
- Never use all three if it makes the description feel forced — clarity over formula

---

## Absolute Format Prohibitions

These apply regardless of section type, category, or brief:

- Never write a paragraph over its word count range ceiling
- Never write a paragraph that contains two separate ideas
- Never write a bullet list with more than 6 items
- Never write a bullet list whose total word count exceeds 45 words
- Never write a bullet list without a summary sentence before it
- Never write a table with more than 4 columns
- Never write a table with more than 7 data rows
- Never write a table cell with more than 15 words
- Never write a table without a summary sentence above it and a follow-on below it
- Never write a sentence over 30 words
- Never use a complex word when a simple word is accurate

---

## Keyword Strategy

### Keyword Density Rules

These limits are hard caps, not guidelines.

| Keyword Type | Maximum Per Page | Placement Logic |
|---|---|---|
| Primary keyword (exact match) | 3 | H1 once, intro paragraph once, one natural body mention |
| Secondary keywords | 2 each | H2 field where natural, one body paragraph |
| "1:1" or "one-to-one" | 1 | Body copy only — never in H1 or H2 |
| "live sessions" / "live classes" | 2 | Distributed — not in the same section |
| "personalised" / "personalized" | 2 | Not in the same paragraph |
| Any 3+ word exact phrase | 2 | Distributed across page |
| Subject name alone (e.g. "Chemistry") | Natural — no cap | But never in consecutive sentences as the subject opener |
| Platform name "Tuitional" | Max 8 per page | Use "our tutors," "the platform," "your Academic Consultant" as variants |

**Do not keyword-stuff.** One natural mention per section is sufficient. The internal linking structure of the site handles broader keyword coverage.

### Keyword Placement Rules

| Location | Rule |
|---|---|
| H1 | Primary keyword — mandatory |
| H2 | Secondary keyword — where naturally relevant |
| H3 | Descriptive variation — where relevant |
| Intro paragraph | Primary keyword or close variant — 1 natural mention |
| Body paragraphs | No forced insertion — only if natural |
| FAQ questions | Long-tail variations of keywords — natural phrasing |
| Meta description | Primary keyword — mandatory |

### Semantic Keyword System (LSI)

Every page must include 6–8 LSI terms specific to the subject and curriculum. Each term must appear at least twice across the page, naturally embedded in body copy or table content.

LSI terms are NOT secondary keywords. They are specific vocabulary from the curriculum — topic names, assessment terms, exam formats — that prove the content is genuinely about this subject at this level.

**Examples by subject:**
- Chemistry: titration, bonding, equilibrium, stoichiometry, electrolysis, organic chemistry, molar mass, required practicals
- Physics: moments, electromagnetic induction, specific heat capacity, wave properties, nuclear radiation, P-E diagrams
- Maths: differentiation, algebraic fractions, circle theorems, trigonometry identities, proof, vectors
- Economics: elasticity, multiplier effect, balance of payments, monetary policy, market failure, trade cycles
- Biology: homeostasis, photosynthesis, DNA replication, natural selection, enzyme activity, osmosis
- History: source evaluation, historiography, causation, consequence, narrative assessment, contextualisation
- Accounting: trial balance, ledger accounts, depreciation, accruals, balance sheet, income statement
- Computer Science: binary arithmetic, Boolean logic, sorting algorithms, database normalisation, TCP/IP, encryption

Write LSI terms into topic descriptions, syllabus table cells, exam prep paragraphs, and FAQ answers — wherever they appear naturally. Never force them as keyword insertions.

### Semantic Variants (Keyword Rotation)

Never repeat the primary keyword structure more than allowed. Rotate to semantic variants:

| Instead of (overused) | Use instead |
|---|---|
| "Chemistry tutor" | "Chemistry teacher," "Chemistry specialist," "A Level Chemistry support" |
| "online tutoring" | "online sessions," "virtual lessons," "remote learning support" |
| "1:1 sessions" | "private sessions," "individual lessons," "dedicated tutor time" |
| "improve your grade" | "raise your mark," "close the gap to Grade A," "build to a 7 in IB" |
| "exam preparation" | "exam readiness," "paper practice," "revision strategy" |

---

## Internal Linking Rules

### Contextual Links in Body Copy

Every subject page must include a minimum of 2 contextual interlinks in the body copy before the link list section. These must:
- Arise from a natural subject mention (e.g. a Biology page mentioning Chemistry links to the Chemistry tutors page)
- Use keyword-matching anchor text: "[Related Subject] Tutors" (e.g. "Physics Tutors")
- Never be forced — only link where the related subject is genuinely relevant to the discussion

### Link List — Sibling Subject Pages Only

The link list component must contain:
- All sibling pages in the same category (same URL prefix)
- The current subject page excluded from the array
- Correct and live URLs only — verify against the confirmed URL list
- Display names matching the page H1 format — e.g. "Physics Tutors" not "online physics"

### Anchor Text Rules

| Anchor Text | Allowed |
|---|---|
| "[Subject] Tutors" | Yes |
| "[Subject] Tutoring" | Yes |
| "[Board] [Subject] Tutors" | Yes |
| "click here" | Never |
| "read more" | Never |
| "here" | Never |
| URL as anchor text | Never |

---

## Featured Snippet Optimisation

Google awards featured snippets for three formats. Every page must target at least two.

### Paragraph Snippet (Definition / Explanation)

**Target queries:** "What is [subject] IGCSE?" / "How does online chemistry tutoring work?" / "What do IGCSE Chemistry tutors teach?"

**Format rules:**
- First sentence of the paragraph must answer the query directly in 40 words or fewer
- No preamble ("In this section we will discuss...")
- No hedge language ("generally," "typically," "in most cases")
- The paragraph must stand alone — it must make complete sense without the surrounding content

Note: The 40-word snippet limit is intentionally tighter than the 50-word paragraph ceiling. Snippet-targeted paragraphs must be shorter than regular body paragraphs.

### List Snippet (Steps / How-To)

**Target queries:** "How to improve IGCSE Chemistry grade" / "Steps to prepare for A Level Maths exam"

**Format rules:**
- Use a numbered or bulleted HTML list (not inline commas)
- 5–8 items maximum
- Each item: 8–15 words, starts with a verb
- Introduce the list with one sentence under 20 words
- The list must answer the query without reading the rest of the page

### Table Snippet (Comparison / Data)

**Target queries:** "Cambridge IGCSE Chemistry topics" / "Difference between IGCSE and GCSE Chemistry"

**Format rules:**
- HTML table with clear column headers
- 5–8 rows
- Column headers must include the subject or curriculum name
- Table intro sentence: under 25 words, states what the table shows

---

## AEO/GEO Optimisation Rules

Apply these rules to every paragraph written, not just FAQs. AI Overviews, Perplexity, and ChatGPT extract content based on directness, factual density, and entity specificity.

### Core Paragraph Rules

1. **Open with the answer, not the question** — AI engines scan for direct statements, not build-ups
2. **One idea per sentence** — Complex compound sentences cannot be easily extracted and cited
3. **Use specific numbers and facts** — "94–97% student success rate" is citable; "great results" is not
4. **Avoid hedging language** — "We try to," "we hope to," "students may" will not be cited
5. **Name the subject, curriculum, or service explicitly** — Don't rely on pronouns; AI needs clear referents
6. **Keep paragraphs self-contained** — Each paragraph should make complete sense on its own, out of context. Do not reference "the section above" or "as mentioned." Restate necessary context briefly in each paragraph.

### Declarative Sentence Structure

Every paragraph must open with a declarative sentence that:
- Names the subject explicitly (not "it" or "the subject")
- Names the curriculum or board explicitly (not "the exam" or "your course")
- Contains a specific fact, number, or named process
- Can be read as a standalone quote out of context

**Pass:** Tuitional's Cambridge IGCSE Chemistry tutors cover specification 0620 in full, including Core and Extended tiers.

**Fail:** Our tutors cover everything you need for your chemistry exams.

### Entity Specificity Rules

AI systems rank explicit entities over vague references. Name everything:
- Always say "Cambridge IGCSE Chemistry (0620)" not "Cambridge Chemistry"
- Always say "Edexcel 1CH0" not "Edexcel Chemistry"
- Always say "AQA 8462" not "AQA"
- Always say "Grade A*" not "top grade"
- Always say "4.7 on Trustpilot" not "highly rated"
- Always say "1,100+ tutors" not "hundreds of tutors"

### People Also Ask (PAA) Targeting

Every FAQ question must map to a real PAA box. Format FAQ questions as natural search queries, not as brand-focused questions.

**Pass (maps to PAA):** "Which exam boards do online Chemistry tutors cover?"

**Fail (too branded):** "Why is Tuitional the best choice for Chemistry tutoring?"

---

## E-E-A-T Signals (Experience, Expertise, Authoritativeness, Trustworthiness)

Google's quality guidelines place particular weight on E-E-A-T for YMYL-adjacent topics, which includes educational services affecting exam results and university admissions.

### Experience Signals

Write copy that shows Tuitional's tutors have real, direct experience with these exams — not just knowledge of them.

**Experience signal patterns:**
- "Our tutors have marked real Cambridge 0620 papers" (not "are familiar with the mark scheme")
- "Sessions use past papers from the last 5 exam series" (not "we use past papers")
- "Your tutor will have sat A Level [Subject] at a Russell Group university" — only write this if it is verifiably true for Tuitional's tutor pool. If uncertain, use: "All [Subject] tutors hold a degree in [Subject] or a related discipline"

### Expertise Signals

Per-subject expertise markers to include in the tutor expertise section:
- The subject's degree requirement for tutors
- The specification code(s) the tutors are trained on
- At least one mark-scheme-specific reference (e.g. "stoichiometry calculations require the working to be shown to earn method marks under all three boards")
- At least one board-comparison insight (e.g. "Cambridge 0620 uses Core and Extended tiers; Edexcel 1CH0 does not — our tutors are trained on both structures")

### Authoritativeness Signals

Include at least two in the page body:
- "4.7 out of 5 on Trustpilot" — with "Trustpilot" always named
- "120,000+ tutoring hours delivered across all subjects"
- "1,100+ tutors, each screened through a 16-step process"
- "UAE-licensed and registered"
- Success rate: "87–97.2% of students working with featured Tuitional tutors reach their target grade"

### Trustworthiness Signals

- No contracts: state this explicitly in FAQ and/or How It Works section
- Matching speed: less than 6 hours — always a specific claim
- Parent dashboard: name all five features (attendance records, upcoming classes, real-time schedule, platform updates, tutor chat)
- Free academic counselling: mention in context of the onboarding process

---

## Citation Eligibility Criteria

These determine whether AI engines can extract and cite your content. Apply to every paragraph. Note: these criteria are intentionally tighter than the page-level word count ranges to maximise AEO/GEO eligibility.

| # | Rule | Requirement |
|---|---|---|
| 1 | Answer Placement | Lead with a direct answer in the first sentence — under 20 words |
| 2 | Paragraphs | 42 words or less. Plain language. Grade 5–7 reading level |
| 3 | Bullet Points | 1 summary sentence (under 40 words) before bullets. Max 6 bullets. All bullets combined: 45 words or less |
| 4 | Tables | 3–7 rows, 2–4 columns max. 5–15 words per cell. 80 words total. Add 30–40 word summary above and 1–2 line explanation below |
| 5 | Headings | Question-based where possible. Under 10 words |