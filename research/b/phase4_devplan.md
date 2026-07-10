# CONCEPT B, PHASE 4: DEVELOPMENT PLAN, COST, AND TIMELINE

Governed by `00_framework.md` (section 4 cost conventions, section 5 evidence rules). Builds on Phase 0 (`phase0_scope.md`, safety envelope, claims matrix), Phase 1 (`phase1_markers.md`, V1 shortlist, the two daily surfaces), Phase 2 (`phase2_data_inputs.md`, lab ingest Model 1, self report over affect inference, content corpus split, clinical reviewer as permanent opex), Phase 3 (`phase3_architecture.md`, rules engine plus narrating model, enforced safety layer, consent as spine, derived only wearable layer), and the shared files `shared_infra_cost.md` and `shared_capital_landscape.md`. Does not re research what those settled. All access dates 2026-07-10.

## Thesis, stated first

This product is not gated by code. It is gated by three non engineering constraints, and the development plan is built around that fact.

1. **The binding constraint to G4 is content authoring plus clinical review plus a run of the pilot cohort, not software.** At the recommended headcount the engineering build (~15 calendar months) and the clinically reviewed content build (~12 calendar months) finish at roughly the same time, and the pilot observation window (~3 to 4 months) sits on top of both. Adding a fourth engineer compresses code but not the content or the pilot, so it barely moves G4. This is the single most important planning conclusion in this phase.
2. **A pure engineering headcount model is wrong for this product** (concept brief Phase 4 note). Two non engineering roles are load bearing and are not optional: a retained OB-GYN clinical reviewer (Phase 2, 2.4) and a full time content lead who owns the grounding corpus. They are costed here as first class headcount, not overhead.
3. **The AI assisted velocity multiplier applies to the engineering workstreams only, and the engineering workstreams are not the critical path.** The empirically defensible multiplier is modest (mid case 1.2x, section 5), and it accelerates exactly the work that is not binding. It does not touch clinical review, content authoring, wearable and lab data partnerships, or the pilot clock.

---

## 1. COST MODEL ASSUMPTIONS (framework section 4)

### 1.1 Loaded engineer cost (San Diego, fully loaded)

| Input | Value | Basis | Confidence |
|---|---|---|---|
| Base salary, mid to senior software engineer, San Diego | ~$155,000/yr | 2026 San Diego market: Glassdoor $147,026 avg, ZipRecruiter $156,628 avg, Indeed $133,332 avg, Levels.fyi total comp $189,000 | HIGH |
| Fully loaded multiplier (payroll tax, benefits, equipment, software, facilities and G&A overhead) | 1.4x | Standard startup fully loaded factor 1.25 to 1.4; upper end used for a small team carrying its own overhead per capita | MEDIUM |
| **Fully loaded cost per engineer** | **~$220,000/yr = ~$18,300/mo** | Framework section 4: state loaded cost, not salary alone | MEDIUM |

The framework forbids using salary alone. All timelines below cost engineers at $18,300 per month fully loaded. Sensitivity: a 1.25x loading drops this to ~$194k/yr; a senior heavy team at $185k base and 1.4x reaches ~$259k/yr. The $220k figure is the planning point estimate.

### 1.2 The non engineering roles this product cannot ship without

| Role | Structure | Fully loaded cost | Basis | Confidence |
|---|---|---|---|---|
| **Clinical Reviewer / Medical Director** (retained OB-GYN, 1099) | Part time retainer, 8 to 15 hrs/week, scaling with content volume | $60,000/yr (10 hrs/wk) rising to ~$90,000/yr (15 hrs/wk) near pilot | Phase 2, 2.4: telehealth OB-GYN reviewer $115/hr (ZipRecruiter 2026, range $102 to $175). 10 hrs/wk x 52 x $115 = $59,800 | HIGH (rate), MEDIUM (hours) |
| **Content Lead** (full time) | Owns the grounding corpus: sources the free public domain content (CDC, USDA, WHO, NIH), authors original normalization and education copy, manages the clinical review queue, versions content against gestational and child age, and runs the licensed content roadmap (ACOG, AAP) | Base ~$110,000, loaded 1.4x = **~$155,000/yr = ~$12,900/mo** | 2026 digital health content lead / editorial manager band $84k to $127k+ (ZipRecruiter digital health $98k avg to $158k top; editorial manager $84k avg); upper band for a perinatal role with clinical literacy | MEDIUM |

Why these are not optional. The strategic center of the product is the CDC and AIM warning sign layer (Phase 1) and a full year of clinically reviewed postpartum content. Every warning sign string, every normalization message, and every escalation interstitial must pass verbatim source match plus clinical sign off before it ships (Phase 1 Assumption 3; Phase 0 section 5). That is a content operation with a clinician gate, and it is the critical path. A team of engineers with no content lead and no reviewer produces a working app with nothing safe to say in it.

Deferred roles (not in the G4 model, flagged for G5+): pediatric reviewer and lactation reviewer (added as the infant layer ships, Phase 2, 2.4); a second content hire; dedicated regulatory/legal counsel (retained, not headcount).

### 1.3 Build versus buy (framework section 4)

Established in prior phases and not re decided here. The plan buys, it does not build, everywhere a credible off the shelf option exists.

| Capability | Decision | Source |
|---|---|---|
| Cross platform mobile runtime | BUY (React Native / Expo, MIT) | Phase 3, 1.1 |
| Vector search | BUY (`pgvector` on existing Postgres; no dedicated vector DB) | Phase 3, 2.2 |
| Client side encryption | BUY (SQLCipher community, BSD-3) | Phase 3, 1.1 |
| Grounded generation model | BUY (Claude Haiku 4.5 API tier; no model training) | Phase 3, 2.3 |
| Lab ingest | BUY (health data aggregator, Model 1; no in house FHIR network) | Phase 2, 2.2 |
| Wearable ingest | BUY (HealthKit / Health Connect + vendor connectors; no device) | Phase 3, 7 |
| V1 grounding corpus | BUILD original copy on FREE public domain content (zero license cost); BUY ACOG/AAP depth at V2 | Phase 2, 2.4 |
| Rules engine, safety classifier, consent system | BUILD (this is the differentiated IP and the safety critical code) | Phase 3, 3/4/5 |

The build surface is deliberately narrow: the rules engine, the enforced safety layer, the dual user consent system, and the daily loop. Everything else is integration of bought components.

### 1.4 Brooks's law coordination overhead

Adding engineers does not scale output linearly. Communication paths grow as n(n-1)/2, and integration, review, and onboarding tax the team (Fred Brooks, The Mythical Man-Month, 1975; and the corollary that adding people to a late software project makes it later). This is modeled as a per head efficiency haircut, calibrated to the classic result and deliberately conservative for a team this small:

| Engineers | Communication paths | Modeled efficiency per engineer | Effective raw engineer-months delivered per calendar month |
|---|---|---|---|
| 1 | 0 | 100% | 1.00 |
| 2 | 1 | 95% | 1.90 |
| 3 | 3 | 90% | 2.70 |
| 4 | 6 | 85% | 3.40 |

This is a modeling assumption, not a measured value for this team (flagged in Assumptions). It is applied on top of, and separately from, the AI velocity multiplier (section 5).

### 1.5 Effective engineering capacity (Brooks x AI multiplier, mid case)

Combining section 1.4 with the mid case AI multiplier of 1.2x (section 5), effective engineering output per calendar month:

| Engineers | Raw EEM/mo (Brooks) | x AI 1.2 (mid) | **Effective EEM/mo** |
|---|---|---|---|
| 1 | 1.00 | 1.2 | 1.20 |
| 2 | 1.90 | 1.2 | 2.28 |
| 3 | 2.70 | 1.2 | 3.24 |
| 4 | 3.40 | 1.2 | 4.08 |

---

## 2. WORK BREAKDOWN STRUCTURE TO EACH GATE

Gates per framework section 3. For Concept B (a pure cloud SaaS with a client side sensitive tier, no hardware), the gate definitions map as: G1 bench (algorithms and pipeline running on dev hardware), G2 self test (founder runs the full daily loop for 30 days), G3 friends and family (5 to 15 real users, instrumented), G4 pilot (50 to 200 user structured cohort, efficacy signal for a partner conversation, unit economics measured), G5 limited commercial, G6 full commercial.

### 2.1 Raw engineering effort by workstream, cumulative to G4

Effort is in baseline engineer-months (EM), before AI multiplier and before Brooks overhead. These are founder-facing engineering estimates calibrated to the Phase 3 architecture, flagged as estimates (Assumptions).

| Workstream | Scope (to G4) | Raw EM | Notes |
|---|---|---|---|
| Mobile | RN iOS+Android at parity; onboarding; the two daily surfaces; symptom logger; consent UI; BP/weight/kick entry; content reader; partner app | 10 | Largest single workstream; two user types |
| Backend | TypeScript API; Postgres data model (5 domains, Phase 3 1.3); auth; event sourced logs; notification service | 8 | Deliberately boring stack (Phase 3 1.2) |
| Retrieval / AI | RAG pipeline; corpus ingest + embedding; `pgvector` HNSW; hybrid retrieve + rerank; generation orchestration; corpus constraint gate | 5 | Standard 2026 RAG (Phase 3 2.2) |
| Rules / personalization engine | Gestational clock; trend math; threshold checks; nudge ranking; daily brief assembly | 4 | The differentiated deterministic core (Phase 3 3) |
| Safety layer | Red flag classifier (deterministic, on device + server); escalation interstitials; refusal guardrails; immutable logging; unit test suite | 3 | Small code, high test and review burden; life safety |
| Consent / dual user | UMA style scoped grants; server side enforcement at the data boundary; revocation; visible share state | 4 | Differentiator and legal exposure if wrong (Phase 3 4) |
| Wearable integration | HealthKit + Health Connect; 1 to 2 vendor connectors (Oura, Whoop); normalized derived scalar schema | 3 | V2 feature, partial for pilot; degrades gracefully (Phase 3 7) |
| Lab ingest | Aggregator integration (Model 1); FHIR `Observation`/`DiagnosticReport` parse; Model 3 photo fallback | 4 | Aggregator per unit price still UNKNOWN (Phase 2 Open Q1) |
| Privacy / security | Client side encrypted tier (SQLCipher); retention + deletion; region pinning; reproductive field minimization | 3 | First order, not afterthought (Phase 3 6) |
| QA | Test automation; device matrix; safety layer verification; consent enforcement tests; pilot instrumentation | 5 | Weighted to safety and consent correctness |
| Design | UX, visual, content design, the 30 second surfaces | (contract) | Contracted, not engineering headcount (section 3) |
| **Total raw engineering to G4** | | **~49 EM** | Rounded to ~50 for planning |

### 2.2 Cumulative raw engineering by gate

| Gate | Exit criteria (Concept B mapping) | Cumulative raw EM | What is newly complete |
|---|---|---|---|
| G1 Bench | RAG answers a grounded question with citations on dev hardware; red flag classifier passes its unit tests on recorded inputs; rules engine computes the daily brief for one synthetic user | ~8 | Retrieval spine, safety classifier prototype, rules skeleton |
| G2 Self test | Founder runs the full daily loop for 30 days continuous; mood, BP, symptom, kick logging; warning sign strip live; false positive behavior of the safety layer characterized | ~20 | End to end single user app, notifications, self report loop |
| G3 Friends and family | 5 to 15 real users; dual user consent live; partner app; instrumentation; retention and failure modes cataloged | ~34 | Consent system, partner surface, multi user, analytics |
| G4 Pilot | 50 to 200 user structured cohort; lab ingest; hardened privacy tier; scale; efficacy signal and unit economics measured | ~50 | Lab ingest, hardening, scale, pilot analytics |

### 2.3 Non engineering WBS (the critical path work), cumulative to G4

This runs in parallel with engineering and, per the thesis, gates G4 as hard as code does.

| Workstream | Owner | Scope to G4 | Duration (calendar) |
|---|---|---|---|
| Content operations | Content Lead | Source and structure the free public domain corpus; author original normalization and education copy across pregnancy weeks and the full postpartum year; version by stage; build the licensed content roadmap | ~12 months, front loaded, continuous thereafter |
| Clinical review | Retained OB-GYN | Verbatim source match on every warning sign string; sign off on all education and escalation copy; review the safety layer behavior; review the intrusive thought prompt wording | Gates content release throughout; ~8 to 15 hrs/wk |
| Wearable data access | Eng + founder | Confirm terms per vendor (done, Phase 2); implement connectors; V2, not a G4 blocker | Parallel, non blocking for V1 |
| Lab data access | Eng + founder | Select aggregator; close per unit pricing (Phase 2 Open Q1); integrate | ~3 months, lands by G4 |
| Legal / regulatory | Retained counsel | BP threshold reminder review (Phase 0 Open Q1); reproductive data retention boundary (Phase 3 Open Q7); EPDS license if used; escalation copy sign off | Parallel, gates specific features |

---

## 3. TIMELINE AND COST AT 1, 2, 3, 4 ENGINEERS

The two non engineering roles (clinical reviewer, content lead) are held constant across every column because they are not optional. Design is a contract line (~$9k/mo during active design, G1 to G3). Infrastructure and SaaS tooling run per `shared_infra_cost.md` small tier fixed overhead, ~$2k/mo early rising to ~$5 to 6k/mo at pilot.

### 3.1 Discipline mix at each headcount

| Headcount | Engineering discipline mix | Non eng (constant) | Verdict |
|---|---|---|---|
| 1 engineer | 1 full stack generalist owning mobile + backend + AI + safety + consent, fully serialized | Content lead, clinical reviewer, contract design/QA | REJECT. Single point of failure on a life safety product; safety and consent code get no independent review; timeline absurd |
| 2 engineers | 1 mobile leaning full stack; 1 backend/infra + AI/retrieval | + contract QA and design | Viable, slow. Safety layer QA and consent enforcement under resourced |
| **3 engineers (RECOMMENDED)** | **1 mobile; 1 backend/infra; 1 full stack owning retrieval/AI + rules engine.** Safety layer and consent code peer reviewed across the three | + embedded QA effort + contract QA for device matrix and safety verification; contract design | **Minimum credible config for a product with an enforced life safety layer and a dual user consent system** |
| 4 engineers | 3 above + 1 dedicated to consent/privacy/security + safety QA | Same | Fastest code, but code stops being the binding constraint (section 4); highest burn; Brooks overhead rising |

### 3.2 Timeline to G4 (build plus pilot run), mid case AI

Build months = 50 raw EM / effective EEM per month (section 1.5). Pilot run adds ~3 to 4 months of cohort observation to satisfy the G4 exit criteria (efficacy signal + unit economics), partially overlapping late build. Content critical path (~12 months) floors the schedule independent of engineers.

| Config | Effective EEM/mo | Build months (code) | Content floor | Pilot run | **Calendar months to G4** |
|---|---|---|---|---|---|
| 1 eng | 1.20 | ~42 | 12 | 3 to 4 | **~44+** (reject) |
| 2 eng | 2.28 | ~22 | 12 | 3 to 4 | **~26** |
| 3 eng | 3.24 | ~15 | 12 | 3 to 4 | **~18 to 20** |
| 4 eng | 4.08 | ~12 | 12 | 3 to 4 | **~15 to 16** |

Read the 3 versus 4 engineer rows together. At 3 engineers the code build (~15 months) and the content build (~12 months) finish close together, and the pilot clock runs on top. At 4 engineers the code finishes in ~12 months but the content floor (~12 months) and the pilot run do not move, so G4 improves only marginally (~15 to 16 versus ~18 to 20 months) at materially higher burn. Adding the fourth engineer buys schedule only if content and clinical review are also accelerated, which requires a second content hire, not a fourth engineer.

### 3.3 Monthly burn and cumulative cost to G4

Monthly fully loaded burn at steady state (excludes ramp; early months are lower as the team onboards):

| Line | 2 eng | 3 eng (rec) | 4 eng |
|---|---|---|---|
| Engineers | $36,600 | $54,900 | $73,200 |
| Content Lead | $12,900 | $12,900 | $12,900 |
| Clinical Reviewer (retained) | ~$5,000 | ~$5,500 | ~$6,000 |
| Design (contract, active phases) | ~$9,000 | ~$9,000 | ~$9,000 |
| Infra + SaaS + misc | ~$4,500 | ~$5,000 | ~$5,500 |
| **Steady state monthly burn** | **~$68,000** | **~$87,300** | **~$106,600** |
| Calendar months to G4 | ~26 | ~19 | ~16 |
| **Cumulative cost to G4 (approx)** | **~$1.6M to $1.8M** | **~$1.5M to $1.7M** | **~$1.6M to $1.8M** |

Cumulative cost to G4 is nearly flat across 2, 3, and 4 engineers (roughly $1.5M to $1.8M) because faster burn offsets shorter duration. The decision is therefore not about total capital, it is about time to a partner conversation and about de risking the safety critical code with more than one reviewer. Three engineers is both near the cost floor and materially faster than two, and it puts a second and third set of eyes on the life safety and consent code. **Recommended config: 3 engineers, content lead, retained clinical reviewer, ~19 months to G4, ~$1.6M cumulative.** Take the fourth engineer only if a second content hire is funded alongside, so content stops being the floor.

### 3.4 Cumulative burn by gate (3 engineer recommended config)

Reflects team ramp (content lead and clinical reviewer onboard first because they are the critical path; engineers ramp to full complement by month 2 to 3).

| Gate | Approx month | Cumulative burn | What the gate unlocks |
|---|---|---|---|
| G1 Bench | ~3 | ~$0.22M | Internal proof; angel/pre seed conversation; NSF SBIR pitch on the sensing/AI engineering (`shared_capital_landscape.md` 1.4) |
| G2 Self test | ~7 | ~$0.60M | Founder validated daily loop; demo for pre seed/seed |
| G3 Friends and family | ~12 | ~$1.05M | Retention and failure data; NICHD SBIR Phase I ($256k) and seed round evidence (`shared_capital_landscape.md` 1.3, 2.2) |
| G4 Pilot | ~19 | ~$1.6M | Efficacy signal + unit economics; the partner conversation (employer, payer, OB group) and Series A / NICHD Phase II ($1.71M) |

---

## 4. CRITICAL PATH

The critical path to G4 is not code. It is, in order of bind:

| Rank | Critical path item | Why it binds | Compressible by more engineers? |
|---|---|---|---|
| 1 | **Content authoring + clinical review** | A full pregnancy plus full postpartum year of grounded, versioned, clinically signed off content is ~12 months of content lead + reviewer work. Every warning sign string needs verbatim source match and sign off (Phase 0 section 5; Phase 1 Assumption 3) | No. Compressible only by a second content hire and more reviewer hours |
| 2 | **Pilot cohort run** | G4 exit requires efficacy signal and measured unit economics, which requires a 50 to 200 person cohort observed over ~3 to 4 months, including a postpartum window that is itself multi month | No. It is a clock, not a labor input |
| 3 | **Lab data access commercial terms** | Aggregator per unit pricing is still UNKNOWN (Phase 2 Open Q1); the contract and integration gate the lab feature | Partly (integration), not the contracting |
| 4 | **Legal review of the BP threshold reminder and the reproductive data retention boundary** | Phase 0 Open Q1 (does the BP reminder survive the 2026 FDA sensor section) and Phase 3 Open Q7 (client side field boundary) both need legal sign off before those features ship | No. External counsel timeline |
| 5 | Engineering build | ~15 months at 3 engineers, roughly matching the content floor | Yes, but it is not the binding constraint past 3 engineers |

The wearable data access question, which the framework flagged as a potential company killer, is **not** on the critical path: Phase 1 and Phase 2 established that no V1 marker needs wearable data and the product ships V1 with no wearable integration at all if required. Wearables are a V2 enhancement supplying derived scalars only (Phase 3 7). The critical path is content, clinical review, and the pilot clock. The AI velocity multiplier accelerates rank 5 and nothing above it, which is exactly why it does not move G4.

---

## 5. AI ASSISTED VELOCITY MULTIPLIER (framework section 4)

The framework forbids inventing a productivity number and requires cited empirical evidence with low, mid, and high cases. The published evidence is genuinely contested, and the honest reading is that the multiplier is small and highly context dependent.

### 5.1 The evidence

| Study | Design | Finding | Context relevance to this build | Confidence |
|---|---|---|---|---|
| METR, Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity (arXiv 2507.09089, Jul 2025) | RCT, 16 experienced devs, 246 real tasks, mature repos (~1M LOC), Cursor Pro + Claude 3.5/3.7 | Developers were **19% slower** with AI, while believing they were 20% faster | Our build is greenfield, not a mature 1M LOC repo; METR itself notes the equation differs for greenfield. Sets the pessimistic floor | HIGH (RCT) |
| Google DORA, Accelerate State of DevOps 2024 | Survey, 1000s of respondents | High AI adoption associated with **-1.5% delivery throughput and -7.2% stability** | Team level delivery, not individual task; warns that AI inflates change size | HIGH |
| Google DORA 2025 | Survey | Reversal: **positive** relationship between AI adoption and throughput once integration practices mature | A learning curve exists; a disciplined team can get to net positive | MEDIUM |
| GitClear (2025, via Stack Overflow / industry) | Code analysis | ~41% of committed code is AI generated; 84 to 90% of developers use AI tools | Confirms ubiquity, not delivery speedup | MEDIUM |
| Peng et al., The Impact of AI on Developer Productivity: Evidence from GitHub Copilot (arXiv 2302.06590, 2023) | RCT, isolated task (implement an HTTP server in JS) | Treated group **55.8% faster** (95% CI 21 to 89%); larger benefit for less experienced devs | An isolated greenfield boilerplate task, the best case; not whole project delivery. Sets the optimistic ceiling | HIGH (RCT, narrow task) |

### 5.2 The reconciliation

The two RCTs bracket the truth. Copilot's +55% is a single, isolated, greenfield boilerplate task (the kind of work where autocomplete shines). METR's -19% is sustained work on a large mature codebase with strict quality bars (the kind of work where verifying AI output costs more than it saves). DORA shows that at the team-delivery level the net effect is near zero to slightly negative in 2024 and slightly positive in 2025 with mature practice. This product is a greenfield build with a meaningful boilerplate share (RN screens, CRUD API, RAG scaffolding, connectors) but also a high review burden component (the life safety classifier and the consent enforcement, where AI output must be verified as carefully as METR's subjects verified theirs).

### 5.3 Cases used

| Case | Multiplier | Justification |
|---|---|---|
| Low | **1.0x** | Net neutral. Consistent with DORA 2024 flat-to-negative delivery and METR's caution; assumes AI gains on boilerplate are offset by review and cleanup on the safety critical code |
| **Mid (used in this plan)** | **1.2x** | A disciplined greenfield team captures a modest ~20% net gain on the boilerplate heavy majority (mobile screens, CRUD, RAG plumbing, connectors), consistent with DORA 2025's positive-with-maturity signal, while the safety and consent code sees little to none. Deliberately far below the Copilot 55% because that figure is a narrow task, not whole project delivery |
| High | **1.4x** | Favorable case: strong prompt discipline, a codebase that is largely greenfield and integration heavy, and the team realizing the upper end of the greenfield benefit the Copilot RCT direction implies without claiming its magnitude |

Per framework guidance, because the evidence is contested and the two RCTs disagree by direction, the plan defaults to the conservative mid case (1.2x) and never assumes the Copilot best case. The low case (1.0x) is the one to underwrite capital against for a safety critical build.

### 5.4 Timeline sensitivity to the multiplier (3 engineer config, build months only)

| Case | Multiplier | Effective EEM/mo (3 eng) | Build months (50 EM) |
|---|---|---|---|
| Low | 1.0 | 2.70 | ~18.5 |
| Mid | 1.2 | 3.24 | ~15.4 |
| High | 1.4 | 3.78 | ~13.2 |

The full swing across the entire credible multiplier range is ~5 build months at 3 engineers. Because the content critical path is ~12 months and the pilot clock is ~3 to 4 months regardless, the AI multiplier moves the G4 date by at most ~2 to 3 months. It is a real but second order lever. The critical path dominates.

---

## 6. COMPARABLE VENTURES

What each raised, at what stage, time to revenue, and exits, including the failures. Amounts are total raised unless a round is specified. Two are already profiled in `shared_capital_landscape.md` (Maven, Pomelo) and are summarized here for completeness; the rest are newly researched in this phase.

### 6.1 The scaled and the exited

| Company | Model / buyer | Total raised | Latest stage | Time to revenue | Outcome / status | Confidence |
|---|---|---|---|---|---|---|
| **Progyny** | Fertility + family building benefits to employers | Private raise modest pre IPO | **IPO Oct 2019** at $13/share, ~$130M raised, ~$1.31B day-one market cap; $103.4M revenue H1 2019 | Revenue from launch (B2B benefit, PEPM/utilization) | **Public (NASDAQ: PGNY).** The category's proof that maternal/family benefits sold to employers is a public-scale business | HIGH |
| **Maven Clinic** | Virtual women's + family health, fertility to pediatrics; employers + payers | $425M+ cumulative; **$125M Series F Oct 2024 at $1.7B** | Series F, unicorn | Revenue from B2B contracts early | Private, scaled; the category leader (`shared_capital_landscape.md` 4.2) | HIGH |
| **Pomelo Care** | Virtual value-based maternity + newborn care; payers/value-based | $141M+; **$92M Series C Jan 2026 at $1.7B** (Stripes, a16z) | Series C, unicorn | Revenue via value-based/payer contracts | Private, fast scaling (`shared_capital_landscape.md` 4.2) | HIGH |
| **Carrot Fertility** | Fertility benefits to employers + health plans | **$115M** ($75M Series C Aug 2021, Tiger Global lead) | Series C | Revenue from B2B benefit contracts | Private, operating | HIGH |
| **Cleo** | Family + caregiving benefits to employers | **~$87M** ($40M Series C Mar 2021, Transformation Capital) | Series C | Revenue from employer contracts; reported 8x membership growth, 100%+ revenue growth (2021) | Private, operating | HIGH |
| **Ovia Health** | Pregnancy/fertility/parenting apps + employer/payer benefit | **~$23.5M** over 7 rounds (last Series A 2020) | **Acquired by Labcorp Aug 2021** (terms undisclosed) | ~$20M annual revenue at acquisition | **Exit (strategic acquisition).** DTC app that found its business in the employer/payer channel, then sold to a lab | HIGH |
| **Babyscripts** | Remote prenatal/postpartum monitoring to OB practices + health systems | **~$37M** (Series B $19M total: MemorialCare, Philips, Cigna Ventures) | Series B | Revenue via provider/health-system contracts; 200k+ pregnancies, 30 states | Private, operating; strategic + payer investors | HIGH |

### 6.2 The consumer / community plays

| Company | Model / buyer | Total raised | Stage | Time to revenue | Status | Confidence |
|---|---|---|---|---|---|---|
| **Peanut** | Social network for women (fertility, motherhood, menopause); ad/subscription DTC | **~$21.8M** ($12M Series A 2020, EQT Ventures) | Series A | Slow; community-first monetization | Private, operating | HIGH |
| **Elvie** (Chiaro Technology) | Connected breast pump + pelvic-floor hardware, DTC + insurance | **$186M+** over 12 years (Series C topped to $97M, 2021; BlackRock, Octopus) | Late stage / growth | Product revenue from launch, but never profitable | **Distressed exit: entered administration and assets acquired by Willow, Mar 2025**, ~170 staff affected. A cautionary tale on hardware + DTC femtech burn | HIGH |
| **Bloomlife** | Started DTC contraction monitor; pivoted to B2B2C remote fetal/maternal monitoring | **~$35M** ($12.2M Series A; $14M Series B-II Jun 2025) | Series B | Delayed by pivot; now provider/payer reimbursed (18 payers) | Private, operating; **survived by pivoting off DTC into a cleared medical device + reimbursement model** | HIGH |

### 6.3 The failures (framework requires including the dead)

| Company | Model | Raised | What happened | Lesson for Concept B | Confidence |
|---|---|---|---|---|---|
| **Oath Care** | Group-based continuous care + AI parenting advice + matched parent circles (pregnancy through pediatrics); DTC/community | **~$8M** (General Catalyst, XYZ, OMERS Ventures; founded 2019) | **Shut down (deadpooled, 2024).** Founders publicly described the painful decision | A DTC community + AI-advice parenting product, exactly adjacent to this concept, could not find a durable business at ~$8M raised. Reinforces framework B6: DTC parenting community does not monetize; the buyer is an employer or payer | HIGH (status), MEDIUM (exact date) |
| **Poppy Seed Health** | On-demand text telehealth with doulas/midwives/nurses; DTC + some B2B | **~$4.2M seed** (Jun 2023; Seven Seven Six, Rebalance) | Site/socials still present as of 2026-07-10; no confirmed shutdown, but no growth round after the 2023 seed. Status: **stalled at seed, at-risk** | A thin-capitalized DTC maternal support service struggles to raise past seed without a payer/employer contract engine | MEDIUM |

### 6.4 The pattern, stated bluntly

Every scaled and exited company in this set sells to an employer, a payer, or a provider (Maven, Pomelo, Progyny, Carrot, Cleo, Ovia post-acquisition, Babyscripts). Every DTC or community-first play either stayed small (Peanut), burned out on hardware (Elvie), pivoted into reimbursement to survive (Bloomlife), or died (Oath Care, and Poppy Seed stalled). This is direct external confirmation of founder assumption B6 (Phase 0): the pregnancy DTC subscription is not where the money is; the buyer is the employer or the health plan. It also validates the postpartum + full-year extension thesis (Phase 1, Phase 3 8.3) as the answer to the churn cliff that the pure-pregnancy DTC plays could not escape. Time to revenue tracks the model, not the product: the B2B benefit companies had revenue from contract signing; the DTC plays chased monetization for years and mostly lost.

---

## 7. TEST PLAN BY GATE, AND THE TESTER RECRUITING PROBLEM

### 7.1 Test plan by gate

| Gate | Population | What is tested | Method | Exit criteria |
|---|---|---|---|---|
| G1 Bench | Synthetic + recorded inputs; the engineering team | Red flag classifier recall/precision on a labeled symptom corpus; RAG citation faithfulness; rules engine correctness | Unit + integration tests; adversarial red-team of the safety layer (paraphrase attacks on the classifier); citation eval set | Classifier passes on the full labeled set with zero missed red flags; no ungrounded health claim generated |
| G2 Self test | **Founder circle** (founder + co-founders + a small number of trusted internal users who are or recently were pregnant/postpartum) | Full daily loop over 30 days continuous; notification reliability; false positive rate of the safety layer in real use; the two 30-second surfaces | Dogfooding; instrumented session logs; daily diary | 30 days continuous uptime; safety-layer false positive rate characterized; the surfaces are worth opening (Phase 1 measure) |
| G3 Friends and family | **5 to 15 real users**, real pregnancies/postpartum, recruited from the founders' networks | Onboarding time; retention; consent flows (mother grants/revokes, partner view); failure modes; the partner surface with a real partner | Instrumented cohort; structured interviews; consent audit-log review | Install/onboarding time measured; retention measured across a stage transition; failure modes cataloged; consent enforcement verified server-side |
| G4 Pilot | **50 to 200 users**, structured cohort, ideally via one design partner (an OB practice, an employer, a doula/midwife network) | Efficacy signal (engagement with warning signs, mood-trend surfacing, escalation events); unit economics (infra cost/user per `shared_infra_cost.md`, CAC in the chosen channel); retention across the churn cliff | Cohort study with a design partner; pre/post measures; the escalation event log as the safety evidence base | Efficacy evidence sufficient for a partner conversation; unit economics measured; churn cliff quantified (input to Phase 5/6) |

### 7.2 The tester recruiting problem, solved

The concept brief flags it correctly: the tester population is narrow and time bounded, which makes recruiting harder than it looks. A pregnancy is a moving target. A user recruited at 30 weeks is postpartum in 10 weeks and out of the antepartum test surface; a user recruited to test the postpartum-year features must already be postpartum; and the windows the product most needs to observe (late pregnancy, the first postpartum weeks, the 2-to-12-month mood window) each require a tester who is in that exact window right now. You cannot fast-forward a tester through gestation, and the cohort naturally ages out of the surface being tested.

This is a real constraint. The solution is a rolling, window-matched recruiting strategy plus deliberate sequencing, not a one-time recruit:

| Problem | Solution |
|---|---|
| A tester ages out of the stage under test in weeks | **Recruit a rolling cohort continuously, stratified by stage** (early/mid/late pregnancy, 0-6 weeks postpartum, 6 weeks-12 months postpartum). Always have testers entering each window as others exit. Treat recruiting as a standing operation for the whole G3-G4 period, not an event |
| The postpartum-year features need users you cannot manufacture | **Recruit postpartum users directly** for the postpartum surfaces rather than waiting for antepartum testers to deliver. The postpartum year is long (12 months), so a postpartum recruit gives the longest usable test window and covers the highest-value, highest-mortality surface (Phase 1) |
| Narrow eligible population, low incidence in any one network | **Recruit through the channel that already aggregates the population**: a design-partner OB practice, a doula or midwife network, a childbirth-education class, an employer with a maternity benefit, or an existing pregnancy community (the same channels that are the eventual B2B buyers). This doubles as channel validation for Phase 5 |
| Partner-facing features need a real, engaged partner, not a proxy | **Recruit couples, not individuals**, for the subset of G3 testers assigned to the consent and partner surfaces. Screen for an engaged partner at intake (framework note: the partner-engaged subset is itself a market-sizing input for Phase 5) |
| Safety-critical product, real frightened users at 3am | **Stage the risk**: G2 is founder circle only (internal, controlled), so the enforced safety layer is exercised by people who understand it before any external user relies on it. External users enter only at G3, after the classifier is characterized. Every external tester gets the persistent disclaimer and a briefed escalation path, and every escalation event is logged and reviewed by the clinical reviewer |
| Time-bounded engagement decays as testers deliver/age out | **Overlap the pilot with a design partner** at G4 so recruiting, consent, and clinical oversight run through an institution that already sees a continuous flow of the population, rather than through the founders' personal network, which exhausts quickly |

The recruiting strategy and the go-to-market channel are the same channel. Recruiting testers through an OB practice, a doula network, or an employer benefit is simultaneously the cheapest way to reach the narrow population and a live test of the distribution channel the business will actually use (Phase 5). Do not recruit testers through a channel you would not sell through.

---

## Register Entries

Per framework section 9. Staged for the register keeper; this phase does not edit the registers.

### Sources (stage into `research/registers/sources.md`)

| Source | Org | URL | Pub/accessed | Used for | Credibility |
|---|---|---|---|---|---|
| Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity | METR / arXiv | arxiv.org/abs/2507.09089 | 2025, accessed 2026-07-10 | Velocity low case: -19% RCT, mature codebase | HIGH (RCT) |
| We are Changing our Developer Productivity Experiment Design | METR | metr.org/blog/2026-02-24-uplift-update/ | 2026-02-24 | Follow-up experiment; participation bias caveat | HIGH |
| The Impact of AI on Developer Productivity: Evidence from GitHub Copilot | Peng et al. / arXiv | arxiv.org/abs/2302.06590 | 2023, accessed 2026-07-10 | Velocity high case: +55.8% on isolated greenfield task | HIGH (RCT, narrow) |
| Announcing the 2024 DORA Report | Google Cloud / DORA | dora.dev/research/2024/dora-report/ | 2024, accessed 2026-07-10 | -1.5% throughput, -7.2% stability at high AI adoption | HIGH |
| Announcing the 2025 DORA Report | Google Cloud / DORA | dora.dev/dora-report-2025/ | 2025, accessed 2026-07-10 | Positive throughput relationship with mature practice | MEDIUM |
| The Mythical Man-Month (Brooks's law) | F. Brooks | (book, 1975; anniversary ed. 1995) | 1975 | Coordination overhead model | HIGH (canonical) |
| Software Engineer salary San Diego | Glassdoor / ZipRecruiter / Indeed / Levels.fyi | glassdoor.com; ziprecruiter.com; indeed.com; levels.fyi | 2026, accessed 2026-07-10 | Loaded engineer cost base ($147k-$189k) | HIGH |
| Digital Health Content Creator / Editorial Manager pay | ZipRecruiter | ziprecruiter.com/Jobs/Digital-Health-Content-Creator | 2026, accessed 2026-07-10 | Content lead base band ($84k-$158k) | MEDIUM |
| Telemedicine Ob Gyn hourly pay | ZipRecruiter | ziprecruiter.com/Jobs/Telemedicine-Ob-Gyn | 2026 (via Phase 2) | Clinical reviewer rate $115/hr | HIGH |
| Progyny IPO pricing | GlobeNewswire / Forbes / Bloomberg | globenewswire.com; forbes.com; bloomberg.com | 2019, accessed 2026-07-10 | Progyny IPO $13/share, $130M, $1.31B mkt cap, $103.4M H1 rev | HIGH |
| Labcorp acquires Ovia Health | Fierce Biotech / MedCity / Boston Globe | fiercebiotech.com; medcitynews.com | 2021-08, accessed 2026-07-10 | Ovia $23.5M raised, ~$20M rev, acquired | HIGH |
| Babyscripts Series B | Babyscripts / FinSMEs / BuiltIn | babyscripts.com; finsmes.com; builtin.com | 2021-12, accessed 2026-07-10 | ~$37M total, $19M Series B, investors | HIGH |
| Carrot Fertility Series C | Fierce Healthcare / Femtech Insider / Crunchbase | fiercehealthcare.com; femtechinsider.com | 2021-08, accessed 2026-07-10 | $115M total, $75M Series C, Tiger Global | HIGH |
| Cleo Series C | BusinessWire / Forbes / Femtech Insider | businesswire.com; forbes.com | 2021-03, accessed 2026-07-10 | ~$87M total, $40M Series C | HIGH |
| Peanut Series A | TechCrunch / Forbes / Tracxn | techcrunch.com; forbes.com | 2020, accessed 2026-07-10 | ~$21.8M total, $12M Series A | HIGH |
| Willow acquires Elvie assets; Elvie into administration | TechCrunch / Sifted | techcrunch.com/2025/03/28; sifted.eu | 2025-03, accessed 2026-07-10 | Elvie $186M+ raised, administration, Willow asset buy | HIGH |
| Bloomlife pivot + funding | Femtech Insider / DH Insights / PitchBook | femtechinsider.com; dhinsights.org | 2025, accessed 2026-07-10 | ~$35M raised, DTC-to-B2B2C pivot, FDA clearance, 18 payers | HIGH |
| Oath Care shutdown | TechCrunch / CBInsights / Slice of Healthcare | techcrunch.com; cbinsights.com; sliceofhealthcare.com | 2021-2024, accessed 2026-07-10 | $8M raised, deadpooled 2024 | HIGH (status), MEDIUM (date) |
| Poppy Seed Health seed | Crunchbase / PitchBook | crunchbase.com; pitchbook.com | 2023-06, accessed 2026-07-10 | ~$4.2M seed, Seven Seven Six/Rebalance | MEDIUM |

### Competitors / comparables (stage into `research/registers/competitors.md`)

| Company | Model | Buyer | Raised | Status | Confidence |
|---|---|---|---|---|---|
| Progyny | Fertility/family benefits | Employer | IPO 2019, public | Public (PGNY) | HIGH |
| Maven Clinic | Virtual women's/family health | Employer/payer | $425M+, $1.7B val | Private, scaled | HIGH |
| Pomelo Care | Value-based maternity | Payer | $141M+, $1.7B val | Private, scaling | HIGH |
| Carrot Fertility | Fertility benefits | Employer/health plan | $115M | Private | HIGH |
| Cleo | Family/caregiving benefits | Employer | ~$87M | Private | HIGH |
| Ovia Health | Pregnancy/parenting app + benefit | DTC then employer/payer | $23.5M | Acquired (Labcorp, 2021) | HIGH |
| Babyscripts | Remote prenatal/postpartum monitoring | OB practice/health system | ~$37M | Private | HIGH |
| Peanut | Women's social network | DTC (ad/sub) | ~$21.8M | Private, small | HIGH |
| Elvie | Connected breast pump/pelvic hardware | DTC + insurance | $186M+ | Administration; assets to Willow (2025) | HIGH |
| Bloomlife | Remote fetal/maternal monitor (post-pivot) | Provider/payer | ~$35M | Private, pivoted to survive | HIGH |
| Oath Care | Group care + AI parenting advice | DTC/community | $8M | Dead (2024) | HIGH |
| Poppy Seed Health | On-demand doula/midwife text telehealth | DTC + B2B | ~$4.2M | Stalled at seed | MEDIUM |

### Funding (stage into `research/registers/funding.md`)

Milestone-to-round map for Concept B, tied to gates (section 3.4): angel/pre-seed at G1-G2; NICHD SBIR Phase I (~$256k) and seed at G3; Series A / NICHD SBIR Phase II (~$1.71M) at G4. Investor/deal detail already staged in `shared_capital_landscape.md` section 4.2 (Pomelo, Nanit, Millie, Delfina, Maven) and is not duplicated.

---

## Open Questions

1. **Aggregator per-user lab ingest price (Model 1).** Still UNKNOWN (inherited Phase 2 Open Q1). It sits in the lab-ingest workstream (section 2.1) and the per-user COGS in Phase 6. Does not change the timeline; does affect unit economics measured at G4.
2. **Content authoring duration (~12 months) is an estimate, not a measured value.** The critical-path floor depends on it. If the free public-domain corpus plus original copy takes materially longer to write and clinically review, G4 slips regardless of engineering headcount. Highest-leverage number to validate.
3. **Raw engineering effort (~50 EM to G4) is a founder-facing estimate.** A 20% error moves the build timeline by ~3 months at 3 engineers, still inside the content floor at the mid case, so the G4 date is robust to it; the burn is not.
4. **The AI velocity multiplier is genuinely contested.** The two RCTs disagree by direction. The mid case (1.2x) is a judgment between them, not a measured value for this team. Underwrite capital against the low case (1.0x).
5. **Brooks efficiency haircut (95/90/85%)** is a modeling assumption calibrated to the classic result, not measured for this team on this codebase.
6. **Content Lead base band ($110k)** is anchored to a 2026 digital-health editorial/content-manager range; a perinatal role with clinical literacy may command more. MEDIUM.
7. **Pilot run window (~3 to 4 months)** to reach a credible efficacy + unit-economics signal is an estimate; a payer-grade efficacy signal on the postpartum mortality thesis could require a longer observation window, pushing G4 out. Reconcile with Phase 5/6.
8. **Oath Care exact shutdown date within 2024** not pinned; status (dead) is confirmed. Poppy Seed Health current operating status is inferred from an active site and no post-2023 round; not a confirmed shutdown.

## Assumptions Made

1. **Fully loaded engineer cost $220k/yr** (base ~$155k x 1.4 loading). If the team is senior-heavy or the loading is 1.25x, the figure moves ~$194k to $259k. Impact: linear on burn, not on timeline.
2. **The two non-engineering roles are constant across all headcount columns** because they are not optional (Phase 2, 2.4; concept brief Phase 4 note). Removing them to flatter the engineering-only cost would be the exact error the brief warns against.
3. **Raw engineering ~50 EM to G4**, allocated by workstream (section 2.1) as founder-facing estimates. Flagged.
4. **Mid-case AI multiplier 1.2x, applied to engineering workstreams only.** Not applied to content, clinical review, wearable/lab partnerships, or the pilot clock, which is why it does not move the critical path.
5. **Brooks per-head efficiency 100/95/90/85%** for 1/2/3/4 engineers, calibrated to the n(n-1)/2 communication-path growth in Brooks 1975.
6. **Pilot observation window ~3 to 4 months** on top of build to satisfy the G4 exit criteria. If a payer-grade signal needs longer, G4 slips.
7. **Content authoring critical-path floor ~12 months.** Load-bearing; it is what makes the fourth engineer nearly worthless for the G4 date.
8. **Design is a contract line (~$9k/mo during G1-G3), not engineering headcount.** If design is brought in-house, add ~$14k/mo loaded and remove the contract line; net cost similar.
9. **Comparable-venture figures are total-raised or specified-round from company press, trade press, and Crunchbase/PitchBook secondary profiles.** Private valuations and exact acquisition terms (Ovia) are undisclosed where noted.

## Confidence Summary

Overall confidence: HIGH on the structural conclusions, MEDIUM on the precise cost and timeline point estimates (which rest on effort and duration estimates, not measured actuals).

Strongest (HIGH): the critical-path finding (content + clinical review + pilot clock, not code), which follows directly from prior-phase facts and from the flat cost-to-G4 across headcounts; the comparable-venture pattern (every scaled/exited company sells B2B; every DTC/community play stayed small, pivoted, or died), which is well-sourced and directly confirms founder assumption B6; the loaded engineer cost and the clinical-reviewer rate (primary 2026 market data); the AI velocity evidence base (two RCTs plus DORA, correctly bracketed).

Weakest (MEDIUM to LOW): the absolute raw-engineering effort (~50 EM) and the content-authoring floor (~12 months), which together set the timeline and are estimates; the AI multiplier mid case (1.2x), a judgment between two contradictory RCTs; the Brooks haircut, a calibrated assumption; the Content Lead base band. None of these weaknesses changes the recommendation: **3 engineers plus a content lead plus a retained clinical reviewer, ~19 months and ~$1.6M to G4, with the critical path running through content and the pilot clock, not code.** The strategic conclusion is robust to the estimation weaknesses because the fourth engineer's near-zero effect on the G4 date is driven by the content floor, and even a large error in the engineering estimate leaves the content floor binding.
