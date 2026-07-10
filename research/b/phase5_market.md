# Concept B, Phase 5: Market, Competition, and Channel

Governed by `00_framework.md`. Bottom up sizing is primary. Analyst TAM is a secondary check only. Every material number carries source, URL, date, and confidence. Date of research: 2026-07-10. No prior Concept B phase outputs existed at the time of this phase, so nothing is inherited from earlier phases.

The controlling fact of this phase: a pregnancy subscription has a hard, dated churn cliff at birth. That single fact invalidates the direct to consumer pregnancy only business and reorders every channel. The rest of this document quantifies that.

---

## 1. BOTTOM UP SIZING

### 1.1 The funnel, step by step

| Step | Population | Value | Basis | Confidence |
|------|-----------|-------|-------|-----------|
| A | US annual births, 2024 final | 3,628,934 | CDC NVSR final 2024 | HIGH |
| A' | US annual births, 2023 final | 3,596,017 | CDC NVSR final 2023 | HIGH |
| B | First births share | approx 38 to 39 percent | Derived from CDC first birth rate 21.4 per 1,000 women 15 to 44, 2023, applied to approx 65.4M US women 15 to 44 gives approx 1.40M first births against 3.60M total | MEDIUM |
| C | First births, count | approx 1,400,000 per year | Derived, step B | MEDIUM |
| D | First births with an engaged co-parenting partner | approx 65 to 75 percent of C, approx 910,000 to 1,050,000 | Approx 77 percent of first births in the US occur to women who are married or cohabiting at the time of birth per NCHS nonmarital birth data; "engaged enough to open a partner app daily" is a stricter filter, so haircut to the lower band | LOW |
| E | Digitally reachable and smartphone-first, first-time expectant households | approx 85 percent of D | Near universal smartphone ownership among adults under 40 | MEDIUM |
| F | Serviceable first-time-parent households per year | approx 775,000 to 890,000 | D x E | LOW |

The natural annual customer intake ceiling for a first-time-parent product with a partner surface is roughly 800,000 US households per year. Every household enters and exits the pregnancy window inside a single year. This is not a stock of 800,000. It is a flow that fully refreshes annually and, for a pregnancy only product, fully exits at birth.

### 1.2 Reachable subset per channel, and the resulting SAM

SAM below is annual recurring revenue capturable at a plausible mid-term share, not the theoretical ceiling. Price and penetration are deliberately conservative and are defended in Sections 2, 4, and 7.

| Channel | Reachable first-time households per year | Realistic mid-term penetration of that pool | Effective annual revenue per acquired household | Annual SAM at that penetration | Confidence |
|---------|------------------------------------------|---------------------------------------------|-------------------------------------------------|-------------------------------|-----------|
| DTC subscription | approx 800,000 | 3 to 5 percent | approx $60 (see churn model, Section 2) | approx $1.4M to $2.4M | LOW |
| Employer benefit (PEPM) | approx 45 to 55 percent of births are commercially insured, first-time subset approx 350,000; reachable through benefits platforms approx 40 percent | 8 to 12 percent of reachable | approx $150 blended annual value per covered pregnancy | approx $17M to $25M | LOW |
| Health plan / Medicaid managed care (PMPM or case rate) | Medicaid finances approx 41 percent of births, first-time subset approx 575,000; commercial plans add reach | 5 to 10 percent of Medicaid first-time pregnancies | approx $200 to $600 per managed pregnancy episode | approx $60M to $170M | LOW |
| OB practice / health system (RPM enabled) | first-time pregnancies at contracted practices, approx 5 percent of births reachable early | 20 percent of contracted practice volume | approx $300 per monitored pregnancy (Section 5) | approx $10M to $20M | LOW |
| Retail / wearable bundle | attach to a wearable sale, low intent | under 2 percent | approx $40 | under $5M | LOW |

The bottom up read: the DTC pregnancy market measured as a standalone consumer subscription is a rounding error, on the order of one to a few million dollars of annual recurring revenue at realistic penetration and realistic price. The money is in the payer and employer channels, where a single contract covers thousands of pregnancies at a per-member price and the consumer churn cliff is absorbed by the buyer relationship rather than by the consumer's willingness to re-subscribe. This matches founder assumption B6 and confirms it.

### 1.3 Analyst TAM check (secondary only)

| Source | Market defined | 2024 size | Forecast | CAGR | Note |
|--------|----------------|-----------|----------|------|------|
| Grand View Research | Global femtech | $39.29B (2024) | $97.25B by 2030 | 16.37 percent | Broadest possible envelope, includes menopause, contraception, fertility, general women's health. Overstates the addressable slice for this product by an order of magnitude. |
| Acumen Research | Global femtech | not stated | $97.3B by 2030 | 16.3 percent | Corroborates the Grand View envelope. |
| Mordor Intelligence / Grand View | Pregnancy tracking and postpartum care apps (the actual category) | UNKNOWN precise 2024 dollar figure | growth to 2030/2031 | double digit | The correct category for this product. Precise dollar figure not captured; listed under Open Questions. |

The femtech TAM is a vanity number for this concept. The relevant analyst figure is the pregnancy and postpartum app category, which is a small fraction of femtech, and even that top-down figure is dominated by ad-supported content players (BabyCenter, What to Expect) and by employer or plan-contracted clinical services (Maven, Ovia), not by DTC pregnancy subscriptions. The bottom up finding stands: DTC is small, payer and employer channels are where budget exists.

---

## 2. THE CHURN CLIFF, MODELED

### 2.1 Why this is the whole question

A pregnancy has a maximum natural product life of roughly ten months, and in practice less, because acquisition happens after pregnancy confirmation (typically gestational week 6 to 10) and the terminal event, birth, is hard-dated and non-negotiable. A DTC pregnancy subscription therefore cannot amortize acquisition cost over years the way a normal SaaS or consumer subscription does. It has one bounded window and then a cliff at which every remaining subscriber exits at once.

Published category evidence for the cliff: new-mother churn is approximately 70 percent by week 4 postpartum, and the standard vendor countermeasure is to extend content into infant care and maternal recovery (Mordor Intelligence, pregnancy tracking and postpartum care apps market report). That number is the single most important retention statistic in this category.

### 2.2 Assumptions (stated, sourced, and flagged)

| Assumption | Value | Basis | Confidence |
|-----------|-------|-------|-----------|
| DTC price | $12.00 per month | Between Flo premium (approx $40 per year, approx $3.33 per month) and premium parenting course pricing (Big Little Feelings $99). A differentiated AI companion can command a premium over commodity trackers but not much. | MEDIUM |
| Gross margin | 75 percent | Digital subscription net of LLM inference, content licensing, clinical review allocation, payment processing, and support. Inference and clinical review are the material costs in this product. Founder assumption pending Phase 3/4 validation. | LOW |
| Acquisition point | gestational week 8, approx month 2 of a 9-month gestation | Pregnancy confirmation and app search behavior | MEDIUM |
| Active pregnancy window | approx 7 payable months | Week 8 to birth | MEDIUM |
| Monthly churn during pregnancy | 10 percent | Motivated but leaky; conservative | LOW |
| Terminal churn at birth, pregnancy-only product | 100 percent | Definitional cliff | HIGH |
| Postpartum transition churn, extended product | 65 percent at the birth event | Consistent with approx 70 percent by week 4 | MEDIUM |
| Postpartum/infant monthly churn (months 0 to 12 postpartum) | 12 percent | Higher than pregnancy; exhausted user | LOW |
| Toddler monthly churn (months 12 to 36 postpartum) | 8 percent | Survivor cohort, habit formed | LOW |

Expected paying months are computed as the sum of monthly survival probabilities (a subscriber pays in month t with probability equal to cumulative retention to t).

### 2.3 LTV, pregnancy only

Expected paying months, week 8 to birth, at 10 percent monthly churn across 7 months: sum of 0.90^t for t = 0 to 6 = approximately 5.2 months. Then 100 percent terminal churn.

LTV (contribution) = 5.2 months x $12 x 0.75 = **approximately $47 per acquired subscriber.**

### 2.4 LTV, with postpartum and early-childhood extension

| Phase | Retention logic | Expected incremental paying months per original subscriber |
|-------|-----------------|-----------------------------------------------------------|
| Pregnancy (week 8 to birth) | 0.90^t, 7 months | 5.2 |
| Birth transition | 35 percent survive the cliff (65 percent churn) | (multiplier applied below) |
| Postpartum / infant (0 to 12 mo) | 0.35 x sum of 0.88^t over 12 months | 2.3 |
| Toddler (12 to 36 mo) | survivors to month 12 (0.35 x 0.88^12 = 0.076) x sum of 0.92^t over 24 months | 0.8 |
| Total expected paying months | | 8.3 |

LTV (contribution), base extension case = 8.3 months x $12 x 0.75 = **approximately $75 per acquired subscriber.**

High case, if the product is engineered to own the postpartum window (payer-funded engagement, maternal warning-sign safety layer driving daily open rates, birth-transition churn held to 45 percent and infant monthly churn to 8 percent): expected paying months rise to approximately 13 to 14, giving LTV of **approximately $120 to $130.**

### 2.5 The delta, which is the strategic argument

| Scenario | Expected paying months | LTV (contribution) | Multiple vs pregnancy only |
|----------|------------------------|--------------------|----------------------------|
| Pregnancy only | 5.2 | approx $47 | 1.0x |
| With extension, base | 8.3 | approx $75 | 1.6x |
| With extension, high | 13 to 14 | approx $120 to $130 | 2.6x to 2.8x |

The extension raises DTC LTV by approximately $28 (base) to approximately $80 (high), a 1.6x to 2.8x lift. That is the quantified case for building postpartum and early childhood into v1 rather than bolting it on.

But the more consequential finding is what the numbers say against CAC. DTC health-app CAC runs approximately $30 to $100 per install and materially higher per paying subscriber. At an LTV of $47, pregnancy only is LTV to CAC below 1.0 and is structurally unprofitable. Even the base extension at $75 barely clears a $50 CAC and does not clear a blended paid-acquisition CAC. **The extension is necessary but not sufficient. It fixes the churn cliff's slope but not the fundamental problem that a consumer paying $12 a month for under a year cannot cover the cost to acquire her.** The channel has to change. See Section 4.

---

## 3. COMPETITION

Two distinct businesses wear the same "pregnancy app" label. Confusing them is the central strategic error this concept is exposed to.

### 3.1 Ad-supported content plays (monetize attention and data, not the user's wallet)

| Company | Model | Buyer | Price to user | Funding / ownership | Status | Confidence |
|---------|-------|-------|---------------|---------------------|--------|-----------|
| BabyCenter | Ad and data monetization, editorial + week-by-week content | Advertisers | Free | Owned by Everyday Health Group / Ziff Davis (acquired from J&J 2019) | Active, approx 100M monthly global reach, 7 in 10 US new/expectant mothers | HIGH |
| What to Expect | Ad-supported content and community | Advertisers | Free | Everyday Health Group / Ziff Davis | Active, sister brand to BabyCenter | HIGH |
| The Wonder Weeks | Paid content app, developmental "leaps" | Consumer | One-time / low-cost app | Twise Victory Publishing B.V. (private, no institutional funding found) | Active, content-only | MEDIUM |
| Big Little Feelings | DTC toddler-behavior video courses | Consumer | $99 ("Winning the Toddler Stage"), $79 ("Big Feelers") | Bootstrapped, no disclosed VC | Active, approx 400,000 course-takers, 3.5M Instagram | MEDIUM |

### 3.2 Consumer subscription / tracker plays (monetize the user's wallet, exposed to the churn cliff)

| Company | Model | Buyer | Price | Funding | Status | Confidence |
|---------|-------|-------|-------|---------|--------|-----------|
| Flo Health | Freemium cycle + pregnancy tracker, premium subscription | Consumer (plus emerging B2B) | approx $40 per year premium, approx $40 ARPU | $200M Series C (Jul 2024), $1B+ valuation, first pure-digital women's-health unicorn | Active, approx 70M MAU, approx 5M paid, >$200M gross bookings 2024 | HIGH |
| Peanut | Social network for women / mothers, ad + subscription | Consumer / advertisers | Freemium | approx $32M total raised | Active, approx 3.5M MAU | MEDIUM |
| Ovia Health (consumer side) | Fertility, pregnancy, parenting apps | Consumer, but real revenue is B2B (see 3.3) | Free consumer tier | Acquired by Labcorp 2021, approx $20M revenue at acquisition | Active under Labcorp | HIGH |

### 3.3 Clinical-services plays (monetize employers and health plans, not the churn cliff)

| Company | Model | Buyer | Price / basis | Funding | Status | Confidence |
|---------|-------|-------|---------------|---------|--------|-----------|
| Maven Clinic | Virtual women's and family health clinic, care navigation | Employers and health plans (PEPM / value-based) | Enterprise contract | $437M total, $125M Series F (Oct 2024), $1.7B valuation, approx $268M ARR | Active, category leader | HIGH |
| Ovia Health (enterprise) | Pregnancy/parenting apps sold as employer and health-plan benefit | Employers and health plans | Enterprise contract | Labcorp subsidiary | Active | HIGH |
| Progyny | Fertility and family-building benefits | Employers (self-insured) | PEPM / utilization | Public (Nasdaq PGNY), approx $1.17B revenue 2024, approx $1.46B market cap | Active, public | HIGH |
| Carrot Fertility | Fertility and family-building benefits | Employers and health plans | Enterprise contract | $115M total, $75M Series C | Active | HIGH |
| Cleo | Family and caregiving benefits (broader than maternity) | Employers | PEPM | $83M total, $40M Series C | Active | HIGH |
| Pomelo Care | Virtual value-based maternity and newborn care | Health plans (Medicaid and commercial) and employers | PMPM / value-based, shared savings | $92M Series C, $1.7B valuation (Jan 2026), approx $171M+ total | Active, approx 25M covered lives, approx 7 percent of US births, published outcomes | HIGH |
| Babyscripts | Remote pregnancy monitoring (BP, education) delivered through the OB | OB practices and health systems (who then bill RPM) | Per-pregnancy license to provider | approx $37M total, $19M Series B | Active, approx 200,000 pregnancies, 30 states | HIGH |
| Bloomlife | Prescription remote maternal/fetal monitoring device (pivoted from DTC contraction monitor) | Providers (B2B2C) | Device + service | $12.2M Series A (2024), FDA-cleared MFM-Pro | Active after B2B pivot; the DTC consumer version was shut down | HIGH |

### 3.4 Connected-hardware plays (device sale plus subscription; separate BOM and liability)

| Company | Model | Buyer | Price | Funding / status | Confidence |
|---------|-------|-------|-------|------------------|-----------|
| Owlet | Infant sock/monitor, wearable + app subscription | Consumer (some medical) | Hardware approx $199 to $399 + app | Public (NYSE OWLT), approx $74M to $77.5M revenue 2024, FDA-authorized product | HIGH |
| Nanit | AI baby monitor + subscription | Consumer | Hardware + subscription | approx $125M total raised, $50M growth round Dec 2025 | HIGH |
| Huckleberry | Infant sleep guidance app + subscription | Consumer | Subscription | $16M total raised, approx 1.2M families | HIGH |

### 3.5 Where this concept sits, and why that is dangerous

The concept as written straddles all three. It has the content ambition of BabyCenter, the tracker/subscription monetization of Flo, the clinical-companion positioning of Maven and Pomelo, and an optional wearable dependency like Owlet. Straddling is not a differentiator, it is an unfunded middle. The content plays give the same content away free and monetize ads. The subscription plays are the ones exposed to the churn cliff and are, with the sole exception of Flo (which reached scale on cycle tracking, not pregnancy), sub-scale or acquired. The businesses that reached durable value (Maven, Progyny, Carrot, Ovia-in-Labcorp, Pomelo) all sell to employers or plans. The concept must pick the clinical-services lane to have a fundable business, and must treat DTC as an acquisition and engagement surface, not the revenue model.

---

## 4. CHANNEL COMPARISON

Estimates. CAC, cycle, and margin figures are order-of-magnitude and flagged LOW to MEDIUM. They are directionally reliable and rank-order correctly even where the absolute figures are soft.

| Channel | CAC (per acquired pregnancy) | Sales cycle | Contract size | Gross margin | Exposure to churn cliff | Verdict |
|---------|------------------------------|-------------|---------------|--------------|-------------------------|---------|
| DTC subscription | $30 to $100+ | Instant | $47 to $130 LTV | approx 75 percent | Full. Every subscriber exits at birth unless extended | LTV to CAC below or near 1.0. Not a standalone business. Use as top of funnel only. |
| Employer benefit (PEPM) | High upfront sales and broker cost, amortized over thousands of employees; effective per-pregnancy CAC low | 6 to 18 months | Six to seven figures annual per large employer | 60 to 75 percent | Buyer absorbs it; the employer pays per eligible employee regardless of individual churn | Strong. Buyer has budget and a retention/productivity rationale. |
| Health plan / Medicaid managed care | Very high upfront (long procurement), very low per-member | 12 to 24+ months | Seven to eight figures; PMPM or case rate over a large member panel | 55 to 70 percent (clinical delivery cost) | Buyer absorbs it entirely | Strongest on budget and mission alignment; slowest to close. |
| OB practice / health system (RPM) | Moderate; sell to the practice, they enroll patients | 3 to 9 months | Per-pregnancy license; provider bills RPM | 55 to 70 percent | Provider relationship persists across patients | Best reimbursement on-ramp; converts wellness app into billable service. |
| Retail / wearable bundle | Low marketing, high channel/margin give-up | Retail cycle | Low per unit | 20 to 40 percent (hardware) | Full consumer churn | Weak. Hardware margins and consumer churn compound. |

### 4.1 The Medicaid and quality-measure argument (the buyer with a budget)

- Medicaid finances approximately 41 percent of US births (2023), and a higher share among the youngest and lowest-income mothers, who overlap heavily with first-time parents. A product that improves a maternal outcome a Medicaid plan is graded on has a funded buyer.
- CMS maintains a Maternity Core Set of quality measures for state Medicaid and CHIP agencies. Beginning with the 2024 Core Set, the Prenatal and Postpartum Care (PPC) measure reports both prenatal and postpartum rates, and NCQA's Prenatal Depression Screening and Follow-Up (PND-E) and Postpartum Depression Screening and Follow-Up (PDS-E) measures entered the Core Set as voluntary measures in 2024. These are exactly the surfaces this product touches: postpartum follow-up and mood screening/routing.
- CMS's Transforming Maternal Health (TMaH) Model selected 15 state Medicaid agencies in January 2025 for a 10-year (2025 to 2034) value-based maternity model, with up to $17M per state and an explicit mandate to integrate behavioral health and build value-based payment. This is a named, funded, multi-year buyer channel forming right now.
- 48 states plus DC have extended Medicaid postpartum coverage to 12 months (from 60 days). The postpartum year, which the concept correctly identifies as the unwatched high-risk window, is now a covered, measured, and funded period. This is the single most favorable policy tailwind for the extension thesis in Section 2.

The conclusion: the churn cliff is an argument for a payer or employer channel, because in those channels the "subscription" is a B2B contract priced per covered member. The consumer leaving at birth does not end the contract, and in Medicaid the postpartum year is now precisely where the buyer wants engagement.

---

## 5. REIMBURSEMENT AND COVERAGE

| Mechanism | Codes / vehicle | Billable by | What it requires | Relevance | Confidence |
|-----------|-----------------|-------------|------------------|-----------|-----------|
| Remote Physiologic Monitoring (RPM) | CPT 99453 (setup), 99454 (device supply, 16+ days), 99457 (first 20 min management), 99458 (each add'l 20 min) | Ordering clinician (OB) | A physiologic measurement device (e.g., a validated BP cuff), an established patient, and clinician time | Medically necessary and reimbursed for hypertensive disorders of pregnancy and gestational diabetes. Medicare national rates approx $46.50 (99454) + $48.14 (99457), approx $102 to $142 per patient per month combined. Medicaid coverage varies by state. | HIGH |
| Remote Therapeutic Monitoring (RTM) | CPT 98975 to 98981 | Broader set of practitioners | Non-physiologic therapeutic data (e.g., adherence, symptoms) | Fits self-report symptom and adherence data where no physiologic device exists | MEDIUM |
| Behavioral Health Integration / Collaborative Care (CoCM) | CPT 99492 to 99494, plus BHI codes | Treating clinician with a behavioral care manager and psychiatric consultant | A care-management workflow, not just an app | Direct fit for perinatal depression screening and follow-up, the exact Core Set measures above | MEDIUM |
| Postpartum coverage extension | Medicaid 12-month postpartum (48 states + DC) | n/a (coverage, not a code) | State plan amendment / waiver | Extends the funded window from 60 days to 12 months, aligning payer incentive with the postpartum extension product | HIGH |
| Value-based / case rate | TMaH APMs, plan-specific maternity bundles | Contracted provider or risk-bearing entity | Outcome accountability and data | The vehicle Pomelo uses; rewards measurable reduction in preterm birth, NICU days, ER use | MEDIUM |

### 5.1 The tension with wellness positioning (same problem as Concept A)

Everything reimbursable in the table above is a clinical service. RPM requires a physiologic measurement ordered by a clinician for a medical indication. CoCM requires treatment of a diagnosed behavioral health condition. The moment the product bills any of these codes, it is asserting a clinical function, and the general-wellness lane (framework Section 2) no longer shields it. The two postures cannot occupy the same SKU.

The resolvable architecture, to be validated in Phase 6:
- The consumer-facing app stays firmly in the wellness lane: measurement, trend, self-report, education, and hard-coded warning-sign escalation, making no claim.
- The billable clinical service is delivered by, or in partnership with, a licensed clinician or provider group (the OB practice, a telehealth network, or a risk-bearing entity like the plan), who orders the monitoring and bills the code. The app is the instrument, not the biller.
- This is exactly Babyscripts' structure (the app enables the OB to bill RPM) and Pomelo's structure (a clinical entity bills value-based care). It is the only way to hold both the wellness claim boundary and the reimbursement upside at once.

Naming the tension plainly: you cannot bill RPM and simultaneously claim you are not a medical service. Choose the entity that bills, keep the consumer app out of the claim, and contract between them.

---

## 6. PARTNERS

| Category | Candidates | Role | Notes |
|----------|-----------|------|-------|
| Wearable vendors | Oura, Whoop, Apple HealthKit, Garmin, Withings, Samsung, Fitbit/Google | Physiologic input | Raw-data access is the gating risk (founder assumption B2); resolve in Phase 2 before depending on any of them. |
| Validated BP devices | Omron, Withings (pregnancy-validated cuffs only) | Preeclampsia RPM device | Many consumer cuffs are not validated in pregnancy; device choice is reimbursement-relevant. |
| Lab / diagnostics | Labcorp (owns Ovia, a competitor), Quest | Lab ingestion (Model 1, ingest) | Labcorp is conflicted; Quest is the cleaner partner. |
| Health-data interoperability | Health Gorilla, Particle Health, 1up Health, patient-portal aggregators | Pull existing prenatal labs | Enables the cheap "ingest" model over the expensive "order" model. |
| Telehealth networks | Wheel, SteadyMD, and similar clinician networks | Provide the ordering/billing clinician for RPM and CoCM | Necessary to bill codes without becoming a provider directly. |
| Content licensors | ACOG, AAP, evidence-based nutrition sources | Grounded retrieval corpus | Content licensing and clinical review are recurring operating cost, not one-time. |
| Employer benefit platforms and brokers | Employer benefits marketplaces, brokers | Distribution to self-insured employers | The route Maven, Carrot, Cleo, Progyny all took. |
| Health plans / Medicaid MCOs | Medicaid managed care organizations, commercial plans | The buyer with a budget | TMaH's 15 states are a targeted list. |
| OB practice groups and health systems | Independent OB groups, IDNs | Enroll patients, bill RPM | Babyscripts' channel. |
| Doula and lactation networks | Certified doula and IBCLC networks | Human layer, engagement and trust | Differentiator; extends the postpartum surface. |

---

## 7. WILLINGNESS TO PAY AND PUBLISHED RETENTION DATA

### 7.1 Consumer spend context

- US first-year baby cost averages approximately $20,384 (BabyCenter, 2025), with childcare the largest line at approximately $14,802 per year (2024). The category spends, heavily, but overwhelmingly on childcare, gear, and feeding, not on information subscriptions.
- Prenatal, delivery, and postpartum medical care averages approximately $18,865, most of it insured. This is the pool a payer or employer is already spending, and the pool a value-based product redirects.

Implication for WTP: expectant parents spend enormously, but their information and companion needs are met free by BabyCenter and What to Expect, and cheaply by Flo. Consumer WTP for a pregnancy information subscription is therefore low and price-anchored to approximately $40 per year. Premium content (Big Little Feelings at $99, one-time) shows parents will pay for high-trust, high-specificity guidance, but as a one-time course, not a durable subscription.

### 7.2 Published price points (competitive anchors)

| Product | Price | Model |
|---------|-------|-------|
| Flo premium | approx $40 per year | Subscription |
| Big Little Feelings | $99 / $79 | One-time course |
| Huckleberry | subscription (undisclosed exact tier) | Subscription |
| Owlet / Nanit | $199 to $399 hardware + app | Device + subscription |

### 7.3 Published retention data

| Finding | Value | Source | Confidence |
|---------|-------|--------|-----------|
| New-mother churn postpartum | approximately 70 percent by week 4 | Mordor Intelligence, pregnancy tracking and postpartum apps market | MEDIUM |
| General app Day 30 retention (context) | approximately 4 to 7 percent median across categories | Multiple app-analytics benchmarks | MEDIUM |
| Flo engagement study | 84.6 percent of users report improved pregnancy knowledge within 30 days | Flo 2022 study with academic co-authors | LOW (vendor-run) |
| Precise pregnancy-app Day 1/7/30 retention curve | UNKNOWN | not found in primary form | n/a |

The 70 percent postpartum churn figure is the empirical spine of Section 2 and the reason the extension exists. It is a market-report figure rather than a peer-reviewed one, so it is marked MEDIUM and flagged for primary-source confirmation.

---

## Register Entries

The following are staged for the maintainers of `research/registers/` to append. This phase does not write to the registers directly.

### competitors.md (append)

| Company | Product | Buyer | Price | Funding | Status | Date | Confidence |
|---------|---------|-------|-------|---------|--------|------|-----------|
| Maven Clinic | Virtual women's/family health clinic | Employers, plans | Enterprise | $437M total, $1.7B val, approx $268M ARR | Active leader | 2024-10 | HIGH |
| Flo Health | Cycle/pregnancy tracker subscription | Consumer | approx $40/yr | $200M Series C, $1B+ val | Active, 70M MAU, 5M paid | 2024-07 | HIGH |
| Ovia Health | Fertility/pregnancy/parenting, enterprise | Employers, plans | Enterprise | Labcorp subsidiary (2021), approx $20M rev at acq | Active | 2021-08 | HIGH |
| Progyny | Fertility benefits | Employers | PEPM/utilization | Public PGNY, $1.17B rev 2024 | Active public | 2024 FY | HIGH |
| Carrot Fertility | Fertility benefits | Employers, plans | Enterprise | $115M total, $75M Series C | Active | 2021-08 | HIGH |
| Cleo | Family/caregiving benefits | Employers | PEPM | $83M total, $40M Series C | Active | 2021-03 | HIGH |
| Pomelo Care | Value-based virtual maternity/newborn | Plans (Medicaid+commercial), employers | PMPM/value-based | $92M Series C, $1.7B val, approx $171M+ total | Active, 25M lives, approx 7 percent of US births | 2026-01 | HIGH |
| Babyscripts | RPM pregnancy via OB | OB practices/systems | Per-pregnancy license | approx $37M total | Active, 200K pregnancies, 30 states | 2021-12 | HIGH |
| Bloomlife | Prescription remote maternal/fetal monitor | Providers (B2B2C) | Device+service | $12.2M Series A, FDA-cleared MFM-Pro | Active post-pivot; DTC shut | 2024-09 | HIGH |
| Peanut | Social network for mothers | Consumer/advertisers | Freemium | approx $32M total | Active, 3.5M MAU | 2023-08 | MEDIUM |
| BabyCenter | Ad/data content | Advertisers | Free | Everyday Health/Ziff Davis | Active, 100M monthly reach | 2019 | HIGH |
| What to Expect | Ad content/community | Advertisers | Free | Everyday Health/Ziff Davis | Active | 2019 | HIGH |
| The Wonder Weeks | Paid content app | Consumer | Low one-time | Twise Victory Publishing (private) | Active | n/a | MEDIUM |
| Big Little Feelings | Toddler-behavior courses | Consumer | $99/$79 | Bootstrapped | Active, 400K takers | n/a | MEDIUM |
| Owlet | Infant monitor wearable+app | Consumer | $199 to $399+app | Public OWLT, approx $74M to $77.5M rev 2024 | Active | 2024 FY | HIGH |
| Nanit | AI baby monitor+subscription | Consumer | Device+sub | approx $125M total, $50M round Dec 2025 | Active | 2025-12 | HIGH |
| Huckleberry | Infant sleep app+subscription | Consumer | Subscription | $16M total | Active, 1.2M families | 2021-11 | HIGH |

### funding.md (append)

Deals as thesis evidence: Maven $125M Series F (2024, StepStone) at $1.7B; Flo $200M Series C (2024, General Atlantic) at $1B+; Pomelo $92M Series C (2026, Stripes) at $1.7B; Carrot $75M Series C (2021, Tiger Global); Cleo $40M Series C (2021, Transformation Capital); Babyscripts $19M Series B (2021, MemorialCare/Cigna Ventures); Nanit $50M (2025, Springcoast). Category signal: capital concentrates in employer/plan clinical-services and value-based maternity, not DTC pregnancy subscriptions.

### vendors.md (append)

Interoperability: Health Gorilla, Particle Health, 1up Health. Telehealth clinician networks: Wheel, SteadyMD. Labs: Quest (Labcorp conflicted via Ovia). BP devices: Omron, Withings (pregnancy-validated only). Content: ACOG, AAP. Distribution: employer benefits brokers/platforms; Medicaid MCOs (TMaH 15-state list).

### sources.md (append)

| Source | URL | Pub date | Used for | Credibility |
|--------|-----|----------|----------|-------------|
| CDC NVSR Births Final 2024 | https://www.cdc.gov/nchs/data/nvsr/nvsr75/nvsr75-02.pdf | 2025-07 | US births 3,628,934 | HIGH |
| CDC NCHS Births 2023 (PMC) | https://pmc.ncbi.nlm.nih.gov/articles/PMC11615961/ | 2024 | 2023 births, first-birth rate 21.4 | HIGH |
| KFF / March of Dimes Medicaid births | https://www.marchofdimes.org/peristats/data?reg=99&top=11&stop=154 | 2024 | 41 percent Medicaid share | HIGH |
| Grand View Research femtech | https://www.grandviewresearch.com/industry-analysis/femtech-market-report | 2025 | Femtech TAM $39.29B to $97.25B | MEDIUM |
| Mordor Intelligence pregnancy/postpartum apps | https://www.mordorintelligence.com/industry-reports/pregnancy-tracking-and-postpartum-care-apps-market | 2025 | 70 percent postpartum churn | MEDIUM |
| Maven Series F (PRNewswire/Fierce) | https://www.fiercehealthcare.com/finance/maven-clinic-clinches-125m-invest-tech-value-based-care | 2024-10 | Maven funding/valuation | HIGH |
| Flo Series C (TechCrunch) | https://techcrunch.com/2024/07/30/fertility-tracking-app-flo-health-raises-200m-at-a-1b-valuation/ | 2024-07 | Flo funding/users | HIGH |
| Progyny 10-K FY2024 (SEC) | https://www.sec.gov/Archives/edgar/data/1551306/000155130625000040/pgny-20241231.htm | 2025 | Progyny revenue | HIGH |
| Labcorp acquires Ovia | https://ir.labcorp.com/news-releases/news-release-details/labcorp-extends-leadership-womens-health-acquisition-ovia-health | 2021-08 | Ovia status | HIGH |
| Carrot Series C | https://www.fiercehealthcare.com/payer/carrot-fertility-raises-75-million-series-c-round | 2021-08 | Carrot funding | HIGH |
| Cleo Series C | https://www.businesswire.com/news/home/20210330005113/en/ | 2021-03 | Cleo funding | HIGH |
| Pomelo Series C | https://www.prnewswire.com/news-releases/pomelo-care-raises-92-million-series-c-reaches-1-7-billion-valuation... | 2026-01 | Pomelo funding/scale | HIGH |
| Babyscripts Series B | https://babyscripts.com/babyscripts-raises-additional-series-b-funding-for-virtual-maternity-care-solution | 2021-12 | Babyscripts funding | HIGH |
| Bloomlife pivot/FDA | https://www.biospace.com/bloomlife-announces-fda-clearance-of-bloomlife-mfm-pro | 2024 | Bloomlife status | HIGH |
| Owlet FY2024 (SEC 10-K) | https://www.sec.gov/Archives/edgar/data/1816708/000162828025012035/owlt-20241231.htm | 2025 | Owlet revenue | HIGH |
| Nanit $50M | https://www.prnewswire.com/news-releases/nanit-raises-50m... | 2025-12 | Nanit funding | HIGH |
| Huckleberry Series A | https://www.prnewswire.com/news-releases/huckleberry-raises-12-5-million-series-a... | 2021-11 | Huckleberry funding | HIGH |
| Peanut funding | https://www.crunchbase.com/organization/peanut-2 | 2023 | Peanut funding/users | MEDIUM |
| BabyCenter ownership | https://en.wikipedia.org/wiki/BabyCenter | 2019 | Everyday Health ownership | MEDIUM |
| Big Little Feelings | https://biglittlefeelings.com/pages/courses | 2026 | Course pricing | MEDIUM |
| CMS Maternity Core Set 2024 | https://www.medicaid.gov/medicaid/quality-of-care/downloads/2024-maternity-core-set.pdf | 2024 | Quality measures | HIGH |
| Policy Center MMH (PND-E/PDS-E) | https://policycentermmh.org/the-role-of-medicaid-in-advancing-obstetric-provider-maternal-mental-health-screening-and-treatment/ | 2024 | Depression screening measures | MEDIUM |
| KFF postpartum coverage tracker | https://www.kff.org/medicaid/medicaid-postpartum-coverage-extension-tracker/ | 2025 | 48 states + DC | HIGH |
| CMS TMaH model | https://www.cms.gov/priorities/innovation/innovation-models/tmah | 2025 | 15 states, value-based | HIGH |
| RPM CPT codes / Medicare rates | https://blog.prevounce.com/quick-guide-remote-patient-monitoring-rpm-cpt-codes-to-know | 2024 | RPM codes and $102 to $142 PMPM | HIGH |
| RPM in pregnancy (Cigna policy) | https://static.cigna.com/assets/chcp/pdf/coveragePolicies/medical/mm_0563... | 2024 | RPM medical necessity HDP/GDM | MEDIUM |
| Baby first-year cost | https://www.cradlewise.com/how-much-does-a-baby-cost/ | 2026 | $20,384 first-year, $18,865 maternity | MEDIUM |

---

## Open Questions

1. Exact first-birth count and percentage of total births for 2023/2024 in primary NCHS tabular form. CDC pages returned HTTP 403 to automated fetch; the 38 to 39 percent figure is derived from the published first-birth rate (21.4 per 1,000) and a population estimate, not read directly from a birth-order table. Confirm against CDC NVSR Table (births by live-birth order) before it anchors a fundraising deck.
2. Precise dollar size of the pregnancy-tracking-and-postpartum-app category (the correct analyst market), separated from the broad femtech TAM.
3. Primary-source, peer-reviewed pregnancy-app retention curve (Day 1/7/30 and postpartum). The 70 percent-by-week-4 figure is from a market report, not a peer-reviewed study.
4. State-by-state Medicaid RPM and CoCM reimbursement for maternity (rates and coverage vary; Medicare rates used as proxy).
5. Actual PEPM and PMPM contract values realized by Maven, Ovia, and Pomelo (not publicly disclosed; contract-size estimates are inference).
6. True DTC CAC for a pregnancy app specifically (used a health-app range).
7. Big Little Feelings and Wonder Weeks revenue (private, undisclosed).

## Assumptions Made

1. First-birth share approx 38 to 39 percent, derived not directly cited. Impact if wrong: shifts the top of the funnel by low single-digit percent; does not change the conclusion.
2. Engaged-partner share haircut to 65 to 75 percent of first births. LOW confidence, materially affects the partner-surface addressable count. Impact: could halve or double the "partner app" reachable pool.
3. DTC price $12/month and 75 percent gross margin are founder assumptions pending Phase 3/4 unit-cost work (LLM inference and clinical review are the swing costs). Impact: LTV scales linearly with both; the qualitative conclusion (DTC LTV to CAC below or near 1.0) holds across the plausible range.
4. Churn assumptions (10 percent pregnancy, 65 percent birth transition, 12 percent infant, 8 percent toddler) are calibrated to the single published anchor (70 percent by week 4) and otherwise estimated. Impact: the base-case LTV of $75 could range roughly $60 to $130; the extension multiple (1.6x to 2.8x) is robust to this.
5. Channel CAC, cycle, and contract-size figures are order-of-magnitude estimates. They rank-order channels correctly even where absolute values are soft.
6. Medicare RPM national rates used as a proxy for maternity RPM economics; state Medicaid varies.

## Confidence Summary

Overall confidence: MEDIUM to HIGH on the strategic conclusion, MEDIUM on the absolute numbers.

- HIGH: US births, Medicaid birth share, the competitive map and funding figures, the reimbursement code structure, the policy tailwinds (postpartum extension, Core Set measures, TMaH), and the central finding that capital and durable value sit in employer and payer clinical-services channels, not DTC.
- MEDIUM: bottom-up SAM ranges (penetration and price assumptions), the LTV figures (churn assumptions calibrated to a single market-report anchor), and the femtech TAM as a loose upper bound.
- LOW / weakest: the engaged-partner haircut, the precise DTC CAC, and the exact first-birth percentage (derived, not read from a primary table). None of these weak points reverse the phase's conclusion.

The conclusion is robust even where the inputs are soft: a pregnancy-only DTC subscription cannot cover its own acquisition cost against a 10-month churn cliff; the postpartum and early-childhood extension lifts LTV 1.6x to 2.8x but does not by itself make DTC profitable; the fundable business is a clinical-services play sold to employers and, above all, to Medicaid managed care plans, where the postpartum year is now covered, measured, funded, and unwatched.
