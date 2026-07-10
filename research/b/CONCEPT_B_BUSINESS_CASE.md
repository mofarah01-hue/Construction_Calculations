# CONCEPT B BUSINESS CASE: PREGNANCY AND PARENTING COMPANION

Prepared 2026-07-10. Governed by `00_framework.md`. This document synthesizes Concept B Phases 0 through 6 (`research/b/phase0_scope.md` through `phase6_businesscase.md`), the `regulatory_risk_register.md`, and the Phase 0 regulatory record. Every material number is traced to its source phase in parentheses. It is written for a reader deciding whether to fund the company.

---

# PART 1: EXECUTIVE SUMMARY

## Recommendation

**Fund the build to G4.** Commit approximately $1.6M to reach a pilot with efficacy evidence and measured unit economics in approximately 19 months (Phase 4). Structure the raise as pre seed plus non dilutive NIH funding, hold the B2B channel as the thesis, and gate the next tranche on a signed institutional design partner. Do not fund a direct to consumer pregnancy subscription as the business.

## The core thesis

| Pillar | Statement | Source |
|---|---|---|
| Defensible center | The urgent maternal warning signs that CDC Hear Her and the Alliance for Innovation on Maternal Health already instruct every pregnant and postpartum person to watch for, surfaced at the right moment to an exhausted person in the postpartum window when no clinician is watching. It is patient education, makes no diagnostic claim, requires no wearable and no inference, and addresses the leading preventable causes of maternal death | Phase 1 strategic finding; Phase 0 section 1 |
| Self report over inference | Passive affect inference from consumer physiology is not defensible for a new user: generalized cross person, cross device emotion detection is near chance, and vendor stress scores are unvalidated and unauditable. A daily self report scale of the product's own design is a journal, asserts nothing, is cheap and accurate, and is what the user already expects | Phase 2 section 2.3; framework section 2; founder assumption B4 |
| Wearable dependency not fatal | No V1 marker requires raw consumer wearable data. Every V1 marker survives on self report plus published reference alone. The one clinical fidelity input, blood pressure, comes from a validated home cuff the user already buys, not a wristband. Derived wearable scalars are an optional V2 enhancement behind a swappable data layer | Phase 1 section 3; Phase 2 section 2.1; Phase 3 section 7 |
| B2B/payer over DTC | A pregnancy has a roughly ten month churn cliff and a 100 percent terminal exit at birth. DTC LTV is approximately $47 pregnancy only against a CAC of $30 to $100, so DTC LTV to CAC is at or below 1.0 and structurally unprofitable. The postpartum and early childhood extension lifts LTV to approximately $75 to $130 but does not by itself clear paid acquisition. The fundable business prices the covered pregnancy to an institution | Phase 5 sections 2 and 4; Phase 6 thesis |

The four pillars reinforce each other. The defensible center needs no wearable and no inference, which is why the wearable dependency is not fatal and why self report is the right posture. That same center, delivered daily across the full postpartum year, is the retention hook that extends subscriber life past the churn cliff, and the churn cliff is the reason the channel must be B2B.

## The capital ask and what it buys

| Round | Gate | Size | What it buys | Source |
|---|---|---|---|---|
| Pre seed | G0 to G2 | $0.5M to $1.5M | Founder validated daily loop, the enforced safety layer, first content build. Includes NICHD SBIR Phase I (~$256K) and NSF SBIR (~$305K) non dilutive | Phase 4 section 3.4; Phase 6 section 3.3 |
| Seed | G3 to G4 | $3M to $9M | Consent system, 50 to 200 person pilot cohort, first paid design partner, G4 evidence package. Includes NICHD SBIR Phase II (~$1.71M) | Phase 6 section 3.3 |
| Path to breakeven | G4 to G6 | $35M to $45M cumulative over ~6 years | Payer and employer sales motion, scale to ~50,000 engaged episodes, EBITDA breakeven | Phase 6 sections 1.2 and 3.3 |

The build to G4 is cheap and nearly flat across engineering headcount (roughly $1.5M to $1.8M at 2, 3, or 4 engineers, because faster burn offsets shorter duration). The recommended configuration is 3 engineers plus a full time content lead plus a retained OB-GYN clinical reviewer at approximately $87,300 per month steady state, reaching G4 in approximately 19 months at approximately $1.6M cumulative (Phase 4 section 3.3). The capital that matters is the $35M to $45M from G4 to breakeven, which is where every scaled comparable spent (Babyscripts reached ~200,000 pregnancies on ~$37M total raised; Phase 4 section 6.1).

## Top risks and kill criteria

| Risk | Why it is severe | Mitigation | Source |
|---|---|---|---|
| No institutional buyer contracts by G4 (K1, the decisive risk) | If the only willing buyer is the consumer, the business is DTC only, and DTC only is structurally unprofitable against the churn cliff | Lead the sale with the OB per patient channel (fastest B2B cycle), convert to employer PEPM, build toward Medicaid PMPM | Phase 6 section 6 K1 |
| The enforced safety layer fails in production (K2) | A delayed care event is the highest severity, highest liability failure and is the reason the product exists. Any evidence the red flag layer reassures against an enumerated warning sign is a ship blocker | Deterministic red flag classifier that runs before the model and cannot be jailbroken, unit tested, logged, adversarially tested every release | Phase 0 section 5; Phase 6 K2; risk register R3, R9 |
| Reproductive health data legal event (K3) | Post Dobbs, this data is subpoena and warrant exposed; the HIPAA Reproductive Health Rule was vacated nationwide (Purl v. HHS, 2025-06-18) | Data minimization as architecture, client side encryption of the most sensitive fields so a subpoena yields least plaintext, never share with advertising or analytics third parties | Phase 3 section 6; Phase 6 K3; risk register R5 |
| Efficacy fails to move a payer quality measure at G4 (K4) | Without a measure the buyer is graded on, the payer has no budget rationale and the PMPM thesis collapses | Target the postpartum follow up (PPC) and depression screening measures (PND-E, PDS-E) that entered the Medicaid Core Set in 2024 | Phase 5 section 4.1; Phase 6 K4 |
| Content critical path slips (K5) | Content authoring plus clinical review is the binding constraint to G4, not code. There is nothing safe to ship without it | Content lead and retained reviewer onboarded first; second content hire to break the floor if it slips past ~18 months | Phase 4 section 4; Phase 6 K5 |

Two founder assumptions are contradicted by evidence and are parked, not built around: B1 (a cash pay lab panel duplicates insured prenatal labs and adds nothing) and B5 (an at home ultrasound is a Class II device, not a feature) (Phase 0 section 1; Phase 2 section 2.2).

---

# PART 2: THE CASE

## 2.1 Product and claims scope

The product is a subscription companion for first time parents spanning pregnancy, postpartum, and early childhood. A grounded language model fronts the whole surface, personalized by three inputs: maternal physiology, ingested lab data, and gestational or child developmental stage. It speaks to the mother and, separately and only by her granular revocable consent, to the partner. Positioning is general wellness, a settled decision (framework section 2; Phase 0).

Feature classification (Phase 0 section 3):

| Class | Count | Features |
|---|---|---|
| CORE | 10 | Maternal physiological tracking, lab ingestion, nutrition guidance, sleep guidance, symptom normalization, week by week content, mood self report, postpartum recovery tracking, infant milestones, infant feeding and sleep |
| DIFFERENTIATOR | 3 | Partner facing guidance (item 7), postpartum mental health support (item 10), urgent maternal warning sign surfacing and escalation (item 14) |
| LATER | 1 | Long horizon parenting guidance for the older child (item 13) |

No feature is blocked in whole. Every feature has a wellness variant that ships; eight carry a blocked sub variant that is engineered out and logged in the risk register (Phase 0 section 3).

The claims discipline is the single most important design rule and it is what keeps the product inside the lane by construction (framework section 2; Phase 0 section 4):

| Data type | Posture | Example that ships | Example that crosses the line |
|---|---|---|---|
| Self report | A journal. Asserts nothing | "You logged low mood 9 of the last 14 days, which you flagged yourself. That is worth a conversation with your provider." | "Your scores indicate depression." |
| Measurement plus reference | Not a claim about disease | "Your resting heart rate is 12 percent above your first trimester baseline. RHR typically rises across pregnancy." | "Your HRV pattern is consistent with preeclampsia." |
| Inference of a named disease from passive data | A claim. Architecturally impossible to emit | (not emitted) | "This pattern is consistent with depression." |

The regulatory environment is current as of the FDA revision of its General Wellness and Clinical Decision Support guidances on 2026-01-06, which retained the two intended use categories and added a sensor boundary section (Phase 0 section 4, HIGH). The one live regulatory question is whether the blood pressure threshold reminder survives that sensor section, which places outside the lane any physiological output that includes an alarm directing medical management. The mitigation is that the escalation restates the user's own provider's threshold and routes to "contact your provider or 911," never an app generated clinical alarm tied to a named disease. This is flagged for legal review before the BP feature ships (Phase 0 landmine 6, MEDIUM; Phase 4 critical path rank 4).

For the mood screening landmine, the recommended v1 default is the product's own design daily scale (unambiguously a journal, zero licensing, HIGH confidence). PHQ-9 is public domain and free if a validated instrument is wanted; EPDS is copyright of the Royal College of Psychiatrists and requires a written commercial license, so it is deferred (Phase 0 landmine 2).

## 2.2 Markers and the daily surfaces

Markers define the data requirement; no wearable is selected before knowing what the product needs (Phase 1). The ranked v1 shortlist, by actionability times evidence strength divided by data acquisition cost (Phase 1 section 2):

| Rank | Marker or bundle | Evidence | Data cost | Wearable required |
|---|---|---|---|---|
| 1 | Urgent maternal warning signs logger and escalation (14 signs) | HIGH, CDC and ACOG verbatim | Lowest | No |
| 2 | Postpartum daily mood across the full year | HIGH prevalence and mortality data | Lowest | No |
| 3 | Postpartum blood pressure, home cuff | HIGH | Low, validated cuff she buys | No |
| 4 | Antepartum blood pressure, home cuff | HIGH | Low | No |
| 5 | Antepartum daily mood and anxiety, own scale | HIGH prevalence | Lowest | No |
| 6 to 10 | Gestational weight gain vs IOM range; fetal movement and kick counts; gestational content; partner perinatal depression check in; partner consent layer | HIGH to MEDIUM | Low to build cost | No |

All top five clear on self report and published reference alone. The evidentiary spine (Phase 1): mental health conditions are the single leading underlying cause of US pregnancy related death (22.7 percent, MMRC 36 states 2017 to 2019), 53 percent of pregnancy related deaths occur 7 to 365 days postpartum, and more than 80 percent are preventable (MMRC-3619, HIGH). Postpartum preeclampsia drives readmission at a median of 6 days, before the six week visit (PP-HTN, HIGH). Postpartum depression has two onset peaks with late onset at 2 to 12 months, the window six week screening misses (PPD-ONSET, HIGH).

The two daily surfaces are the product's whole retention argument: if they are not worth opening, nothing else matters (Phase 1 section 4). Each is a 30 second read. Hers leads with a one tap private mood check, her BP trend, and an always present warning sign strip that restates the CDC list verbatim and taps to a one tap call, quoting that serious problems can appear up to a year after birth. His view renders only what she has granted, tells him one concrete thing that helps today, carries the same warning sign strip, and asks after his own mental health (paternal perinatal depression runs 8 to 10 percent; PAT-DEP, HIGH). The share state is visible to both.

Markers killed or deferred: home uterine activity monitoring is KILL on evidence (ACOG and USPSTF do not recommend it; FDA reclassified it Class III to II in 2001; HUAM, HIGH); passive affect inference is redesigned to self report; food photo nutrient estimation ships as a diary, not a nutrient claim (median error ~22 percent; FOOD-AI, MEDIUM) (Phase 1 section 5).

## 2.3 Data inputs and feasibility

Three load bearing findings (Phase 2):

| Input | Finding | Consequence |
|---|---|---|
| Wearable | No consumer device exposes raw PPG, continuous skin temperature, or continuous SpO2 under commercial terms. Derived scalars (RHR, derived HRV, temperature deviation, sleep summaries, spot SpO2) are obtainable from Apple, Oura, Fitbit/Google, Garmin, or Withings and are sufficient for the V2 physiological layer. No V1 marker needs any of it | The product ships V1 with no wearable integration at all if required (Phase 2 section 2.1) |
| Labs | Model 1 (ingest the labs her OB already ordered, via a health data aggregator over the Cures Act (g)(10) FHIR API and TEFCA) is the correct answer, roughly two orders of magnitude cheaper per user than Model 2 (order a cash pay panel). Model 2 re sells insured prenatal tests and adds nothing a prenatal panel lacks | Recommend Model 1, with manual photo upload (Model 3) as fallback. Reject Model 2. Confirms founder assumption B1's own hedge (Phase 2 section 2.2) |
| Content | The obstetric safety spine, nutrition layer, growth charts, and infant milestone checklists are free public domain government content (CDC, USDA, WHO, NIH). Licensed proprietary content (ACOG, AAP, parenting frameworks) maps onto exactly the V2 and LATER features | V1 grounding corpus carries zero licensing cost. A retained OB-GYN reviewer at ~$115/hr is a permanent operating cost, not a launch expense (Phase 2 section 2.4) |

The affect inference finding is decisive and multiply sourced: generalized emotion recognition reaches only ~67 percent (near chance for multiclass) against ~95 percent for personalized models that a new user cannot support, and stress detection does not reproduce across devices (Phase 2 section 2.3, HIGH). Self report is confirmed as the correct posture.

## 2.4 Architecture and consent

Three architectural decisions govern the build (Phase 3):

1. **A rules engine that a language model narrates, not a language model that infers.** Every clinical, safety, and personalization decision is deterministic code (the gestational clock, trend math, threshold checks, content selection, red flag detection, nudge ranking). The model receives a fully resolved decision and phrases it warmly. It is never asked what the data means. This is forced by the claims boundary, the affect inference finding, and the safety layer's need for testable behavior (Phase 3 section 3).

2. **The consent layer is the spine, not a setting.** The mother is the resource owner; the partner sees only scoped, revocable grants modeled on User Managed Access semantics, defaulting closed on mood and reproductive fields, revocable in one tap with no notification that could create relational pressure. Enforcement is server side at the data delivery boundary, so a revoked grant means the partner client never receives the data, not merely that a UI hides it. Done well this is the moat no competitor serves; done badly it is a nonconsensual disclosure of one person's reproductive data to another (Phase 3 section 4).

3. **Pure cloud SaaS with a client side encrypted sensitive tier.** Reproductive status and loss fields are held in a client side encrypted store (SQLCipher, key in the secure element), so the operator cannot produce plaintext under subpoena, only ciphertext. This is a first order design input given the post Dobbs environment and the Purl v. HHS vacatur of the HIPAA Reproductive Health Rule, not a compliance afterthought (Phase 3 section 6).

The safety enforcement layer sits first in the daily pipeline, before the model. Every input passes a deterministic red flag classifier matching the CDC Hear Her / AIM list plus a BP threshold trigger and any self harm response. On a match the pipeline short circuits, the model is bypassed, and a fixed legally reviewed direct to care interstitial is served and logged. The model is a downstream presentation layer for the cleared, non urgent majority; on a red flag it is never invoked. The corpus constraint is the output side complement: no citable passage, no health claim (Phase 3 sections 2.2 and 5).

The grounded AI layer costs roughly $0.50 to $1.50 per user per month, dominated by model inference; retrieval overhead is immaterial. Full platform cost per user is $7 to $19 (small), $1.50 to $4.50 (mid), $1 to $3 (large) (Phase 3 section 2.3).

## 2.5 Development plan and cost to each gate

This product is gated by content and clinical review and the pilot clock, not by code (Phase 4 thesis). At the recommended headcount the engineering build (~15 months) and the clinically reviewed content build (~12 months) finish close together, and the pilot observation window (~3 to 4 months) sits on top. A fourth engineer compresses code but not content or the pilot, so it barely moves G4.

Cost model (Phase 4 sections 1 and 3): fully loaded engineer ~$220K/yr (~$18,300/mo), content lead ~$155K/yr, retained OB reviewer ~$60K to $90K/yr. The AI velocity multiplier is genuinely contested (METR RCT shows 19 percent slower on mature code; Copilot RCT shows 55 percent faster on isolated greenfield tasks); the plan defaults to the conservative mid case of 1.2x applied to engineering only, and underwrites capital against 1.0x (Phase 4 section 5).

| Config | Calendar months to G4 | Steady state monthly burn | Cumulative cost to G4 |
|---|---|---|---|
| 2 engineers | ~26 | ~$68,000 | ~$1.6M to $1.8M |
| 3 engineers (recommended) | ~19 | ~$87,300 | ~$1.5M to $1.7M |
| 4 engineers | ~16 | ~$106,600 | ~$1.6M to $1.8M |

Cumulative cost to G4 is nearly flat, so the decision is time to a partner conversation and putting more than one reviewer on the life safety and consent code, not total capital. Three engineers is near the cost floor, materially faster than two, and peer reviews the safety critical code (Phase 4 section 3.3).

Cumulative burn by gate (3 engineer config, Phase 4 section 3.4): G1 Bench ~month 3, ~$0.22M; G2 Self test ~month 7, ~$0.60M; G3 Friends and family ~month 12, ~$1.05M; G4 Pilot ~month 19, ~$1.6M.

The comparable venture pattern is unambiguous and confirms the channel thesis (Phase 4 section 6): every scaled or exited company sells B2B (Maven $425M+ raised at $1.7B; Progyny public since 2019; Pomelo $141M+ at $1.7B; Carrot $115M; Cleo ~$87M; Ovia acquired by Labcorp 2021; Babyscripts ~$37M). Every DTC or community first play stayed small (Peanut ~$21.8M), burned out on hardware (Elvie $186M+ into administration 2025), pivoted to survive (Bloomlife), or died (Oath Care, an AI parenting community, deadpooled 2024 at ~$8M raised).

The tester recruiting problem is real: the population is narrow and time bounded and ages out of the stage under test in weeks. The solution is a rolling, stage stratified cohort recruited through the same OB, doula, and employer channels that are the eventual B2B buyers, which doubles as channel validation (Phase 4 section 7).

## 2.6 Market, channel, and churn

Bottom up sizing (Phase 5 section 1): US annual births ~3.63M (2024, HIGH); first births ~1.4M (MEDIUM); serviceable first time parent households with an engaged partner ~800,000 per year (LOW). This is a flow that fully refreshes annually and, for a pregnancy only product, fully exits at birth.

The churn cliff is the whole question (Phase 5 section 2). New mother churn is ~70 percent by week 4 postpartum (Mordor Intelligence, MEDIUM). LTV under a DTC $12/month subscription at 75 percent margin:

| Scenario | Expected paying months | LTV (contribution) | Multiple |
|---|---|---|---|
| Pregnancy only | 5.2 | ~$47 | 1.0x |
| With extension, base | 8.3 | ~$75 | 1.6x |
| With extension, high | 13 to 14 | ~$120 to $130 | 2.6x to 2.8x |

The extension lifts LTV 1.6x to 2.8x, the quantified case for building postpartum and early childhood into v1. But against a DTC CAC of $30 to $100, pregnancy only is LTV to CAC at or below 1.0 and even the base extension does not clear blended paid acquisition. The extension fixes the cliff's slope, not the fundamental problem. The channel must change (Phase 5 section 2.5).

Channel comparison (Phase 5 section 4):

| Channel | Effective CAC per pregnancy | Cycle | Churn cliff exposure | Verdict |
|---|---|---|---|---|
| DTC subscription | $30 to $100+ | Instant | Full | Top of funnel only, not a standalone business |
| Employer PEPM | Low per pregnancy, high upfront | 6 to 18 months | Buyer absorbs it | Strong; first scalable recurring revenue |
| Health plan / Medicaid PMPM | Very low per member, very high upfront | 12 to 24+ months | Buyer absorbs it | Strongest on budget and mission; slowest to close |
| OB practice RPM | Moderate | 3 to 9 months | Irrelevant at contract level | Best reimbursement on ramp, fastest B2B cycle |
| Retail / wearable bundle | Low marketing, high margin give up | Retail | Full | Weak |

The policy tailwind is decisive for the extension thesis (Phase 5 section 4.1): Medicaid finances ~41 percent of US births; the 2024 Medicaid Maternity Core Set added postpartum depression screening measures (PND-E, PDS-E); 48 states plus DC have extended Medicaid postpartum coverage to 12 months; and the CMS Transforming Maternal Health model selected 15 states for a 10 year value based maternity program (2025 to 2034, up to $17M per state). The postpartum year, which the product identifies as the unwatched high risk window, is now covered, measured, and funded.

Reimbursement runs through a clinician, not the app: RPM (CPT 99453/99454/99457/99458, ~$102 to $142 per patient per month at Medicare rates) is billed by the ordering OB, and the app is the instrument, not the biller. This is Babyscripts' structure and it holds the wellness claim boundary and the reimbursement upside at once (Phase 5 section 5).

## 2.7 Business case and capital

Three scale scenarios on the recommended enablement plus engagement model, the unit being an engaged maternity episode (Phase 6 section 1):

| Line | Small (hundreds) | Mid (thousands) | Large (tens of thousands) |
|---|---|---|---|
| Engaged episodes (annual) | 300 to 500 | ~5,000 | ~50,000 (~1.4 percent of US births) |
| Annual revenue | $50K to $250K | ~$1.5M | ~$20M |
| Gross margin (enablement) | n/m | ~70 percent | ~75 to 80 percent |
| Annual burn (loaded) | $1.5M to $1.8M | $3.5M to $5M | $14M to $18M |
| Cumulative capital to sustain stage | $3M to $4M | $12M to $20M | $35M to $45M |
| Months to company breakeven | none (sub scale) | not yet | ~60 to 84 from founding |

Company breakeven requires ~50,000 engaged episodes across multiple concurrent payer and employer contracts, consistent with Babyscripts reaching ~200,000 pregnancies on ~$37M raised. The value based clinical delivery variant (Pomelo model) raises revenue per episode but drops gross margin to 40 to 55 percent and pushes capital to breakeven toward $100M+; same requirement to reach tens of thousands of covered lives, more capital, lower margin (Phase 6 section 1.3).

Pricing verdict (Phase 6 section 2.6): lead with per patient to an OB practice for the fastest paid pilot and reimbursement proof, convert to employer PEPM for the first scalable recurring revenue, and build toward Medicaid PMPM as the largest and most defensible pool. Consumer monthly and the wearable bundle are engagement surfaces only.

Capital plan, non dilutive first (Phase 6 section 3): the NIH IMPROVE Initiative funds AI and ML tools that predict or indicate maternal morbidity and mortality risk, including tools measuring blood pressure and maternal physiology, which is the exact surface of this product. NICHD SBIR Phase I (~$256K) and NSF SBIR (~$305K) can cover ~$0.5M early, and NICHD Phase II (~$1.71M) can sequence against the G4 pilot, materially offsetting the build. Early stage deal evidence confirms the thesis: Malama Health, a Medicaid first, postpartum year, app enabled maternal company, raised a $9.2M seed (Acumen America), the single most on thesis recent datapoint, and Matresa, an AI maternal companion nearly identical in concept, set a pre seed benchmark.

Risk register in business terms (Phase 6 section 5), cross referenced to the regulatory register:

| Risk | Cross ref | Likelihood | Impact | Status |
|---|---|---|---|---|
| Wearable API dependency | R7 | HIGH naive, LOW engineered | SEVERE if depended on | Already de risked; V1 needs no wearable |
| Content licensing | R8 | MEDIUM | HIGH | V1 corpus is free public domain; ACOG/AAP is a costed V2 line |
| Reproductive health data legal risk | R5 | HIGH | SEVERE | Mitigated by minimization and client side encryption; mostly design discipline |
| Clinical liability (failure to escalate) | R3, R9 | MEDIUM | SEVERE | Enforced, logged red flag layer; insurance at G5 |
| The churn cliff | Phase 5 | HIGH for DTC, LOW for B2B | SEVERE for DTC only | Neutralized by the B2B channel, not solved at the consumer level |

---

# PART 3: APPENDICES

## Appendix A: Traceability of key numbers to phases

| Number | Value | Source phase |
|---|---|---|
| US annual births 2024 | 3,628,934 | Phase 5 section 1.1 (CDC NVSR, HIGH) |
| First births per year | ~1,400,000 | Phase 5 section 1.1 (derived, MEDIUM) |
| Serviceable first time parent households/yr | ~800,000 | Phase 5 section 1.1 (LOW) |
| Postpartum churn by week 4 | ~70 percent | Phase 5 section 2.1 (Mordor, MEDIUM) |
| DTC LTV pregnancy only | ~$47 | Phase 5 section 2.3 |
| DTC LTV base extension | ~$75 | Phase 5 section 2.4 |
| DTC LTV high extension | ~$120 to $130 | Phase 5 section 2.4 |
| DTC CAC | $30 to $100+ | Phase 5 section 4 |
| Mental health share of pregnancy related death | 22.7 percent (leading cause) | Phase 1 (MMRC-3619, HIGH) |
| Pregnancy related deaths 7 to 365 days postpartum | 53 percent | Phase 1 (MMRC-3619, HIGH) |
| Medicaid share of US births | ~41 percent | Phase 5 section 4.1 (HIGH) |
| Medicaid 12 month postpartum extension | 48 states plus DC | Phase 5 section 4.1 (HIGH) |
| TMaH model | 15 states, 2025 to 2034, up to $17M/state | Phase 5 section 4.1 (HIGH) |
| RPM reimbursement | ~$102 to $142 per patient per month | Phase 5 section 5 (HIGH) |
| Fully loaded engineer cost | ~$220K/yr | Phase 4 section 1.1 (MEDIUM) |
| Content lead cost | ~$155K/yr | Phase 4 section 1.2 (MEDIUM) |
| Retained OB reviewer | ~$115/hr, ~$60K to $90K/yr | Phase 2 section 2.4; Phase 4 section 1.2 (HIGH rate) |
| AI velocity multiplier (mid) | 1.2x | Phase 4 section 5 (contested) |
| Months to G4 (3 eng) | ~19 | Phase 4 section 3.2 |
| Cumulative cost to G4 | ~$1.6M | Phase 4 section 3.3 |
| Grounded AI cost per user/month | $0.50 to $1.50 | Phase 3 section 2.3 |
| Platform cost per user/month | $7 to $19 / $1.50 to $4.50 / $1 to $3 | Phase 3 section 2.3 |
| Breakeven scale | ~50,000 engaged episodes | Phase 6 section 1.2 |
| Large scenario revenue | ~$20M at ~75 to 80 percent margin | Phase 6 section 1.2 |
| Cumulative capital to breakeven | ~$35M to $45M over ~6 years | Phase 6 sections 1.2 and 3.3 |
| NICHD SBIR Phase I / Phase II | ~$256K / ~$1.71M | Phase 6 section 3.1 (HIGH mechanics) |
| Malama Health seed (on thesis comparable) | $9.2M | Phase 6 section 3.2 (HIGH deal) |
| Babyscripts (leanest scaled comparable) | ~$37M raised, ~200,000 pregnancies | Phase 4 section 6.1; Phase 5 section 3.3 (HIGH) |

## Appendix B: Open questions carried from the phases

| # | Open question | Blocks | Source |
|---|---|---|---|
| 1 | Does the BP threshold reminder survive the 2026-01-06 FDA sensor section? Needs legal review before it ships | The BP feature | Phase 0 OQ1; Phase 4 critical path |
| 2 | Aggregator per user lab ingest price (Model 1) is UNKNOWN; all five vendors price custom | Per episode COGS precision, not the ranking | Phase 2 OQ1 |
| 3 | ACOG and AAP content license fees are quote based and UNKNOWN | V2 content cost precision ($0.3M to $3M estimate) | Phase 2 OQ4 |
| 4 | Whether payers require a validated screening instrument (EPDS/PHQ-9) versus the own design scale plus CDC self harm routing for reimbursement | Mood feature design for the payer channel | Phase 1 OQ3; Phase 2 OQ8 |
| 5 | Actual PEPM and PMPM contract values realized by Maven, Ovia, Pomelo are undisclosed; the revenue model rests on per episode ranges, not observed prices | The revenue model (largest single unknown) | Phase 5 OQ5; Phase 6 OQ1 |
| 6 | Blended net revenue per engaged episode ($100 to $400) is a model estimate; a 2x error moves breakeven scale and capital materially | Breakeven scale and capital | Phase 6 OQ2 |
| 7 | Stratified normative physiological curves by age, BMI, parity appear not to exist in published form | V2 personalization ceiling (not V1) | Phase 1 OQ1; Phase 2 |
| 8 | Content authoring duration (~12 months) is an estimate; it floors the G4 schedule | The G4 date | Phase 4 OQ2 |
| 9 | SBIR-STTR reauthorization timeline and current IMPROVE NOSI re issue status must be confirmed before filing | Non dilutive capital timing | Phase 6 OQ3, OQ4 |
| 10 | Reproductive field retention and client side storage boundary needs legal review against the launch state footprint | The privacy architecture implementation | Phase 3 OQ7 |

## Appendix C: Risk register summary (regulatory register R1 to R9)

Scored over the first 36 months of commercial operation absent mitigation; impact on the worst credible outcome (`regulatory_risk_register.md`).

| ID | Risk | Concept | Likelihood | Impact | Primary control |
|---|---|---|---|---|---|
| R1 | FDA reclassification (device creep) | A and B | MEDIUM | SEVERE | Claims linter in CI blocking any named disease inference from passive data; input versus inference discipline |
| R2 | FTC substantiation (measurement claims) | A and B | HIGH | HIGH | Every shipped metric becomes a validation line item; withhold or trend without an accuracy claim until validated |
| R3 | Product liability: failure to escalate | A and B | MEDIUM | SEVERE | Enforced, logged red flag layer independent of the LLM; never position detection as a guarantee |
| R4 | State biometric privacy (BIPA/CUBI/MHMDA) | A primary, B (health data) | HIGH | SEVERE | Consent architecture as a first class feature; on device inference; Meta CUBI $1.4B and Facebook BIPA $650M anchor the tail |
| R5 | Reproductive health data legal risk | B primary | HIGH | SEVERE | Minimization and short retention as architecture; client side encryption; never share with ad/analytics third parties (the Flo and GoodRx trigger) |
| R6 | Wiretap / two party consent audio | A only | MEDIUM | HIGH | Not applicable to Concept B (no ambient audio) |
| R7 | Wearable API dependency | B primary | HIGH naive, LOW engineered | SEVERE | Make wearable data optional; V1 needs none; Fitbit Web API turndown Sept 2026 is the template event |
| R8 | Content licensing | B | MEDIUM | HIGH | Free public domain V1 corpus; never embed a proprietary instrument as a scored result; license explicitly if used |
| R9 | Any output that delays care | A and B | MEDIUM | SEVERE | Hard coded red flag layer that overrides the assistant; never emit "you are fine" to a symptom query; adversarial test every release |

Weakest register entries are R3 and R9 on the quantitative side: product liability exposure and delayed care severity are real and severe but resist dollar estimation before a characterized false negative rate exists at G3/G4. The causation defense that has protected PERS vendors is genuine but fragile and is not a design strategy (`regulatory_risk_register.md` R3, S6).

---

## Open Questions

The ten open questions in Appendix B are the material unresolved items. The three that most affect the funding decision:

1. **No observed B2B contract prices (Phase 5 OQ5; Phase 6 OQ1).** The entire revenue model rests on per episode ranges inferred from public data because Maven, Ovia, and Pomelo contract values are undisclosed. This is the largest single unknown and it is what the G4 pilot must resolve empirically.
2. **The BP threshold reminder's regulatory standing (Phase 0 OQ1).** MEDIUM risk, needs legal sign off before the feature ships, and it is on the critical path.
3. **Content authoring duration (Phase 4 OQ2).** The ~12 month content floor sets the G4 date and is an estimate, not a measured value; it is the highest leverage schedule number.

## Assumptions Made

This synthesis introduces no new numbers. Every figure is carried from a phase output with its confidence rating preserved. The material inherited assumptions the reader should weigh:

1. **The recommended model is B2B enablement, not value based clinical delivery** (Phase 6 A1). If the company must deliver clinical care directly to bill, gross margin falls to 40 to 55 percent and capital to breakeven roughly triples toward $100M+.
2. **The churn cliff is neutralized by the B2B channel, not solved at the consumer level** (Phase 6 A6). The extension lifts consumer LTV but the model is never underwritten on consumer revenue. If no institutional buyer contracts, kill criterion K1 fires.
3. **The wearable dependency is non fatal because no V1 marker needs it** (Phase 2). This is HIGH confidence and load bearing; it is what makes the wearable API revocation risk (R7) an engineered LOW rather than a naive SEVERE.
4. **Self report is the correct posture over affect inference** (Phase 2 section 2.3). HIGH confidence across multiple 2024 to 2025 sources; the own design mood scale is the safe v1 default.
5. **The enforced safety layer can be made deterministic at acceptable latency** (Phase 3 section 5; risk register OQ3). This is a ship blocker if it cannot; it is the K2 kill criterion.
6. **Cost and timeline point estimates (engineer cost, ~50 engineering months, ~12 month content floor, 1.2x AI multiplier) are founder facing estimates**, not measured actuals (Phase 4). The structural conclusions are robust to error in them because the content floor binds the G4 date regardless.

## Confidence Summary

Overall confidence: HIGH on the strategic recommendation and the structural conclusions, LOW to MEDIUM on the absolute financials.

Strongest (HIGH), and multiply confirmed across phases and primary sources: the defensible center is the warning sign safety layer, which needs no wearable and no inference and addresses the leading preventable maternal deaths (Phase 1, primary CDC/MMRC/ACOG); self report beats affect inference (Phase 2, multiple RCTs); the wearable dependency is non fatal (Phase 1, Phase 2); the churn cliff makes DTC LTV to CAC at or below 1.0 and the fundable business is B2B to payers, employers, and OB practices (Phase 5, Phase 6, and the comparable venture pattern where every scaled company sells B2B and every DTC play stayed small, pivoted, or died); the policy tailwind (Medicaid postpartum extension, Core Set mood measures, TMaH) gives the payer a budget rationale (Phase 5, HIGH primary gov sources); the non dilutive plan mechanics and the IMPROVE maternal funding line (Phase 6, HIGH).

Weakest (LOW to MEDIUM), and the reason the G4 pilot exists: the per episode contract prices and scenario revenue lines rest on inferred ranges because real B2B contract values are undisclosed (Phase 5 and Phase 6, the recurring unknown); the ~$35M to $45M capital to breakeven is triangulated from the Babyscripts comparable and scenario burn, not a bottom up financing model; the mid and large headcount and burn are planning estimates; the engaged partner haircut and precise first birth count are derived, not read from primary tables. None of these weaknesses reverses the recommendation. The decision to fund the ~$1.6M build to G4 is robust because the G4 pilot is precisely what converts the LOW confidence financial assumptions into measured evidence, and the decisive kill criterion (K1: no institutional buyer contracts by G4) is a clean, pre committed test of the one thesis the whole business rests on.
