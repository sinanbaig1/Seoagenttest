# humanizer.md — Tuitional Humanizer Skill
### Version 3.1 | Scope: Service Pages Only

---

## Purpose

This skill removes AI writing patterns from Tuitional service page copy. It does not add personality, opinions, or voice. It cleans. The goal is copy that reads as professionally written by a human — not copy that reads as creative or editorial.

This skill runs as **Step 8** in the page creation workflow, after the content from Step 6 is complete.

---

## Scaffold-Aware + Stage-1 Operation (updated 2026-05-07)

This file is now Stage-1 loaded (alongside `skills.md`, `facts.md`, `context.md`, `memory.md`, `subject-intelligence.md`). The two-pass model — draft in Step 6, humanize in Step 8 — was retired on 2026-05-07 because it produced three drafts of every paragraph and cost ~10 minutes per page.

**The new operating model is single-pass:** the agent writes humanized copy directly into the scaffold during Step 6. The numeric and structural rules below are now caught by `tools/validate_page.py` in Step 8, not by a Triple-Pass Audit.

**What this means for the rules below:**

- All rules still apply. None are relaxed.
- They apply *during writing*, not after. If the agent writes a paragraph with two em-dashes, the validator flags it; the agent rewrites that paragraph and re-runs the validator. No batch humanization pass.
- The Triple-Pass Audit at the end of this file is now an emergency-only routine. If the validator surfaces issues that look like AI-templated prose (uniform sentence rhythm, "Tuitional"-heavy openers, mechanical -ing endings), run the audit on those specific paragraphs. Do not run it across the whole page.

**Mapping old steps to new flow:**

| Old | New |
|---|---|
| Step 6 (draft) → Step 8 (humanize) | Step 6 writes humanized copy in one pass |
| Triple-Pass Audit | `tools/validate_page.py` (Pass 2 numeric checks) + targeted manual rewrites for AI-pattern flags |
| Loaded at Step 7.5 | Loaded at Stage 1 |

---

## ARCHITECTURAL RULE 1 — Write From Notes, In One Pass

**Compose every body paragraph from notes, not from a drafted version.** When an LLM edits its own output, it uses the same probability distributions that generated the original — surface word swaps do not change the statistical signature that AI detectors look for.

The original version of this rule (2026-04) instructed the agent to *first* draft a paragraph in Step 6, *then* discard the draft and rewrite from notes in Step 8. That two-pass model was retired on 2026-05-07. The agent now writes from notes directly, the first time, in Step 6.

**The correct process for every body copy paragraph:**

1. Extract from the slot's inline comments and the lookup data (subject row in `subject-intelligence.md`, city row in `city-intelligence.md`): the key fact(s), keyword(s), and word-count range.
2. Hold those notes in mind. Do not draft prose in `<thinking>` blocks before writing to the file.
3. Write the paragraph straight into the YAML, applying humanizer rules from the first sentence (contractions, opener variety, sentence-length variation, no em-dashes).
4. Run `tools/validate_page.py` after the YAML is complete. If a paragraph fails (over word cap, em-dash present, banned word, etc.), rewrite that one paragraph from notes and re-run the validator.

**When a validator pass surfaces "this still reads as AI-templated":** that is the only case where the original rule's "discard and rewrite" approach kicks in. Discard the failing paragraph's text, re-extract its notes, write a structurally different version. The Triple-Pass Audit at the end of this file is the manual rewrite routine for those cases.

**Example (single-pass writing from notes):**

Notes: [board-specific tutors / CAIE or OCR / sessions follow syllabus / 15–25 words]

Written direct to file:
> Your tutor covers one board, either CAIE or OCR, and every session follows that syllabus directly.

---

## ARCHITECTURAL RULE 2 — Process Sections in Isolation, Not as a Batch

**Do not pass the entire page to the humanizer at once.** Batch processing applies the same humanization lens uniformly across every paragraph. Uniform quality across all sections is itself an AI pattern — detectors look for it.

**The correct process:**
- Pass one CMS component at a time
- For each component, vary the approach deliberately — some get heavy restructuring, some get a lighter pass
- Never apply identical sentence rhythm strategies to two consecutive components
- The deliberate variation in treatment across sections creates the natural inconsistency detectors expect from human writing

---

## Scope — What This Skill Applies To

### Run humanizer on:
- Body copy paragraphs (intro, service description blocks, supporting paragraphs)
- FAQ questions and answers

### Never run humanizer on:
- H1, H2, H3, H4 headings
- Bullet point terms and descriptions
- CTA button text
- Meta title and meta description
- Tutor profile snippets
- Table cell content (cells are labels, not prose)
- Summary sentences above tables
- Follow-on sentences below tables

Structural elements are off-limits. Word count limits and keyword placements in those sections must not be disturbed.

---

## Person and Voice Framework

Tuitional service pages use a deliberate person structure. The humanizer must preserve this — never flatten it to a single voice.

| Section Type | Person | Purpose |
|---|---|---|
| Hook / Opening | Second-person | Speak to the parent's pain or desire |
| Value Proposition | Second-person | Make the outcome about them |
| Credibility / Proof | First-person (we/our) | Introduce Tuitional's track record |
| CTA | Second-person | Push to action |

**Example of correct person usage:**

> "Is your child struggling with IGCSE Maths?" *(second-person hook)*
>
> "Give your child 1:1 personalised support from qualified tutors." *(second-person value prop)*
>
> "We've helped students across the Middle East achieve A and A* results." *(first-person credibility)*
>
> "Book a demo class today." *(second-person CTA)*

The humanizer must not convert first-person credibility statements to second-person, or vice versa. The structure is intentional.

---

## Do Not Touch List

The humanizer must never rephrase, remove, or soften the following:

- Specific success rate figures — "97.2%," "87–97.2% per featured tutor" (see `facts.md` §1)
- Tutoring hour counts — "120,000+ tutoring hours"
- Tutor credential specifics — "16-step screening process," "15,000+ hours taught"
- Trustpilot rating — "4.7/5 on Trustpilot"
- Student and tutor counts — "600+ students," "1,100+ tutors screened"
- Primary keyword placement in the intro paragraph
- Any term on the approved hyphenated whitelist (see below)
- Any term explicitly included per the page brief

These are trust signals and SEO anchors. They are not promotional inflation — they are verifiable facts and must remain intact and in their original position.

---

## Approved Hyphenated Terms — Do Not Flag

The following hyphenated compounds are standard in education and ed-tech copy. Do not flag or remove them:

> one-to-one, student-centered, exam-focused, curriculum-aligned, real-time, live-online, AI-powered, on-demand, high-quality, exam-ready, test-ready, risk-free

All other hyphenated word pairs should not be included.

---

## Keyword Preservation Rule

Before humanizing any paragraph, identify whether it contains:
- The primary keyword
- A secondary keyword
- A heading keyword variation

If yes — the keyword must appear in the same position (ideally same sentence) after humanization. The humanizer may rephrase around it but never move, dilute, or remove it.

After humanization, run a keyword check on every paragraph that was modified. If any keyword has been displaced, restore it before finalising.

---

## Word Count and Format Compliance

All word count ranges, bullet rules, table rules, and readability standards are defined in `skills.md`. Do not restate them here.

The humanizer must:
1. Stay within the word count ranges from `skills.md` for every paragraph it rewrites
2. Vary lengths within each range — do not cluster every paragraph at the midpoint or ceiling. Clustering is a detectable AI signal.
3. Not modify any structural element (tables, bullets, headings, card grids)
4. Verify in Pass 3 of the Triple-Pass Audit that all `skills.md` format rules still pass after body copy edits

---

## ARCHITECTURAL RULE 3 — Opener Variety (Max 30% "Tuitional" Openers)

AI defaults to leading every paragraph with the subject entity. On Tuitional pages this produces a page where 80%+ of paragraphs open with "Tuitional" or "Tuitional's." That uniformity is a strong detection signal.

**Rule:** No more than 30% of body copy paragraphs on a page may open with "Tuitional" or "Tuitional's."

**Permitted opener types to rotate through:**
- Student/parent perspective: "Your child's tutor is matched to..." / "When your child starts..."
- Benefit-first: "Every session follows..." / "Results are tracked..."
- Conditional: "If your child is sitting CAIE exams..."
- Imperative (for CTA-adjacent paragraphs): "Book a demo session..."
- Credibility-first: "We've delivered 120,000+ hours..."
- Mid-thought: "Matched to your exam board, each tutor..."

After humanizing, count how many paragraphs open with "Tuitional." If the count exceeds 30%, rewrite the openers of the excess paragraphs using the types above before finalising.

---

## ARCHITECTURAL RULE 4 — Sentence Length Variation (Standard Deviation, Not Insertion)

Do not insert short sentences as a mechanical burstiness fix. AI detectors have caught up to this pattern — a fragment inserted after every first long sentence becomes detectable across pages.

**The correct rule:** Aim for a standard deviation of at least 5 words in sentence length across all sentences in each component. This means genuinely varying how thoughts are constructed — not adding a 4-word fragment to satisfy a checklist.

**Variation should arise from:**
- Sometimes using a question instead of a statement
- Sometimes using a compound sentence where two short ones would be expected
- Sometimes using a parenthetical aside (in brackets, not em dashes) mid-sentence
- Sometimes letting a long thought breathe across 25+ words when the content warrants it

**Check:** After writing each component, list approximate word counts for each sentence. If the range spans fewer than 5 words (e.g. all sentences are 16–20 words), restructure until at least one sentence is under 12 words and at least one is over 22 words — but only where the content naturally supports it.

---

## Pattern Priority System

Not all AI patterns are equally important. The humanizer must allocate its effort according to the priority tiers below. Fix as per this weightage and stop when the word count limit is reached.

### CRITICAL — 65% of all changes must come from this tier
These directly affect trust, clarity, SEO ranking, accessibility, and parent comprehension. Always fix these first.

- **Readability** — Grade 5–6 level. Short sentences, simple words, easy to understand.
- **Em and en dashes** — Remove all em dashes and en dashes from body copy. Do not replace with other dashes. Rewrite the sentence using commas, periods, or separate sentences instead.
- **AI vocabulary** — Remove detectable AI word tells immediately
- **Significance inflation** — Strip all filler importance language
- **Excessive hedging** — Remove all over-qualifying statements
- **Generic positive conclusions** — Replace vague closers with specific facts

### MEDIUM — 25% of all changes must come from this tier
These improve sentence flow and style but are secondary to critical patterns.

- Superficial -ing endings
- Transition phrase dependency
- Copula avoidance
- Negative parallelisms

### LOW — 10% of all changes must come from this tier
Do not force these fixes if doing so affects sentence flow or pushes past the defined word count range. Skip and move on.

- Rule of three
- Synonym cycling
- False ranges
- Hyphenated pair overuse

---

## AI Pattern Detection — What to Fix

The following patterns must be identified and removed. Each includes the problem, what to watch for, and the fix. Apply fixes according to the weightage in the Pattern Priority System.

---

### CONTENT PATTERNS

---

**1. Significance Inflation**

Words to watch: *stands as, serves as, is a testament to, marks a pivotal moment, setting the stage for, evolving landscape, underscores, highlights its importance, reflects broader, symbolising its ongoing, contributing to the, indelible mark, deeply rooted*

Problem: Adds importance to statements that don't earn it. Pure filler.

Before:
> Tuitional's IGCSE programme marks a pivotal moment in personalised education, reflecting broader trends in student-centred learning.

After:
> Tuitional's IGCSE programme delivers 1:1 live sessions tailored to each student's syllabus and pace.

---

**2. Superficial -ing Endings**

Words to watch: *highlighting, showcasing, underscoring, emphasising, reflecting, symbolising, contributing to, cultivating, fostering, encompassing*

Problem: Tacked onto sentences to add fake depth. Reads as constructed, not written.

Before:
> Our tutors use structured lesson plans, ensuring comprehensive syllabus coverage and fostering student confidence.

After:
> Our tutors follow structured lesson plans that cover the full syllabus and build student confidence.

---

**3. Generic Positive Conclusions**

Problem: Vague, upbeat endings that say nothing specific.

Before:
> The future looks bright for students who choose Tuitional. Exciting times lie ahead as they continue their journey toward excellence.

After:
> Students who complete Tuitional's IGCSE programme reach a success rate of 87–97.2% per featured tutor.

---

**4. Excessive Hedging**

Problem: Over-qualifying statements damages trust and AEO eligibility simultaneously.

Before:
> Our tutors could potentially help your child improve their results over time.

After:
> Our tutors help students improve their results with structured, curriculum-aligned sessions.

---

### LANGUAGE PATTERNS

---

**5. AI Vocabulary**

Words to watch: *actually, additionally, testament, landscape, showcasing, furthermore, it is worth noting, in today's world, groundbreaking, renowned, vibrant, rich (figurative), profound, breathtaking, must-visit, stunning, nestled, in the heart of, commitment to (vague usage), exemplifies, enhancing its*

Fix: Replace with plain, direct language. If the sentence needs the word to function, rewrite the sentence.

Before:
> In today's educational landscape, it is worth noting that Tuitional offers a groundbreaking approach to IGCSE tutoring.

After:
> Tuitional offers live 1:1 IGCSE tutoring matched to each student's curriculum and learning pace.

---

**6. Copula Avoidance**

Words to watch: *serves as, functions as, stands as, boasts, features* (used instead of is/has)

Problem: Makes copy feel constructed. Simple is/has is clearer and more natural.

Before:
> Tuitional serves as a trusted platform for IGCSE students across the Gulf.

After:
> Tuitional is a trusted IGCSE tutoring platform for students across the Gulf.

---

**7. Negative Parallelisms**

Pattern: *"It's not just X, it's Y"*

Problem: Always weaker than stating the point directly.

Before:
> It's not just tutoring, it's a fully personalised academic support system.

After:
> Tuitional provides personalised academic support, not standard group instruction.

---

**8. Rule of Three**

Problem: AI defaults to grouping items in threes regardless of whether three is the natural number. Use however many items are actually needed, no more, no less.

Before:
> Our tutors deliver clarity, confidence, and consistency in every session.

After:
> Our tutors deliver consistent, curriculum-aligned sessions that build exam confidence.

---

**9. Synonym Cycling**

Problem: Rotating between "tutor / educator / instructor / mentor" unnecessarily. Confuses AI citation engines and feels unnatural on page.

Fix: Pick the most accurate term and repeat it. On Tuitional pages, use "tutor" consistently unless the specific context calls for "Academic Consultant" (which has a defined meaning in the Tuitional model).

---

**10. False Ranges**

Pattern: *"from X to Y, from A to B"*

Problem: Sounds structured, means nothing specific.

Before:
> Tuitional supports students from beginners to advanced learners, from Grade 6 through A-Levels.

After:
> Tuitional supports students from Grade 6 through A-Levels across all major exam boards.

---

**11. Em and En Dash Removal — HARD CONSTRAINT**

Problem: AI overuses em dashes and en dashes as sophistication signals. These are a top AI detection trigger. Remove all em and en dashes from body copy. Do not replace one dash type with another. Rewrite the sentence using a comma, a period, or two separate sentences instead.

Before:
> Our tutors work with your child's school schedule — not against it — to build a consistent routine.

After:
> Our tutors work with your child's school schedule. Sessions fit around school hours to build a consistent routine.

**Step 8.5 — Em Dash Hard Validation (mandatory, runs after all humanization)**

After completing humanization on every component, run a dedicated scan before marking any section complete:

1. Search the full output for em dashes and en dashes
2. For every instance found: reject the sentence and rewrite it without any dash
3. Do not mark the section HUMANIZER PASS: Complete until this scan returns zero results
4. A section is not considered humanized if it contains a single em or en dash, regardless of all other fixes applied

This is a hard constraint, not a guideline. It takes precedence over word count preservation. If removing a dash forces a rewrite that adds 2–3 words, allow it.

---

**12. Transition Phrase Dependency**

Words to watch: *Furthermore, Moreover, In addition, Additionally, It is important to note, It should be noted, In conclusion, To summarise*

Fix: Remove the transition phrase and connect the idea directly, or start a new sentence without a connector.

Before:
> Furthermore, our tutors are available across all time zones. Additionally, sessions can be scheduled around school hours.

After:
> Our tutors are available across all time zones and schedule sessions around school hours.

---

**13. Chatbot Artifacts**

Patterns: *Great question!, Certainly!, Of course!, I hope this helps!, Let me know if you'd like me to expand, Feel free to ask*

These must never appear in any service page output. Flag and delete immediately.

---

**14. Hollow Intensifiers**

Words to watch: *truly, certainly, undoubtedly, it is clear that, without a doubt, absolutely, incredibly*

Problem: They add nothing and weaken the sentence they appear in.

Before:
> Tuitional is truly committed to helping every student achieve their academic potential.

After:
> Tuitional matches every student with a tutor aligned to their curriculum and subject needs.

---

**15. Lack of Contractions**

AI writes "do not" instead of "don't," "it is" instead of "it's," "we have" instead of "we've." Human service page copy, even professional copy, uses contractions naturally. Their absence is a measurable detection signal.

**Rule:** At least 50% of "do not / it is / we have / you are / they are / cannot / will not / does not" instances in body copy and FAQ answers must be contracted.

Before:
> If the match is not right, your Academic Consultant will rematch you at no extra cost.

After:
> If it's not the right match, your Academic Consultant will rematch you at no extra cost.

Do not contract in headings or bullet point labels. Body copy and FAQ answers only.

---

**16. Sentence-Initial Uniformity**

Detectors specifically measure the distribution of first words and first phrases across all sentences on a page. AI defaults to: subject-first, subject-first, subject-first. The result is a page where 70%+ of sentences open with a noun phrase.

**Rule:** Across any three consecutive sentences, at least one must open with something other than a noun phrase. Permitted non-noun openers:

- Prepositional phrase: "Before each session..."
- Adverbial clause: "When your child's results come in..."
- Coordinating conjunction (natural usage): "But the structure matters..."
- Participial phrase (sparingly): "Matched to your exam board..."
- Direct question: "What does that mean in practice?"

After humanizing each component, scan the first word of every sentence. If more than two consecutive sentences start with the same grammatical type (especially noun/proper noun), restructure at least one opener.

---

**17. Lexical Diversity (Narrow Vocabulary Under Word Count Pressure)**

AI constrained by tight word limits draws from a smaller vocabulary, repeating the same nouns, verbs, and modifiers across paragraphs. On a Tuitional page this typically means overuse of: "tutors," "sessions," "students," "board," "syllabus," "matched."

**Rule:** Within any single component, no content word (noun, verb, adjective) should appear more than twice unless it is a keyword or a term on the Do Not Touch list.

Fix by: using pronouns where the referent is clear, restructuring the sentence to avoid the repeated word, or choosing a more specific word (e.g. "lesson" instead of a third "session").

---

**18. Grammatical Perfection as an AI Signal**

Human copy occasionally has a preposition at the end of a sentence, a slightly informal turn of phrase, or a sentence that starts with "And" or "But." AI produces grammatically flawless output throughout. That flawlessness is itself a signal.

**Rule:** Allow one mild imperfection per page section, not an error, but a natural informal construction. Options:

- Sentence-ending preposition: "...the board they're qualified for."
- Conjunction opener: "And that's what the 16-step screening process is for."
- Contracted informal phrase: "That's usually sorted within 10 minutes."

Do not introduce more than one per section. Do not introduce grammatical errors. The goal is one natural human moment per section, not deliberate awkwardness.

---

**19. Hyphenated Pair Overuse**

Problem: AI hyphenates common word pairs with perfect consistency. Humans are less uniform.

Fix: Remove hyphens from common compound modifiers unless they are on the approved whitelist or are technical compounds required for clarity.

Approved whitelist terms are exempt — do not flag them. See the Approved Hyphenated Terms section above.

---

## FAQ Answer Structure Rotation

Every FAQ answer on an AI-generated page follows the same structural pattern: [Brand/Entity] + [specific claim] + [supporting detail]. Six identical structures in a row is a strong detection signal.

**Define the answer structure for each FAQ before writing it. Rotate through these four templates — no two consecutive FAQ answers may use the same template.**

| Template | Structure | Example opener |
|---|---|---|
| A — Direct answer first | Lead with the answer in one sentence. Follow with one supporting detail. | "Yes. Every tutor at Tuitional clears a 16-step screening process..." |
| B — Concern acknowledgement | Name the concern or scenario, then answer it. | "If your child is sitting OCR, their tutor is matched to OCR specifically..." |
| C — Conditional / It depends | Open with the condition, then give the specific answer. | "Pricing varies by subject level and session frequency. Your Academic Consultant..." |
| D — Outcome first | Lead with the outcome or result, then explain how. | "Most students are matched within 10 minutes. Your Academic Consultant manages..." |

After writing all 6 FAQ answers, review the template sequence. Fix any two consecutive answers using the same template before finalising.

---

## The Triple-Pass Audit

After writing all body copy paragraphs, run all three passes before finalising output.

**Pass 1 — Pattern Scan**
Re-read every paragraph that was modified. Ask:
> "What in this paragraph still reads as obviously AI-generated?"

List remaining tells briefly. Fix each one.

**Pass 2 — Hard Constraint Checks (all must pass before marking complete)**
- [ ] Step 8.5 em/en dash scan: zero dashes in output (see pattern 11)
- [ ] Opener check: no more than 30% of paragraphs open with "Tuitional" or "Tuitional's"
- [ ] Sentence length SD: at least one sentence under 12 words and one over 22 words per component
- [ ] Contractions: at least 50% of eligible "do not / it is / we have" instances are contracted
- [ ] FAQ templates: no two consecutive answers use the same template (A/B/C/D)
- [ ] Sentence-initial variety: no three consecutive sentences open with the same grammatical type
- [ ] No sentence exceeds 30 words
- [ ] Grade 5–7 readability throughout

**Pass 3 — Tuitional Compliance Check**
For every modified paragraph, confirm:
- [ ] Word count is within the range defined in `skills.md` for that section type
- [ ] Primary or secondary keyword is in its original position (if applicable)
- [ ] No item from the Do Not Touch list has been changed
- [ ] Person (first/second) matches the section type in the Voice Framework above
- [ ] No banned words from `claude.md` have been introduced
- [ ] No AI vocabulary words remain
- [ ] All `skills.md` format rules still pass (bullet summary sentences, table dimensions, etc.) — the humanizer must not have broken structural compliance

Only after all three passes are clear should the section be marked ready for CMS entry.

---

## Output Format

The humanizer does not produce a separate document. It updates the content drafted in Step 6 of the workflow in place. The final section sheet formatting happens in Step 10, after humanization is complete.

The humanizer does not need to annotate every paragraph it touches. It silently rewrites body copy and FAQs to remove AI patterns. Only output a brief summary at the end of the humanization pass:

```
HUMANIZER SUMMARY
Paragraphs modified: X of Y
Em dashes removed: X
Tuitional opener count: X% (cap: 30%)
FAQ template sequence: A/B/C/D/A/B (no consecutive repeats)
Triple-pass audit: Pass
```

Do not output per-paragraph CHANGES MADE annotations during humanization — they consume tokens without improving output. The Pass 3 compliance check covers verification.

---

## What This Skill Does Not Do

To be explicit — this skill does not:

- Add opinions, personality, or editorial voice
- Introduce first-person unless the section type calls for credibility statements
- Expand copy beyond word count ranges
- Rewrite headings, bullets, CTAs, or table content
- Remove or soften trust signals, statistics, or credentials
- Apply voice calibration or style matching
- Produce a separate humanized draft — it updates the existing output sheet