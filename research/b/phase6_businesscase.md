# CONCEPT B, PHASE 6: BUSINESS CASE AND CAPITAL

Governed by `00_framework.md` (section 4 cost conventions, section 5 evidence rules, section 6 output contract). Builds on and does not re derive: Phase 5 (`phase5_market.md`, sizing, churn cliff, LTV, channels), Phase 4 (`phase4_devplan.md`, burn, headcount, timeline, comparables), Phase 2 (`phase2_data_inputs.md`, wearable non dependency, Model 1 lab ingest, content and clinical review opex), Phase 3 (`phase3_architecture.md`, pure cloud SaaS, rules engine plus narrating model, consent spine), and the shared files `shared_capital_landscape.md`, `shared_infra_cost.md`, and `regulatory_risk_register.md`. All access dates 2026-07-10. Only capital plan specifics (recent early stage maternal and family health deals, named NIH maternal funding lines) were newly researched this phase; everything else is inherited.

## Thesis, stated first

Three inherited facts govern this business case and every number below serves them.

1. **The churn cliff kills the DTC pregnancy subscription and reorders every channel** (Phase 5, section 2). A pregnancy only consumer product amortizes acquisition over roughly five paying months and then loses 100 percent of subscribers at birth. LTV is approximately $47, below plausible CAC of $30 to $100. The postpartum and early childhood extension lifts LTV to approximately $75 (base) or $120 to $130 (high), a 1.6x to 2.8x improvement, but does not by itself clear paid acquisition. DTC is an acquisition and engagement surface, not the revenue model.

2. **The fundable business is a B2B clinical services or enablement play sold to payers, employers, and OB practices** (Phase 4 section 6, Phase 5 sections 3 to 5). Every scaled or exited comparable (Maven, Pomelo, Progyny, Carrot, Cleo, Ovia post acquisition, Babyscripts) sells to an institution. Every DTC or community first play stayed small (Peanut), pivoted to survive (Bloomlife), or died (Oath Care). In a B2B channel the "subscription" is a per covered member contract, so the consumer leaving at birth does not terminate revenue, and in Medicaid the postpartum year is precisely the covered, measured, funded window the buyer wants engaged.

3. **This is a capital intensive, multi year healthcare business, not a quick consumer flip.** Company breakeven requires reaching tens of thousands of covered pregnancies across multiple contracted payers and employers, which the comparables reached on cumulative capital of roughly $37M (Babyscripts, enablement) to $171M or more (Pomelo, value based delivery). The build to G4 is cheap (~$1.6M, Phase 4); the path from G4 to breakeven is where the capital goes.

---

## 1. THREE SCALE SCENARIOS

Scenarios are defined per framework section 4 by covered pregnancy volume: small (hundreds), mid (thousands), large (tens of thousands). The unit is an **engaged maternity episode**: one pregnancy served for approximately seven antepartum months plus up to twelve postpartum months. All three scenarios model the **recommended enablement plus engagement model** (app as instrument, provider or plan holds the billing and clinical relationship, per Phase 5 section 5.1). A value based clinical delivery variant (Pomelo style, carrying care managers and doulas as delivered cost) is noted where it changes the shape.

Every revenue per episode figure is a model estimate anchored to the Phase 5 channel table (employer approximately $150 blended annual value per covered pregnancy; Medicaid managed episode $200 to $600; OB RPM approximately $300 per monitored pregnancy). These are marked LOW confidence. Burn and headcount extend the Phase 4 recommended configuration (3 engineers, content lead, retained clinical reviewer, ~$87,300 per month steady state to G4).

### 1.1 The churn cliff, carried explicitly into each scenario

| Channel context | How the birth cliff behaves | Net effect on the scenario |
|---|---|---|
| DTC consumer (all scenarios, top of funnel only) | 100 percent terminal churn at birth unless extended; base extension holds ~35 percent across the cliff (65 percent transition churn), then 12 percent monthly infant, 8 percent monthly toddler (Phase 5 section 2.2) | Consumer LTV ~$47 to $75, below CAC. Consumer revenue is not underwritten in any scenario P&L; DTC funds engagement, not the model |
| B2B payer or employer contract (the revenue engine) | The contract is priced per covered member or per episode. The individual's exit at birth does not end the contract. In Medicaid the 12 month postpartum extension (48 states plus DC) makes the postpartum year the covered, funded window (Phase 5 section 4.1) | The cliff is absorbed by the buyer relationship. Revenue is a function of covered lives contracted, not of consumer re subscription |
| OB practice per patient (RPM on ramp) | Provider relationship persists across a continuous flow of patients; each patient episode is finite but the practice contract is not | Cliff is irrelevant at the contract level; per episode economics only |

The strategic consequence, stated plainly: the churn cliff is not a reason the business fails, it is the reason the business must be B2B. Every scenario below prices the covered pregnancy to an institution, not the subscription to a consumer.

### 1.2 Scenario P&L shape, burn, headcount, capital, breakeven

| Line | Small (hundreds) | Mid (thousands) | Large (tens of thousands) |
|---|---|---|---|
| Stage mapping | G4 pilot to early G5 | G5 limited commercial | G6 full commercial |
| Engaged maternity episodes (annual) | ~300 to 500 | ~5,000 | ~50,000 (~1.4 percent of US births, well below Pomelo's ~7 percent) |
| Buyers under contract | 1 to 2 design partners (one OB group or one employer or one MCO pilot) | ~5 to 10 (employers plus 1 to 2 Medicaid MCO or commercial plan contracts) | ~15 to 40 (multiple MCO and employer contracts) |
| Blended net revenue per engaged episode | ~$100 to $250 (pilot pricing, much unpaid) | ~$300 | ~$400 |
| **Annual revenue** | **~$50K to $250K** | **~$1.5M** | **~$20M** |
| Infra COGS per user per month (`shared_infra_cost.md` section 7) | $7 to $19 (fixed overhead dominates) | $1.50 to $4.50 | $1.00 to $3.00 |
| Annual infra COGS | ~$40K to $90K | ~$180K | ~$1.2M |
| Content licensing (ACOG or AAP at V2) plus clinical review allocation | in opex (free corpus V1) | ~$0.3M to $0.6M | ~$1.5M to $3M |
| Gross margin (enablement model) | n/m (pre scale) | ~70 percent | ~75 to 80 percent |
| Headcount (FTE plus retained) | ~6 to 8 | ~14 to 18 | ~45 to 65 |
| Headcount composition | 3 eng, content lead, retained OB reviewer, 1 to 2 founders on product and BD, fractional design and QA | + 2 to 3 eng, 2nd content hire, pediatric and lactation reviewers, 2 to 3 payer and employer BD, 1 to 2 clinical ops or CS, retained compliance counsel | + payer sales team, clinical ops or care navigation, data and analytics, regulatory and privacy, G&A |
| **Annual burn (opex, loaded)** | **~$1.5M to $1.8M** | **~$3.5M to $5M** | **~$14M to $18M** |
| EBITDA | ~ negative $1.5M | ~ negative $2.5M to $3.7M | ~ breakeven to slightly positive |
| **Cumulative capital required to reach and sustain the stage** | **~$3M to $4M** | **~$12M to $20M** | **~$35M to $45M** |
| **Months to company breakeven** | None at this scale (structurally sub scale) | Not yet; contribution positive per contract, company EBITDA negative | **~60 to 84 months from founding** (breakeven achieved at this scale) |

### 1.3 Reading the scenarios

- **Small is a proof stage, not a business.** At hundreds of episodes the P&L is dominated by fixed platform overhead ($7 to $19 per user per month, `shared_infra_cost.md`) and by the load bearing non engineering roles (content lead, clinical reviewer) that cannot be removed (Phase 4 section 1.2). Revenue is immaterial and largely unpaid pilot work. The purpose of this stage is the G4 evidence package, not margin.
- **Mid proves the contract economics but still burns.** At ~5,000 episodes the per episode contribution can turn positive (revenue ~$300 against infra ~$36 per episode per year and a clinical review allocation), but company level EBITDA is negative because the payer and employer sales motion (6 to 24 month cycles, Phase 5 section 4) and the clinical and content operation must be funded ahead of revenue. This is the Series A burn zone.
- **Large is where breakeven lives.** Company breakeven requires roughly 50,000 engaged episodes, which requires multiple concurrent payer and employer contracts and a real payer sales organization. At ~$20M revenue and ~75 to 80 percent gross margin the enablement model reaches EBITDA breakeven with ~$14M to $18M opex. This is consistent with Babyscripts reaching ~200,000 cumulative pregnancies across 30 states on ~$37M total raised (Phase 5, `shared_capital_landscape.md`).
- **The value based delivery variant changes the shape, not the conclusion.** If the company bills value based maternity care directly (Pomelo model) rather than enabling a provider, revenue per episode rises (Medicaid episodes $200 to $600, plus shared savings) but gross margin falls to ~40 to 55 percent as clinical delivery staff (care managers, doulas, lactation) become delivered cost, headcount at large scale exceeds 100, and cumulative capital to breakeven rises toward the $100M+ range Pomelo raised. Higher revenue, lower margin, more capital, same requirement to reach tens of thousands of covered lives.

**Recommended scenario: the enablement plus engagement B2B model scaled to the large tier, reaching EBITDA breakeven at ~50,000 engaged episodes on ~$35M to $45M cumulative capital over ~6 years.** This is the lower capital, higher margin path and the one the leanest successful comparable (Babyscripts) validates.

---

## 2. PRICING MODELS MODELED

Five models, each modeled with its buyer, unit, illustrative economics, exposure to the churn cliff, and verdict. Illustrative PEPM and PMPM figures are model estimates marked LOW; the Phase 5 finding that actual Maven, Ovia, and Pomelo contract values are undisclosed still holds (Phase 5 Open Question 5).

### 2.1 Consumer monthly

| Attribute | Value |
|---|---|
| Buyer | The pregnant or postpartum consumer |
| Unit and price | Subscription, ~$12 per month (Phase 5 section 2.2, anchored between Flo ~$40 per year and Big Little Feelings $99 one time) |
| Gross margin | ~75 percent (digital, net of inference, content, clinical review allocation, processing, support) |
| LTV | ~$47 pregnancy only; ~$75 base extension; ~$120 to $130 high extension (Phase 5 section 2) |
| CAC | ~$30 to $100+ per acquired subscriber (Phase 5 section 4) |
| LTV to CAC | Below 1.0 (pregnancy only) to ~1.5 (high extension against a $50 CAC) |
| Churn cliff exposure | Full. 100 percent terminal at birth unless extended |
| Verdict | **Not a standalone business.** Use as top of funnel and engagement surface only. Never underwrite the model on it |

### 2.2 Consumer bundle with a wearable

| Attribute | Value |
|---|---|
| Buyer | The consumer, one time hardware plus subscription |
| Unit and price | Device $199 to $399 (Owlet, Nanit comparables, Phase 5 section 3.4) plus app subscription |
| Gross margin | 20 to 40 percent on hardware; ~75 percent on the software attach (Phase 5 section 4) |
| Churn cliff exposure | Full consumer churn compounds with hardware margin give up |
| Cautionary precedent | Elvie (Chiaro) raised $186M+ over 12 years, never profitable, entered administration March 2025, assets bought by Willow (Phase 4 section 6.2). Hardware plus DTC femtech burns capital |
| Verdict | **Weak.** Hardware margins and consumer churn compound. Wearable data is a V2 enhancement, not a revenue model, and Phase 2 established no V1 marker needs it. Do not build the business around a device |

### 2.3 PMPM to a payer (the recommended revenue engine)

| Attribute | Value |
|---|---|
| Buyer | Medicaid managed care organization or commercial health plan |
| Unit | Per member per month across an attributed pregnant and postpartum panel, or a per episode case rate |
| Illustrative economics | Medicaid managed maternity episode ~$200 to $600 (Phase 5 section 1.2, MEDIUM); alternatively a PMPM on attributed members. Value based contracts add shared savings on reduced preterm birth, NICU days, and ER use (Pomelo structure) |
| Sales cycle and contract size | 12 to 24+ months; seven to eight figures over a large member panel (Phase 5 section 4) |
| Churn cliff exposure | Absorbed entirely by the buyer. Medicaid's 12 month postpartum extension makes the cliff the covered window |
| Policy tailwind | CMS Transforming Maternal Health (TMaH) model, 15 states, 2025 to 2034, up to $17M per state, explicit behavioral health and value based payment mandate; NCQA PND-E and PDS-E depression screening measures in the 2024 Medicaid Core Set (Phase 5 section 4.1) |
| Verdict | **Strongest on budget and mission alignment; slowest to close.** This is the winning model. Medicaid finances ~41 percent of US births and grades plans on exactly the postpartum and mood surfaces this product touches |

### 2.4 PEPM to an employer

| Attribute | Value |
|---|---|
| Buyer | Self insured employer, via a benefits platform or broker |
| Unit | Per employee per month across all eligible employees, not only pregnant ones |
| Illustrative economics | Point solution PEPM is typically low single dollars; illustratively ~$1.50 PEPM across 50,000 employees is ~$900K per year, of which ~3 to 4 percent become pregnant annually (~1,500 to 2,000 episodes), implying ~$450 to $600 realized per served pregnancy. LOW confidence, illustrative bridge only |
| Sales cycle and contract size | 6 to 18 months; six to seven figures per large employer (Phase 5 section 4) |
| Churn cliff exposure | Absorbed by the buyer; the employer pays per eligible employee regardless of individual churn |
| Comparable | The route Maven, Carrot, Cleo, Progyny all took (Phase 4 section 6.1) |
| Verdict | **Strong.** Faster to close than a plan, buyer has a retention and productivity rationale and a budget. The natural first paid B2B channel |

### 2.5 Per patient to an OB practice (the reimbursement on ramp)

| Attribute | Value |
|---|---|
| Buyer | OB practice or health system; the provider then bills RPM |
| Unit and price | Per pregnancy license to the practice; ~$300 per monitored pregnancy (Phase 5 section 1.2) |
| Reimbursement mechanism | Provider bills RPM: CPT 99453, 99454, 99457, 99458, approximately $102 to $142 per patient per month combined at Medicare national rates, medically necessary for hypertensive disorders of pregnancy and gestational diabetes (Phase 5 section 5) |
| Sales cycle and contract size | 3 to 9 months; per pregnancy license (Phase 5 section 4) |
| Churn cliff exposure | Irrelevant at the contract level; the practice sees a continuous patient flow |
| Comparable | Babyscripts (~$37M raised, ~200,000 pregnancies, 30 states) |
| Verdict | **Best reimbursement on ramp and fastest B2B cycle.** Converts the wellness app into a billable service without the company becoming the biller (the app is the instrument, the OB is the biller, Phase 5 section 5.1). The right first design partner channel and the right tester recruiting channel (Phase 4 section 7.2) |

### 2.6 Pricing verdict

**Lead with per patient to an OB practice for the fastest paid pilot and reimbursement proof, convert to PEPM employer contracts for the first scalable recurring revenue, and build toward PMPM Medicaid managed care as the largest and most defensible pool.** Consumer monthly and the wearable bundle are engagement and acquisition surfaces only and are never the revenue model. This sequence matches the channel CAC and cycle ranking in Phase 5 section 4 and the comparable venture pattern in Phase 4 section 6.

---

## 3. CAPITAL PLAN

Non dilutive first, per the concept brief. The plan pairs NIH and NICHD maternal funding lines against the gate map (section 4) and then layers angel, pre seed, and seed dilutive capital, with actual recent deals as thesis evidence.

### 3.1 Non dilutive, by name (lead)

Inherited from `shared_capital_landscape.md` section 1.3 and extended with this phase's research on the named IMPROVE maternal funding line.

| Program | Vehicle and name | Award ceiling | Thesis fit to this product | Confidence | Source |
|---|---|---|---|---|---|
| NIH NICHD SBIR-STTR | R43/R41 (Phase I), R44/R42 (Phase II) | Phase I ~$256,580; Phase II ~$1,710,531 (NIH statutory guideline; NOFO specific) | Direct maternal, infant, pregnancy, and child health mandate | HIGH (mechanics), MEDIUM (per NOFO cap) | NICHD SBIR-STTR types page (`shared_capital_landscape.md` 1.3) |
| NIH IMPROVE Initiative | Implementing a Maternal health and PRegnancy Outcomes Vision for Everyone; co led by NICHD, NIH OD, and ORWH; multi institute | Draft FY2026 budget adds ~$20M to IMPROVE; awards flow through SBIR-STTR NOSIs and the mechanisms above | Explicitly funds technologies, tools, devices, and interventions that predict or indicate increased risk for maternal morbidity and mortality (MMM), including AI and ML tools measuring blood pressure, heart rate, and maternal or fetal physiology. This is the exact surface of the warning sign and BP monitoring product | HIGH | NICHD IMPROVE pages; ORWH; NIH news (this phase) |
| NIH SBIR maternal NOSIs (IMPROVE) | NOT-EB-21-001 (Innovative Diagnostic Technology for Improving Outcomes for Maternal Health); NOT-EB-23-005 (Innovative Tools and Technologies for Improving Outcomes for Maternal Health); NIBIB led, cross institute | Uses standard SBIR-STTR caps | Named, recurring small business channel targeting AI and ML tools that identify, phenotype, and stratify patients at greater risk of MMM. Both NOSIs are expired but establish a recurring, re issued funding line to track for the current cycle | HIGH (existence), MEDIUM (current re issue status) | NIH Guide NOT-EB-21-001, NOT-EB-23-005 (this phase) |
| NSF SBIR-STTR (26-510) | Phase I / Phase II | Phase I $305,000; Phase II $1,250,000 | Funds the sensing, retrieval, and AI engineering layer; will not fund clinical efficacy, which suits the general wellness positioning | HIGH | NSF 26-510 (`shared_capital_landscape.md` 1.4) |

Timing gate carried from `shared_capital_landscape.md` section 1.1: SBIR-STTR authority lapsed 2025-10-01, reportedly reauthorized 2026-04-13, NOFOs re released 2026-05-29, next NIH standard receipt date 2026-09-05. Confirm against SBA.gov and the NIH Guide before filing (Open Question). Eligibility caveat carried from the shared file: NIH review favors a health outcome hypothesis, so a pure wellness framing may score worse; frame the NICHD and IMPROVE applications around the maternal morbidity and mortality prediction and postpartum warning sign thesis (which is a health outcome), and reserve the pure wellness framing for NSF and for the commercial claims boundary.

**Non dilutive strategy:** file an IMPROVE aligned NICHD SBIR Phase I (~$256K) on the warning sign and postpartum risk surfacing engine at G2 to G3, and an NSF SBIR (~$305K) on the retrieval and rules engineering. Sequence a NICHD Phase II (~$1.71M) against the G4 pilot evidence. Non dilutive can plausibly cover ~$0.5M (two Phase I awards) early and ~$1.71M at Phase II, materially offsetting the ~$1.6M build to G4 and the mid stage burn, at the cost of the filing timeline and the outcome hypothesis framing.

### 3.2 Dilutive: angel, pre seed, seed, with actual recent deals as evidence

Funds and syndicate detail inherited from `shared_capital_landscape.md` section 2.2 and 4.2 (a16z Bio+Health, Stripes, TMV, Foreground Capital, USVP, ARTIS, Mayo Clinic, Tokio Marine Future, Springcoast, Rhia Ventures, Avestria, Portfolia; deals: Pomelo $92M Series C 2026-01, Delfina $17M Series A 2025-01, Millie $12M Series A 2025-02, Nanit $50M 2025-12, Maven $125M Series F 2024-10). This phase adds the **early stage (pre seed and seed) deals** that the shared file did not carry, which are the direct evidence for an angel, pre seed, and seed raise in this category.

| Company | What it does | Stage and amount | Lead or notable investor | Date | Why it is evidence for this concept | Confidence |
|---|---|---|---|---|---|---|
| Malama Health | Medicaid first maternal health; doula led continuous care pregnancy through the postpartum year; app for remote monitoring, care navigation, social support referrals | Seed, $9.2M | Acumen America | ~2026 (this phase) | Nearly the exact recommended model: Medicaid first, postpartum year, app enabled. A seed at $9.2M validates the payer channel and postpartum thesis at the stage this concept would raise | HIGH (deal), MEDIUM (exact date) |
| Flourish Care | Maternal healthcare platform scaling an in person and virtual doula network before, during, and after pregnancy | Seed, $5.7M | Undisclosed lead | 2026-03 | Recent seed for postpartum and full arc maternal support; confirms seed capital is flowing to the postpartum extension thesis | MEDIUM |
| Partum Health | Expands access to pregnancy and postpartum care services in the US | Seed, $3.1M | Undisclosed | recent (this phase) | Seed scale precedent for a pregnancy plus postpartum care platform | MEDIUM |
| Ruth Health | Pregnancy and postpartum support (telehealth) | ~$2.4M | Undisclosed | recent | Seed scale precedent, DTC plus B2B maternal support | MEDIUM |
| Wavelet Medical | Non invasive AI fetal brain (EEG) monitoring for labor and delivery | $7M | Undisclosed | 2026 | Maternal AI monitoring raising at seed to A; adjacent (device, intrapartum), less on point | MEDIUM |
| Matresa | AI powered preventative maternal health platform (clinical expertise plus behavioral science plus AI) | Pre seed, GBP 315K | Undisclosed | 2026 (this phase) | A pre seed benchmark for an AI maternal companion nearly identical in concept; sets the pre seed check size for this exact product shape | MEDIUM |

Category signal (this phase, corroborating Phase 5 and the shared file): femtech funding was ~$724M in 2025 with ~$239M in the first half of 2026; seed rounds were ~52 percent of deals but only ~9 percent of disclosed capital, and North America captured ~93 percent of capital. Money concentrates in companies with clinical, regulatory, or care delivery validation, and in the payer and care delivery models, not in DTC content. The Medicaid first seed (Malama, $9.2M) is the single most on thesis recent datapoint.

**Named investors most likely to fit this concept's pre seed and seed** (from the shared file and this phase): Acumen America (Medicaid first maternal, direct fit), Foreground Capital and TMV (women's health, Millie), Rhia Ventures and Avestria Ventures (women's and reproductive health thesis funds), USVP and Mayo Clinic and Tokio Marine (maternal outcomes and payer alignment, Delfina), a16z Bio+Health (Pomelo, scale). Accelerators: Cedars-Sinai Accelerator+ (women's and maternal cohort) and Techstars Healthcare (payer and provider sponsors are the exact buyers), per `shared_capital_landscape.md` section 3.

### 3.3 Capital plan against the gates

| Round | Timing (gate) | Size | Source mix | What it funds |
|---|---|---|---|---|
| Angel / pre seed | G0 to G2 | ~$0.5M to $1.5M | Angels plus NICHD SBIR Phase I (~$256K) plus NSF SBIR (~$305K); pre seed benchmark Matresa GBP 315K | Founder validated daily loop, safety layer, first content build |
| Seed | G3 to G4 | ~$3M to $9M (Malama $9.2M, Flourish $5.7M, Partum $3.1M as the observed band) | Seed funds (Acumen America, Foreground, TMV, Rhia, Avestria) plus NICHD SBIR Phase II (~$1.71M) | Consent system, pilot cohort, first paid OB or employer design partner, G4 evidence package |
| Series A | Post G4 / early G5 | ~$12M to $20M (Delfina $17M, Millie $12M band) | USVP, Mayo, Tokio Marine, a16z class | Payer and employer sales motion, mid tier scale to ~5,000 episodes |
| Series B+ | G5 to G6 | ~$20M to $90M+ | Growth (Stripes, a16z) | Scale to tens of thousands of episodes and company breakeven |

Cumulative dilutive plus non dilutive to breakeven in the recommended enablement scenario: **~$35M to $45M over ~6 years.** The value based delivery variant requires ~$100M+ (Pomelo reference).

---

## 4. MILESTONE TO UNLOCK MAP PER GATE

Gate definitions and cumulative burn per Phase 4 section 3.4. For each gate: what it proves, who cares, the conversation it opens, and what it is worth.

| Gate | Approx month / cumulative burn | What it proves | Who cares | Conversation it opens | What it is worth |
|---|---|---|---|---|---|
| G1 Bench (~month 3, ~$0.22M) | The grounded RAG answers with citations, the red flag classifier passes its unit tests with zero missed red flags, the rules engine computes a daily brief. The safety spine is technically real | Angels; NSF and NICHD SBIR reviewers | Pre seed angel round; NSF SBIR on the sensing and AI engineering; NICHD IMPROVE SBIR on the MMM risk surfacing engine | Unlocks ~$0.5M to $1.5M pre seed plus non dilutive; de risks the single most dangerous technical claim (the enforced safety layer) |
| G2 Self test (~month 7, ~$0.60M) | Founder runs the full daily loop for 30 days; the safety layer false positive behavior is characterized in real use; the two 30 second surfaces are worth opening | Pre seed and seed investors | Seed conversations begin on a working, dogfooded product; NICHD SBIR Phase I submission | Converts a deck into a demo; supports the seed narrative and the Phase I award (~$256K) |
| G3 Friends and family (~month 12, ~$1.05M) | 5 to 15 real users; the dual user consent system works and is enforced server side; retention measured across a stage transition; failure modes cataloged; the partner surface works with a real partner | Seed investors; the first OB or employer design partner | Seed round close; the first paid design partner pilot (OB practice per patient, the fastest cycle); NICHD SBIR Phase II submission | Unlocks the ~$3M to $9M seed (Malama, Flourish, Partum band) and the Phase II (~$1.71M); proves the consent differentiator |
| G4 Pilot (~month 19, ~$1.6M) | 50 to 200 user cohort with a design partner; efficacy signal (warning sign engagement, mood trend surfacing, escalation events); unit economics measured; churn cliff quantified in the field | Payers, employers, OB groups; Series A investors | The institutional buyer conversation (PEPM employer, PMPM Medicaid MCO, per patient OB) and the Series A; a TMaH state or a Medicaid MCO on the postpartum quality measures | The gate that unlocks the entire B2B thesis and the Series A (~$12M to $20M). Efficacy on a payer quality measure (PPC, PND-E, PDS-E) is what gives the buyer a budget rationale |
| G5 Limited commercial (mid scenario) | Positive contribution margin per covered episode; a repeatable payer or employer sale; the reimbursement structure (app as instrument, provider or plan bills) works in production | Growth investors; expansion payers | Multi contract expansion; Series A extension or Series B | Proves the unit economics the large scenario compounds; supports ~$20M+ growth capital |
| G6 Full commercial (large scenario) | Target CAC and LTV achieved at the contract level; tens of thousands of covered episodes; EBITDA breakeven | Growth and strategic acquirers (a lab like Labcorp bought Ovia; a plan or Maven class consolidator) | Scale financing or strategic exit | Company breakeven and the exit optionality the comparables realized (Ovia acquisition, Progyny IPO) |

---

## 5. RISK REGISTER

Cross references `regulatory_risk_register.md` (risk IDs R1 to R9). This section scores the five risks the concept brief names for Phase 6, in business case terms: likelihood, impact, mitigation, and leading indicator. Scoring convention matches the regulatory register (likelihood over the first 36 months of commercial operation absent the mitigation; impact on the worst credible outcome).

| Risk | Cross ref | Likelihood | Impact | Mitigation (business and product) | Leading indicator |
|---|---|---|---|---|---|
| Wearable API dependency (a vendor can revoke access and end the company) | R7 | HIGH (as a naive dependency); LOW (as engineered) | SEVERE if depended on | **Already de risked by architecture.** Phase 2 established no V1 marker needs wearable data; the product ships V1 with zero wearable integration and treats derived wearable scalars as an optional V2 enhancement behind a swappable data access layer. The core defensible value (self report plus warning sign education plus BP from a cleared cuff) runs with no wearable at all. Support at least two device ecosystems (HealthKit and Health Connect) when V2 wearables ship | Any vendor deprecation notice or terms change restricting commercial use; the legacy Fitbit Web API turndown September 2026 as the template event (R7, S14) |
| Content licensing | R8 | MEDIUM | HIGH | V1 grounding corpus is built entirely on free public domain government content (CDC Hear Her, Learn the Signs, WHO and CDC growth charts, USDA, NIH ODS) plus original clinically reviewed copy, carrying zero license cost (Phase 2 section 2.4). ACOG and AAP depth is a deliberate, costed V2 line ($0.3M to $0.6M mid, $1.5M to $3M large, section 1.2). Never embed a proprietary screening instrument (ASQ-3, a Brookes trademark) as a scored result; license explicitly and present as an educational self check routed to the provider if used | A cease and desist from an instrument publisher; a licensor changing terms; clinical review determining ACOG must be quoted rather than paraphrased in V1, pulling licensing cost forward |
| Reproductive health data legal risk | R5 | HIGH | SEVERE | Data minimization and short retention as architecture (Phase 3 section 6): reproductive sensitive fields held client side encrypted so a warrant to the company yields least plaintext; never share health data with advertising or analytics third parties (the Flo and GoodRx trigger); published law enforcement request policy; treat every partner facing disclosure (the consent spine) as a reproductive data disclosure. This is mostly design discipline and cheap relative to the exposure | Any FTC or state AG action against a femtech app for data sharing; a subpoena received; a state expanding reproductive data liability; MHMDA class filings expanding (R5, S9 to S12) |
| Clinical liability (failure to escalate, and any output that delays care) | R3, R9 | MEDIUM | SEVERE | Never position detection as a safety guarantee. Hard coded red flag escalation layer, enforced and logged, independent of the LLM, that cannot reassure against an enumerated ACOG or CDC warning sign; enforced refusal on danger assessment questions; surfaced disclaimers that the product is not a monitored medical alarm; every escalation event logged and reviewed by the retained clinical reviewer; product liability insurance at G5; marketing claim matched to the validated false negative rate to preserve the causation defense | Any G3 or G4 transcript where the assistant reassured against a red flag; a user reported delayed care incident; a plaintiff bar advertisement targeting a competitor (R3, R9, S6) |
| The churn cliff | Phase 5 section 2 (business risk, not in the regulatory register) | HIGH (for DTC); LOW (for the recommended B2B model) | SEVERE for a DTC only model | Do not build a DTC only business. Price the covered pregnancy to an institution (PMPM, PEPM, per patient OB) so the individual's exit at birth does not terminate revenue; build the postpartum and early childhood extension to lift consumer LTV 1.6x to 2.8x and to serve the funded Medicaid postpartum year; use consumer subscription strictly as an acquisition and engagement surface | DTC LTV to CAC persistently below 1.0 in the pilot; postpartum transition churn worse than the 65 percent modeled; inability to sign a B2B design partner (this is also the top kill criterion, section 6) |

Portfolio note: R1 (FDA reclassification) and R2 (FTC substantiation) from the regulatory register also apply and are controlled by the general wellness positioning and the input versus inference discipline (framework section 2). They are not re scored here because Phase 6 is a business case; they land as validation cost lines (R2) and a claims linter engineering line (R1) in the dev plan, and are carried in `regulatory_risk_register.md`.

---

## 6. KILL CRITERIA

Stated in advance, per the concept brief. Each is a pre committed decision rule, not a discretionary judgment. If a criterion is met and the stated remediation window closes without recovery, stop.

| # | Kill criterion | Why it is fatal | Gate to test it | Remediation window |
|---|---|---|---|---|
| K1 (top) | **No institutional buyer will contract for a paid pilot on per covered pregnancy economics by the end of G4 (~month 24).** If the only willing buyer is the consumer, the business is DTC only, and DTC only is structurally unprofitable against the churn cliff (LTV ~$47 to $75 vs CAC $30 to $100) | The entire fundable thesis (Phase 4 section 6, Phase 5) is that the buyer is a payer, employer, or OB group. No B2B buyer means no business | G4 | One additional pilot cycle in a different B2B channel (OB to employer to plan). If still no paid contract, kill |
| K2 | **The enforced safety layer cannot hold in production**: any G3 or G4 evidence that the red flag escalation layer reassures against an enumerated warning sign, or that danger assessment refusal cannot be enforced at acceptable latency | This is the highest severity failure mode (R3, R9). A delayed care event is existential legally and reputationally, and it is the reason the product exists (the warning sign layer, Phase 1) | G2 to G4 | Non negotiable. Ship blocker at G1 to G2. If it cannot be enforced deterministically, the product cannot ship |
| K3 | **A reproductive data legal event materializes and cannot be contained**: an FTC or state AG action, or a subpoena that the architecture cannot minimize, that makes the data liability uninsurable or uncontractable with payers | Reproductive data is subpoena and warrant exposed post Dobbs (R5). A payer will not contract with an uncontainable data liability | G4 to G5 | Architecture remediation (client side encryption, retention deletion). If payers still will not contract, kill the payer thesis |
| K4 | **Efficacy fails to move a payer quality measure at G4.** The pilot cohort shows no credible signal on postpartum follow up (PPC), depression screening and follow up (PND-E, PDS-E), or an equivalent measure the buyer is graded on | Without a measure the buyer is graded on moving, the payer has no budget rationale and the PMPM thesis collapses to a nice to have (Phase 5 section 4.1) | G4 | Re target the measure or the population (higher risk, higher signal cohort). If no measure moves, the value based and payer thesis is dead |
| K5 | **Cumulative capital to G4 exceeds ~$3M with no line of sight to a design partner, or content and clinical review slip past ~18 months with no path to the corpus.** The content critical path is the binding constraint (Phase 4 section 4); if it cannot be built and cleared, there is nothing safe to ship | The business cannot reach the G4 evidence gate that unlocks everything downstream | G3 to G4 | Second content hire to break the floor (Phase 4 section 3.3). If the corpus still cannot be built and cleared, kill |

---

## Register Entries

Per framework section 9. Staged for the register keepers; this phase does not edit `research/registers/`.

### funding.md (append)

Early stage maternal and family health deals as pre seed and seed thesis evidence (this phase, extending `shared_capital_landscape.md` section 4.2 which carried the later stage rounds):

| Company | Stage / amount | Investor | Date | Thesis fit | Confidence |
|---|---|---|---|---|---|
| Malama Health | Seed $9.2M | Acumen America | ~2026 | Medicaid first, doula led, postpartum year, app enabled; the on thesis datapoint | HIGH (deal), MEDIUM (date) |
| Flourish Care | Seed $5.7M | Undisclosed | 2026-03 | Full arc doula network, in person plus virtual | MEDIUM |
| Partum Health | Seed $3.1M | Undisclosed | recent | Pregnancy plus postpartum care access | MEDIUM |
| Ruth Health | ~$2.4M | Undisclosed | recent | Pregnancy and postpartum telehealth support | MEDIUM |
| Wavelet Medical | $7M | Undisclosed | 2026 | AI fetal brain monitoring (adjacent, device) | MEDIUM |
| Matresa | Pre seed GBP 315K | Undisclosed | 2026 | AI preventative maternal companion; near identical concept; pre seed benchmark | MEDIUM |

Non dilutive line added this phase: NIH IMPROVE Initiative (NICHD, NIH OD, ORWH co led), SBIR-STTR NOSIs NOT-EB-21-001 and NOT-EB-23-005 (Small Business Initiatives for Innovative Diagnostic Technology / Tools and Technologies for Improving Outcomes for Maternal Health), funding AI and ML tools that predict or indicate MMM risk; draft FY2026 budget +$20M to IMPROVE. Named investors with maternal or Medicaid thesis fit for this raise: Acumen America, Foreground Capital, TMV, Rhia Ventures, Avestria Ventures, USVP, Mayo Clinic, Tokio Marine Future.

### sources.md (append)

| Source | Org | URL | Pub / accessed | Used for | Credibility |
|---|---|---|---|---|---|
| IMPROVE Initiative (about) | NICHD / NIH | nichd.nih.gov/research/supported/IMPROVE | accessed 2026-07-10 | IMPROVE co leads, scope, SBIR-STTR funding of MMM prediction tools | HIGH (primary gov) |
| NIH launches IMPROVE Initiative | NIH ORWH | orwh.od.nih.gov/in-the-spotlight/all-articles/nih-launches-improve-initiative-prevent-maternal-morbidity-and | accessed 2026-07-10 | IMPROVE launch, causes of maternal mortality targeted | HIGH (primary gov) |
| NOSI: Small Business Initiatives for Innovative Diagnostic Technology for Maternal Health | NIH Guide | grants.nih.gov/grants/guide/notice-files/NOT-EB-21-001.html | accessed 2026-07-10 | Named SBIR maternal NOSI; AI/ML tools measuring BP, HR, maternal/fetal physiology | HIGH (primary gov) |
| NOSI: Innovative Tools and Technologies for Improving Outcomes for Maternal Health | NIH Guide | grants.nih.gov/grants/guide/notice-files/NOT-EB-23-005.html | accessed 2026-07-10 | Named SBIR maternal NOSI (successor) | HIGH (primary gov) |
| Senate Committee Advances Maternal Health Initiatives FY2026 | ACOG | acog.org/news/news-articles/2025/08/senate-committee-advances-maternal-health-initiatives-and-health-research-funding-for-fiscal-year-2026 | 2025-08, accessed 2026-07-10 | Draft FY2026 +$20M IMPROVE, +$20M NICHD | MEDIUM (advocacy org on primary budget) |
| Malama Health $9.2M seed | TAMradar / MedCity News | tamradar.com/funding-rounds/malama-health-seed-9-2m ; medcitynews.com | 2026, accessed 2026-07-10 | Medicaid first maternal seed, Acumen America | MEDIUM (trade) |
| Flourish Care $5.7M seed | MedCity News | medcitynews.com/2026/03/flourish-care-doula-seed-funding/ | 2026-03, accessed 2026-07-10 | Doula network seed | MEDIUM (trade; fetch 403, from search snippet) |
| Partum Health $3.1M seed | Femtech Insider | femtechinsider.com/partum-health-seed-round-investment/ | accessed 2026-07-10 | Pregnancy and postpartum care seed | MEDIUM (trade) |
| Ruth Health $2.4M | MobiHealthNews | mobihealthnews.com/news/ruth-health-scores-24m-pregnancy-postpartum-support | accessed 2026-07-10 | Pregnancy and postpartum support raise | MEDIUM (trade) |
| Matresa GBP 315K pre seed | Femtech Insider | femtechinsider.com/matresa-raises-315k-pre-seed-to-build-ai-powered-maternal-health-platform/ | 2026, accessed 2026-07-10 | AI maternal companion pre seed benchmark | MEDIUM (trade) |
| Femtech funding 2025-2026 analysis | New Market Pitch | newmarketpitch.com/blogs/news/femtech-funding-analysis | accessed 2026-07-10 | ~$724M 2025, ~$239M H1 2026, seed ~52 percent of deals ~9 percent of capital, NA ~93 percent | LOW to MEDIUM (curated) |

---

## Open Questions

1. **Actual PEPM and PMPM contract values** realized by Maven, Ovia, and Pomelo remain undisclosed (inherited Phase 5 Open Question 5). The pricing model economics in section 2 are illustrative bridges anchored to the Phase 5 per episode ranges, not to observed contract prices. This is the largest single unknown in the revenue model.
2. **Blended net revenue per engaged episode** ($100 to $250 small, $300 mid, $400 large) is a model estimate, not an observed price. A 2x error moves the breakeven scale and the capital to breakeven materially.
3. **Current re issue status of the IMPROVE SBIR NOSIs** (NOT-EB-21-001 and NOT-EB-23-005 are both expired). The recurring maternal small business line clearly exists; the specific active NOFO for the 2026-09-05 cycle must be read before filing.
4. **SBIR-STTR reauthorization timeline** (2026-04-13 reauth, 2026-05-29 NOFO release, 2026-09-05 receipt) is single source from the NIA page (inherited `shared_capital_landscape.md` Open Question 1). Confirm against SBA.gov and the NIH Guide.
5. **Malama Health seed exact date and full syndicate**, and Flourish, Partum, Ruth, and Matresa lead investors and dates, were taken from search snippets (several primary trade URLs returned 403 to automated fetch). Confirm before citing in a fundraising deck.
6. **Aggregator per user lab ingest price** (Model 1) still UNKNOWN (inherited Phase 2 and Phase 4). Affects per episode COGS at the margin, not the scenario conclusions.
7. **ACOG and AAP license fees** still quote based and UNKNOWN (inherited Phase 2 Open Question 4). The V2 content licensing lines ($0.3M to $3M) are order of magnitude estimates.
8. **Cumulative capital to breakeven** (~$35M to $45M enablement) is triangulated from the Babyscripts total raised (~$37M) and the scenario burn, not from a bottom up financing model. The value based variant figure (~$100M+) is anchored to Pomelo. Both are directional.

## Assumptions Made

1. **The recommended model is B2B enablement plus engagement, not value based clinical delivery.** This is the lower capital, higher margin path (Babyscripts reference). If the company must deliver clinical care directly to bill (Pomelo path), gross margin falls to ~40 to 55 percent, headcount at scale exceeds 100, and capital to breakeven rises toward $100M+. Impact if wrong: the capital plan roughly triples.
2. **Scenario revenue per episode and the resulting revenue lines are model estimates** anchored to Phase 5 channel ranges. Flagged LOW. Impact: breakeven scale and capital to breakeven scale inversely with the realized price.
3. **Burn and headcount extend the Phase 4 recommended configuration** (3 engineers, content lead, retained clinical reviewer, ~$87,300 per month to G4) into mid and large stages by adding BD, clinical ops, and G&A. The mid and large headcount and burn are planning estimates, not a staffing model. Impact: linear on burn.
4. **Breakeven at ~50,000 engaged episodes (~1.4 percent of US births)** assumes the enablement gross margin (~75 to 80 percent) and ~$14M to $18M opex hold. If S&M for payer sales runs heavier (long cycles, Phase 5), breakeven pushes to a higher episode count and later month.
5. **Non dilutive can offset ~$0.5M early and ~$1.71M at Phase II** assumes the NICHD and IMPROVE applications score despite the general wellness positioning, framed on the MMM prediction and postpartum warning sign outcome hypothesis. If NIH scores the wellness framing poorly (inherited shared file Open Question 3), non dilutive shrinks and dilutive need rises.
6. **The churn cliff is neutralized by the B2B channel, not solved at the consumer level.** The extension lifts consumer LTV but the model is never underwritten on consumer revenue. Impact if wrong (if no B2B buyer contracts): kill criterion K1 fires.
7. **Recent early stage deal figures** (Malama, Flourish, Partum, Ruth, Matresa) are from trade press and search snippets; several primary URLs returned 403. Treated as directional evidence of the seed and pre seed band, not as audited figures.

## Confidence Summary

Overall confidence: HIGH on the structural conclusions, LOW to MEDIUM on the absolute scenario financials.

Strongest (HIGH): the strategic spine, which is inherited and multiply confirmed. DTC pregnancy only cannot cover its acquisition cost against the churn cliff; the fundable business is B2B to payers, employers, and OB practices; the winning pricing model is PMPM to a Medicaid managed care plan (with per patient OB as the fastest on ramp and PEPM employer as the first scalable recurring revenue); breakeven requires reaching tens of thousands of covered episodes. The non dilutive plan is HIGH on mechanics (NICHD SBIR caps, the named IMPROVE maternal funding line and its SBIR NOSIs targeting exactly this product's risk surfacing surface). The early stage deal evidence is HIGH on the headline datapoint (Malama, Medicaid first maternal, $9.2M seed) and the pre seed benchmark (Matresa).

Weakest (LOW to MEDIUM): the scenario revenue lines and the per episode prices, which rest on the Phase 5 channel ranges rather than observed contract values (the recurring unknown across Phases 5 and 6); the mid and large headcount and burn, which are planning estimates; and the ~$35M to $45M capital to breakeven, triangulated from a comparable (Babyscripts) and the scenario burn rather than a bottom up financing model. None of these weaknesses reverses the recommendation: build the B2B enablement model, lead the sale with the OB per patient and employer PEPM channels toward Medicaid PMPM, fund the ~$1.6M build to G4 with pre seed plus NICHD and IMPROVE SBIR non dilutive, and underwrite the ~$35M to $45M path to breakeven over ~6 years against the kill criteria in section 6, with K1 (no institutional buyer by G4) as the decisive gate.
