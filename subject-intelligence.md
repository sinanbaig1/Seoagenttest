# subject-intelligence.md — Subject Reference for Service + Subject Pages

Version: 1.0

This file is the single source of truth for subject-level facts used in subject pages and Subject + Location pages. The agent reads this once per session and looks up the subject row at Step 3. Never re-derive these facts from `component-variance.md` or `page-differentiation.md` mid-session — that round-trip costs minutes.

If a fact in this file disagrees with the source files, treat the source files as authoritative and update this file. Source-of-truth pointers are listed under each table.

Every row below is a single lookup. The agent copies the values into the page YAML's `_validation` block and the BUDGET block of the scaffold. No interpretation needed.

---

## Master Subject Table

Every row is one subject. All thirteen subject pages on tuitionaledu.com appear here.

Sources: `component-variance.md` (pain points), `page-differentiation.md` PART 1 (recommended angles) and PART 4 (lead stats).

| Subject | Suggested angle | Lead stat | Pain point opener (one sentence) |
|---|---|---|---|
| Chemistry | Curriculum Precision (4) | "97.2% student success rate across featured IGCSE tutors" | Most marks lost on stoichiometry calculations requiring method shown step by step — even when the final answer is correct. |
| Physics | Exam Technique (1) | "94% of featured tutors' students reach their target grade" | Students apply the correct formula but omit the unit or give the answer to the wrong significant figures. Both cost marks under every board. |
| Biology | Syllabus Depth (8) | "97.2% student success rate across featured IGCSE tutors" | Six-mark extended response questions require a specific sequence: definition, mechanism, example, evaluation. Students who answer in their own order lose structure marks. |
| Mathematics | Grade Gap Closure (3) | "94% of featured tutors' students reach their target grade" | Grade plateaus caused by algebraic manipulation errors at step 2 or 3 of multi-stage questions. Correct understanding, wrong execution. |
| Further Mathematics | Concept Mastery (2) | "Students matched to a tutor in under 10 minutes" | The step from IGCSE Maths to Further Maths is the steepest transition. Complex numbers, matrices, and polar coordinates have no equivalent in the standard syllabus. |
| Additional Mathematics | Exam Technique (1) | "Students matched to a tutor in under 10 minutes" | The most algebra-intensive IGCSE course. Students struggle not because they cannot do maths, but because foundational algebra is not yet precise enough. |
| Accounting | Curriculum Precision (4) | "1,100+ tutors, each cleared through a 16-step process" | Mark losses in the trial balance and income statement come from sign errors and misclassified account types, not conceptual misunderstanding. |
| Economics | Concept Mastery (2) | "4.7 out of 5 on Trustpilot" | Extended response questions reward structured argument. Students who write factual content without evaluative framing regularly score 4/8 where they could score 7/8. |
| Business Studies | Past Paper Mastery (7) | "1,100+ tutors, each cleared through a 16-step process" | Case study answers are marked down for generic application. Examiners penalise answers that state theory without applying it to the specific firm. |
| Computer Science | Syllabus Depth (8) | "120,000+ tutoring hours delivered across all subjects" | Pseudocode and algorithm trace questions are the highest-mark, lowest-scoring section in Cambridge 0478. Students understand the concept but cannot write the format. |
| History | Confidence Building (9) | "4.7 out of 5 on Trustpilot" | Answers lose marks at the analysis stage. Students describe events but do not explain causation, consequence, or significance. |
| Geography | University Gateway (5) | "120,000+ tutoring hours delivered across all subjects" | Fieldwork and data response questions underperform. Students describe data patterns rather than explaining geographical processes. |
| Arabic | Parent Confidence (6) | "4.7 out of 5 on Trustpilot" | Formal Modern Standard Arabic writing at IGCSE level is the primary barrier. Most students do not encounter this style in daily conversation. |
| Psychology | Confidence Building (9) | "87–97.2% per featured tutor" | Psychology students lose marks on evaluation questions. They describe studies correctly but fail to analyse limitations, identify confounding variables, or propose alternative explanations — and that is where the assessment marks sit. |

---

## Specification Codes per Subject

Use these exact codes in the `why_igsce_4` paragraph (curriculum specifics) and in FAQ answers about board differences.

Source: Cambridge International (CAIE) and Pearson Edexcel published specifications, plus IB and AQA where applicable.

| Subject | Cambridge IGCSE | Edexcel IGCSE | A Level (Cambridge) | AQA GCSE | IB |
|---|---|---|---|---|---|
| Chemistry | 0620 | 4CH1 / 1CH0 | 9701 | 8462 | HL/SL |
| Physics | 0625 | 4PH1 / 1PH0 | 9702 | 8463 | HL/SL |
| Biology | 0610 / 0970 | 4BI1 / 1BI0 | 9700 | 8461 | HL/SL |
| Mathematics | 0580 / 0980 | 4MA1 / 1MA1 | 9709 | 8300 | AA HL/SL, AI HL/SL |
| Further Mathematics | 0606 (Add Maths) | 4PM1 | 9231 | — | — |
| Additional Mathematics | 0606 | 4PM1 | — | — | — |
| Accounting | 0452 | 4AC1 | 9706 | — | — |
| Economics | 0455 / 0987 | 4EC1 | 9708 | — | HL/SL |
| Business Studies | 0450 / 0986 | 4BS1 | 9609 | 8132 | HL/SL |
| Computer Science | 0478 / 0984 | 4CP0 | 9618 | 8525 | HL/SL |
| History | 0470 / 0977 | 4HI1 | 9489 | 8145 | HL/SL |
| Geography | 0460 / 0976 | 4GE1 | 9696 | 8035 | HL/SL |
| Arabic | 0508 (First Lang) / 0544 (Foreign Lang) | — | 9680 | — | A HL/SL, B HL/SL |
| Psychology | 0983 | — | 9990 | 8182 (GCSE) / 7182 (A Level) | HL/SL |

When a subject is offered as both First Language and Foreign Language (Arabic, English) name both codes. When CAIE has a 9-series double award (0970 Biology, 0980 Maths), the agent picks the spec the city's schools use — this is rarely worth naming both.

---

## LSI Terms per Subject

Each subject's LSI bank. Pick 6–8 from the subject's row, copy them to the YAML's `_validation.lsi_terms` block, and ensure each appears at least twice in body copy. The validator (`tools/validate_page.py`) flags terms below the threshold.

Source: `skills.md` Keyword Strategy section, with one or two extras per subject pulled from real exam syllabi.

| Subject | LSI bank (pick 6–8) |
|---|---|
| Chemistry | titration, ionic bonding, equilibrium, stoichiometry, electrolysis, organic chemistry, molar mass, required practicals |
| Physics | moments, electromagnetic induction, specific heat capacity, wave properties, nuclear radiation, P-E diagrams, scalars and vectors, refraction |
| Biology | homeostasis, photosynthesis, DNA replication, natural selection, enzyme activity, osmosis, mitosis, transpiration |
| Mathematics | differentiation, algebraic fractions, circle theorems, trigonometry identities, proof, vectors, simultaneous equations, quadratic formula |
| Further Mathematics | complex numbers, matrices, polar coordinates, hyperbolic functions, parametric equations, summation of series, induction proof |
| Additional Mathematics | binomial expansion, calculus introduction, kinematics, logarithms, partial fractions, sets and probability, identities |
| Accounting | trial balance, ledger accounts, depreciation, accruals, balance sheet, income statement, cash flow, double-entry |
| Economics | elasticity, multiplier effect, balance of payments, monetary policy, market failure, trade cycles, exchange rates, fiscal policy |
| Business Studies | break-even, cash flow forecast, marketing mix, stakeholders, organisation structure, ratio analysis, motivation theory |
| Computer Science | binary arithmetic, Boolean logic, sorting algorithms, database normalisation, TCP/IP, encryption, pseudocode, flowchart |
| History | source evaluation, historiography, causation, consequence, narrative assessment, contextualisation, significance, change and continuity |
| Geography | weathering, urbanisation, ecosystems, plate tectonics, fieldwork data, choropleth maps, sustainable development, microclimate |
| Arabic | Modern Standard Arabic, Fusha, IGCSE 0508, IGCSE 0544, Arabic composition, oral expression, reading comprehension, A Level Arabic |
| Psychology | observational study, cognitive approach, social learning theory, biological approach, research methods, ethical guidelines, operationalisation, confounding variable, case study, nature vs nurture |

---

## Card Title Sets per Subject

The `tutor_program` component (Format A, 6 feature cards) requires subject-specific card titles. Generic titles ("Learning Gaps", "Concept Mastery", "Progress Tracking") are banned. Use the set below as a starting point — the agent may swap one or two titles for variety across a batch but must not invent titles already used on another subject.

Source: `component-variance.md` examples + extension to all 13 subjects.

| Subject | Card title set (6) |
|---|---|
| Chemistry | Stoichiometry Method \| Mark Scheme Precision \| Practical Paper Prep \| Equation Recall \| Board Comparison \| Topic Sequencing |
| Physics | Formula Application \| Unit and Sig-Fig Discipline \| Required Practical Setup \| Mark Scheme Literacy \| Past Paper Drill \| Topic Triage |
| Biology | Six-Mark Structure \| Mechanism Recall \| Required Practical Notes \| Diagram Labelling \| Mark Scheme Wording \| Topic Sequencing |
| Mathematics | Algebraic Method Work \| Proof Writing \| Calculator vs Non-Calculator \| Mark Scheme Literacy \| Grade Boundary Targeting \| Topic Triage |
| Further Mathematics | Complex Numbers \| Matrix Operations \| Polar Coordinates \| Hyperbolic Functions \| Step-by-Step Proof \| Past Paper Drill |
| Additional Mathematics | Binomial Expansion \| Calculus Foundations \| Kinematics Setup \| Logarithm Rules \| Algebraic Precision \| Mark Scheme Literacy |
| Accounting | Trial Balance Discipline \| Ledger Account Setup \| Depreciation Method \| Accrual Treatment \| Balance Sheet Layout \| Income Statement Format |
| Economics | Evaluative Framing \| Multiplier Worked Example \| Elasticity Diagrams \| Market Failure Analysis \| Policy Comparison \| Past Paper Structure |
| Business Studies | Case-Study Application \| Quantitative Analysis \| Stakeholder Mapping \| Marketing Mix Drill \| Cash Flow Forecasting \| Mark Scheme Wording |
| Computer Science | Pseudocode Writing \| Algorithm Trace \| Binary and Logic \| Database Normalisation \| Network Concepts \| Past Paper Drill |
| History | Source Analysis \| Essay Structure \| Causation Arguments \| Markband Awareness \| Context and Significance \| Practice Papers |
| Geography | Data Response Skills \| Process Explanation \| Fieldwork Method \| Map and Diagram Drill \| Case Study Recall \| Past Paper Drill |
| Arabic | MSA Writing Technique \| Oral Expression Practice \| Reading Comprehension Skills \| Cambridge vs Edexcel Arabic \| Fusha Grammar and Root Words \| Primary to Adult Fusha |
| Psychology | Study Evaluation \| Research Methods Drill \| Theory Application \| Key Study Recall \| Ethics and Methodology \| Past Paper Drill |

---

## University / Career References per Subject

The `why_igsce_5` instance ("All Levels Coverage" or "Why Study X" depending on the angle) calls for a university or career hook. Use these references — never write generic phrases like "builds critical thinking".

Source: UCAS course requirements + Russell Group entry profiles (2024–2025 academic year). Refresh once per academic year.

| Subject | University / career reference |
|---|---|
| Chemistry | Grade A* in A Level Chemistry is required for Medicine at Oxford, Cambridge, and Imperial. A Grade A is the minimum for Pharmacy and Biomedical Science at most Russell Group institutions. |
| Physics | A Grade A in A Level Physics is required for Engineering at Imperial, UCL, and most Russell Group universities. Aerospace and Mechanical Engineering require A* at top entry tiers. |
| Biology | A Level Biology Grade A* is required for Medicine, Dentistry, and Veterinary Medicine at Oxford, Cambridge, Edinburgh, and Glasgow. Grade A unlocks most Biomedical and Biological Sciences degrees. |
| Mathematics | Grade A or A* in A Level Maths is required for Economics at LSE and Oxford PPE, and for Computer Science at Cambridge and Imperial. Engineering departments expect A* across most institutions. |
| Further Mathematics | A Level Further Maths is essential for Mathematics at Cambridge, Imperial, and Warwick. Grade A* in Further Maths unlocks the strongest STEM programmes worldwide. |
| Additional Mathematics | The course bridges IGCSE Maths to A Level Maths. Strong performance signals readiness for the Further Maths track, opening Cambridge and Imperial maths-heavy programmes. |
| Accounting | A Level Accounting Grade A is the standard entry point for ACCA, ICAEW, and CIMA professional pathways. UK Business and Accounting degrees at Russell Group level expect A or A*. |
| Economics | A Level Economics Grade A or above is required for PPE at Oxford, Economics at LSE, and Business Management at Warwick. Grade A* is standard for the strongest UK programmes. |
| Business Studies | A Level Business Grade A unlocks Business Management at Warwick, Bath, and Manchester. Strong case-study technique transfers directly to the Cambridge BMAT and Oxford pre-interview tasks. |
| Computer Science | Grade A* in A Level Computer Science is required for Computer Science at Cambridge and Imperial. Grade A is the standard entry for Edinburgh, UCL, and Manchester. |
| History | A Level History Grade A is required for History at Oxford, Cambridge, and the LSE. The same grade unlocks Law and PPE pathways across the Russell Group. |
| Geography | A Level Geography Grade A is the standard entry for Geography, Environmental Science, and Urban Planning at UCL, Bristol, and Durham. Strong fieldwork analysis transfers to Earth Sciences entry. |
| Arabic | A Level Arabic Grade A unlocks Arabic and Middle Eastern Studies at Oxford, Cambridge, SOAS, and Edinburgh. Career routes include translation, diplomacy, journalism, and international development. |
| Psychology | A Level Psychology Grade A is the standard entry requirement for Psychology at UCL, King's College London, and the University of Edinburgh. A Grade A also opens pathways to Medicine, Counselling, and Social Work degrees across Russell Group universities. |

---

## Lookup Workflow

The agent's Step 3 (parse prompt) must perform these lookups before scaffold copy:

1. **Subject row** — find the subject in the Master Subject Table. Copy: angle, lead stat, pain point opener.
2. **Spec codes** — find the subject in the Specification Codes table. Copy the code(s) into the BUDGET block as `# spec_codes: 0508, 0544`.
3. **LSI bank** — find the subject in the LSI Terms table. Pick 6–8 terms. Copy into the page YAML's `_validation.lsi_terms` block.
4. **Card title set** — find the subject in the Card Title Sets table. Copy all 6 titles into `tutor_program.cards[*].title`.
5. **University/career hook** — find the subject in the University / Career References table. Use the sentence in the `why_igsce_5` paragraph.

For Subject + Location pages, also do the city lookup in `city-intelligence.md`. Schools and timezone are independent of subject.

---

## Update Discipline

When a fact in this file changes:

1. Edit the exact row. Do not duplicate values across rows.
2. If the change invalidates a fact in `component-variance.md` or `page-differentiation.md`, edit those files in the same session — they are the source of truth for prose; this file is the source of truth for lookups.
3. When a new subject is added to the platform, add a row to every table here in the same session. A subject is not "live" for the agent until it has a row in every table.
