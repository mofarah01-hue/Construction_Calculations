# PORTFOLIO DECISION

## Concept A (Elder Home Monitoring) and Concept B (Pregnancy and Parenting Companion)

Governed by `00_framework.md`. Run after both concept business cases exist (`research/a/CONCEPT_A_BUSINESS_CASE.md`, `research/b/CONCEPT_B_BUSINESS_CASE.md`). This is the top of house decision document. Every figure is traceable to a concept phase; no new number is introduced. Where a reuse ratio is a synthesis estimate rather than a phase output, it is flagged as such in Assumptions Made. Prepared 2026-07-10.

---

# PART 1: THE DECISION, STATED FIRST

**Sequence them. Build Concept B first. Concept A second, inheriting B's entire software spine.**

Neither concept is dead: each cleared its own conditional kill gate and each independently earned a "fund to G4" recommendation at a near identical price (Concept A ~$1.8M to $2.0M, Phase 6 2.5; Concept B ~$1.6M, Phase 4 3.3). Building both concurrently is rejected: each needs $30M to $45M and 5 to 7 years to reach breakeven on its own (Concept A Phase 8 1.1; Concept B Phase 6 1.2), so running them in parallel doubles the capital and the team against two unrelated critical paths, one of them a hardware program. The framework's own execution discipline (one phase per session, no more than three agents, never build around an implausible pitch) is the same posture at the portfolio level: do the lower risk, faster, cheaper one first, harden the shared brain as working software, then carry it into the harder one.

The decisive reason B goes first: **B's dominant kill risk is commercial and cleanly testable at a 19 month, $1.6M G4 pilot (K1, will an institution contract). A's dominant kill risk is technical, capital bound, and calendar bound (K1, the field false positive rate, which cannot be resolved by planning and which the category has never cleared to a fundable pilot in under roughly 6 years).** B also rides a dated policy tailwind that gives its buyer a budget line today. Sequencing costs A almost nothing, because A's true critical path is its edge sensing and certification work, which no amount of prior software buys down, while B pre builds and production hardens the exact interpretation, consent, safety, claims, and privacy layers A would otherwise build cold.

---

# PART 2: WHAT IS GENUINELY SHARED

The framework asserted the two concepts are one underlying system: passive multimodal sensing, a fusion layer, a language model interpretation layer, delivered into a care context (framework section 8). The business cases confirm that the **software brain is genuinely common and the sensing body is not.** Five things carry across; one large thing does not.

## 2.1 The five shared foundations

| Shared foundation | What carries across | Where it lives | Evidence in both cases |
|---|---|---|---|
| Grounded AI interpretation layer | The same decision: cloud API over on device, Claude Haiku 4.5 for the presentation majority reserving a higher tier for complex turns, corpus constrained RAG so no health fact ships without a citable passage, cache and batch economics, ~$0.50 to $1.50 per user per month, inference dominant, retrieval overhead immaterial | `shared_llm_layer.md`; Concept B Phase 3 section 2; Concept A Phase 4 assistant, "under $1/resident/month" | B Phase 3 2.3; A Appendix A (assistant LLM under $1/resident/mo, Phase 4 3.4.3) |
| Sensing and fusion discipline: rules engine, model narrates | Every clinical, safety, and personalization decision is deterministic code; the model phrases a resolved decision and is never asked what the data means. The evidence rich backbone runs on deterministic state machines and classical statistics, not neural inference | Concept B Phase 3 section 3; Concept A Phase 4 (ADL, spatial, sleep, circadian layer on deterministic state machines, zero neural inference) | B Phase 3 3.1 to 3.4; A Phase 4 3.2 |
| Consent and dual user architecture | The buyer and the data subject are different people with divergent interests, so a role and capacity model with server side enforcement, not a single owner account, and covert operation is not a configuration. B: mother is resource owner, partner sees scoped revocable grants (UMA semantics), enforced at the data delivery boundary. A: resident is the data subject, caregiver is the buyer, role and capacity model, no covert mode | Concept B Phase 3 section 4; Concept A Phase 5 section 3 | B Phase 3 4.1 to 4.4; A business case 2.6 |
| Enforced safety and escalation layer | A deterministic red flag classifier that runs before the model and cannot be jailbroken, hard coded escalation, immutable audit logging, disclaimer surfaced by the shell not the model. "Not a prompt, an enforced layer" is the identical phrase in both | Concept B Phase 3 section 5; Concept A Phase 4 (fall duration gating and escalation state machine, the two hard cannot buy safety items) | B Phase 3 5.1 to 5.3; A business case 2.5 |
| Wellness claims discipline, regulatory dossier, and risk register | One claims boundary (self report is not a claim, measurement plus reference is not a claim, named disease inference is a claim), one claims linter in CI blocking disease inference from passive data, one `regulatory_precedent_dossier.md`, and one `regulatory_risk_register.md` scoring both concepts R1 to R9 | framework section 2; `regulatory_precedent_dossier.md`; `regulatory_risk_register.md` | Register R1 to R9 is authored once for A and B; A business case 2.1, B business case 2.1 |

Two further common substrates sit underneath these: the privacy and security baselines (AES 256 at rest, TLS 1.3, KMS envelope encryption, per user keys, MHMDA as the binding state constraint, `shared_privacy_security.md`), and the non dilutive capital playbook (NSF SBIR plus NIH SBIR, NIA for A and NICHD for B, `shared_capital_landscape.md`). Both are written once and serve both concepts.

## 2.2 The one large thing that does not carry across

| Not shared | Concept A owns it | Concept B owns it |
|---|---|---|
| The sensing body and its critical path | An entire edge hardware program: mmWave radar, PIR and door mesh, under mattress bed mat, one oblique on sensor inference camera (IMX500), embedded computer vision, the fall and long lie classifier, duration gating, the field false positive characterization effort, hardware BOM, NRE $80K to $210K, triple UL/ETL certification, and manufacturing (Phase 2, Phase 3, Phase 6) | An entire content and clinical operation: the obstetric and pediatric corpus, a retained OB-GYN reviewer and a full time content lead as permanent operating cost, FHIR and TEFCA lab ingest, the gestational clock, and a rolling stage stratified tester cohort (Phase 2, Phase 4) |

This is the heart of the portfolio finding. What is common is the cloud brain. What is unique is exactly the part that dominates each concept's cost, risk, and calendar. A's un shareable half is a capital intensive, calendar bound hardware and false positive program. B's un shareable half is a content and clinical review operation that is not code at all.

## 2.3 Quantified reuse

No phase computed a single reuse percentage, so the ratios below are synthesis estimates built from the sourced engineering breakdowns (Concept A ~355 raw engineer weeks across three disciplines to G4, Phase 6 1.1; Concept B content and clinical review, not code, is the binding G4 constraint, Phase 4 thesis). They are flagged as estimates in Assumptions Made, not presented as findings.

| Reuse lens | Estimate | Reasoning from the sourced breakdowns |
|---|---|---|
| Shared software as a share of the second build's engineering | High, roughly half of the pure software effort | The grounded LLM layer, corpus constrained RAG, the rules engine pattern, the consent and role model, the enforced safety layer, the claims linter, the privacy plumbing, the cloud backend, and the notification stack are common. In B these are the bulk of the code; in A they are the backend and assistant third of the three discipline build |
| Shared software as a share of Concept A's total build | Lower, roughly a fifth to a quarter | A's total build is dominated by the non shared edge stack, embedded CV, and the false positive characterization program (Phase 2, Phase 4, Phase 6). The shared brain is real but small against A's hardware and certification mass |
| Shared software as a share of Concept B's total path | Moderate, roughly a quarter to a third | B's binding constraint is the ~12 month clinically reviewed content floor and the OB reviewer, which are non code and non shared (Phase 4 section 4). The shared brain is a larger share of B's code but a smaller share of B's gated path |
| Documents reused verbatim, near 100 percent | The regulatory dossier and the R1 to R9 risk register | Authored once for both concepts by design (framework section 2; `regulatory_risk_register.md`) |

The load bearing reading: reuse is high on the interpretation, consent, safety, claims, and privacy layers and near zero on each concept's dominant cost driver. That asymmetry is the entire argument for sequencing over parallel, and for ordering by which concept's non shared half is the cheaper and faster to clear.

---

# PART 3: HEAD TO HEAD COMPARISON

All figures carried from the two business cases. Ranges are the cases' own ranges.

| Dimension | Concept A (Elder Home Monitoring) | Concept B (Pregnancy and Parenting Companion) | Edge |
|---|---|---|---|
| Capital to first revenue (paying design partner at G4) | ~$1.8M to $2.0M all in to G4 (Phase 6 2.5) | ~$1.6M to G4 (Phase 4 3.3) | B, modestly |
| Time to first revenue | ~27 engineering months at 3 engineers, but comparables adjusted elapsed to a fundable G4 is 3 to 4 years, and category history shows nobody reached a fundable pilot in under ~6 years (Phase 6 2.4, 4.1) | ~19 months to G4 at 3 engineers, content gated not code gated (Phase 4 3.2) | B, clearly |
| Regulatory exposure | FTC gait substantiation is a hard measurement cost (instrumented walkway study, K4, $30K to $80K estimated); state biometric and home video is the most regulated data category (BIPA/CUBI/MHMDA, R4 HIGH SEVERE); two party consent audio (R6); reimbursement structurally foreclosed by the wellness lane (the central tension, Phase 7 4.2) | Reproductive health data post Dobbs is subpoena exposed, HIPAA Reproductive Health Rule vacated (Purl v. HHS 2025-06-18, R5 HIGH SEVERE); failure to escalate a 3am symptom is the highest severity path (R3/R9); FTC exposure is lighter because self report needs no accuracy substantiation; no ambient audio (R6 N/A) | Different, not lesser. A carries a hard FTC measurement cost and reimbursement foreclosure; B carries reproductive data legal risk and life safety. B avoids the gait substantiation line and the audio wiretap line |
| Defensibility | Higher technical moat if K1 is solved: real world false positive reduction is hard and calendar bound, on sensor inference is a hardware privacy property competitors cannot assert, the hazard inventory is RCT backed and uncontested. Category funding is hot and dated: Sage $65M, Inspiren $100M, SafelyYou $43M, Nobi EUR 35M (Phase 8 3.2) | Softer technical moat (RAG plus rules is replicable) but real via the consent and dual user architecture ("the moat no competitor serves"), clinically reviewed content plus OB reviewer, and payer contracts tied to Medicaid quality measures. On thesis capital is dated: Malama Health $9.2M seed, Babyscripts ~200K pregnancies on ~$37M (Phase 6 3.2) | A on raw technical defensibility if it works; B on time to a defensible buyer relationship and policy fit |
| Founder fit | UNKNOWN. Demands embedded CV, mmWave radar, and hardware plus certification competence, and a senior living operator or home care agency sales motion | UNKNOWN. Demands clinical content operations, an OB-GYN clinical partnership, consumer mobile product, and payer, employer, and OB practice enterprise sales | Cannot call without the founder profile. See Open Questions |
| Market size | DTC SAM ~2.0M households, ~$840M/yr ceiling, DTC mature ARR only $40M to $80M (not venture scale on DTC). Real market is operator per bed: ~1.2M senior living beds across ~1,000 concentrated operators; breakeven at ~18K to 28K beds; large scenario ~$18.6M ARR (Phase 7 1.1 to 1.3, Phase 8 1.1) | US births ~3.63M/yr, first births ~1.4M, serviceable ~800K/yr. Medicaid finances ~41 percent of births; large scenario ~50,000 engaged episodes (~1.4 percent of births) at ~$20M revenue, 75 to 80 percent margin; policy tailwind (48 states 12 month postpartum extension, Core Set mood measures, TMaH up to $17M/state x 15 states) (Phase 5 1, 4.1; Phase 6 1.2) | Comparable magnitude. Both reach ~$18M to $20M at large scale and both need $30M to $45M to breakeven. B has a clearer near term payer budget rationale |

Two facts jump off the table. First, the two businesses converge on strikingly similar destinations: ~$18M to $20M revenue at large scale, $30M to $45M capital to breakeven, and both are B2B channel businesses that structurally reject DTC (A: operators, agencies, payers; B: payers, employers, OB practices). Second, they diverge sharply on the shape of the risk to get there. A's risk is front loaded, technical, and capital bound. B's risk is a single clean commercial test.

---

# PART 4: THE RECOMMENDATION AND THE EVIDENCE

## 4.1 Why sequence, not build both, not kill one

- **Not kill one.** Both cleared their conditional kill gates and both earned an independent fund to G4 at ~$1.6M to $2.0M. Nothing in either case supports abandonment. The bulb is dead inside Concept A, but Concept A itself (the reshaped mesh) survives.
- **Not both.** Each requires $30M to $45M and 5 to 7 years to breakeven on non overlapping critical paths, one of them a hardware and certification program. Parallel execution doubles capital and splits a team across an edge sensing problem and a clinical content problem that share only their cloud brain. The shared half is real but is not enough to make two concurrent companies one company.
- **Sequence.** Build the shared brain once, as production software, inside the concept that is faster, cheaper, and lower risk to a paying partner, then carry it into the harder concept.

## 4.2 Why Concept B goes first

| Reason | Evidence |
|---|---|
| Faster and cheaper to a paying design partner | ~19 months and ~$1.6M to G4 (B Phase 4 3.2, 3.3) versus ~27 engineering months, a 3 to 4 year comparables adjusted elapsed, and ~$1.8M to $2.0M for A (A Phase 6 2.4, 2.5, 4.1) |
| Its dominant kill risk is commercial and cleanly testable, not a multi year technical grind | B K1 (no institutional buyer contracts by G4) is exactly what the $1.6M pilot resolves (B Phase 6 6). A K1 (field false positive rate) cannot be resolved by planning, only characterized at G2, and the category has never reached a fundable pilot in under ~6 years (A Phase 6 4, Phase 8 B10) |
| Lower technical risk across the board | No hardware, no NRE, no certification, no manufacturing; the wearable dependency is already engineered out (no V1 marker needs it); self report beats affect inference; the V1 corpus is free public domain (B Phase 2, Phase 3) |
| A dated policy tailwind gives the buyer a budget line now | Medicaid finances ~41 percent of US births, 48 states plus DC extended postpartum coverage to 12 months, the 2024 Core Set added postpartum depression measures, and TMaH funds 15 states up to $17M each (B Phase 5 4.1, HIGH primary government sources) |
| Going first, B builds and hardens the exact shared spine A later inherits | The grounded LLM layer, the rules engine pattern, the consent and role model, the enforced safety layer, the claims linter, the regulatory dossier and risk register, and the privacy and cloud backend are all first delivered in B (Part 2) |

The counter case for A first is honest and narrow: A's category funding is hotter right now (four dated large checks in 18 months) and its technical moat is higher if K1 is solved. But hot funding does not buy down a false positive rate that only real homes and calendar time can characterize, and a higher moat conditional on the single hardest, least controllable risk in either portfolio is not a reason to take that risk first with the company's first dollars.

## 4.3 What Concept A inherits when it goes second

| Inherited from B, production hardened | Still built fresh for A, un shareable |
|---|---|
| The grounded LLM interpretation and assistant layer (RAG, corpus constraint, Haiku tier economics, cache and batch) | The entire edge sensing stack: mmWave radar, PIR and door mesh, bed mat, oblique IMX500 camera |
| The dual user consent architecture (role and capacity, server side enforcement, scoped revocable grants), which is A's resident versus caregiver model | Embedded computer vision, the fall and long lie classifier, and duration gating |
| The enforced safety and escalation layer (deterministic red flag classifier, immutable logging), which is A's red flag escalation layer | The field false positive characterization program (K1), which is calendar bound in real homes |
| The claims discipline and the claims linter in CI, plus the shared `regulatory_precedent_dossier.md` and `regulatory_risk_register.md`, authored once | Hardware BOM, NRE $80K to $210K, triple UL/ETL certification, and manufacturing |
| The privacy and security baselines, KMS posture, cloud backend plumbing, and notification stack | The FTC gait substantiation study against an instrumented walkway |
| The B2B enterprise sales motion and the NSF plus NIH non dilutive playbook, run once | The senior living operator and home care agency channel |

The inheritance is exactly the software brain and nothing of the sensing body, which is the correct division: A's hard, expensive, un shareable work is untouched by going second, so sequencing costs A little on its true critical path while removing the cost and risk of building the entire interpretation, consent, safety, and claims stack cold. The one fixed cost paid once and inherited regardless of order is the regulatory dossier and the claims linter, which alone argues for sequencing over any parallel build.

## 4.4 The one condition that would flip the order

Founder fit is UNKNOWN and it is the single input that could reverse this. If the founder is a hardware, embedded vision, or sensor engineer with an existing senior living or home care channel, A first is defensible on fit despite the higher technical and capital risk, because a founder cannot execute B's clinical content and payer motion on a hardware background any more than the reverse. This must be asked before the order is locked. On every dimension that does not depend on the founder, B first is the call.

---

## Open Questions

1. **Founder profile and channel access are UNKNOWN and are the only input that could flip the sequence order** (Part 4.4). A hardware and senior living founder argues A first; a clinical content and payer founder argues B first. Ask before locking the order.
2. **Whether a single team can carry the shared spine from B into A without a full re platform** is untested. The reuse is asserted at the pattern level (role and capacity model, enforced safety layer, RAG); the concrete B implementation was built for a pure cloud SaaS with a client side encrypted tier (B Phase 3), whereas A runs a T4 hybrid with a T1 on device fall path (A Phase 2 1.3). The cloud brain transfers; the edge integration seam is new work.
3. **Concept A's primary kill risk (K1, field false positive rate) remains UNKNOWN and unresolvable by planning** (A Phase 2 OQ2, Phase 4 OQ1). It is the reason A is the harder, later concept and it does not improve by sequencing.
4. **Concept B's revenue model rests on undisclosed B2B contract prices** (B Phase 5 OQ5, Phase 6 OQ1), the largest single unknown in B and precisely what its G4 pilot must resolve.
5. **The reuse ratios in Part 2.3 are synthesis estimates, not phase outputs.** No phase computed a portfolio reuse percentage. See Assumptions Made.
6. **Both concepts still carry the same unresolved shared item: SBIR/STTR reauthorization timing** (lapsed 2025-10-01, reportedly reauthorized 2026-04-13, single source), which gates the non dilutive runway either concept leads with (`shared_capital_landscape.md`; A Phase 8 OQ5; B Phase 6 OQ3).

## Assumptions Made

1. **The reuse percentages in Part 2.3 are my estimates, derived from the sourced engineering breakdowns (A ~355 engineer weeks across three disciplines to G4; B content and clinical review gated, not code gated), not figures any phase produced.** They are directional (high on the shared software, low against A's total hardware heavy build, near 100 percent on the two shared regulatory documents). If wrong, the qualitative conclusion (reuse is concentrated in the cloud brain and absent from each sensing body) is robust because it rests on the architecture of the two builds, not on the exact ratio.
2. **"First revenue" is taken as the first paying design partner at G4** in both cases, consistent with each brief's G4 definition. Full commercial revenue and breakeven are far later and are quoted separately ($30M to $45M, 5 to 7 years, both cases).
3. **Neither concept's absolute financials are underwritten here.** They are carried at each case's stated confidence (MEDIUM on scenario magnitudes, LOW on the flagged UNKNOWNs: A's PERS churn, per bed price, and real DTC CAC; B's undisclosed B2B contract prices). The sequence decision does not depend on resolving them, because it rests on the risk shape (B commercial and testable, A technical and calendar bound), not on the point estimates.
4. **Founder fit is treated as neutral to slightly favoring B** for the base recommendation, with the explicit override in Part 4.4 if the founder profile is hardware and senior living. This is the one assumption that carries decision weight and it is flagged as UNKNOWN.
5. **Building both concurrently is rejected on capital and focus grounds** ($30M to $45M each to breakeven, non overlapping critical paths). If external capital and two distinct teams were assured, parallel is a different question; on the evidence in these cases it is not the top of house call.

## Confidence Summary

Overall confidence: HIGH on the structural conclusions, MEDIUM on the reuse ratios, and gated by one UNKNOWN (founder fit).

- **HIGHEST confidence:** the shared value is the cloud interpretation, consent, safety, claims, and privacy brain, and it is common; each concept's dominant cost, risk, and calendar lives in its non shared sensing body (A's edge hardware and false positive program, B's content and clinical operation). This rests directly on the two architecture phases and both business cases.
- **HIGH confidence:** sequence rather than build both or kill one; and B first on every dimension that does not depend on the founder, because B is faster and cheaper to a paying partner (~19 months, ~$1.6M), its kill risk is a clean commercial test, its technology is largely de risked, and it rides a dated policy tailwind, while A's kill risk is technical, capital bound, and historically the slowest gate in its category.
- **MEDIUM confidence:** the reuse ratios (synthesis estimates, Part 2.3), and the assumption that B's cloud implementation transfers into A's T4 hybrid without a re platform at the edge seam.
- **WEAKEST and decision relevant (UNKNOWN):** founder fit, the single input that could reverse the order (Part 4.4). Resolve it before the sequence is locked.

The load bearing conclusion, robust to the weak cells: sequence the portfolio, build Concept B first because it is the lower risk, faster, cheaper path to a paying partner and it hardens the exact software spine Concept A inherits, then build Concept A second, where its hard and un shareable edge sensing and certification work is untouched by having gone second and its interpretation, consent, safety, and claims layers arrive already built.
