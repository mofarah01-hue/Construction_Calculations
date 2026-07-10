# Concept A, Phase 6: Development Plan, Cost, and Timeline

Governed by `00_framework.md` (section 4 cost model, sections 5, 6, 9) and `01_concept_a_elder_monitoring.md` (Phase 6). Builds on and does not re derive: the selected architecture A1 (distributed mesh, one oblique T1 camera, T4 hybrid) in `research/a/phase2_architecture.md`; the BOM, landed cost, COGS, and hardware NRE in `research/a/phase3_hardware.md`; the build versus buy table and engineering week estimates per subsystem in `research/a/phase4_software.md`; the privacy controls and consent build requirements in `research/a/phase5_privacy.md`; the recurring cloud cost in `research/shared/shared_infra_cost.md`; and the funding landscape and comparable rounds in `research/shared/shared_capital_landscape.md`.

Confidence tags HIGH, MEDIUM, LOW per framework section 5. New citation keys are `[D#]` and resolve in Register Entries. Prior keys `[S#]`, `[H#]`, `[P#]` resolve in their source phase files.

---

## 0. The two cost inputs, stated before any estimate

### 0.1 Loaded engineer cost assumption (San Diego, fully loaded)

Per framework section 4, salary alone is not used. The figure below is fully loaded: base plus employer payroll tax, benefits, equipment, software, facilities, and recruiting and administrative overhead.

| Input | Value | Basis | Confidence |
|---|---|---|---|
| San Diego software engineer base, mid to senior | approx $140,000 to $165,000 | levels.fyi, Built In, Glassdoor San Diego 2026 [D6] | HIGH |
| Specialist premium (embedded vision, radar DSP, staff level) | +15 to 30 percent over generalist base | Scarcity of embedded CV and mmWave DSP talent; market inference | MEDIUM |
| Fully loaded multiplier | 1.35x base | Published rule of thumb 1.25x to 1.4x for US knowledge workers; 1.35x for generous benefits or higher tax state; California sits at the upper half [D5] | HIGH |
| **Fully loaded cost per engineer per year (planning figure)** | **$200,000** | Blended $148,000 base x 1.35, rounded to absorb the specialist premium on part of the team | MEDIUM |
| Fully loaded cost per engineer week | $3,846 | $200,000 / 52 | MEDIUM |

The $200,000 planning figure is deliberately blended. A pure generalist runs below it; the embedded vision and mmWave DSP roles that the fall and gait critical path requires run above it. Using one blended number avoids false precision the headcount plan cannot support.

### 0.2 AI assisted development velocity multiplier, cited, low, mid, high

Framework section 4 forbids an invented productivity number. The published empirical record is contested and the effect is strongly conditional on task type and developer experience. The three anchor studies below span the credible range.

| Case | Multiplier | Anchor evidence | What the study actually measured | Confidence |
|---|---|---|---|---|
| Low (drag) | 0.95x (net neutral to slightly slower) | METR randomized controlled trial, 16 experienced open source developers, 246 real issues on their own mature repositories, early 2025 frontier tools (Cursor Pro, Claude 3.5/3.7). Result: 19 percent SLOWER with AI, while developers believed they were 20 percent faster [D1] | Complex, high context work on a codebase the developer already knows well. This is the closest analog to the hard parts of this product | HIGH on the result, MEDIUM on transfer |
| Mid (planning case) | 1.15x | Google internal RCT, approx 100 of its own engineers, realistic enterprise task: approx 21 percent faster with in house AI tooling [D4] | Enterprise task, mixed experience, professional setting. A reasonable central estimate for blended real work | MEDIUM (result reported via secondary summaries) |
| High (greenfield) | 1.40x to 1.55x | Peng et al. 2023, RCT, 95 professional contractors, greenfield HTTP server in JavaScript: 55.8 percent faster with GitHub Copilot; gains largest for less experienced developers [D3] | A self contained, well specified, greenfield task with no legacy, no safety criticality, no hardware. The clean upper bound | HIGH on the result, LOW on transfer to this product |

Two facts discipline how this multiplier is applied.

1. The effect inverts by task type. The high case (Peng, 55.8 percent) is a greenfield, single language, well bounded task, exactly the profile of the caregiver mobile and web app, backend CRUD, dashboards, and integration glue. The low to negative case (METR, minus 19 percent) is complex work on a codebase the developer already knows, exactly the profile of the fall false positive reduction loop, on sensor model porting, radar sensor fusion, and the safety critical escalation state machine, which are the critical path. AI accelerates the cheap work and does little or nothing for the expensive work. Applying a single blended multiplier to the whole plan would overstate the gain, because the gain lands mostly on work that is not on the critical path.

2. The evidence is weak and moving. METR itself published a methodology walk back in February 2026, conceding selection effects severe enough that developers who benefit most from AI declined the no AI arm even at $50 per hour, and it is redesigning the study [D2]. This is a reason to hold the multiplier conservative, not aggressive.

**Decision: plan at the mid multiplier of 1.15x blended, applied differentially (high on app and glue, near neutral on the safety critical CV and embedded work). Report the range. The low case (0.95x) is the honest floor because the critical path work is precisely the work AI does not accelerate.** HIGH confidence in the direction, MEDIUM in the exact 1.15x.

---

## 1. Work Breakdown Structure to each gate

Nine disciplines per the Phase 6 brief. Effort is in raw engineer weeks (before the AI multiplier and before Brooks coordination tax), grounded in the Phase 4 build versus buy week estimates where those exist and estimated where Phase 4 did not cost the discipline (firmware, backend infrastructure, industrial design, certification management, QA, operations). Gates per framework section 3. G1 through G4 carry essentially all development; G5 and G6 are certification, manufacturing scale up, and support, covered lighter.

Object memory and free form scene query are DEFERRED to v2 per Phase 0 and Phase 4 (they force a hub into the BOM and add 16 to 30 plus weeks). They are not in this WBS.

### 1.1 Effort by discipline, cumulative raw engineer weeks to each gate

| Discipline | Scope | To G1 | +To G2 | +To G3 | +To G4 | Cum G4 |
|---|---|---|---|---|---|---|
| Firmware / embedded | Node firmware, mesh (Thread/Zigbee via ESP32-C6), radar SDK integration, bed mat AFE, camera host SoC, OTA, secure boot, power and dying gasp holdup, provisioning | 20 | 14 | 8 | 8 | 50 |
| Computer vision / ML | Pose port to edge silicon (MoveNet/RTMPose on IMX500), fall plus long lie duration gating, gait extraction, radar plus camera fusion, per home generalization, efficacy and FTC gait substantiation support | 26 | 22 | 12 | 10 | 70 |
| Backend / cloud | Derived metric ingest, time series store, ADL and circadian rules engine, per resident baseline and anomaly, trend analytics, notification and escalation service, multi tenant and fleet telemetry, scale hardening | 12 | 10 | 12 | 10 | 44 |
| Mobile / app | Caregiver iOS, Android, web; resident UI; onboarding with the role and capacity consent model (Phase 5 build requirement); escalation UI; report rendering; BLE provisioning | 4 | 12 | 10 | 8 | 34 |
| Assistant / LLM | Wake word (custom trained), on device STT, hybrid edge plus cloud routing, deterministic safety and escalation envelope, RAG retrieval scaffolding, older adult speech tuning | 13 | 12 | 6 | 4 | 35 |
| Hardware / electrical | Board bring up oversight, DFM, thermal validation on sealed nodes, pilot build support | 6 | 4 | 4 | 6 | 20 |
| Industrial design | Enclosures, mounts, light pipe, active indicator; self test housings; DFM iteration; production intent tooling | 2 | 4 | 4 | 4 | 14 |
| Certification | FCC Part 15B/15C and UL/ETL planning and pre scans; formal FCC and UL test management at G4/G5; FTC gait measurement substantiation study management | 1 | 3 | 4 | 14 | 22 |
| QA / test | Test harness, event instrumentation, the ground truth pipeline (section 6), 30 day telemetry rig, field labeling ops, cohort retention and efficacy measurement, PERS integration test | 6 | 10 | 14 | 12 | 42 |
| Operations | Install and support playbooks, PERS monitoring partner integration, cohort field ops, fleet management | 0 | 2 | 10 | 12 | 24 |
| **Raw engineer weeks** | | **90** | **93** | **84** | **88** | **355** |

Reading: approximately 355 raw engineer weeks (approximately 6.8 engineer years) to reach a G4 pilot of 50 to 200 units. Computer vision and ML (70 weeks) and QA including the ground truth pipeline (42 weeks) are the two largest buckets, and together with firmware they carry the critical path. The caregiver app (34 weeks) is large but is the most AI amplifiable and the least critical.

### 1.2 What each gate unlocks (per framework section 3)

| Gate | Definition | Exit criterion (concept specific) | Unlocks |
|---|---|---|---|
| G1 Bench | Algorithms on dev hardware, no enclosure | Fall plus long lie, gait speed, and ADL pipeline run on recorded and live desk data at stated accuracy | Internal proof; NSF SBIR sensing/AI pitch [shared_capital 1.4] |
| G2 Self test | Founder home, continuous | 30 days continuous uptime; real world false positive rate CHARACTERIZED (the make or break number, Phase 4 3.1.3) | The angel and pre seed conversation; NIA SBIR Phase I ($300K, or $500K AD/ADRD) [shared_capital 1.2] |
| G3 Friends and family | 5 to 15 real homes, instrumented | Install time, retention, and failure modes measured; per home FP rate across varied geometry | Seed round; design partner conversations |
| G4 Pilot | 50 to 200 units, structured cohort | Efficacy evidence for a partner conversation; unit economics measured; FCC/UL certification underway; FTC gait substantiation study run | Series A style round; senior living or payer pilot contract; NIA SBIR Phase II ($2.0M, or $2.5M AD/ADRD) |
| G5 Limited commercial | Sellable, low volume manufacturing, support exists, certifications complete | FCC Part 15B/15C granted, triple UL/ETL listing complete; positive contribution margin per subscriber | First revenue; channel launch |
| G6 Full commercial | Scaled manufacturing, full feature set, channel established | Target CAC and LTV | Growth round; scale |

---

## 2. Timeline and cost at 1, 2, 3, and 4 engineers

### 2.1 The AI multiplier applied

Raw 355 engineer weeks to G4, at the mid 1.15x blended multiplier, becomes approximately **309 effective engineer weeks**. Range: high 1.40x gives approximately 254 weeks; low 0.95x gives approximately 374 weeks. The planning case is 309.

### 2.2 Brooks coordination tax, stated with its source

Adding engineers does not add capacity linearly. Communication paths grow as n(n-1)/2, so two engineers have one link, three have three, four have six [D7, Brooks, The Mythical Man Month, 1975]. The coordination tax assumption used here, applied as a per head efficiency decay, is explicit:

| Team size | Communication links | Assumed efficiency per head | Effective capacity (heads x efficiency) |
|---|---|---|---|
| 1 | 0 | 1.00 | 1.00 |
| 2 | 1 | 0.95 | 1.90 |
| 3 | 3 | 0.88 | 2.64 |
| 4 | 6 | 0.80 | 3.20 |

The decay (5, 12, 20 percent) is a modeling assumption grounded in the n(n-1)/2 growth of coordination overhead, not a measured constant for this team; it is deliberately moderate because a small team with clear discipline ownership coordinates better than Brooks's large late project premise. Confidence MEDIUM.

### 2.3 The discipline mix problem, which dominates Brooks at low headcount

For THIS product the binding constraint at low headcount is not coordination overhead, it is discipline coverage. The system requires, at minimum, three distinct and largely non transferable skill sets:

1. Embedded computer vision and mmWave DSP (on sensor pose on IMX500, radar fall fusion, the safety critical detection loop).
2. Mobile and application (iOS, Android, web caregiver app, consent and onboarding flows).
3. Backend and cloud (ingest, time series, rules engine, escalation service, infrastructure, security).

One engineer cannot do embedded vision, iOS, and cloud infrastructure well. This is the named tradeoff. At n=1 the plan is not merely slow, it is unsafe: whichever two of the three disciplines the solo engineer is weak in will ship amateur, and the discipline most likely to be weak, embedded CV, is exactly the safety critical fall path where a poor false positive rate gets the product unplugged (Phase 4 3.1.3). At n=1 the honest verdict is infeasible to do to a shippable safety standard, independent of calendar time. The discipline floor for this product is three. The fourth engineer is the first one that is purely about speed rather than coverage, and the right place to put a fourth is on the CV and QA false positive critical path.

### 2.4 Timeline and cost to G4 at each headcount

Calendar weeks = 309 effective weeks / effective capacity. Engineering labor cost = headcount x calendar weeks x $3,846.

| Headcount | Discipline coverage | Effective capacity | Calendar weeks to G4 | Calendar time | Engineering labor to G4 | Verdict |
|---|---|---|---|---|---|---|
| 1 | One of three disciplines covered well; CV or mobile or cloud ships amateur | 1.00 | 309 | approx 5.9 years | approx $1.19M | INFEASIBLE to a safety standard. Rejected regardless of cost |
| 2 | Two of three; a persistent gap (typically no dedicated cloud or no dedicated mobile) | 1.90 | 163 | approx 3.1 years | approx $1.25M | Feasible but gapped; the uncovered discipline is a quality risk |
| 3 | The three discipline floor covered (embedded/CV, mobile, backend); hardware, ID, cert, PERS contracted | 2.64 | 117 | approx 2.3 years (approx 27 months) | approx $1.35M | RECOMMENDED. Minimum team that covers the disciplines |
| 4 | Floor plus a second CV/QA head on the false positive critical path | 3.20 | 97 | approx 1.9 years (approx 22 months) | approx $1.49M | Buys approx 5 months by attacking the longest pole; justified if capital allows |

Note the shape: total labor cost RISES with headcount (Brooks tax, $1.19M to $1.49M) while calendar time FALLS. Adding people is buying time, not saving money, exactly as Brooks predicts. The fourth head is worth it only because it lands on the critical path (false positive reduction), which is the one thing that determines whether the product survives contact with real homes.

### 2.5 All in cost to G4 at the recommended 3 engineers (labor plus non labor)

Engineering labor is not the whole G4 bill. The non labor lines below are drawn from Phase 3 and the framework and are additive.

| Line | Estimate | Source |
|---|---|---|
| Engineering labor, 3 engineers, approx 27 months | approx $1.35M | Section 2.4 |
| Hardware NRE (tooling, PCB spins, FCC + UL/ETL certification) | $80,000 to $210,000 | Phase 3 2.5 NRE table [H10][H11] |
| Pilot hardware, 200 systems at G4 COGS approx $327 to $452 | $65,000 to $90,000 | Phase 3 COGS at 100 to 1k tier |
| FTC gait measurement substantiation study (instrumented walkway validation) | $30,000 to $80,000 (UNKNOWN, estimated) | Framework 2, 4; Phase 3 flagged, not costed |
| RAG health content license and vetting | UNKNOWN (Phase 4 open item) | Phase 4 3.6 |
| PERS monitoring partner integration and per seat during pilot | UNKNOWN (Phase 4 open item) | Phase 4 3.5 |
| Recurring cloud during pilot (200 users, small tier) | approx $7 to $17 per user per month, immaterial at pilot scale | shared_infra_cost 7 |
| **All in to G4 (excluding the two UNKNOWN content and PERS lines)** | **approx $1.55M to $1.75M** | |

With the two UNKNOWN lines and a normal contingency, **budget approximately $1.8M to $2.0M all in to reach G4 at 3 engineers over approximately 27 months.** MEDIUM confidence, driven by the labor estimate and the two UNKNOWN lines.

---

## 3. Critical path: the longest pole is not features

The longest pole is real world false positive rate reduction on the fall and long lie path, followed by certification. Neither is feature development, and neither parallelizes with more engineers or accelerates with AI.

| Pole | Why it is the critical path | Why headcount and AI do not compress it | Gate it gates |
|---|---|---|---|
| **Real world false positive rate reduction (the true longest pole)** | Lab fall accuracy collapses in the field: 13 algorithms at approx 94 percent scripted sensitivity fell to approx 57 percent on real falls, with 3 to 85 false alarms per day in some settings; one real deployment logged 84 alarms of which 83 were false [P17][S35][S36, Phase 4 3.1.3]. A 2 percent per event FP rate is dozens of nuisance alerts per day. This is the "unplugged in month two" failure. The rate is UNKNOWN per modality because radar vendors publish only marketing multipliers (Phase 2 OQ2, Phase 4 OQ1) | It is an empirical loop bound by calendar time in real homes, not by engineer hours. You need continuous days of real occupancy to observe rare true events and the long tail of confusers (lying on the floor to exercise, sudden sits, dropped objects). More engineers cannot manufacture more real world days. AI cannot generate the ground truth. It is gated by G2 (30 days, one home) then G3 (multi home, varied geometry) | G2, G3, G4. This is why G2's exit criterion is a characterized FP rate, not a feature list |
| **Certification (the second pole)** | FCC Part 15C intentional radiator testing on a 60 GHz radar plus a triple UL/ETL listing (camera, radar, hub) is a fixed duration, serial, external lab process. Phase 3 sizes it at $20K to $45K FCC and $24K to $60K UL/ETL, and calls it the single most underestimated line [H11] | Test lab queues and re test cycles are external and serial; you cannot add your own engineers to the lab. The 60 GHz band and antenna testing is the slow item | G5. It is the pole to commercial sale, not to the pilot |
| Efficacy evidence and FTC substantiation | A partner or payer conversation needs efficacy data and the gait measurement claim must be substantiated to an instrumented walkway reference under FTC standards (framework 2) | Requires a cohort over time (G4) and a validation study; time bound, not headcount bound | G4, G5 |

Feature development (the 34 week caregiver app, the assistant, the ADL rules engine) is real work but it is parallelizable, AI amplifiable, and off the critical path. The mistake a founder timeline makes is budgeting the features and treating false positive reduction and certification as afterthoughts, when they are the poles that set the calendar.

---

## 4. Comparable ventures: the sanity check most likely to contradict a founder timeline

Six comparables, with what they actually took and raised before each milestone. The pattern is uniform and it contradicts any lean, fast, direct to consumer timeline.

| Company | Founded | Sensing approach | Funding path and timing | Time to a fundable pilot / Series A scale | Status and lesson | Confidence |
|---|---|---|---|---|---|---|
| SafelyYou | 2014 to 2016 (tech from 2015 PhD research) | Wall camera, AI fall detection, memory care (B2B senior living) | CITRIS seed 2015; NIA SBIR Phase I 2017; **Series A $19.5M Sept 2021**; Series B $30M 2021; Series C $43M Jan 2025; total >$100M [D8][shared_capital 4.1] | Approx 6 years from tech origin to Series A | Alive and scaling, but only after pivoting AWAY from consumer to B2B senior living, and after years of non dilutive (CITRIS, SBIR) funding the early science | HIGH |
| Nobi | 2018 | Smart light (ceiling) AI fall detection, B2B senior care facilities | **Series B EUR 35M / $37M Jan 2025** co led by Angelini and Nexus NeuroTech [D9][shared_capital 4.1] | Approx 6 to 7 years to Series B | The direct analog to the founder bulb concept, and instructive: it ships in nursing homes and long term care, NOT consumer homes, and took most of a decade. The ceiling light form factor lives in B2B, not DTC | HIGH |
| CarePredict | 2013 | Wearable plus environmental sensors, senior activity | Seed 2015 and 2016; Series A 2017 and 2019; another $29M round July 2023; total approx $46M over 5 rounds across a decade [D10] | Approximately a decade and still raising "Series A" scale rounds | The DTC and home care play that never reached escape velocity; a slow, capital hungry grind. A caution against the consumer wearable model (founder assumption A4/A7) | MEDIUM |
| Vayyar | 2011 | 60 GHz imaging radar (the exact bathroom modality in A1) | Series A $12M Aug 2012; total approx $296M over 5 rounds; unicorn 2022, 11 years in [D11] | 11 years to unicorn, across MULTIPLE markets (automotive, retail, care) | Radar is real and buildable, but Vayyar reached scale by being a multi market silicon company, not an elder monitoring product. The care vertical alone did not carry it | MEDIUM |
| Cherry Labs (Cherry Home) | 2016 | Home AI cameras, behavior change detection | $5.2M seed from GSR Ventures, 2018 [D12] | Never reached a visible Series A | Raised a seed, went quiet, no growth round surfaced. The DTC camera in the home thesis, under funded, stalled. A direct cautionary tale for the camera path | MEDIUM |
| Tellus You Care | 2017 | Wireless sensor, no wearable, elder monitoring | Acquired by AIP Healthcare (Japan) approx Oct 2024 [D13] | Soft landing acquisition, pivoted testing to Japan | The US consumer channel did not sustain it; it exited via a modest acquisition and an overseas pilot market. Another DTC caution | MEDIUM |
| Lively / GreatCall (reference) | Lively 2013 | PERS and passive monitoring | Lively acquired by GreatCall Dec 2015; GreatCall acquired by Best Buy $800M 2018; Alexa Together caregiver monitoring discontinued approx May 2025 [D14][S22] | n/a | The successful exits in this category are PERS and channel consolidation plays, and even a giant (Amazon Alexa Together) exited consumer caregiver monitoring. The money is in channel, not DTC hardware | HIGH |

### 4.1 What the comparables say about the internal estimate

1. Nobody reached a fundable pilot or Series A in under approximately 6 years, and every survivor leaned on non dilutive funding early (SafelyYou CITRIS plus NIA SBIR). The section 2 engineering estimate of approximately 27 months to G4 at 3 engineers is faster than any comparable achieved, and it should be read as the engineering floor, not the elapsed calendar to a fundable pilot.

2. The gap between the 27 month engineering estimate and the 6 year comparable reality is not engineering. It is exactly the two critical path poles from section 3 (field false positive tuning across many homes, and certification) plus the non engineering realities the comparables lived: efficacy evidence generation, channel and pilot partner sales cycles, and regulatory and payer diligence. A realistic elapsed time to a fundable G4, comparables adjusted, is **3 to 4 years**, not 27 months, even with a competent 3 to 4 person AI assisted team. The engineering is the shorter part.

3. Every survivor that scaled did so in B2B senior living or channel (SafelyYou, Nobi, GreatCall), and every DTC consumer play stalled or soft landed (CarePredict, Cherry, Tellus, Alexa Together). This corroborates founder assumption A7's warning and belongs in the Phase 7 and Phase 8 channel decision, but it also reshapes the development plan: building for a senior living or payer pilot at G4 is both the faster funding path (Series A capital is present, Inspiren $100M Sept 2025, SafelyYou $43M Jan 2025 [shared_capital 4.1]) and the more survivable one.

---

## 5. The recommended plan

| Decision | Recommendation | Rationale |
|---|---|---|
| Headcount | 3 engineers core through G2, add a 4th (CV/QA) for G3 to G4 | 3 is the discipline floor (section 2.3); the 4th lands on the false positive critical path (section 3) when field data starts flowing |
| Discipline mix | Head 1: embedded CV + mmWave DSP. Head 2: mobile + application. Head 3: backend + cloud + security. Head 4 (G3+): second CV plus QA and the ground truth pipeline | One engineer cannot cover embedded vision, iOS, and cloud well; this is the named tradeoff |
| Contract, do not hire | Industrial design, hardware DFM, FCC/UL certification, PERS monitoring, RAG content | Phase 4 build versus buy; these are bounded, external, and not continuous |
| AI multiplier | Plan at 1.15x blended; expect near neutral on the CV and embedded critical path | Section 0.2 |
| Non dilutive first | NIA SBIR Phase I at G2, Phase II at G4; NSF SBIR for the sensing/AI engineering | shared_capital 1.2, 1.4; every survivor did this |
| Channel target for G4 | Build the pilot for a senior living or payer partner, not DTC | Section 4.1; the comparables |

**Headline: approximately $1.35M engineering labor, approximately $1.8M to $2.0M all in, over approximately 27 engineering months to G4 at 3 engineers; comparables adjusted elapsed time to a fundable G4 is 3 to 4 years.**

---

## 6. Test plan by gate, and solving the ground truth problem

The ground truth problem is severe and under appreciated, and the architecture makes it harder on purpose: by design no video leaves the device (Phase 5), so nobody can centrally annotate footage to decide whether an alert was real. In a real home nobody is labeling video. Two questions must still be answered: was an escalated alert a true or a false positive (precision), and did the system miss a real fall (recall, the harder one, because you do not know what you did not detect). The plan below solves both without central video annotation.

### 6.1 Definitions, fixed before any measurement

| Term | Definition used |
|---|---|
| Escalated false positive | An alert that reached a human tier (caregiver push or PERS handoff) for which no fall plus long lie actually occurred, as adjudicated by the resident or caregiver. This is the metric that gets the product unplugged. The headline number |
| Suppressed nuisance detection | A low confidence detection gated out before escalation (duration gating, modality disagreement). Logged internally, not escalated. Not counted as an escalated FP |
| Missed fall (false negative) | A real fall plus long lie that produced no alert. The hardest to observe |
| Exit metric | Escalated false positives per home per month, and sensitivity on staged falls per install geometry |

### 6.2 The instrumentation, common to all gates

Every node logs, to the local encrypted buffer: event type, timestamp, model confidence, the contributing modalities and whether they agreed, and the derived pre and post event feature window (keypoint or radar point cloud derived features, never raw video, never raw point cloud). On escalation, the derived feature bundle plus the human adjudication label syncs to the cloud. A labeling console computes precision and recall from adjudications and staged fall logs. No raw modality ever leaves, consistent with Phase 5.

### 6.3 Gate by gate

| Gate | Setting | How ground truth is established (no central video annotation) | What is measured | Exit |
|---|---|---|---|---|
| **G1 Bench** | Desk hardware, recorded plus live | Public and self recorded fall datasets with known labels; scripted falls on a cushioned mat with a countable denominator; motion capture or instrumented walkway as the gait reference (OpenCap class comparator, Phase 4 3.1.4) | Detection accuracy on labeled data; gait speed error versus walkway (target approx 0.04 m/s) | Core detection works at stated accuracy |
| **G2 Self test (founder home)** | Founder's own home, 30 days continuous | The founder IS the ground truth oracle. (a) One tap confirm or deny on every alert plus a maintained event diary of real ADL, to catch false positives. (b) A staged fall protocol (cushioned, scripted, repeated across rooms and times of day) to measure sensitivity against a known denominator. (c) A locally retained, auto expiring on device verification clip that the FOUNDER, as the data subject, may review in their own home to adjudicate a disputed event; never uploaded, consistent with Phase 5 path 6. This is the one setting where local footage review is ethical, because the founder consents and reviews their own home. (d) A temporary reference sensor (a worn IMU or a second consented camera in the founder's home only) as a gold-ish reference to catch misses, removed before field | Escalated FP per day; sensitivity on staged falls; long lie timing accuracy | 30 days uptime; **characterized real world FP rate** (the make or break exit) |
| **G3 Friends and family (5 to 15 homes)** | Real homes, real older adults | You cannot annotate and cannot assume the founder oracle. Ground truth is built from converging weak signals: (a) one tap resident or caregiver adjudication on every escalated alert (precision labels). (b) A scheduled weekly caregiver diary and structured check in call to surface unreported real events, the recall proxy. (c) A staged fall run once per home at install by the field tech (sensitivity per real install geometry, which varies by room and furniture). (d) On device, locally retained, auto expiring verification snippets the RESIDENT may optionally review and share to adjudicate a disputed event, consent gated, never centralized. (e) A small reference instrument sub cohort (a few homes get a consented secondary sensor) to estimate the miss rate the self report cannot see. (f) Reconciliation against any real world incident that left an external trace: a fall that led to a call, an urgent care or ER visit, or a caregiver visit | Install time; retention; per home escalated FP rate across varied geometry; failure mode catalog; estimated miss rate from the sub cohort | FP rate and install and retention measured across real homes |
| **G4 Pilot (50 to 200 units)** | Structured cohort, senior living or payer site | Same adjudication and diary pipeline at scale; the reference instrument sub cohort continues on a sample; efficacy measured against the cohort baseline (fall rate, long lie duration, caregiver response time); the FTC gait substantiation study runs against an instrumented walkway on a sample | Efficacy evidence sufficient for a partner conversation; unit economics; escalated FP per home per month at target | Fundable pilot |
| **G5 to G6** | Limited then full commercial | Fleet wide adjudication telemetry becomes the continuous FP monitor; certification complete; a per install staged fall check becomes a standard commissioning step | Continuous FP and sensitivity monitoring; contribution margin | Commercial |

### 6.4 The load bearing ground truth moves

1. Sensitivity (did we miss falls) is measured by staged falls with a known denominator, not by waiting for real falls, because real falls are too rare and unobservable to yield a denominator in a small cohort. Staged falls per install also capture the geometry dependence that the literature says dominates.
2. Precision (were alerts real) is measured by one tap human adjudication at the moment of the alert, which is cheap, immediate, and does not require any footage.
3. The un observable misses (real falls that produced no alert and no external trace) are estimated, not measured, from a small consented reference instrument sub cohort and reconciled against external incident traces. This is the honest limit: in a no central video, no annotation design, the miss rate is an estimate with error bars, and the plan says so rather than pretending to a number it cannot get.
4. Local, consented, auto expiring, on device only clip review by the data subject is the ethical escape valve that lets a disputed event be adjudicated without ever centralizing video, preserving the Phase 5 privacy claim while still generating a label.

---

## Register Entries

Per framework section 9, staged for the register owner. This phase does not edit `research/registers/`.

### Sources (stage into registers/sources.md)

| Key | Source | URL | Date | Used for | Credibility |
|---|---|---|---|---|---|
| D1 | METR, Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity (RCT, 16 devs, 246 issues) | https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/ ; https://arxiv.org/abs/2507.09089 | 2025-07-10 / accessed 2026-07-10 | Low case: experienced devs 19 percent slower with AI on complex own code | HIGH result / MEDIUM transfer |
| D2 | METR, We are Changing our Developer Productivity Experiment Design (methodology walk back, selection effects) | https://metr.org/blog/2026-02-24-uplift-update/ | 2026-02-24 / accessed 2026-07-10 | Reason to hold the multiplier conservative | MEDIUM |
| D3 | Peng, Kalliamvakou, Cihon, Demirer, The Impact of AI on Developer Productivity: Evidence from GitHub Copilot (RCT, 95 contractors) | https://arxiv.org/abs/2302.06590 | 2023 / accessed 2026-07-10 | High case: 55.8 percent faster on greenfield JS task | HIGH result / LOW transfer |
| D4 | Google internal RCT approx 100 engineers, approx 21 percent faster (reported via secondary summaries) | https://addyo.substack.com/p/the-reality-of-ai-assisted-software ; https://www.index.dev/blog/ai-coding-assistants-roi-productivity | accessed 2026-07-10 | Mid case anchor | MEDIUM (secondary) |
| D5 | Fully loaded employee cost multiplier 1.25x to 1.4x, US knowledge workers | https://www.glencoyne.com/guides/fully-loaded-cost-us-employee ; https://scalearmy.com/blog/calculate-fully-loaded-cost-of-an-employee/ | accessed 2026-07-10 | Loaded multiplier 1.35x | HIGH |
| D6 | San Diego software engineer salary 2026 | https://www.levels.fyi/t/software-engineer/locations/greater-san-diego-area ; https://builtin.com/salaries/us/san-diego-ca/software-engineer ; https://www.glassdoor.com/Salaries/san-diego-software-engineer-salary-SRCH_IL.0,9_IM758_KO10,27.htm | accessed 2026-07-10 | San Diego base salary band | HIGH |
| D7 | Fred Brooks, The Mythical Man-Month (1975); n(n-1)/2 communication overhead | https://effectiviology.com/brooks-law/ | 1975 / accessed 2026-07-10 | Brooks coordination tax, communication path growth | HIGH |
| D8 | SafelyYou funding and history | https://www.safely-you.com/news/powered-by-43m-in-series-c-funding-safelyyou... ; https://www.prnewswire.com/news-releases/safelyyou-accelerates-growth-by-closing-19-5-million-series-a-funding-round-301378733.html ; https://www.nia.nih.gov/news/nia-funded-small-business-spotlight-safelyyou ; https://techcrunch.com/2025/01/28/ | accessed 2026-07-10 | Comparable: 2014-16 founded, Series A 2021, total >$100M, B2B pivot | HIGH |
| D9 | Nobi Series B and history | https://www.globenewswire.com/news-release/2025/01/28/3016061 ; https://xtalks.com/nobi-raises-37m-in-series-b-funding-... | 2025-01-28 / accessed 2026-07-10 | Comparable: 2018 founded, Series B $37M 2025, smart light, B2B senior care | HIGH |
| D10 | CarePredict funding history | https://www.crunchbase.com/organization/carepredict ; https://homehealthcarenews.com/2023/07/after-29m-fundraising-round-carepredict... | accessed 2026-07-10 | Comparable: 2013 founded, approx $46M over 5 rounds across a decade, DTC/home care grind | MEDIUM |
| D11 | Vayyar funding history | https://techcrunch.com/2022/06/06/imaging-sensor-startup-vayyar-lands-108m... ; https://tracxn.com/d/companies/vayyar/ | accessed 2026-07-10 | Comparable: 2011 founded, approx $296M over 5 rounds, unicorn 2022, multi market | MEDIUM |
| D12 | Cherry Labs / Cherry Home seed | https://techcrunch.com/2018/12/21/cherryhome-raises-5-2m... ; https://venturebeat.com/ai/cherry-labs-raises-5-2-million... | accessed 2026-07-10 | Comparable/failure: 2016 founded, $5.2M seed 2018, stalled, DTC camera caution | MEDIUM |
| D13 | Tellus You Care acquired by AIP Healthcare | https://www.linkedin.com/company/tellus-you-care ; https://tracxn.com/d/companies/tellus/ | approx Oct 2024 / accessed 2026-07-10 | Comparable/soft landing: 2017 founded, acquired, pivoted to Japan; DTC caution | MEDIUM |
| D14 | Lively / GreatCall / Best Buy consolidation | https://en.wikipedia.org/wiki/Lively_(company) ; https://medcitynews.com/2015/12/greatcall-acquires-lively... | accessed 2026-07-10 | Reference: category exits are PERS/channel; Best Buy $800M GreatCall 2018 | HIGH |

### Comparables / competitors (stage into registers/competitors.md)

| Company | Product | Founded | Total raised / key round | Status | Lesson for the dev plan | Confidence |
|---|---|---|---|---|---|---|
| SafelyYou | AI fall detection, memory care | 2014-16 | >$100M; Series A $19.5M 2021 | Alive, B2B senior living | 6 yr to Series A; SBIR funded early; pivoted off DTC | HIGH |
| Nobi | Smart light fall detection | 2018 | Series B $37M 2025 | Alive, B2B nursing homes | Direct bulb analog; lives in B2B, took ~7 yr | HIGH |
| CarePredict | Wearable + environment monitoring | 2013 | approx $46M / 5 rounds | Alive, slow | A decade, capital hungry, DTC grind | MEDIUM |
| Vayyar | 60 GHz imaging radar | 2011 | approx $296M | Unicorn 2022 | Radar real; scaled as multi market silicon, not elder product | MEDIUM |
| Cherry Labs | Home AI cameras | 2016 | $5.2M seed 2018 | Stalled | DTC camera thesis, under funded, no growth round | MEDIUM |
| Tellus You Care | Wireless sensor monitoring | 2017 | UNKNOWN | Acquired (AIP Healthcare) ~2024 | DTC did not sustain; soft landing to Japan | MEDIUM |

### Funding (stage into registers/funding.md)

Cross references existing shared_capital_landscape entries. New evidence tie: SafelyYou Series A $19.5M (2021-09-16) and NIA SBIR Phase I (2017) as the non dilutive plus dilutive sequence a comparable actually used; Nobi Series B $37M (2025-01-28) as the smart light B2B comparable. No new fund identified this phase; the relevant funds (Insight, Touring, Angelini, NIA SBIR, NSF SBIR) are already logged in `shared_capital_landscape.md`.

---

## Open Questions

1. Real world false positive rate per fall modality is UNKNOWN and is the critical path (section 3). It cannot be resolved by planning; it is characterized at G2 and refined at G3. Every timeline number downstream of it is provisional until it is measured.
2. The AI velocity multiplier is contested and the strongest study (METR) walked back its methodology [D2]. The 1.15x planning figure is a judgment, not a measured constant. If the real blended multiplier on this product's hard critical path work is below 1.0 (the METR result on complex code), the section 2 timelines extend by roughly 20 percent.
3. The Google 21 percent mid anchor [D4] is from secondary summaries; the primary study parameters were not read directly. Confidence MEDIUM.
4. Two G4 non labor lines are UNKNOWN: the RAG health content license (Phase 4 OQ5) and the PERS monitoring partner per seat terms (Phase 4 OQ6). Both could move the all in G4 figure.
5. FTC gait substantiation study cost ($30K to $80K) is an estimate, not a quote (framework flagged it as a real line at G3/G4). The instrumented walkway validation scope and site are unpriced.
6. The miss rate (false negatives) in the field is estimable but not directly measurable in a no central annotation design (section 6.4). The error bars on the estimate depend on the reference instrument sub cohort size, which is a G3 design decision not yet made.
7. The comparables adjusted elapsed time of 3 to 4 years to a fundable G4 (section 4.1) is an analogy, not a bottom up schedule; it depends on the channel choice (DTC versus senior living or payer) which is owned by Phase 7 and Phase 8.
8. The Brooks coordination decay (5, 12, 20 percent) is a moderate modeling assumption, not measured for this team. A more coupled codebase or a distributed team would deepen the tax and lengthen the multi engineer timelines.

## Assumptions Made

1. Fully loaded engineer cost is $200,000 per year ($3,846 per week), blended across generalist and specialist roles, at a 1.35x loaded multiplier on an approx $148,000 base [D5][D6]. If California benefits and the embedded/DSP specialist premium push the blend to $220,000, the labor lines rise approximately 10 percent. Impact MEDIUM.
2. Raw effort is approximately 355 engineer weeks to G4, built from the Phase 4 per subsystem week estimates plus estimates for the disciplines Phase 4 did not cost (firmware, backend infra, ID, cert management, QA, ops). These are integration and hardening estimates, not build from scratch, and are MEDIUM confidence. If the fall false positive work (the largest ML bucket) runs long, which is the most likely overrun, G2 to G4 extends.
3. The AI multiplier is 1.15x blended (mid), applied differentially, with a 0.95x low floor and a 1.40x high ceiling. Assumes AI helps the app and glue and does little for the safety critical CV and embedded work. Impact HIGH on the headline timeline.
4. The Brooks coordination tax uses a per head efficiency decay of 5, 12, 20 percent at 2, 3, 4 engineers, grounded in n(n-1)/2 but not measured. Impact MEDIUM.
5. The three discipline floor (embedded CV, mobile, backend) is treated as a hard constraint, so n=1 is judged infeasible to a safety standard regardless of calendar time. This is an engineering judgment, HIGH confidence given the breadth of the system.
6. Object memory and free form scene query are DEFERRED to v2 (Phase 0, Phase 4), so no in home inference hub and no 16 to 30 plus weeks are in the v1 WBS. If they re enter v1, add the hub BOM and the weeks. Impact HIGH if wrong.
7. Hardware NRE, pilot unit cost, and certification are carried from Phase 3 without re deriving. The FTC substantiation and content and PERS lines are estimates or UNKNOWN.
8. The comparables are used as a sanity check on elapsed time, not as a bottom up schedule. Assumes the category dynamics (6 plus years to Series A, B2B survival, DTC stall) transfer to this venture. Impact MEDIUM.

## Confidence Summary

Overall confidence: HIGH on the structure and the critical path, MEDIUM on the absolute timeline and cost numbers.

- HIGHEST confidence: the longest pole is real world false positive rate reduction, not features, and it is bound by calendar time in real homes rather than by engineer hours or AI; certification is the second pole and is a fixed duration external process; the discipline floor is three engineers and n=1 is infeasible to a safety standard because one engineer cannot do embedded vision, iOS, and cloud well; the ground truth problem is real and is solved by staged falls for sensitivity, one tap human adjudication for precision, and a small reference sub cohort plus external incident reconciliation for the un observable miss rate, all without central video annotation.
- HIGH confidence: the comparables contradict any lean fast DTC timeline. Nobody in the category reached a fundable pilot in under approximately 6 years, every survivor used non dilutive funding early and pivoted to B2B, and every DTC consumer play stalled or soft landed. The engineering estimate of approximately 27 months to G4 at 3 engineers is the engineering floor; the comparables adjusted elapsed time is 3 to 4 years.
- MEDIUM confidence, the numbers: the 355 raw engineer weeks, the 1.15x AI multiplier (the evidence is contested and the strongest study walked back its method), the Brooks decay, the $200,000 loaded cost, and therefore the approximately $1.35M labor and approximately $1.8M to $2.0M all in to G4. These are defensible planning figures, not quotes.
- The single load bearing conclusion, HIGH confidence: build with 3 engineers covering the embedded CV, mobile, and backend disciplines, add a 4th on the false positive critical path at G3, contract hardware ID and certification and PERS, fund the early gates with NIA and NSF SBIR, and plan for the false positive reduction loop and certification, not feature development, to set the calendar. Budget approximately $1.8M to $2.0M and 3 to 4 elapsed years to a fundable G4.
