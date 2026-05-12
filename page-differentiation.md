# page-differentiation.md — Content Variation and Anti-Duplicate System

Version: 1.1 — Tuitional SEO Copywriter Agent

This file exists because the agent has previously produced near-identical content across subject pages — same headings with the subject name swapped, same statistics used as leads, same H2 patterns repeated. This file prevents that.

**Load this file at Stage 2 (Step 3.5 of the workflow), alongside `component-variance.md`.** The rules here apply at H2-selection time, not before — loading earlier wastes tokens.

---

## BATCH UNIQUENESS MATRIX — Fill Before Writing Page 1

Before writing any page in a batch, fill this table. The rest of the file lists 10 cross-page uniqueness rules; the matrix is how you satisfy them in one place. After the matrix is filled, batch-uniqueness checks during writing become a lookup, not an in-head derivation.

For a single-page run, fill row 1 only. For a batch, fill one row per page.

| # | Page (subject + city) | Angle | First-H2 framework | Opening structure | Lead stat | Pain point opener | tutor_program card title set (anchor) | University / career ref | FAQ Q7-8 angle | Testimonial detail | Anchor phrasing |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 |   |   |   |   |   |   |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   |   |   |   |   |
| 3 |   |   |   |   |   |   |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   |   |   |   |   |
| 5 |   |   |   |   |   |   |   |   |   |   |   |

**Fill rules:**
- Angle — pick from PART 1 (subject pages, 1-10) or PART 7.1 (location pages, L1-L8). No two pages share the same angle.
- First-H2 framework — pick from PART 2 (Outcome-first / Challenge-first / Question / Stat-led / Curriculum-specific / Subject insight). No two pages share.
- Opening structure — S1-S4 for subject pages (PART 3) or CL1-CL4 for location pages (PART 7.3). No two pages share.
- Lead stat — pick from PART 4 table. No two pages share. Each stat lands on at most one page in the batch.
- Pain point opener — for subject pages, the first `why_igsce` opener pain point (component-variance.md table). No two pages share.
- Card title set anchor — name the most distinctive card title; the full set is in the page YAML. No two pages share any card title.
- University / career ref — university name or career route used in `why_igsce_5`. No two pages share.
- FAQ Q7-8 angle — even though most templates only show Q1-Q6, the differentiation rule still applies to whichever Qs cover schools and outcomes.
- Testimonial detail — grade range + subject detail used in `what_our_student_says`. No two pages share.
- Anchor phrasing — the exact link text used in contextual interlinks. No two pages share.

**Verification:** after filling, scan each column. If any column has the same value in two rows, change one before starting Page 1.

---

---

## PART 1 — CONTENT ANGLE ASSIGNMENT

Every subject page must be written from one primary content angle. The angle shapes the emphasis of the whole page — which problems get named first, which proofs get featured, which outcomes get highlighted.

### The 10 Content Angles

Before writing, select one angle from this list. Record it in the pre-writing block of your output.

| # | Angle Name | Lead with | Best for subjects |
|---|---|---|---|
| 1 | Exam Technique | The gap between knowing content and earning marks — command words, mark allocation, worked examples | All sciences, Maths, English |
| 2 | Concept Mastery | The specific hard concepts that trip students up in this subject — what they are and how to actually grasp them | Chemistry, Physics, Further Maths, Economics |
| 3 | Grade Gap Closure | The measurable distance between current and target grade, and the plan to close it | Any subject where student has a specific target grade |
| 4 | Curriculum Precision | What makes this board's exam different from others — Core vs Extended, HL vs SL, required practicals | Multi-board pages (Chemistry, Biology, Physics, Maths) |
| 5 | University Gateway | What this grade means for university applications and future careers — specific courses and requirements | A Level subjects, IBDP subjects |
| 6 | Parent Confidence | How parents stay informed, track progress, and remain in control of their child's learning | All subjects — particularly for parents of IGCSE students |
| 7 | Past Paper Mastery | Past papers as the primary preparation tool — how to use them, what marks reward, how sessions are structured | Any exam board subject |
| 8 | Syllabus Depth | The breadth and specificity of the curriculum — what students are actually expected to learn and do | Subjects with complex or long syllabi: Maths, History, Biology |
| 9 | Confidence Building | The psychological journey from academic anxiety to exam confidence — and the role of personalised support | Any subject — particularly for students who have failed or underperformed |
| 10 | Mock Performance | Mocks as a diagnostic — how results identify gaps, how sessions address them, what the data shows | All subjects, particularly pre-exam period |

### How to Assign Angles to a Batch of Pages

If writing multiple subject pages in the same session, assign angles systematically — never use the same angle for two consecutive pages.

**Suggested angle rotation for the 13 subject pages on tuitionaledu.com:**

| Subject | Recommended Angle | Reasoning |
|---|---|---|
| Chemistry | Curriculum Precision (4) | Three boards with distinct structures — Core/Extended, tiers, required practicals |
| Physics | Exam Technique (1) | Marks lost on method and formula recall, not just concepts |
| Biology | Syllabus Depth (8) | One of the longest syllabi — breadth of coverage is a strong proof point |
| Mathematics | Grade Gap Closure (3) | Maths is the most quantifiable — targets are clear, gaps are measurable |
| Further Mathematics | Concept Mastery (2) | The jump in difficulty from Maths to Further Maths is a strong pain point |
| Additional Mathematics | Exam Technique (1) | Algebraic method marks are frequently lost — technique is the core message |
| Accounting | Curriculum Precision (4) | Cambridge 0452 vs Edexcel — specific board knowledge matters |
| Economics | Concept Mastery (2) | Abstract concepts (multiplier, elasticity, BoP) are genuinely hard to grasp |
| Business Studies | Past Paper Mastery (7) | Case study questions require specific paper technique |
| Computer Science | Syllabus Depth (8) | Broad technical syllabus — coverage depth is the reassurance needed |
| History | Confidence Building (9) | Subjective subject — students often lose confidence due to inconsistent marks |
| Geography | University Gateway (5) | Gateway to environmental, planning, and international studies degrees |
| Arabic | Parent Confidence (6) | Language learning — parents want visibility of progress and method |

---

## PART 2 — HEADING VARIATION SYSTEM

No two H2 fields across any two pages in the same batch should follow the same structural pattern. Use this framework library and rotate.

### The 6 Heading Frameworks

Reference these by name, not by code. Do not assign "F1" through "F6" anywhere in planning — write the actual framework name (e.g. "Outcome-first") next to each heading.

| Framework | Pattern | Example |
|---|---|---|
| Outcome-first | "[Specific grade or result] + [what it requires]" | "Grade A in Physics Starts With Mark Scheme Literacy" |
| Challenge-first | "Why Students Lose Marks in [Subject] (And How We Fix It)" | "Why Students Lose Marks in Accounting (And How We Fix It)" |
| Question | "[Searchable question about this subject at this level]" | "Which IGCSE Economics Topics Carry the Most Exam Weight?" |
| Stat-led | "[Specific Tuitional data point] + [implication]" | "94% of Our IGCSE Biology Students Improve By at Least One Grade" |
| Curriculum-specific | "[Board] [Code] + [specific exam feature]" | "Cambridge 0620 Core and Extended: What Each Tier Requires" |
| Subject insight | "[Subject-specific concept] + [what it means for the exam]" | "How Organic Chemistry Builds on Atomic Structure at A Level" |

### H2 Assignment Rules

- Every page must use at least 3 different frameworks across its H2 fields
- Never use the same framework for two adjacent H2s on the same page
- Never repeat an exact heading from a previous page (changing the subject name is not enough — the whole heading must be different)
- Every H2 must pass the searchability test: would someone type this into Google as a search query? If no, rewrite it

**Cross-page rule (batch only, NOT for single pages):** When writing multiple pages in one batch, the first H2 of each page should use a different framework. This rule applies only within a single session's batch — the agent does not need to check what frameworks were used on previously-published pages or on a different batch.

### Banned Heading Patterns

These heading structures are forbidden across all pages, in all sessions:

- "[Subject] Tutoring Online" ❌
- "Why Choose [Subject] Tutoring?" ❌
- "How [Subject] Tutoring Works" ❌
- "About Our [Subject] Tutors" ❌
- "Benefits of [Subject] Tutoring" ❌
- "Our Approach to [Subject]" ❌
- "Get Started with [Subject] Tutoring" ❌
- "[Subject] Tutors You Can Trust" ❌
- "The Best [Subject] Tutors Online" ❌
- "What Makes Our [Subject] Tutors Different" ❌
- Any heading that is just [Subject name] + a generic tutoring word ❌

**Test:** Remove the subject name from the H2. If the remaining words could appear on any tutoring website for any subject, the heading fails. Rewrite it.

---

## PART 3 — OPENING SENTENCE VARIATION

The opening sentence of each `why_igcse` body section must vary across the page and across pages in the same batch.

### 4 Opening Sentence Structures

| # | Type | Pattern | Example |
|---|---|---|---|
| S1 | Stat-led | "[Specific number] + [what it means]" | "94% of Tuitional's IGCSE Chemistry students improve by at least one grade within a term." |
| S2 | Problem-led | "[Specific pain point] + [why it happens]" | "Students lose most marks in Biology not on recall, but on six-mark extended response questions." |
| S3 | Outcome-led | "[Named result] + [how it is achieved]" | "A grade improvement in IGCSE Physics begins with understanding how mark schemes allocate method marks." |
| S4 | Curriculum-specific | "[Board/code] + [specific exam fact]" | "Cambridge IGCSE Maths (0580) sets 40% of its Extended tier marks on algebra and number topics." |

### Rotation Rules

- Never use the same opening structure in two adjacent `why_igcse` sections on the same page
- Never use S1 (stat-led) as the opener for more than 2 sections on the same page
- Across a batch of pages, track which structure was used for the primary intro paragraph. Rotate for every subsequent page

---

## PART 4 — STATISTICS AND DATA ROTATION

The agent has previously used the same statistics as lead facts across multiple pages. These rules prevent that.

### Available Lead Statistics (Pick One Per Page as the Primary Proof Point)

| Stat | Use as primary on |
|---|---|
| "94% of featured tutors' students reach their target grade" | Maths, Physics |
| "97.2% student success rate across featured IGCSE tutors" | Chemistry, Biology |
| "120,000+ tutoring hours delivered across all subjects" | Computer Science, Geography |
| "1,100+ tutors, each cleared through a 16-step process" | Accounting, Business Studies |
| "4.7 out of 5 on Trustpilot" | History, Arabic, Economics |
| "Students matched to a tutor in under 6 hours" | Further Maths, Additional Maths |
| "87% minimum success rate across all featured tutors" | General / fallback |

**Rule:** Assign each primary statistic to one page. Do not use the same stat as the lead proof point on two pages. All statistics can still appear elsewhere on any page — this rule only applies to the primary lead proof point in the first `why_igcse` instance on the page.

---

## PART 5 — ANTI-TEMPLATE BODY CONTENT RULES

These rules ensure the body paragraphs of every page feel original, not templated.

### 5.1 Subject-Specific Content in why_igcse Instances

Subject-specific pain points, why study/university gateway content, and other per-subject content patterns are defined in `component-variance.md`. Refer to that file for the full content examples and rules.

The differentiation rule here is: **no two pages in a batch may use the same pain point lead, the same university reference, or the same opening sentence structure** in the same component instance position.

### 5.2 tutor_program Feature Cards — No Repeated Card Titles Across Pages

The cards in `tutor_program` instances must have unique headings that reflect THIS subject's learning process — not generic tutoring features. Example of what to avoid:

**Banned generic card titles (these appear on multiple pages — never reuse):**
- "Learning Gaps" ❌ (unless rewritten with subject specificity)
- "Concept Mastery" ❌ (generic — every subject page uses this)
- "Progress Tracking" ❌ (describe what progress tracking looks like for THIS subject)
- "Pick Your Time" ❌ (scheduling is not a subject-specific feature)

**Instead:** Card titles must reference the subject's actual structure or exam format. Examples:
- Chemistry: "Stoichiometry Method" | "Mark Scheme Precision" | "Practical Paper Prep" | "Equation Recall" | "Board Comparison" | "Topic Sequencing"
- Maths: "Algebraic Method Work" | "Proof Writing" | "Calculator vs Non-Calculator" | "Mark Scheme Literacy" | "Grade Boundary Targeting" | "Topic Triage"
- History: "Source Analysis" | "Essay Structure" | "Causation Arguments" | "Markband Awareness" | "Context and Significance" | "Practice Papers"

---

## PART 6 — BULK PAGE PRODUCTION PROTOCOL

When writing multiple subject pages in a single session, follow this protocol to guarantee every page is genuinely different.

### Pre-Writing Batch Log

Before writing the first page, create a batch log in your pre-writing block:

```
BATCH LOG — [Date] — [Number of pages]
Pages in this batch: [List all]

Page 1: [Subject] — Angle: [#] — Lead stat: [Which stat] — H2 frameworks: [Which three]
Page 2: [Subject] — Angle: [#] — Lead stat: [Which stat] — H2 frameworks: [Which three]
[Continue for all pages]
```

No two pages in the batch should share the same: angle number, lead stat, or opening framework for the first `why_igcse` instance.

### Cross-Page Uniqueness Checks

Before submitting each page in a batch, verify:
- [ ] The first `why_igcse` H2 is structurally different from the same on the previous page
- [ ] The first `why_igcse` opening sentence uses a different structure (S1/S2/S3/S4) from the previous page
- [ ] The `tutor_program` card titles are all different from the previous page
- [ ] The lead statistic is different from the previous page's lead stat
- [ ] The university/career `why_igcse` instance references a different career path or university route from the previous page

### Mandatory Uniqueness Test

After writing all pages in a batch, read the first `why_igcse` H2 from every page aloud. If any two sound similar enough that you could swap the subject name and they would still make sense — rewrite the weaker one.

---

# PART 7 — LOCATION PAGE DIFFERENTIATION SYSTEM

This part applies exclusively to Subject + Location Pages. Load it in addition to Parts 1–6 when writing any page in that category.

---

## 7.1 Location Content Angles

Every location page must be written from one primary angle. The angle determines what gets lead emphasis — which local pain point is named first, which trust signal is foregrounded, which city-specific fact opens the argument.

| # | Angle Name | Lead with | Best for cities |
|---|---|---|---|
| L1 | School Fit | Specific schools in this city and the boards they use — Tuitional is trained on all of them | Dubai, Abu Dhabi (large diverse school landscapes) |
| L2 | Expat Transition | Students who arrived mid-curriculum and need to bridge between boards or systems | Dubai, Riyadh, Doha (high expat turnover) |
| L3 | Online Advantage | Why online tutoring is specifically advantageous in this city — no commute, traffic, heat, timezone alignment | Dubai, Riyadh, Jeddah |
| L4 | University Pipeline | What this subject grade means for the specific universities these families target | Beirut, Kuwait, Muscat (strong UK/US university focus) |
| L5 | Parent Control | Parents who need real visibility — dashboard, session notes, tutor communication | All cities — use when subject angle already uses parent angle |
| L6 | Exam Recovery | Students who underperformed in mocks and need targeted preparation before the real exam | All cities — strong for peak exam season content |
| L7 | Board Precision | This city's schools use specific boards — Tuitional's tutors are trained on exactly those, not generic | Sharjah (CAIE dominant), Dammam (CAIE + AP) |
| L8 | Local Scarcity | Specialist subject tutors are hard to find locally — online solves the gap | Dammam, Muscat, Beirut, Kuwait |

### Angle Assignment for Bulk City Batches

When writing the same subject across multiple cities, assign angles to ensure no two cities use the same angle:

**Chemistry across all cities — suggested angle assignments:**
| City | Angle |
|---|---|
| Dubai | L1 (School Fit) |
| Abu Dhabi | L4 (University Pipeline) |
| Sharjah | L7 (Board Precision) |
| Riyadh | L3 (Online Advantage) |
| Jeddah | L2 (Expat Transition) |
| Dammam | L8 (Local Scarcity) |
| Doha | L6 (Exam Recovery) |
| Kuwait | L4 (University Pipeline) |
| Muscat | L8 (Local Scarcity) |
| Beirut | L3 (Online Advantage) |

Rotate this pattern for other subjects. No two pages in the same batch should share an angle.

---

## 7.2 Location-Specific Heading Variation

Location page H2s must include the city name OR a board name common in that city. Generic headings without a location signal are not acceptable.

**Banned heading patterns for location pages:**
- "Why Choose Online [Subject] Tutoring" ❌ (no city)
- "How [Subject] Tutoring Works" ❌ (no city, same as subject page)
- "Our [Subject] Tutors Are the Best" ❌
- "Benefits of Online Tutoring" ❌
- "[Subject] Tutoring for All Boards" ❌ (no city)

**Required heading elements (at least one per H2):**
- City name: "in Dubai", "for Dubai Students", "in Riyadh"
- Board name specific to this city: "Cambridge 0620 in Dubai", "CAIE Schools in Muscat"
- Local school reference: "Dubai's International Schools"
- Local outcome: "UK University Entry from Dubai", "IGCSE Results for Riyadh Students"

---

## 7.3 City-Specific Opening Sentence Structures

The opening sentence of the first `why_igcse` instance must vary across pages in the same batch. Use these structures and rotate:

| # | Type | Pattern | Example |
|---|---|---|---|
| CL1 | School-led | "[Number or name] of [City]'s international schools follow [Board] for [Subject]" | "Most of Dubai's international schools follow Cambridge IGCSE Chemistry (0620) or Edexcel 1CH0." |
| CL2 | Gap-led | "[Subject] marks in [City] are most commonly lost on [specific skill], not on topic knowledge" | "Chemistry marks in Riyadh's international schools are most commonly lost on stoichiometry method, not on concept recall." |
| CL3 | Outcome-led | "[Specific % or stat] of Tuitional students in [City/region] reach their target [Subject] grade" | "94% of featured Tuitional tutors' IGCSE Chemistry students reach their target grade — including students across Dubai's school network." |
| CL4 | University-led | "Students in [City] aiming at [destination] universities need [specific grade] in [Subject]" | "Students in Kuwait aiming at UK Russell Group universities need Grade A in A Level Chemistry for Medicine and Pharmacy." |

---

## 7.4 Anti-Duplicate Rules for Location Batch Production

The two most common sources of duplicate content on location pages are:

**1. School landscape `why_igcse` instance — this must be completely unique per city**
Every city has a different school list. Never reuse school names from one city's school landscape section on another city's. The school names in city-intelligence.md are the source — use them precisely.

**2. FAQ Q2 (Which schools do your students attend?) — must be city-specific**
This question's answer is the most obvious templated section. Every city's answer must name different schools. Never write a generic answer like "schools across the city" without naming them.

**Cross-page uniqueness checks for location batches:**
Before writing each page, confirm:
- [ ] `tutor_program` card titles reference this city — not a copy of another city's cards
- [ ] First `why_igcse` H2 includes the city name and uses a different framework from the previous page
- [ ] First `why_igcse` opening sentence uses a different CL structure (CL1–CL4) from the previous page
- [ ] School landscape `why_igcse` schools are from city-intelligence.md for this city only
- [ ] Online advantage `why_igcse` instance is city-specific — references this city's context, not generic
- [ ] FAQ Q2 names schools from city-intelligence.md for this city only
- [ ] FAQ Q3 (timezone/sessions) references this city's correct GMT offset

---

## 7.5 Location Page Batch Log Format

Before writing the first page in a location batch, output this table:

| Page | Subject | City | Angle | Opening Structure | H2 Framework |
|------|---------|------|-------|-------------------|--------------|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |

No two pages in the batch may share the same Angle or Opening Structure.

---

# PART 8 — THE UNIQUENESS ENGINE

This is the most important section in this file. Read it before writing the first page of any batch. Every rule here exists because the agent has previously produced content that looked like a template with the subject or city name swapped.

**The test for every page you write:** Remove the subject name and city name from every heading and every opening sentence. If the remaining text could appear on a different page in this batch, the content has failed. Rewrite it.

---

## 8.1–8.5 — UNIQUENESS PRINCIPLES (SUMMARY)

**The 10 elements that must differ across every page in a batch:**
1. Content angle (assigned in Part 1)
2. H2 frameworks (assigned in Part 2)
3. Opening sentence structure (assigned in Part 3)
4. Lead statistic (assigned in Part 4)
5. Subject pain point in the first `why_igcse` instance (see `component-variance.md`)
6. `tutor_program` card titles (never reuse titles across pages)
7. University/career `why_igcse` heading and reference
8. FAQ questions 7 and 8 (must be subject or city-specific)
9. Testimonial grade range and subject detail
10. Contextual interlink anchors (must differ in phrasing)

**Before submitting any batch:** Run the mandatory uniqueness test — confirm no two pages share the same H2 structure in the same component position, the same lead stat, or the same card title set.