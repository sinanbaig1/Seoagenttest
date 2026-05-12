# component-variance.md — CMS Component Capabilities and Content Patterns

---

## Purpose

This file documents what each CMS component type is designed to hold — its fields, the types of content it supports, and what it cannot hold. The agent uses this file to understand what content fits inside each component when the spreadsheet template defines the page sequence.

The spreadsheet template tells the agent **which components appear and in what order**. This file tells the agent **what each component can contain**.

The page brief tells the agent **what specific content to write** in each component instance.

---

## Component Instance Naming Convention

When a component type is used more than once on a page, the CMS appends a numeric suffix to differentiate instances:

- **Single use:** The component keeps its base name — e.g. `why_igcse`
- **Multiple uses:** The first instance keeps the base name `why_igcse`. Subsequent instances become `why_igcse_1`, `why_igcse_2`, `why_igcse_3`, and so on.

All suffixed instances share the same fields and capabilities as the base component. `why_igcse_3` has exactly the same fields as `why_igcse` — the suffix only identifies which instance it is on the page.

The same rule applies to every reusable component: `tutor_program` / `tutor_program_1`, `what_our_student_says` / `what_our_student_says_1`, etc.

**When reading the template:** Match each suffixed key to its base component type in this file to understand what fields and content it supports. When writing output, always use the exact suffixed key from the template — not the base name.

### Important: Match the template's exact spelling

Some templates use the spelling `why_igsce` (a typo retained in the CMS) instead of `why_igcse`. Other templates capitalise `Faqs` rather than `faqs`. Always use the exact spelling and capitalisation from the template you are given — do not normalise to a "correct" spelling. The template is the source of truth for keys; this file describes the component's capabilities regardless of how the key is spelled.

---

## with_form — Hero Section with Form

**Fields:**
- H1 Tag field → Main page headline
- Paragraph field → Subheading/description text (the hero/intro paragraph)
- Image Alt Text field → Alt text for the hero image

**Content it holds:**
- The page's H1 (primary keyword, under 60 characters / 10 words)
- The hero/intro paragraph (25–50 words) — a declarative, factual opening statement
- Image alt text for SEO/accessibility

**Content it cannot hold:**
- Bullet lists, tables, or multi-paragraph body copy
- FAQ content
- Link arrays or subject lists

**Notes:**
- The right side displays a contact form automatically — no content input needed for the form
- This is the first thing visitors see. Content must establish credibility within 5 seconds
- CTA is built into the form — no separate CTA button field

---

## school_logos — School Logo Strip

**Fields:**
- Checkbox (isShow) → Toggle to show/hide

**Content it holds:**
- None — this is a display toggle only. School logos are pre-loaded in the CMS.

**Notes:**
- Set to `true` to display, `false` to hide
- No text content is written for this component

---

## tutor_program — Content Block (Card Grid with CTA)

**Fields:**
- H2 Tag field → Section heading
- Large text area → Accepts raw HTML (card grid layout)
- Button Title field → CTA button text
- Button Link field → Set to `popup` to trigger contact form

**Content it holds:**
- An H2 heading (under 10 words, must contain a secondary keyword where natural)
- An HTML card grid — either feature cards or sign-up steps (see formats below)
- A CTA button

**Two content formats this component supports:**

### Format A — Feature Cards (primary use)

A grid of 6 cards, each with an H3 title and a short paragraph description. The agent must output the full HTML structure including the `<style>` block.

**HTML template:**
```html
<style>
  .tuitional-program-section {
    max-width: 1100px;
    margin: 20px auto;
    padding: 10px;
    color: #333;
    line-height: 1.6;
  }
  .program-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 25px;
  }
  .program-card {
    padding: 25px;
    border-radius: 12px;
    border: 1px solid rgba(0,0,0,0.08);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    background: rgba(255, 255, 255, 0.4);
    backdrop-filter: blur(5px);
    -webkit-backdrop-filter: blur(5px);
  }
  .program-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0,0,0,0.05);
    border-color: #3498db;
  }
  .program-card h3 {
    margin: 0 0 12px 0;
    font-size: 1.25rem;
    color: #2c3e50;
    display: flex;
    align-items: center;
    font-weight: 700;
  }
  .program-card h3::before {
    content: '✓';
    margin-right: 12px;
    color: #3498db;
    font-weight: bold;
    background: rgba(52, 152, 219, 0.1);
    width: 28px;
    height: 28px;
    min-width: 28px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    font-size: 0.85rem;
  }
  .program-card p {
    margin: 0;
    font-size: 0.95rem;
    color: #555;
  }
  @media (max-width: 768px) {
    .program-grid { grid-template-columns: 1fr; }
  }
</style>
<section class="tuitional-program-section">
  <div class="program-grid">
    <div class="program-card">
      <h3>[Card Title]</h3>
      <p>[Card description — 1–2 sentences]</p>
    </div>
    <!-- Repeat for each card -->
  </div>
</section>
```

**Card rules:**
- Exactly 6 cards
- Each card H3 title must be subject-specific — never generic
- Each card paragraph: 20–30 words, one focused point
- H3 titles do not count toward the 45-word bullet list limit — these are card titles, not bullet labels
- The `<style>` block must be included in full with every instance — it is not loaded globally

### Format B — Sign-Up Steps (secondary use)

A grid of 3 cards showing the sign-up process. Same HTML structure as Format A, but with 3 cards instead of 6, and each H3 is a step name.

**Card rules for sign-up steps:**
- Exactly 3 cards
- Each card H3 is a step name (e.g. "Meet Your Academic Consultant", "Get Matched", "Start Your First Session")
- Each card paragraph: 20–30 words, describes what happens in that step
- Steps must be Tuitional-specific — reference the Academic Consultant, the matching process, or the platform

**Content it cannot hold:**
- Plain paragraphs without the card grid structure
- Tables
- FAQ content
- Link arrays

**Differentiation rule:** Card titles must reference the subject's actual structure or exam format. Never use generic titles like "Learning Gaps," "Concept Mastery," or "Pick Your Time" across multiple pages. Every card title set must be unique to the subject.

**Examples of subject-specific card titles:**
- Chemistry: "Stoichiometry Method" | "Mark Scheme Precision" | "Practical Paper Prep" | "Equation Recall" | "Board Comparison" | "Topic Sequencing"
- Maths: "Algebraic Method Work" | "Proof Writing" | "Calculator vs Non-Calculator" | "Mark Scheme Literacy" | "Grade Boundary Targeting" | "Topic Triage"
- History: "Source Analysis" | "Essay Structure" | "Causation Arguments" | "Markband Awareness" | "Context and Significance" | "Practice Papers"

**Note:** This component is reused multiple times on some page templates (e.g. `tutor_program` and `tutor_program_1`). Each instance can serve a different purpose — one might use Format A (feature cards) while another uses Format B (sign-up steps). The page brief specifies what content goes in each.

---

## why_igcse — Why Choose IGCSE (Rich Content Section)

**Fields:**
- Section Title field (sectionTag) → Top-level section label
- Header field (headerTag) → Sub-heading with tag selector (H2/H3)
- Upload Image → Section image
- Image Alt Text → Alt text for SEO/accessibility
- Paragraph → Main descriptive text
- Button Text → CTA button text
- Button Link → CTA destination

**Content it holds:**
- A section title (top-level label for the section group)
- An H2 or H3 heading (under 10 words)
- One or more paragraphs of body copy (20–50 words each)
- An image with alt text
- A CTA button

**Content it cannot hold:**
- HTML bullet lists (use tutor_program for that)
- FAQ arrays
- Link arrays
- Tutor filter controls

**Content patterns this component supports:**

This is the most versatile content component. It is reused multiple times on a page (typically as `why_igcse` through `why_igcse_6`).

### Default content purpose by position (Service + Location pages)

When a service+location page template includes 7 instances of `why_igcse` interleaved with `tutor_section`, use this default mapping. The agent should follow it unless the page brief explicitly directs otherwise. This removes the need to decide what each section is about.

| Component instance | Content purpose | What goes in it |
|---|---|---|
| `why_igsce` (no suffix) | **City school landscape** | Which schools in the city teach this subject, which boards they follow, and how Tuitional's tutors align. Name 3–5 specific schools. |
| `why_igsce_1` | **Subject pain point** | The single biggest reason students lose marks in this subject (e.g. composition for Arabic, method marks for Maths). Name the gap, then how sessions close it. |
| `why_igsce_2` | **Parent visibility / dashboard** | What the parent dashboard shows: attendance, upcoming classes, real-time schedule, platform updates, tutor chat. All five features. |
| (tutor_section appears here) | — | — |
| `why_igsce_3` | **Online advantage for this city** | Why online beats in-person for this specific city. Reference timezone (GMT+3 for Saudi, GMT+4 for UAE), commute friction, and the LMS. |
| `why_igsce_4` | **Curriculum specifics** | The exam specification(s) for this subject. Name codes (0508/0544 for Arabic IGCSE, 0610 for Biology, etc.) and what each paper assesses. |
| `why_igsce_5` | **All levels coverage** | The platform serves Grade 1 through adult. Each student matched to a tutor by level and goal. Academic Consultant handles the distinction. |
| `why_igsce_6` | **Trust signals / proven outcomes** | Trustpilot 4.7, 1,100+ tutors, 16-step screening, 120,000+ hours, matching speed under 10 minutes. Pull from `context.md` Trust Signals table. |

If the template uses a different sequence or count of `why_igcse` instances, fall back to choosing from the broader content purposes below.

### Broader content purposes (use when default mapping does not apply)

- **Subject expertise / Why our tutors** — Subject-specific pain points, tutor credentials, board-specific knowledge.
- **School landscape** — Which schools in this city use which boards.
- **Curriculum depth / Syllabus coverage** — What the syllabus actually contains.
- **Online advantage** — Why online tutoring works for students in this city.
- **Exam technique** — How marks are lost and how sessions address it.
- **How it works / Process** — Step-by-step explanation of the tutoring process.
- **Parent confidence** — Dashboard features, session notes, tutor communication.

### Curriculum-coverage mapping (6–8 instances, one per board)

Use this mapping when the page brief calls for a curriculum comparison pattern — covering multiple boards taught at schools in the target city. Each `why_igcse` instance covers exactly one curriculum board. Do **not** use this as the default for standard service+location pages; use it only when the brief explicitly mentions "all boards," "curriculum overview," or the keyword targets multiple boards (e.g. "IGCSE and IB tutors in Dubai").

**Paragraph rule for every instance:** 20–40 words. Open with what the board *is* (one sentence). Follow with one sentence on how Tuitional tutors are specifically trained or qualified for that board. No generic phrases like "our expert tutors" without board-specific context.

**Interlinking rule:** Every instance must use a `buttonLink` pointing to the most specific Tuitional page for that board and subject — never the homepage. `buttonText` must name the board explicitly (e.g. "Find a CAIE Tutor", "Explore IB Support"). This is the academic interlinking mechanism for this mapping.

| Instance | Curriculum | What the paragraph must cover | buttonLink target |
|---|---|---|---|
| `why_igcse` (no suffix) | **CAIE** (Cambridge Assessment International Education) | CAIE is the world's largest provider of international education programmes. Name the tiered Core/Extended paper structure and the relevant spec code for the subject (e.g. 0610 Biology, 0620 Chemistry). State that Tuitional tutors are trained on Cambridge mark schemes and paper-specific assessment objectives. | Subject-specific CAIE page (e.g. `/igcse-biology-tutors/`) |
| `why_igcse_1` | **Edexcel** (Pearson) | Edexcel IGCSE and GCSE differ from Cambridge in assessment structure — most specs use linear exams with no Core/Extended tier. Use the 4-digit code format (e.g. 1CH0 Chemistry, 4BS0 Business). State that Tuitional tutors hold Edexcel spec-specific knowledge and practise past papers from Pearson's published mark schemes. | Subject-specific Edexcel page (e.g. `/edexcel-igcse-chemistry-tutors/`) |
| `why_igcse_2` | **IB** (International Baccalaureate) | The IB Diploma Programme offers HL and SL for each subject. Internal Assessment (IA) counts toward the final grade — typically 20–25%. Name the IA component for the subject (e.g. Individual Investigation for Sciences, Written Assignment for Languages). State that Tuitional tutors cover both levels and support IA planning. | Subject-specific IB page (e.g. `/ib-biology-tutors/`) |
| `why_igcse_3` | **AP** (Advanced Placement, College Board) | AP is the US college-level qualification taken in May, scored on a 5-point scale. Name the AP course for the subject (e.g. AP Chemistry, AP Calculus AB/BC). Relevant for families targeting US university admissions. State that Tuitional tutors are familiar with AP course frameworks and Free Response Question (FRQ) technique. | Subject-specific AP page (e.g. `/ap-chemistry-tutors/`) |
| `why_igcse_4` | **OCR** (Oxford, Cambridge and RSA) | OCR is a UK GCSE and A Level board common in British schools abroad. OCR specs differ from AQA in coursework weighting and question style — name the OCR spec code for the subject (e.g. J247 GCSE Chemistry, H432 A Level Chemistry). State that Tuitional tutors know OCR mark schemes and controlled assessment formats. | Subject-specific OCR page (e.g. `/ocr-gcse-chemistry-tutors/`) |
| `why_igcse_5` | **AQA** | AQA is the largest UK GCSE and A Level board by entry volume. It uses linear exams with no coursework on most A Level specs. AQA mark schemes reward structured, point-by-point answers — state this explicitly for the subject. Name the AQA spec code (e.g. 8462 GCSE Chemistry, 7405 A Level Chemistry). State that Tuitional tutors practise AQA past papers and examiner report insights. | Subject-specific AQA page (e.g. `/aqa-gcse-chemistry-tutors/`) |
| `why_igcse_6` | **GED** (General Educational Development) | GED is the US high-school equivalency credential, covering four subjects: Reasoning Through Language Arts, Mathematical Reasoning, Science, and Social Studies. Name which GED module the page subject maps onto. Tuitional tutors support adult learners returning to education and targeting GED qualification as a university entry pathway. | GED subject page (e.g. `/ged-maths-tutors/`) |
| `why_igcse_7` | **SAT** (College Board) | The SAT is the US college admissions test: Evidence-Based Reading and Writing (800 pts) and Math (800 pts). SAT preparation is distinct from curriculum tutoring — timed practice, question strategy, and error-pattern analysis are central. State that Tuitional tutors structure sessions around official College Board practice tests. | SAT prep page (e.g. `/sat-tutors/`) |

**6-instance variant:** Drop `why_igcse_6` (GED) and `why_igcse_7` (SAT) — use CAIE through AQA only.  
**7-instance variant:** Drop `why_igcse_7` (SAT) — use CAIE through GED.  
**8-instance variant:** Use all eight rows above.

**Subject-specific pain point examples (for expertise sections):**

| Subject | Pain Point |
|---|---|
| Chemistry | Most marks lost on stoichiometry calculations requiring method shown step by step — even when the final answer is correct |
| Physics | Students apply the correct formula but omit the unit or give the answer to the wrong significant figures — both cost marks under every board |
| Maths | Grade plateaus caused by algebraic manipulation errors at step 2 or 3 of multi-stage questions — correct understanding, wrong execution |
| Economics | Extended response questions reward structured argument — students who write factual content without evaluative framing regularly score 4/8 where they could score 7/8 |
| Biology | Six-mark extended response questions require a specific sequence: definition, mechanism, example, evaluation. Students who answer in their own order lose structure marks |
| History | Answers lose marks at the analysis stage — students describe events but do not explain causation, consequence, or significance |
| Accounting | Mark losses in the trial balance and income statement from sign errors and misclassified account types, not conceptual misunderstanding |
| Computer Science | Pseudocode and algorithm trace questions are the highest-mark, lowest-scoring section in Cambridge 0478 — students understand the concept but cannot write the format |
| Business Studies | Case study answers marked down for generic application — examiners penalise answers that state theory without applying it to the specific firm |
| Geography | Fieldwork and data response questions underperformed — students describe data patterns rather than explaining geographical processes |
| Further Maths | The step from IGCSE Maths to Further Maths is the steepest transition — complex numbers, matrices, and polar coordinates have no equivalent in the standard syllabus |
| Arabic | Formal Modern Standard Arabic writing at IGCSE level is the primary barrier — most students do not encounter this style in daily conversation |
| Additional Maths | The most algebra-intensive IGCSE course — students struggle not because they cannot do maths, but because foundational algebra is not yet precise enough |

**Why Study examples (for university gateway sections):**

Each "why study" instance must connect the subject to specific next steps — named university courses, career paths, or prerequisite relationships. Never use generic statements like "This subject builds critical thinking."

Example: "A Grade B or above in A Level Economics is required for entry into PPE at Oxford, LSE Economics, and most UK Business degrees."

---

## tutor_section — Tutor Display with Filters

**Fields:**
- H2 Tag field → Section heading
- Curriculum dropdown → Filter tutors by curriculum
- Grade/Level dropdown → Filter by grade
- Subject dropdown → Filter by subject
- Column View dropdown → Controls display layout

**Content it holds:**
- An H2 heading (e.g. "Featured IGCSE Chemistry Tutors")
- Filter selections that control which tutors display

**Content it cannot hold:**
- Body copy, paragraphs, or descriptions
- Bullet lists or tables
- The tutor cards themselves are auto-populated from the tutor database

**Notes:**
- The agent writes the H2 heading and specifies the filter values
- Tutor bios and credentials are pulled from the database — not written per page

---

## igcse_tutoring_program — Benefits Grid

**Fields:**
- H2 Tag field → Section heading
- Checkbox (isShow) → Toggle to show/hide

**Content it holds:**
- An H2 heading (e.g. "Benefits of our Dubai IGCSE Tutoring Program")
- The benefit cards below are pre-loaded in the CMS — the agent writes only the heading

**Content it cannot hold:**
- Custom body copy or paragraphs
- Custom benefit card content (cards are system-defined)

**Notes:**
- Set isShow to `true` to display
- The heading should be subject-specific and city-specific where applicable

---

## what_our_student_says — Testimonials

**Fields:**
- H2 Tag field → Section heading
- Paragraph field → Supporting paragraph text

**Content it holds:**
- An H2 heading (e.g. "What Our Students Say")
- A supporting paragraph (20–50 words)
- Testimonial content is auto-populated from the CMS — the agent writes only the heading and paragraph

**Content it cannot hold:**
- Custom testimonial text (testimonials are managed separately in the CMS)
- Bullet lists, tables, or FAQ content

---

## link_list — Sibling Page Links

**Fields:**
- H2 Tag field → Section heading
- Paragraph field → Optional description
- Link Array → Name (display text) + Link (URL) for each item

**Content it holds:**
- An H2 heading
- An optional paragraph describing the related pages
- An array of links to sibling pages in the same category

**Content rules:**
- Include all sibling pages in the same category (same URL prefix)
- Exclude the current page from the array
- Display names must match the page H1 format (e.g. "Physics Tutors" not "online physics")
- Only include verified, live URLs

**Content it cannot hold:**
- Body copy paragraphs
- Bullet lists or tables
- Links to pages outside the current category

---

## faqs — FAQ Accordion

**Fields:**
- H2 Tag field → Section heading
- Paragraph field → Subheading text
- FAQ Array → Question + Answer pairs

**Content it holds:**
- An H2 heading (e.g. "Frequently Asked Questions")
- A subheading paragraph
- Exactly 6 Q&A pairs

**Content rules (per skills.md):**
- Each answer: 15–42 words
- Answer directly and immediately — no preamble
- Questions must map to real People Also Ask queries
- Answers must name Tuitional, the subject, and the curriculum at least once
- End with a specific fact or outcome — not a soft CTA

**Content it cannot hold:**
- Body copy paragraphs outside the Q&A format
- Bullet lists, tables, or images

---

## main_content — Main Content with Subject Array

**Fields:**
- Tag + Header field → Section heading with tag selector
- Paragraph field → Description text
- Subject Array → Name + Link for each item

**Content it holds:**
- An H2 heading
- A description paragraph
- An array of subject links (similar to link_list but with a different visual layout)

---

## popular_subjects — Subject Array with Icons

**Fields:**
- Focus Area text field → Section description
- Focus Area Array → Name + Icon (image upload) + Link for each item
- Button Title + Button Link → CTA at the bottom

**Content it holds:**
- A descriptive text for the section
- An array of subjects with icons and links
- A CTA button

---

## phone_cta — Phone Call-to-Action

**Fields:**
- H2 Tag field → Section heading
- Paragraph field → Supporting text
- Button text field → CTA button label
- Phone link field → Telephone number

**Content it holds:**
- An H2 heading (e.g. "Call Us Today For a Free Demo")
- Supporting text (e.g. "50000+ Students choose us every month!")
- A CTA button linking to a phone number

---

## demo_pointers — Book A Demo with Feature Pointers

**Fields:**
- H2 Tag field → Section heading
- Paragraph field → Description text
- Button Link → CTA destination
- Array → Header + Body for each pointer

**Content it holds:**
- An H2 heading
- A description paragraph
- An array of feature pointers (each with a short header and body text)
- These pointers are displayed as expandable cards or tiles

---

## book_demo_cta — Book A Demo Banner

**Fields:**
- Checkbox → Toggle to show/hide

**Content it holds:**
- None — this is a display toggle only. The banner content is pre-loaded.

---

## what_we_offer — What We Offer Grid

**Fields:**
- Checkbox → Toggle to show/hide

**Content it holds:**
- None — this is a display toggle only. The offer cards are pre-loaded in the CMS.

---

## get_started — Get Started Steps

**Fields:**
- Checkbox → Toggle to show/hide

**Content it holds:**
- None — this is a display toggle only. The steps are pre-loaded.

---

## education_counseling — Education Counseling Section

**Fields:**
- Tag + Header field → Section heading with tag selector
- Paragraph field → Description text

**Content it holds:**
- An H2 heading
- A description paragraph about educational counselling services

---

## Quick Rules for Mapping Content to Components

1. **Headlines** → always go in H1 (with_form) or H2 tag fields
2. **Feature card grids and sign-up steps** → use tutor_program with the HTML card grid structure (see Format A and Format B above)
3. **Subject/page links** → use link_list or main_content's Subject Array
4. **CTAs** → Button Title + set action to `popup`
5. **FAQs** → always go in the faqs component array
6. **Toggle-only sections** → school_logos, book_demo_cta, what_we_offer, get_started are show/hide only — no custom text
7. **Rich body copy with images** → use why_igcse instances
8. **Tutor display** → use tutor_section with filter dropdowns — tutor cards are auto-populated