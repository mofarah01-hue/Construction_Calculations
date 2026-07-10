# CONCEPT B, PHASE 2: DATA INPUTS AND FEASIBILITY

Governed by `00_framework.md`. Inherits `research/shared/shared_wearable_data_access.md`, `research/shared/shared_llm_layer.md`, and the Phase 1 data requirement matrix (`research/b/phase1_markers.md`, section 3). Input to this phase is that matrix. All access dates 2026-07-10.

## Strategic finding, stated first

The wearable dependency is not fatal, and this phase confirms it against the device level detail. Phase 1 established that no V1 marker requires raw consumer wearable sensor data. This phase adds the harder confirmation: every V1 marker also survives on **self report plus published reference alone**, with derived wearable metrics acting only as an optional fidelity enhancement on V2 physiological markers. The single clinical fidelity input in V1, blood pressure, comes from a cleared home cuff the user already buys, not from a wristband.

The three findings that follow are the load bearing decisions of this phase:
1. **Wearable:** obtainable derived metrics (RHR, derived HRV, temperature deviation, sleep summaries, spot SpO2) are sufficient for V2 enhancement and irrelevant to V1. No wearable is a shipping dependency. (2.1)
2. **Labs:** Model 1 ingest is the correct answer and is an order of magnitude cheaper than Model 2 order. Model 2 (the Function Health model) sells the user something her OB already orders and insurance already covers, and adds nothing a prenatal panel lacks. (2.2)
3. **Content:** the grounding corpus splits cleanly into free public domain government content (CDC, USDA, WHO, NIH) and licensed proprietary content (ACOG, AAP, and every evidence based parenting framework). Content licensing plus a clinician on retainer is a real, permanent operating line item, not a footnote. (2.4)

---

## 2.1 WEARABLE

### The question, settled

Per `shared_wearable_data_access.md` section 4: no consumer device delivers raw PPG plus raw accelerometer plus continuous skin temperature plus continuous SpO2 under commercial terms. Continuous skin temperature and continuous SpO2 are not obtainable from any mainstream consumer wearable at all; raw PPG is obtainable only from a partner gated (Samsung) or contract or prosumer strap (Withings Research, Polar) path. That finding is inherited, not relitigated here.

The Concept B specific question is different and narrower: **does the v1 shortlist need any of it.** It does not. What the product can obtain is the set of vendor **derived** scalars, and that set is more than enough for the only role wearable data plays in this product, which is V2 physiological normalization and education.

### What IS obtainable per device (derived metrics, commercial terms)

Synthesized from `shared_wearable_data_access.md` tables 1 and 2. All rows are derived scalars pulled from a cloud broker API (or HealthKit on device), not raw waveforms. "Commercial" = usable by a commercial app under the vendor's standard developer terms.

| Device / platform | Derived RHR | Derived HRV | Skin temp | SpO2 | Sleep summary | Steps/activity | Commercial terms and the catch |
|---|---|---|---|---|---|---|---|
| Apple Watch (HealthKit) | Yes (integer) | Yes (SDNN) | Nightly wrist deviation only | Spot; HW disabled on many US units (Masimo ban) | Stages | Yes | Free (99 USD/yr program); no health data for ads/sale/mining |
| Oura Ring | Yes | Yes (daily) | Nightly deviation only | Sleep average only | Yes | Yes | Free API, but end user must hold active paid Oura Membership; app approval above 10 users; 5000 req/5 min |
| Whoop | Yes | Yes (rmssd) | One value per cycle | One value per cycle | Yes | Strain | Free API; **redistribution/resale forbidden even with user consent**; revocable grant; 100/min, 10000/day |
| Garmin (Health API) | Yes | Yes | No | Spot pulse ox | Yes | Yes | Partner approval; reported one time ~5,000 USD prod fee (UNVERIFIED, LOW); redistribution governed by agreement |
| Fitbit / Google | Yes | Yes | Nightly | Nightly | Yes | Yes | Free API; Fitbit Web API **sunsets Sept 2026**, build on Google Health API; commercial intraday case by case |
| Withings (Public API) | Yes | Derived | No | Spot | Yes | Yes | Free tier plus paid plans; derived only (raw is separate contract) |
| Samsung Galaxy Watch | Yes | Derivable | UNKNOWN | Derivable | Yes | Yes | Consumer path to raw exists via Privileged SDK (partner gate, cost UNKNOWN); derived via Samsung Health |
| Polar (straps) | Yes | Raw RR/PPI | No sensor | No sensor | n/a | Yes | Free SDK, commercial permitted; wrong form factor (chest/arm strap), no daily wear |

Read across: **any** of Apple, Oura, Fitbit/Google, Garmin, or Withings supplies derived RHR, derived HRV, a nightly temperature deviation, a spot or sleep averaged SpO2, and sleep and activity summaries under commercial terms. This is the full set of inputs the V2 physiological markers need. The rational integration posture is HealthKit and Google Health Connect first (they aggregate whatever band the user already owns at zero incremental cost and zero vendor lock in), with direct Oura, Whoop, and Garmin connectors added on user demand.

### Does the v1 shortlist need it? No.

Mapping the Phase 1 v1 shortlist (phase1_markers.md section 2) to its data source:

| V1 marker | Data source | Wearable role |
|---|---|---|
| Urgent maternal warning signs logger and escalation | Published list plus self report | None |
| Postpartum daily mood, full year | Self report | None |
| Postpartum blood pressure | Validated home cuff (cleared device user buys) | None (cuff is not a wristband) |
| Antepartum blood pressure | Validated home cuff | None |
| Antepartum daily mood and anxiety | Self report | None |
| Gestational weight gain vs IOM range | Home scale or manual entry plus static range table | None |
| Fetal movement and kick counts | Self report timer | None |
| Gestational age developmental content | Due date plus licensed content | None |
| Partner perinatal depression check in | Self report | None |
| Partner facing disclosure and consent | Consent metadata | None |

Zero of the ten v1 items has a wearable data dependency. The product ships v1 with no wearable integration at all if required.

### Which Phase 1 markers survive on derived only or self report, and which die

| Marker | Needs | Survives on derived only? | Survives on self report only? | Verdict under commercial terms |
|---|---|---|---|---|
| RHR trajectory | Nightly resting HR | Yes (all major vendors expose derived RHR) | Partial (illness/symptom self report is a weaker proxy) | SURVIVES (V2), derived path |
| HRV trajectory | Daily HRV scalar | Yes, BUT each vendor computes HRV differently; not comparable to the AWHS/published curve | No | SURVIVES for personal trend only; DIES as a benchmark against literature curves |
| Respiratory rate trajectory | Nightly RR | Yes (Oura, Garmin, Fitbit derive it) | No | SURVIVES (V2), low signal magnitude |
| Skin/wrist temperature | Continuous stream | No stream exists; only a nightly deviation | No | Continuous version DIES; nightly deviation SURVIVES as illness flag only |
| Sleep duration/fragmentation | Nightly stages | Yes (derived) | Yes (self report suffices, lower fidelity) | SURVIVES on both paths |
| Activity/step decline | Step count | Yes (phone pedometer removes wearable entirely) | n/a | SURVIVES; no wearable needed |
| Postpartum RHR/HRV recovery | Prepregnancy baseline plus continuous postpartum | Requires enrollment before conception plus derived access; rarely available | No | RESEARCH FEATURE only; effectively DIES for the general user |
| Continuous SpO2 / raw PPG | Raw waveform | No | No | DIES; not a V1 or V2 dependency anyway |

Net: the passive physiological layer degrades gracefully to derived scalars for personal trending and illness flagging, which is all the general wellness framing permits it to do. The one genuine loss is benchmarking an individual against a published normative HRV or temperature curve, because vendor derived HRV is algorithm specific and not comparable to the literature values, and no vendor exposes a continuous temperature stream. That loss is immaterial to v1 and marginal to v2.

### Normative curve availability (carried from Phase 1)

Published pregnancy trajectories exist and are HIGH confidence for direction and magnitude by gestational week: RHR rises from a prepregnancy median 65.0 to 75.5 bpm in the third trimester, HRV falls from 39.9 to a 29.9 ms nadir, sleep falls to a 6.2 h postpartum nadir (Apple Womens Health Study, 757 pregnancies [AWHS-24]). They are **not** stratified adequately by maternal age, BMI, or parity. Stratified published curves appear to be UNKNOWN (Phase 1 Open Question 1). Consequence for the personalization engine: it can compare an individual to her own baseline and to an unstratified population mean, but cannot claim covariate adjusted normalcy. This caps V2 personalization; it does not touch V1.

---

## 2.2 LABS AND BIOMARKERS

### The three models, costed and evaluated

| Dimension | Model 1: Ingest | Model 2: Order (Function Health model) | Model 3: Manual upload |
|---|---|---|---|
| What it is | Pull the labs her OB already ordered, from the patient portal / health data network | Cash pay panel via a national reference lab plus a telehealth ordering network | User photographs or uploads her lab report |
| Data quality | High (structured FHIR `Observation` / `DiagnosticReport` where available; C-CDA/PDF otherwise) | High (structured, lab native) | Low to medium (OCR/vision extraction error; no structured provenance) |
| Regulatory/legal enablement | 21st Century Cures Act (g)(10) patient access API; USCDI includes the Laboratory data class; info blocking rules; TEFCA IAS for network query; CMS-9115 Patient Access API for payer data | State physician order requirement met by a telehealth physician network; CLIA certified lab; no diagnosis by the app | None; user supplied |
| Partnership required | Health data aggregator (network access) OR direct FHIR patient connections | Reference lab contract (Quest/Labcorp) plus telehealth physician network (e.g. PWNHealth) plus phlebotomy access | None |
| Per unit cost signal | Aggregator pricing is custom/usage based and largely unpublished (per member per month, per query, or per record). UNKNOWN exact figures; structurally a low single digit dollars per patient connection order of magnitude, not per test | Function Health consumer price 365 USD/yr (was 499), 160+ markers via Quest, incl. clinician review [Function]; NY/NJ higher; add-ons push >1,000 USD. Telehealth ordering + phlebotomy + lab COGS are bundled into that price | ~0 USD marginal (OCR/vision inference cost only) |
| Value added over existing prenatal panel | Surfaces and trends labs she already has; zero duplicate testing | **Negligible.** A standard prenatal panel already covers CBC, blood type/Rh, antibody screen, glucose, infection screen, thyroid. A parallel cash pay panel re-sells tests she gets free through insurance | Same data as Model 1 but lower quality and higher user friction |
| Founder assumption tested | Confirms B1's "interesting version is ingesting labs she already has" | **Invalidates** B1's cash pay panel as a viable component for pregnancy | n/a |

### Interoperability rules that make Model 1 work (primary framing)

The legal and technical substrate for Model 1 is settled and enforced as of 2026:
- **21st Century Cures Act information blocking rules** require certified health IT to expose a standardized patient access API; enforcement in effect since Sept 2025. [ONC/ASTP, HIGH]
- The certified **(g)(10) FHIR API** (USCDI v3, FHIR R4) is the technical channel; **USCDI includes the Laboratory data class**, so lab results are in scope for patient mediated access. [ONC, HIGH]
- **TEFCA** (Trusted Exchange Framework and Common Agreement) plus its **Individual Access Services (IAS)** exchange purpose lets an app retrieve records nationwide via QHINs. [ONC, HIGH]
- **CMS-9115 Patient Access API** exposes the payer side (claims, some lab), complementary to the provider side. [CMS, HIGH]

The practical constraint is not legal, it is coverage and structure: not every OB practice's EHR returns labs as discrete FHIR `Observation` resources; many return a C-CDA document or a PDF, which requires parsing and degrades to Model 3 quality for that record.

### Aggregator vendors for Model 1

| Vendor | Access model | Notes | Published pricing |
|---|---|---|---|
| Particle Health | Network query (Carequality/CommonWell), C-CDA to FHIR R4; 160,000+ health systems, 320M+ records | Broad network reach | Custom, UNKNOWN |
| Health Gorilla | Health data network plus a Quest Lab Subscription for cohort lab delivery | Direct lab result channel is relevant here | Custom, per transaction, UNKNOWN |
| Metriport | Open source, FHIR native API; notifies on new lab results; C-CDA/PDF/FHIR | Open source lowers integration risk; new lab notification fits the product | Usage based, published tiers not retrieved |
| Flexpa | Patient access networks (CMS-9115, ONC (g)(10), TEFCA IAS); FHIR, IAL2 identity, built in consent | Consumer/agent facing, consent first; best fit for a DTC app | Published pricing page (403 on fetch); UNKNOWN exact |
| 1upHealth | Patient access API, FHIR | Enterprise custom plan | Custom, UNKNOWN |

Pricing across all five is custom or usage based and not publicly retrievable at line item detail (multiple 403s and "contact us" gates). This is an Open Question, not an invented number. The structural point stands regardless: a per patient record retrieval is cheap relative to ordering a new lab panel, because no phlebotomy, no lab COGS, and no physician order are incurred.

### Model 2 cost structure (the Function Health model), detailed

To stand up Model 2 the company must assemble: (1) a reference lab contract (Function uses Quest [Function, HIGH]); (2) a telehealth physician network to satisfy the state physician order requirement, since a lab order legally requires an ordering provider, the role PWNHealth/Labcorp OnDemand/Quest's PWN affiliate fills, reviewing each purchase for medical appropriateness before submitting the order and covering all 50 states via 80+ CLIA certified labs [PWNHealth, HIGH]; (3) phlebotomy access (patient service centers or at home draw); (4) CLIA certified processing. The consumer facing 365 USD/yr Function price bundles all of this. For a builder, the ordering physician network and phlebotomy are the incremental cost lines that Model 1 entirely avoids.

### Recommendation and cost delta

**Recommend Model 1 (ingest), primary, with Model 3 (manual upload) as the universal fallback for records that do not return structured data. Reject Model 2 (order) for the pregnancy use case.**

Rationale and cost delta:
- Model 1 costs an aggregator integration plus a low, per patient connection fee (order of a few dollars per patient, UNKNOWN exact). It ships zero clinical liability for ordering and requires no physician network.
- Model 2 carries a per member cost on the order of the Function Health price point, roughly **365 USD per user per year of retail equivalent cost structure** (lab COGS plus ordering physician plus phlebotomy plus review), for data the user's insured prenatal panel already produces. The cost delta is therefore roughly **two orders of magnitude per user** (single digit dollars one time for ingest versus hundreds of dollars per year for ordering), and Model 2 adds no clinical content a prenatal panel lacks. [Function 365 USD, HIGH; aggregator per-unit UNKNOWN]
- Model 3 is near zero marginal cost and requires no partnership, but its OCR/vision extraction is error prone and carries no provenance. It is correct as a fallback, wrong as the primary.

This confirms founder assumption B1's own hedge: the interesting version is ingesting labs she already has, not selling her a parallel cash pay panel.

---

## 2.3 MOOD, AFFECT, AND STRESS INFERENCE

### The literature, honestly, including negative findings

The question is whether passive affect (mood, stress, emotion) can be inferred from consumer grade physiology (HRV, sleep, skin temperature) accurately enough to make a defensible product claim. The evidence says no.

| Finding | Source | What it establishes | Confidence |
|---|---|---|---|
| HRV accuracy is satisfactory at rest but degrades in dynamic cognitive/emotional stress, the exact condition affect inference needs | Assessing Stress Level Scores Against Wearable Physiology, PMC12647429 (2025) | The physiological signal is least reliable precisely when affect is changing | HIGH |
| Commercial device stress scores (Garmin, HRV based) require validation before research use; raw IBI access is restricted, blocking independent accuracy assessment | Same, PMC12647429 | Vendor stress scores are unvalidated black boxes and cannot be independently audited | HIGH |
| Personalized emotion models reach 95% (3 class) but participant inclusive generalized models reach only 66.95% | Comparison of Personalized vs Generalized Emotion Recognition, JMIR AI 2024, PMC11127131 | Cross person (the deployable case for a new user with no labeled data) is near chance for multiclass affect | HIGH |
| Stress detection does not reproduce across consumer wearable sensors; pretrained tools underperform (AUROC 0.723) vs in domain (up to 0.953) | Extending Stress Detection Reproducibility to Consumer Wearable Sensors, arXiv 2505.05694 (2025) | Models do not transfer across devices or populations; no shippable generalized detector | MEDIUM |
| Passive sensing for mental health remains an open research area with heterogeneous, non generalizable results | Passive Sensing for Mental Health Monitoring, scoping review, JMIR 2025 (e77066) | The field has no validated, productizable consumer grade affect detector | MEDIUM |

The consistent theme: affect inference works only with per user labeled training data (personalized models), which a consumer product does not have for a new user, and collapses toward chance in the generalized, cross person, cross device condition that a shipping product actually faces. Vendor stress scores are unvalidated and unauditable because raw IBI is withheld.

### Verdict: not defensible. Self report redesign confirmed.

Passive affect inference from consumer grade physiology is **not defensible** as a product claim and is not buildable at usable accuracy for a new user. This aligns with framework section 2 (inference of a named affective state from passive data is a claim) and confirms founder assumption B4. The product does not need it. The Phase 1 redesign stands: **daily self report is cheap, accurate, defensible, and already what the user expects.** A single daily mood question of the product's own design, trended and shown back to her, is a journal and asserts nothing (framework section 2). The product normalizes and educates on a schedule and on self report without claiming to detect. Physiology contributes context (sleep and mood shown as two lines on a chart, correlation not causation), never an affective verdict.

---

## 2.4 CONTENT AND KNOWLEDGE BASE

The AI layer must be grounded on a vetted retrieval corpus, not generated from parametric memory (`shared_llm_layer.md` section 4: retrieval converts the FTC substantiation question into a content licensing line item). The corpus splits cleanly into free public domain content and licensed proprietary content.

### Corpus licensing map

| Corpus | Domain | Licensable / free | Terms | Update cadence | Confidence |
|---|---|---|---|---|---|
| CDC Hear Her urgent maternal warning signs | Obstetric safety | FREE, US government work / public domain | Reusable; match wording verbatim | Periodic CDC revision | HIGH |
| CDC Learn the Signs Act Early milestones | Infant/child development | FREE, US government work / public domain | Reusable; last major revision Feb 2022 | Infrequent (2022 revision) | HIGH |
| WHO growth standards (0 to 24 mo), CDC growth charts (2 yr+) | Infant growth | FREE, public | Reusable reference charts | Stable | HIGH |
| USDA MyPlate, Dietary Guidelines for Americans | Nutrition | FREE, public domain (USDA/HHS) | Reusable without copyright restriction | DGA every 5 years (2020-2025) | HIGH |
| NIH / ODS nutrient requirements (folate, iron, iodine, DHA, calcium) | Nutrition | FREE, US government work | Reusable | Periodic | HIGH |
| FDA dietary advice in pregnancy | Nutrition/safety | FREE, US government work | Reusable | Periodic | HIGH |
| ACOG clinical guidance, committee opinions, patient education pamphlets | Obstetric | LICENSED, proprietary | Reuse requires a license via Copyright Clearance Center; commercial reuse restricted; ACOG seal is a trademark, no use without formal agreement | Guidelines updated continuously | HIGH |
| AAP Bright Futures | Pediatric prevention | MIXED: some materials free, guidelines/pocket guide/nutrition manual/toolkit are purchase or org license | Toolkit Integration Resources require an organization license | Editions (4th ed. current) | HIGH |
| AAP HealthyChildren.org consumer content | Pediatric | LICENSED, copyrighted AAP content | Not public domain; reuse requires AAP permission | Continuous | MEDIUM |
| Developmental screening instruments (ASQ [Brookes], Denver II, M-CHAT) | Development screening | LICENSED / proprietary (M-CHAT free but is a clinical instrument) | Clinical tools; sit in the risk register, not the wellness corpus | Versioned | HIGH |
| Triple P Positive Parenting Program | Parenting (older child) | LICENSED, proprietary; IP held by University of Queensland, licensed via UniQuest | Dissemination/purveyor license required | Program editions | HIGH |
| Incredible Years | Parenting (older child) | LICENSED, proprietary; all programs/materials copyright, brand trademarked | Controlled photocopy/reuse per material | Program editions | HIGH |
| Wonder Weeks | Parenting (infant) | Proprietary commercial content | Commercial license; terms UNKNOWN | Book/app editions | LOW |

Read across: the entire **obstetric safety spine, nutrition layer, growth charts, and infant milestone checklists are free public domain government content.** This is the v1 corpus and it carries **no licensing cost**. The licensed proprietary content (ACOG clinical guidance, AAP Bright Futures and HealthyChildren, and every evidence based parenting framework) is where licensing dollars land, and it maps onto exactly the content that is either V2 (clinical depth) or LATER (older child parenting). The product can ship a defensible v1 grounding corpus on free content plus its own clinically reviewed original copy, and license ACOG/AAP depth as a deliberate V2 investment.

**Content licensing is a real, flagged line item.** ACOG and AAP reuse both require formal licenses (Copyright Clearance Center for ACOG; organization license for AAP toolkits), and both carry trademark restrictions. Exact license fees are quote based and were not retrievable (Open Question). Treat ACOG and AAP licensing as a costed line at V2, not a free assumption.

### Medical review operating cost (clinician on staff / retainer)

Grounded original content and any adaptation of licensed guidance require clinical sign off before it ships, and warning sign copy must pass verbatim source match plus clinical review (Phase 1 Assumption 3). This is a permanent operating cost, not a one time build.

| Role | Rate (US, 2026) | Basis | Source | Confidence |
|---|---|---|---|---|
| Telehealth OB-GYN (reviewer/medical director) | 115 USD/hr avg (range 102 to 153; up to 175) | Hourly telehealth market | ZipRecruiter Telemedicine Ob Gyn, 2026 | HIGH |
| Full time physician (if brought in house) | 200,000 to 300,000+ USD/yr | Digital health staffing benchmark | Telemedicine startup cost guides, 2026 | MEDIUM |
| Nurse practitioner (content/triage support) | 110,000 to 130,000 USD/yr | Same | Same | MEDIUM |
| Non physician clinical content reviewer (remote) | ~24 USD/hr | Generic remote clinical reviewer | ZipRecruiter, 2025 | MEDIUM |

Operating model recommendation: a **part time 1099 OB-GYN medical reviewer on retainer** (framework "buy vs build": retain, do not hire, until volume justifies it), budgeted at the 115 USD/hr market rate, is the correct v1 posture. A pediatric reviewer and a lactation reviewer are added as the postpartum and infant layers ship. This is a recurring content operations cost that scales with content volume and must appear in the Phase 4 dev plan and Phase 6 business case as an ongoing line, not a launch expense. A pure engineering headcount model is wrong for this product (concept brief Phase 4 note).

### The long horizon parenting layer: take a position or present a range

The older child parenting layer (boundaries, discipline, autonomy, problem solving) has a materially weaker, contested, culturally variable evidence base than the obstetric layer (Phase 1, verdict LATER), and its most credible frameworks (Triple P, Incredible Years) are proprietary and licensed. Recommendation: **present a range, disclose contested areas, and do not take a single normative position.** Taking a position on discipline is a reputational and content liability with no evidentiary payoff, and the licensed frameworks would in any case constrain what the product may assert. This layer is a content and trust product, costed as content operations, not a data product.

---

## Register Entries

Per framework section 9. Proposed entries; register files are not edited by this phase.

### Sources (for `sources.md`)

| Title | Org | URL | Accessed | Published | Used for | Credibility |
|---|---|---|---|---|---|---|
| 21st Century Cures Act Final Rule / info blocking | ONC (ASTP) | https://healthit.gov/regulations/cures-act-final-rule/ | 2026-07-10 | living | (g)(10) API, USCDI labs, info blocking, Sept 2025 enforcement | HIGH primary |
| Cures Act information blocking timeline | Particle Health | https://www.particlehealth.com/blog/cures-act-timeline | 2026-07-10 | living | Enforcement timeline, network reach | MEDIUM secondary |
| Patient Access APIs 2026 | Topflight | https://topflightapps.com/ideas/patient-access-apis/ | 2026-07-10 | 2026 | TEFCA IAS, CMS-9115, aggregator landscape | MEDIUM secondary |
| Health Gorilla Health Data Network / Lab Subscription | Health Gorilla | https://www.healthgorilla.com/ | 2026-07-10 | living | Quest lab result cohort delivery | HIGH primary |
| Metriport Medical API | Metriport | https://www.metriport.com/medical | 2026-07-10 | living | Open source FHIR API, new lab notification | HIGH primary |
| Flexpa (product + pricing) | Flexpa | https://www.flexpa.com/ ; /pricing | 2026-07-10 | living | Patient access networks, consent, IAL2; pricing page 403 | HIGH primary (pricing UNKNOWN) |
| Particle Health | Particle Health | https://www.particlehealth.com/ | 2026-07-10 | living | Network reach 160k systems, 320M records | HIGH primary |
| Function Health pricing | Function Health | https://www.functionhealth.com/pricing ; /article/function365 | 2026-07-10 | 2026 | 365 USD/yr (was 499), 160+ markers, Quest, clinician review | HIGH primary (pricing page 403; figure from function365 article + secondary) |
| PWNHealth agreements / services | PWNHealth via Labcorp OnDemand / Quest | https://www.ondemand.labcorp.com/pwnhealth-agreements ; https://www.questhealth.com/faq-what-services-does-pwn-provide.html | 2026-07-10 | living | Telehealth ordering network, 50 states, 80+ CLIA labs, physician order | HIGH primary |
| Assessing Stress Level Scores vs Wearable Physiology | PMC | https://pmc.ncbi.nlm.nih.gov/articles/PMC12647429/ | 2026-07-10 | 2025 | HRV degrades under stress; Garmin score unvalidated; raw IBI restricted | HIGH primary |
| Personalized vs Generalized Emotion Recognition | JMIR AI | https://ai.jmir.org/2024/1/e52171 (PMC11127131) | 2026-07-10 | 2024 | Generalized 66.95% vs personalized 95%; cross person near chance | HIGH primary |
| Extending Stress Detection Reproducibility to Consumer Wearables | arXiv | https://arxiv.org/abs/2505.05694 | 2026-07-10 | 2025 | Non reproducible across devices; pretrained AUROC 0.723 | MEDIUM preprint |
| Passive Sensing for Mental Health, scoping review | JMIR | https://www.jmir.org/2025/1/e77066 | 2026-07-10 | 2025 | No validated productizable consumer affect detector | MEDIUM |
| ACOG Permissions Information | ACOG | https://www.acog.org/Legal/Permissions%20Information | 2026-07-10 | living | Copyright Clearance Center license, commercial reuse restriction, seal trademark | HIGH primary |
| ACOG Patient Education Materials | ACOG | https://www.acog.org/clinical-information/patient-education-materials | 2026-07-10 | living | Pamphlet reuse terms | HIGH primary |
| AAP Bright Futures materials and licensing | AAP | https://www.aap.org/en/practice-management/bright-futures/bright-futures-materials-and-tools/ | 2026-07-10 | living | Some free, some purchase/org license | HIGH primary |
| CDC Learn the Signs Act Early milestones | CDC | https://www.cdc.gov/act-early/milestones/index.html | 2026-07-10 | 2022 rev | Free public domain milestone checklists | HIGH primary |
| USDA MyPlate / FNIC graphics (public domain) | USDA | https://www.nal.usda.gov/fnic/myplate-graphics ; https://www.myplate.gov/ | 2026-07-10 | living | MyPlate resources public domain, reusable | HIGH primary |
| Triple P copyright / dissemination | Triple P Intl / UniQuest | https://www.triplep-parenting.com/us/service-pages/copyright/ ; PMC10640495 | 2026-07-10 | 2023 | Proprietary IP, UQ/UniQuest license | HIGH primary |
| Incredible Years copyright | Incredible Years | https://www.incredibleyears.com/ | 2026-07-10 | living | Copyright/trademark, controlled reuse | HIGH primary |
| Telemedicine Ob Gyn hourly pay | ZipRecruiter | https://www.ziprecruiter.com/Jobs/Telemedicine-Ob-Gyn | 2026-07-10 | 2026 | 115 USD/hr avg (102 to 175) reviewer rate | HIGH secondary |
| Telemedicine startup cost / staffing | Medesk / Folio3 | https://www.medesk.net/en/blog/telemedicine-startup-costs/ | 2026-07-10 | 2026 | FT physician 200 to 300k, NP 110 to 130k, 1099 model | MEDIUM secondary |

### Vendors (for `vendors.md`)

| Vendor | Supplies | Works with startups | Published pricing | Contact path | Confidence |
|---|---|---|---|---|---|
| Particle Health | Health record network query, C-CDA to FHIR | Yes | Custom, UNKNOWN | particlehealth.com | MEDIUM |
| Health Gorilla | Health data network + Quest lab subscription | Yes | Per transaction, UNKNOWN | healthgorilla.com | MEDIUM |
| Metriport | Open source FHIR API, lab notifications | Yes | Usage based, UNKNOWN | metriport.com | MEDIUM |
| Flexpa | Consumer patient access API, consent/IAL2 | Yes (DTC fit) | Published page (403), UNKNOWN | flexpa.com | MEDIUM |
| 1upHealth | Patient access FHIR API | Yes (enterprise) | Custom, UNKNOWN | 1up.health | MEDIUM |
| PWNHealth (Everly/Labcorp affiliate) | Telehealth ordering physician network, 80+ CLIA labs, 50 states | Yes (B2B) | Per order, UNKNOWN | ondemand.labcorp.com/pwnhealth-agreements | HIGH (capability), LOW (price) |
| Quest Diagnostics | Reference lab (Function's partner) | Yes | Function retail 365 USD/yr bundle | questhealth.com | HIGH (retail), LOW (wholesale) |
| ACOG | Obstetric clinical + patient education content license | Via CCC | Quote based, UNKNOWN | acog.org permissions | HIGH (terms), UNKNOWN (fee) |
| AAP | Bright Futures / pediatric content license | Org license | Some free, some purchase, UNKNOWN | aap.org | HIGH (terms), UNKNOWN (fee) |
| Triple P International (UniQuest) | Licensed parenting program content | Purveyor license | Quote based, UNKNOWN | triplep.net | MEDIUM |
| Incredible Years | Licensed parenting program content | License | Quote based, UNKNOWN | incredibleyears.com | MEDIUM |

### Datasets (for `datasets.md`)

| Dataset / corpus | Population | License | Access | Bias/limitation | Confidence |
|---|---|---|---|---|---|
| CDC Hear Her warning signs | Pregnant/postpartum | Public domain (US gov) | Free | Copy must match verbatim | HIGH |
| CDC Learn the Signs Act Early milestones | Infants/children 2mo to 5yr | Public domain (US gov) | Free | Revised 2022; not a diagnostic screen | HIGH |
| WHO growth standards / CDC growth charts | Infants/children | Free public | Free | Standard vs reference distinction | HIGH |
| USDA MyPlate / Dietary Guidelines / NIH ODS | General + pregnancy | Public domain (US gov) | Free | Generic, not condition specific | HIGH |
| ACOG clinical guidance / patient education | Obstetric | Proprietary, licensed | Paid license (CCC) | Commercial reuse restricted | HIGH |
| AAP Bright Futures / HealthyChildren | Pediatric | Mixed free/licensed | Org license for toolkits | Editions | HIGH |

### OSS (for `oss.md`)

No new OSS evaluated in this phase beyond the edge and RAG models already recorded in `shared_llm_layer.md` (Qwen3 `Apache-2.0`, Phi-4-mini `MIT`, Gemma 3 `LicenseRef-Gemma-Terms-of-Use`, Llama 3.2 `LicenseRef-Llama-3.2-Community-License`, llama.cpp `MIT`, Ollama `MIT`). Metriport is open source; its SPDX license was not read from the license file (Open Question) and is not adopted as a dependency in this phase.

---

## Open Questions

1. **Aggregator per unit pricing (Model 1).** Particle, Health Gorilla, Metriport, Flexpa, and 1upHealth all price custom/usage based; exact per patient, per query, or per member per month figures were not retrievable (contact gates and 403s). This blocks a precise Model 1 cost line. Structural conclusion (Model 1 << Model 2) is unaffected; the exact delta is not yet quantified.
2. **Structured lab return rate.** What fraction of OB practices return prenatal labs as discrete FHIR `Observation` resources versus C-CDA/PDF (which degrades to Model 3 quality). Determines real Model 1 data quality. UNKNOWN.
3. **Function Health exact current price and NY/NJ delta.** The 365 USD/yr figure (down from 499) is from the function365 article and secondary reviews; the pricing page itself returned 403. Re verify against primary. Add-on pricing (>1,000 USD) is directional.
4. **ACOG and AAP license fees.** Both confirmed as paid licenses with restricted commercial reuse and trademark constraints, but the dollar figures are quote based and UNKNOWN. Content licensing is flagged as a line item; the amount is not yet costed.
5. **Wonder Weeks and other consumer parenting content licensing terms.** LOW confidence; terms UNKNOWN.
6. **Samsung Galaxy Watch continuous skin temperature exposure.** Inherited UNKNOWN from `shared_wearable_data_access.md`; irrelevant to v1, flagged for any future continuous temperature feature.
7. **Metriport open source license (SPDX).** Not read from the license file per framework section 9; must be closed before adoption as a dependency.
8. **Whether payers require a validated screening instrument (EPDS/PHQ-9) for mood related reimbursement**, versus the product's own self report scale plus the CDC self harm warning sign with crisis routing. Inherited from Phase 1 Open Question 3; a Phase 5 reimbursement item.

## Assumptions Made

1. Aggregator per patient cost is "single digit dollars order of magnitude" for the Model 1 vs Model 2 delta framing. This is an order of magnitude engineering judgment, not a quoted price, because vendor pricing is gated. Impact if wrong: the two orders of magnitude delta narrows, but Model 1 remains cheaper because it incurs no phlebotomy, lab COGS, or physician order.
2. Model 2 cost per user is anchored to the Function Health retail bundle (365 USD/yr) as a proxy for the assembled cost of lab COGS plus ordering physician plus phlebotomy. A builder's wholesale cost could be lower, but the direction (hundreds of dollars per user per year versus single digits for ingest) holds. Impact if wrong: magnitude of delta shifts, recommendation does not.
3. A part time 1099 OB-GYN reviewer at the 115 USD/hr market rate is the correct v1 clinical review posture. If regulators or payers demand an in house medical director, the cost moves to the 200 to 300k/yr full time line. Impact: content operations opex rises materially at scale.
4. The v1 grounding corpus can be built entirely on free public domain government content plus original clinically reviewed copy, deferring ACOG/AAP licensing to V2. If clinical review determines ACOG guidance must be quoted rather than paraphrased in v1, licensing cost pulls forward.
5. Affect inference literature reviewed is representative; the conclusion (not defensible for a new user, cross person, cross device) is robust across the sources found, consistent with framework section 2 and B4.

## Confidence Summary

Overall confidence HIGH on all three load bearing conclusions. The wearable dependency is confirmed non fatal: no v1 marker needs wearable data, and derived scalars cover the v2 physiological layer under commercial terms. This rests on the inherited HIGH confidence shared wearable finding plus the Phase 1 data requirement matrix and is robust.

The lab recommendation (Model 1 ingest over Model 2 order) is HIGH on direction and mechanism, and the interoperability substrate (Cures Act (g)(10), USCDI labs, TEFCA IAS) is HIGH from primary ONC sources. The weakness is the exact per unit aggregator price (UNKNOWN, Open Question 1), which affects the size of the cost delta but not the ranking; Model 2 provably re sells insured prenatal tests and adds nothing, which is the decisive point.

The affect inference conclusion is HIGH: multiple 2024 to 2025 sources converge that generalized, cross device consumer affect detection is near chance and vendor stress scores are unvalidated and unauditable. Self report redesign confirmed.

Content licensing is HIGH on the free versus licensed split (CDC/USDA/WHO/NIH free public domain; ACOG/AAP/parenting frameworks proprietary and licensed) and on the clinician retainer as a permanent operating cost. Weakest content elements: exact ACOG and AAP license fees (UNKNOWN, quote based) and Wonder Weeks terms (LOW). None of these unknowns changes the phase conclusions; they constrain cost precision for Phase 4 and Phase 6, where they are flagged to land.
