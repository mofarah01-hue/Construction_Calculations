# CONCEPT A: ELDER HOME MONITORING
## Business Case for Funding Decision

Governed by `00_framework.md`. Positioning is general wellness (framework section 2), settled with regulatory counsel and not relitigated here. This document synthesizes Phases 0 through 8 (`research/a/phase0_scope.md` through `phase8_businesscase.md`), the regulatory risk register, and the shared research spine. Every number is traceable to the phase named in parentheses. No new figures are introduced. Confidence tags are HIGH, MEDIUM, LOW per framework section 5.

Prepared 2026-07-10.

---

# PART 1: EXECUTIVE SUMMARY

## Recommendation

**Fund to a staged G4 pilot, conditional on the kill gate. Fund it as a B2B, operator sold, distributed sensor product, not as the consumer light bulb the concept describes.** Commit approximately $1.8M to $2.0M to reach G4 (Phase 6), sequenced non dilutive first, with an absolute stop at gate G2 if the field false positive rate cannot be characterized below target (kill criterion K1). Do not fund a direct to consumer (DTC) launch. Do not fund the E26 bulb.

The technology is real and the market need is real. The concept as literally written is not the product, and one revenue pool the concept implicitly counts on is legally closed to it. Both findings are load bearing and both are settled across multiple phases.

## The core thesis

Five conclusions, each established independently and each pointing the same direction:

| # | Thesis | Where established |
|---|--------|-------------------|
| 1 | **The E26 bulb does not survive.** It fails on two independent, disqualifying grounds: switched power (the monitor dies when the resident turns off the light, a safety defect with no fix short of adding a mains node that makes the bulb redundant) and viewing angle (a nadir ceiling view cannot measure the flagship gait and sit to stand metrics, which validate only from a side or oblique view). | Phase 2 (1.2.1, 1.2.2, 1.2.3); Phase 1 (5.3) |
| 2 | **A distributed sensor mesh does survive.** The evidence rich, lowest cost markers (nocturia, life space, circadian rhythm, sleep, out of home trips) want a $13 to $25 per node PIR and door contact mesh, not a camera. The camera earns its place once, obliquely, in one shared room, for gait, hazard inventory, and one fall path. Architecture A1: PIR and door mesh, one bathroom radar node, one under mattress bed mat, one oblique camera, one hub. T4 hybrid compute with a T1 local fall path so no raw video leaves. | Phase 1 (5.2, headline); Phase 2 (1.4, primary A1) |
| 3 | **Long lie detection and the environmental hazard inventory are the highest value defensible features.** Long lie (time on the floor) is the single highest value feature in the catalog, event and duration detection with the lowest claim risk, and it directly changes an outcome. The hazard inventory (loose rugs, clutter, dim stairs) is RCT backed (26 percent fall rate reduction, Cochrane), requires zero inference about the person, is actionable by the caregiver in an afternoon, and no competitor emphasizes it. | Phase 1 (ranks 1 and 6; P7, P12) |
| 4 | **The highest value channel is per bed to senior living operators, not DTC.** Operators are concentrated (approximately 1,000 operators control most of 1.2M beds), financially motivated (they own fall liability), high margin (approximately 67 percent recurring), and low churn (annual facility contracts). Every recent large check in the category landed on a company selling this way: Sage $65M (2026-03), Inspiren $100M (2025-09), SafelyYou $43M (2025-01), Nobi EUR 35M (2025-01). The Amazon Alexa Together shutdown (2025-05) is the warning: the caregiver dashboard subscription this concept centers on is precisely the layer that the company with the lowest CAC on earth found people would not pay for. | Phase 7 (2.2, 3); Phase 8 (2.1, 3.2) |
| 5 | **The central strategic tension: the reimbursement pool requires medical device positioning the wellness lane forbids.** RPM and RTM are the largest and most durable revenue pool in aging in place, and every device paying code is gated behind FDA 201(h) medical device status. The 21st Century Cures Act defines general wellness software by its exclusion from that status. The concept cannot simultaneously be a general wellness product and bill RPM or RTM. This is structural, not a future event, and it caps the revenue map. | Phase 7 (4.2); Phase 8 (B7) |

## The capital ask and what it buys

| Stage | Gate | Instrument | Amount | Buys |
|---|---|---|---|---|
| Non dilutive 1 and 2 | G1 to G2 | NSF SBIR Phase I, NIA SBIR Phase I | up to $305K + up to $300K ($500K under AD/ADRD framing) | Sensing and on device model engineering; founder home characterization of the field false positive rate |
| Angel / pre seed | G2 | SAFE or priced | $500K to $1.5M | Carries the 3 engineer discipline floor team through G2/G3 |
| Seed | G3 | Priced | $3M to $6M | The 4th engineer on the false positive critical path; 5 to 15 home G3; first operator pilot LOIs |
| Non dilutive 3 and 4 | G4 | NIA SBIR Phase II, NSF SBIR Phase II | up to $2.0M ($2.5M AD/ADRD) + up to $1.25M | The 50 to 200 unit cohort; efficacy evidence; FTC gait substantiation study |
| Series A | G4 to G5 | Priced | $12M to $18M | Certification, manufacturing, operator sales motion, scale toward breakeven |

The immediate ask is the path to G4: **approximately $1.8M to $2.0M all in over approximately 27 engineering months** (Phase 6 2.5), funded primarily by approximately $3.3M to $4.6M of winnable NSF and NIA non dilutive plus a modest seed, sharply reducing early dilution (Phase 8 3.1). Comparables adjusted elapsed time to a fundable G4 is 3 to 4 years, not 27 months; the engineering is the shorter part (Phase 6 4.1). Full path to cash flow breakeven is approximately $30M to $45M cumulative capital and 5 to 7 years, at roughly 18,000 to 28,000 beds under contract (Phase 8 1.1).

## Top risks and kill criteria

| Rank | Risk | The number | Kill criterion |
|---|---|---|---|
| 1 | **Field false positive rate (K1, the primary kill risk).** Lab fall detection accuracy collapses in the field: 13 algorithms at approximately 94 percent scripted sensitivity fell to approximately 57 percent on real falls; one real deployment logged 84 alarms of which 83 were false. A 2 percent per event false positive rate is dozens of nuisance alerts per day. This is the "unplugged in month two" failure. | Escalated false positives per home per month | K1: cannot drive below approximately 1 per home per month without sensitivity falling below what a paying operator accepts, after the full ground truth effort. Resolves at G2, confirmed G3. If K1 fails, stop. Nothing downstream matters. |
| 2 | **No operator or payer will pay at margin (K2).** The recommended channel is the only venture scale path. | Pilot to contract conversion at positive contribution margin | K2: no operator, agency, or payer signs a per bed or PMPM pilot at positive margin after a characterized FP rate and efficacy data exist. Resolves G3 to G4. |
| 3 | **DTC is the only channel and its economics do not close (K3).** Base case DTC LTV:CAC is approximately 1.4x. This is the Alexa Together outcome with real CAC. | Blended DTC CAC vs consumer churn | K3: DTC only, CAC above approximately $250 against churn above approximately 3 percent per month. Resolves G3 to G4. |
| 4 | **FTC gait substantiation (K4) and regulatory envelope closure (K5).** The gait speed claim must validate against an instrumented walkway; state biometric and FDA lane shifts could close the passive in home capture envelope. | Gait error bars vs claim; enforcement precedent | K4 and K5 reshape rather than always kill, but each can be terminal in combination. |

Confidence: HIGH on the five thesis conclusions and the kill criteria; MEDIUM on the absolute scenario numbers; LOW on three values that remain UNKNOWN (PERS churn, per bed price, real DTC CAC), which are carried as flagged assumptions and were never invented (Phase 7, Phase 8).

---

# PART 2: THE CASE

## 2.1 Scope and claims

The feature inventory resolves to 6 CORE, 10 DIFFERENTIATOR, 2 LATER, 3 BLOCKED (Phase 0 section 3).

| Class | Features |
|---|---|
| CORE (v1, no product without it) | Fall detection; fall notification and escalation; long lie detection; step, mobility, and life space patterns; trend reporting; red flag escalation layer |
| DIFFERENTIATOR (v1 if affordable) | Gait metrics; sway and steadiness; bathroom frequency; kitchen use; sleep location; time in bed; chair transfers; conversational check in; medication reminders; environmental hazard inventory |
| LATER (v2) | Object location memory; caregiver natural language query |
| BLOCKED (cannot ship as a stated output) | Fall risk prediction score; cognitive decline inference; mood or depression inference |

The governing line (framework section 2) holds throughout: self report is not a claim, measurement and trend are not a claim, inference of a named disease from passive data is a claim. The three BLOCKED features are not abandoned; each has an available reframing (steadiness classification, self report trend plus clinician prompt, mood journal). The most important Phase 0 finding: object memory and natural language scene query force a hub and belong to a later version; the founder assumption that "compute happens on the camera" (A2) is disproven for those features (Phase 0 section 5).

The claims matrix (Phase 0 section 4) assigns every shippable feature a defensible phrasing, its data type, the permitting precedent (Apple Watch fall detection and mobility metrics, Oura deviation signals), the phrasing that would cross the line, and the FTC validation evidence required. The single most expensive validation line is camera derived gait speed accuracy against an instrumented walkway.

## 2.2 Markers and caregiver report

Phase 1 built the catalog first, on purpose, so the markers define the sensing requirement rather than a chosen sensor defining what gets measured. The v1 shortlist, ranked by (actionability x evidence) / sensing cost:

| Rank | Marker | Evidence | Sensing cost |
|---|---|---|---|
| 1 | Long lie detection | HIGH (P7: 30 percent of fallers 90+ lay 1 hour or more) | Shared with fall path |
| 2 | Fall event detection | HIGH need, engineering risk on false positives (P17) | Shared sensor |
| 3 | Nighttime bathroom frequency | HIGH (P10: 3+ voids approximately 2x mortality) | Lowest (door + PIR) |
| 4 | Life space contraction | HIGH construct (P9: 10 point LSA decline raised 6 month mortality odds 72 percent) | Lowest (PIR + door) |
| 5 | Gait speed trend | HIGH (P1, P2: vital sign level; camera validated P3, oblique view only) | Moderate (camera) |
| 6 | Home fall hazard inventory | HIGH (P12: 26 percent fall rate reduction, Cochrane) | Low (one time camera scan) |

Ranks 7 through 15 (circadian rhythm, sit to stand, out of home trips, sleep, contactless vitals, kitchen, self reported mood, medication response, stove safety) complete the v1 set. The load bearing Phase 1 conclusion: the single bulb camera cannot observe most of the highest evidence, lowest cost, most defensible markers; the evidence points to a distributed mesh plus a bed mat plus one oblique camera. Gait speed survives as a trend and substantial change signal (camera error approximately 0.04 m/s sits below the 0.10 m/s substantial change threshold), but only from an oblique or side view, never a nadir ceiling bulb view (Phase 1 5.3).

The caregiver report (Phase 1 section 4) is designed for a busy remote adult child: default state is a single green line, detail is pull not push, escalations interrupt and trends do not. Every trend line pairs the change with a specific action. A trend with no action is deleted from the report, enforcing the framework rule that a marker with no action is telemetry, not a product. The immediate fall alert ("FALL DETECTED / Bathroom, 2:14pm. Still on the floor (4 min)") is the product.

## 2.3 Architecture and the bulb rejection

Phase 2 is the decisive phase; everything downstream is its consequence. Five architectures were scored against the v1 shortlist:

| Architecture | Gait | Fall | Bathroom | Privacy | Per home BOM (est) | Verdict |
|---|---|---|---|---|---|---|
| A0 Single ceiling E26 bulb camera (founder concept) | 1 | 2 | 1 | 2 | ~$40 to $90 | REJECT. Cannot see the shortlist |
| A1 Distributed mesh + one oblique camera | 4 | 5 | 5 | 4 | ~$180 to $360 | PRIMARY |
| A2 All radar + PIR/door mesh, no camera | 3 | 5 | 5 | 5 | ~$250 to $600 | FALLBACK |
| A3 Oblique cameras + radar in private rooms | 5 | 5 | 5 | 2 | ~$300 to $600 | Reject (privacy, cost) |
| A4 WiFi CSI whole home | 1 | 1 | 3 | 5 | Low | REJECT. Not productizable for fall/gait today |

The bulb (A0) fails on two independent disqualifying grounds. Switched power: when the resident turns off the light the monitor is dead and the caregiver may not know; the only robust fix is a continuously powered node, which is not a bulb (Phase 2 1.2.1). Viewing angle: nadir geometry foreshortens the planes where gait speed, step length, and sway live, degrading accuracy by up to 60 percent with no published validation, so the bulb places the camera where the flagship measurement claim cannot be substantiated under FTC standards (Phase 2 1.2.2). Founder assumption A1 is disproven.

A1 is the only architecture that observes the full shortlist at defensible cost while keeping cameras out of the two private rooms. Radar is the only whole room modality that covers the bathroom, the highest fall risk room and a hard no camera room, in darkness and steam. Compute is T4 hybrid: fall and long lie on the node (T1, no video out); assistant and trend layer in the cloud on derived features only. A2 (all radar, zero cameras) is a genuine privacy maximal fallback if any camera proves a hard adoption blocker; it keeps the two highest value features and the bathroom at the cost of the hazard inventory and sit to stand detail (Phase 2 1.4).

## 2.4 Hardware, BOM, and retail vs competitors

The A1 home is 13 devices over 5 zones (Phase 3). Silicon selection: the camera node uses the Sony IMX500 in sensor inference paired with a low cost Allwinner or SigmaStar host, the only path where pixel data never leaves the sensor package (the load bearing privacy claim), and thermally viable in a sealed fanless node where Jetson and RK3588 are not. The radar node runs its own fall detection on the TI IWR6843 on chip DSP.

| Metric (per home system) | 1 | 100 | 1k | 10k | 100k |
|---|---|---|---|---|---|
| Hardware BOM | 485 | 306 | 224.50 | 180 | 148 |
| Landed cost | 655 | 404 | 292 | 227 | 181 |
| COGS | 730 | 452 | 327 | 254 | 201 |

The three mains nodes (radar, camera, hub) are approximately 68 percent of BOM; the 9 piece mesh that carries the highest evidence markers is only approximately $50 (Phase 3 2.5). Hardware NRE is approximately $80,000 to $210,000, dominated by 60 GHz radar intentional radiator testing and a triple UL/ETL listing; certification is the most underestimated line and lands at G5.

Against the market (Phase 3, implied retail):

| Product | Hardware | Recurring | Note |
|---|---|---|---|
| This system (A1) | Implied $400 to $650 at margin; realistic $299 to $499 subsidized | Service TBD | Broader marker set than any single competitor |
| Vayyar Care | $250/device, ~3/home ($750) | $20/mo | Falls only |
| CarePredict @Home | $499 | $69.99/mo | Wearable based |
| Envoy at Home | $399 | $99/mo | PIR/contact class |
| Amazon Alexa Emergency Assist | Uses existing Echo | $7.99/mo | Response only; caregiver monitoring discontinued 2025-05 |

The A1 COGS of approximately $201 to $327 at volume supports a $299 to $499 subsidized price, competitive with CarePredict and Envoy and cheaper than three Vayyar nodes, while delivering a broader marker set. The strategic question the business case must answer: whether that breadth justifies the added hardware cost against a market that has repeatedly failed to sustain consumer hardware plus subscription (Phase 3 2.5).

## 2.5 Software and open source licensing

Almost every perception subsystem has a clean `Apache-2.0` or `MIT` option that runs on non NVIDIA silicon (Phase 4). The load bearing license finding: two of the most cited pose libraries are commercially poisoned. OpenPose is CMU non commercial only; Ultralytics YOLO Pose is `AGPL-3.0`, which forces open sourcing the entire product or a paid Enterprise License. The clean set is MoveNet, MediaPipe BlazePose, and RTMPose, all `Apache-2.0`. Founder assumption A6 (NVIDIA is the right start) is disproven: NVIDIA offers commercially usable pose models but its TensorRT and DeepStream runtime locks the BOM to Jetson class silicon, contradicting the IMX500 direction; NVIDIA is optional, not necessary (Phase 4 3.1.2).

The entire ADL, spatial, sleep, toileting, and circadian layer, which is the evidence rich backbone, runs on deterministic state machines and classical statistics over the mesh, with zero neural inference. The only ML in the sensing layer is pose (gait, sit to stand, hazard) and the fall classifier (Phase 4 3.2). The fall detector's real world false positive rate, not benchmark sensitivity, is the make or break; the fix is duration gated long lie plus modality confirmation (radar plus pose agreement), not a better single classifier (Phase 4 3.1.3). The two hard, cannot buy, safety critical build items are the fall duration gating logic and the escalation state machine. The correct buys are the radar node, the assistant cloud API for the few frontier turns (under $1 per resident per month), the RAG health content, and the PERS emergency monitoring (Phase 4 3.6). Do not build a 24/7 call center; do not build an in house 911 auto dialer.

## 2.6 Privacy and the "no video leaves" posture

The strongest privacy claim in the category is defensible, conditionally (Phase 5). "Raw video is processed on the device and raw video is not transmitted to our servers" is true if and only if eight enumerated code paths (normal inference, debug builds, OTA, crash dumps, remote support, verification clips, model improvement, physical compromise) are affirmatively closed and audited. The decisive control is on sensor inference (IMX500), which converts the promise from a policy assertion into a hardware property: pixels are consumed inside the sensor package and only a metadata tensor crosses to the application SoC. The absolute claim ("your video never leaves your home") is prohibited (Phase 5 section 2).

Two consent facts are load bearing. First, the resident is the data subject and the caregiver is the buyer; these are different people with divergent interests, so the product implements a role and capacity model, not a single owner account, and covert operation is not an available configuration (Phase 5 section 3). Second, MHMDA is the binding privacy constraint: this product's home activity and health inference data is squarely consumer health data, so the whole architecture is built to MHMDA whether or not gait is a biometric identifier. Twelve all party consent states force a no retained audio, wake word only design nationally (Phase 5 section 4). HIPAA attaches through the channel, not the product: a home health agency channel converts the product into a business associate and imposes the full Security Rule from day one. The breach story the architecture permits is materially better than a cloud video product: the company cannot leak video it never received and cannot leak a corpus it never assembled (Phase 5 section 5).

## 2.7 Development plan and cost to each gate

Approximately 355 raw engineer weeks (approximately 6.8 engineer years) to reach a G4 pilot (Phase 6 1.1). The AI velocity multiplier is planned at 1.15x blended and applied differentially (high on app and glue, near neutral on the safety critical CV and embedded critical path), because the strongest study (METR) found experienced developers 19 percent slower on complex code they already know, exactly the profile of the fall false positive loop (Phase 6 0.2).

| Headcount | Discipline coverage | Calendar time to G4 | Engineering labor |
|---|---|---|---|
| 1 | One of three disciplines | ~5.9 years | ~$1.19M — INFEASIBLE to a safety standard |
| 2 | Two of three, a persistent gap | ~3.1 years | ~$1.25M |
| 3 | The discipline floor (embedded CV, mobile, backend) | ~2.3 years (27 months) | ~$1.35M — RECOMMENDED |
| 4 | Floor plus a 2nd CV/QA head on the FP critical path | ~1.9 years (22 months) | ~$1.49M |

The discipline floor is three: one engineer cannot do embedded vision, iOS, and cloud well, and the discipline most likely to be weak (embedded CV) is exactly the safety critical fall path. The fourth head is worth it only because it lands on the false positive critical path (Phase 6 2.3, 2.4).

| Line | Estimate |
|---|---|
| Engineering labor, 3 engineers, ~27 months | ~$1.35M |
| Hardware NRE | $80,000 to $210,000 |
| Pilot hardware, 200 systems | $65,000 to $90,000 |
| FTC gait substantiation study | $30,000 to $80,000 (UNKNOWN, estimated) |
| RAG content license; PERS per seat | UNKNOWN |
| **All in to G4** | **~$1.8M to $2.0M** |

The longest pole is not features. It is real world false positive rate reduction on the fall and long lie path (bound by calendar time in real homes, not engineer hours or AI), followed by certification (a fixed duration external lab process). The ground truth problem is severe and made harder by design (no video leaves, so nobody can centrally annotate footage): the plan solves it with staged falls for sensitivity, one tap human adjudication for precision, and a small consented reference sub cohort plus external incident reconciliation for the unobservable miss rate (Phase 6 sections 3, 6). The comparables are uniform and contradict any lean fast DTC timeline: nobody in the category reached a fundable pilot in under approximately 6 years, every survivor used non dilutive funding early and pivoted to B2B, and every DTC consumer play stalled or soft landed (Phase 6 4).

## 2.8 Market, channel, and reimbursement

Bottom up DTC sizing (Phase 7 1.1): 16.2M US adults 65+ living alone narrows through living adult child (0.80), remote child (0.25), and ability to pay (0.60) to a SAM of approximately 2.0M households, approximately $840M/yr subscription ceiling. A well executed DTC only business captures $40M to $80M ARR at maturity: a real business, not a venture scale outcome on DTC alone, and the number corroborates the founder's own warning (A7).

Channel ranking on CAC to margin (Phase 7 3):

| Channel | Verdict |
|---|---|
| Senior living operators (per bed) | BEST. Concentrated buyer, high margin, large contracts, buyer owns fall liability. SafelyYou's proven lane |
| Home care agencies | Close second. Sensi.ai's proven lane |
| DTC consumer subscription | Fast but CAC and churn bound; the Alexa Together graveyard |
| Health systems / ACOs | Current Health's graveyard; requires medical device positioning |

The failures are the instructive part. Amazon Alexa Together (dead 2025-05) is the most instructive: a $19.99/mo subscription from the company with the lowest CAC on earth could not sustain the caregiver activity feed, so Amazon kept only professional emergency response and discarded the dashboard. The dashboard layer this concept centers on is precisely the layer that had no willingness to pay. Cherry Home (camera based, the closest architectural analog to the concept's default) is dormant since 2019 (Phase 7 2.2).

Reimbursement, the central strategic tension (Phase 7 4.2): RPM (99453/99454) and RTM require the monitoring device to meet the FDA 201(h) definition. The 21st Century Cures Act removed general wellness software from that definition. A product defined by exclusion from device status cannot serve as the qualifying device, and no code pays a non device wellness product. The routes out are all costly and only option (c), forgo reimbursement and live on operator per bed plus agency plus payer PMPM, is consistent with the positioning. That removes the single largest revenue pool from the model.

## 2.9 Business case and capital

Recurring unit economics (Phase 8 0.1): operator per bed yields approximately $20/month gross profit at approximately 67 percent margin; consumer DTC yields approximately $23/month but at a fatal 1.4x LTV:CAC after a $200 CAC and hardware subsidy. The pricing decision is model 4, per bed per month to operators ($25 to $35/bed), the only model where the buyer is concentrated, financially motivated, high margin, and low churn, with hardware absorbed by the contract (Phase 8 2.1).

| Scenario | Homes | ARR | Annual net burn | Cumulative capital | Interpretation |
|---|---|---|---|---|---|
| Small | 300 | ~$112K | ~$1.5M | $3M to $5M | Prove it (G4). No revenue thesis |
| Mid | 5,000 | ~$1.9M | ~$4.5M to $5.5M | $14M to $22M | Bridge it. A Series A waypoint |
| Large | 50,000 | ~$18.6M | breakeven to ~($4M) | $30M to $45M | Earn it. Breakeven at ~18K to 28K beds |

Capital is sequenced non dilutive first, because every category survivor did exactly this. NSF plus NIA non dilutive potential is approximately $3.3M to $4.6M, enough to fund G1 to G4 with only a modest angel bridge (Phase 8 3.1). The capital thesis is confirmed by fresh, dated, named deals flowing to operator sold fall monitoring: Sage $65M (2026-03), Inspiren $100M (2025-09), SafelyYou $43M (2025-01), Nobi EUR 35M (2025-01). The recommended per bed model is the one the market is funding right now (Phase 8 3.2).

---

# PART 3: APPENDICES

## Appendix A: Traceability of key numbers to phases

| Number | Value | Phase |
|---|---|---|
| System COGS at 1k / 100k | $327 / $201 | Phase 3 2.5 |
| System hardware BOM at 1k | $224.50 | Phase 3 2.5 |
| Mains nodes share of BOM | ~68 percent | Phase 3 2.5 |
| Hardware NRE | $80,000 to $210,000 | Phase 3 2.5 |
| Realistic subsidized retail | $299 to $499 | Phase 3 2.5 |
| Raw engineer weeks to G4 | ~355 (~6.8 engineer years) | Phase 6 1.1 |
| Engineering labor to G4, 3 engineers | ~$1.35M | Phase 6 2.4 |
| All in to G4 | ~$1.8M to $2.0M | Phase 6 2.5 |
| Engineering time to G4, 3 engineers | ~27 months | Phase 6 2.4 |
| Comparables adjusted elapsed to G4 | 3 to 4 years | Phase 6 4.1 |
| AI velocity multiplier (planning) | 1.15x (0.95x to 1.40x range) | Phase 6 0.2 |
| Loaded engineer cost | $200,000/yr ($3,846/wk) | Phase 6 0.1 |
| Camera gait speed error (oblique) | ~0.04 m/s RMSE | Phase 1 5.3 (P3) |
| Gait substantial change threshold | 0.10 m/s | Phase 1 (P2) |
| Real world fall sensitivity collapse | ~94 percent lab to ~57 percent field | Phase 4 3.1.3 (P17) |
| Long lie prevalence | 30 percent of fallers 90+ lay 1hr+ | Phase 1 (P7) |
| Hazard reduction (Cochrane) | 26 percent fall rate reduction | Phase 1 (P12) |
| DTC SAM | ~2.0M households, ~$840M/yr | Phase 7 1.1, 1.2 |
| DTC mature ARR ceiling | $40M to $80M | Phase 7 1.2 |
| Senior living beds | ~1.2M across ~30,600 to 33,000 communities | Phase 7 1.3 |
| Operator concentration | ~1,000 operators control most of 1.2M beds | Phase 7 3 |
| PERS subscription band | $25 to $50/mo (avg ~$37) | Phase 7 6.1 |
| 65+ PERS penetration | 9 percent, flat | Phase 7 6.2 |
| Adult child purchase intent | fell 39 percent (2023) to 22 percent (2026) | Phase 7 6.2 |
| Operator per bed GP | ~$20/mo at ~67 percent margin | Phase 8 0.1 |
| Consumer DTC LTV:CAC | ~1.4x | Phase 8 0.3 |
| Cumulative capital to breakeven | $30M to $45M | Phase 8 1.1 |
| Breakeven scale | ~18K to 28K beds, ~5 to 7 years | Phase 8 1.1, 1.3 |
| Non dilutive potential (NSF + NIA) | ~$3.3M to $4.6M | Phase 8 3.1 |
| Assistant LLM cost | under $1/resident/mo | Phase 4 3.4.3 |

## Appendix B: Risk register summary

Full register in Phase 8 section 5 and `regulatory_risk_register.md` (R1 to R9).

| ID | Risk | Likelihood | Impact | Primary mitigation |
|---|---|---|---|---|
| B1 | Field false positive rate cannot be driven low enough (the kill risk) | HIGH | SEVERE | Staged falls, one tap adjudication, duration gating, modality fusion; characterize at G2; 4th engineer lands here |
| B2 | IMX500 model fit fails; costlier SoC, weaker privacy claim | MEDIUM | MODERATE | Fallback to Ambarella CV25 or RK3576; claim degrades from "pixels never leave sensor" to "no video leaves home" |
| B3 | FDA device creep: a wellness output drifts into a screening claim (R1) | MEDIUM | SEVERE | Claims linter in CI blocks named disease inference from passive data |
| B4 | FTC substantiation: gait speed claim unvalidated (R2) | HIGH | HIGH | Fund the instrumented walkway study at G4; ship unvalidated metrics as own baseline trends without accuracy claim |
| B5 | State biometric privacy (BIPA/CUBI/MHMDA) (R4) | HIGH | SEVERE | Consent architecture first class; on device inference; no voice template; geofence by state |
| B6 | All party consent audio from the assistant (R6) | MEDIUM | HIGH | Wake word gated, on device STT, no retained audio, visible indicator |
| B7 | Reimbursement foreclosure (the central tension) | HIGH (structural) | HIGH | Do not chase reimbursement; live on operator, agency, payer PMPM |
| B8 | DTC CAC to churn does not close (Alexa Together graveyard) | HIGH for DTC | SEVERE for DTC | Lead with operator per bed, not DTC |
| B9 | Operator sales cycle long (6 to 12 mo), cash burns | MEDIUM | HIGH | Non dilutive plus seed; parallel pilots; AARP AgeTech Collaborative for warm access |
| B10 | Category history: nobody reached a fundable pilot in under ~6 years | MEDIUM | SEVERE | Build for the B2B pilot; plan 5 to 7 years and ~$30M+ |
| B11 | Single vendor dependency (IMX500, TI radar, PERS partner) | LOW to MEDIUM | HIGH | Abstract sensing and monitoring layers; qualify second sources before G5 |

Kill criteria (Phase 8 section 6): **K1 (field false positive rate, resolves G2)** is primary. If K1 fails, stop. If K2 (no operator or payer pays at margin) and K3 (DTC only, CAC above ~$250 against churn above ~3 percent) both fail, the venture case is dead even if the technology works. K4 (gait substantiation) and K5 (regulatory envelope closure) reshape rather than always kill, but each can be terminal in combination.

## Open Questions

1. **PERS/monitoring subscription churn is UNKNOWN**, held in private filings (Phase 7 OQ1, Phase 8 OQ1). Every LTV, breakeven, and DTC viability number rests on an assumed 2 percent/month consumer and 10 to 15 percent/year B2B churn. The single most material gap; blocks a defensible LTV:CAC.
2. **Senior living per bed per month price is UNKNOWN** (Phase 7 OQ2, Phase 8 OQ2). SafelyYou, Inspiren, and Sage publish nothing. The recommended channel's absolute ARR rests on an assumed $25 to $35/bed. Requires direct RFQ or an operator conversation.
3. **Real category DTC CAC is UNKNOWN** (Phase 7 OQ3). The $200 assumption drives the DTC contrast; if true CAC is $350, DTC dies earlier.
4. **Field false positive rate per fall modality is UNKNOWN** (Phase 2 OQ2, Phase 4 OQ1). Vendors publish marketing multipliers, not sensitivity/specificity. This is the make or break number and the primary kill gate; it cannot be resolved by planning, only characterized at G2.
5. **Single low cost oblique camera node gait accuracy is UNVALIDATED** (Phase 1 OQ1, Phase 4 OQ2). Published 0.04 m/s is research grade capture; a low cost node may not hit it. Bench test at G1. If it fails, gait weakens to a coarse trend and the all radar fallback A2 gains.
6. **IMX500 model fit is UNVALIDATED** (Phase 3 OQ1). If the Phase 4 pose model does not fit in package memory at 30 fps, the camera node moves to a costlier SoC and a weaker privacy claim.
7. **PERS monitoring partner per seat cost is UNKNOWN** (Phase 4 OQ6, Phase 8 OQ4). A recurring COGS line ($4 to $5 assumed) that moves the recurring gross margin.
8. **RAG health content license is unscoped** (Phase 4 OQ5). Source, license cost, and update cadence are UNKNOWN and are a real line item.
9. **FTC gait substantiation study cost** ($30K to $80K) is an estimate, not a quote (Phase 6 OQ5, Phase 8 OQ7).
10. **SBIR/STTR reauthorization timing** (lapsed 2025-10-01, reportedly reauthorized 2026-04-13) is single source; confirm against SBA.gov before modeling non dilutive runway (Phase 8 OQ5). A general wellness framing may also score worse at NIH review, arguing for leading the sensing work through NSF.
11. **Whether a consumer wellness product may rely on the clinical surrogate consent hierarchy** for cognitively impaired residents is untested and belongs in launch state legal review (Phase 5 OQ1).
12. **Whether gait qualifies as a biometric identifier under BIPA/CUBI** is unresolved; MHMDA captures it regardless. Do not build a voice template (Phase 5 OQ2).

## Assumptions Made

1. **The recommended strategy departs from the concept as written.** The concept assumes a light bulb camera, vision primary, DTC to the adult child. This synthesis carries the multi phase findings that each of those is wrong (bulb rejected in Phase 2, mesh primary in Phases 1 and 2, DTC subordinated to operator per bed in Phases 7 and 8). This is a finding, not an assumption, but it is stated plainly so the funding decision is made on the reshaped product, not the original pitch.
2. **Churn (2 percent/month consumer, 10 to 15 percent/year B2B), consumer CAC ($200), operator CAC ($50 to $120/bed), per bed price ($25 to $35), and PERS seat cost ($4 to $5)** are planning assumptions carried from Phase 8, each flagged there and never sourced. They drive every LTV and breakeven figure. If materially wrong, the scenario magnitudes move, though the channel ranking (B2B over DTC) is robust because it rests on the structural CAC and churn difference, not the absolute values.
3. **The 1.15x AI multiplier** is a judgment on contested evidence (the strongest study walked back its methodology). If the real blended multiplier on the critical path is below 1.0, timelines extend roughly 20 percent (Phase 6 OQ2).
4. **Reimbursement remains foreclosed** under the wellness positioning, treated as fixed (Phase 8 assumption 12). If a compliant bridge opens (partnering an FDA device RPM vendor), the revenue map expands materially; that is upside, not downside.
5. **The 5 zone, single resident, 13 device home** is the costing and sizing unit (Phase 3, Phase 2). A payer or operator channel may standardize a different kit, moving the system BOM.
6. **Non dilutive is winnable and additive** (approximately $3.3M to $4.6M across NSF and NIA, both phases). If SBIR is not won or timing slips, dilutive need rises by that amount at the earliest, most expensive gates (Phase 8 assumption 10).
7. **The comparables** (6+ years to Series A, B2B survival, DTC stall) are used as an elapsed time sanity check, assumed to transfer to this venture (Phase 6 assumption 8).

## Confidence Summary

Overall confidence: HIGH on the five thesis conclusions and the kill criteria; MEDIUM on the absolute scenario numbers; LOW on the three values that remain UNKNOWN and are carried as flagged assumptions.

- **HIGHEST confidence:** the bulb does not survive (switched power and viewing angle, two independent disqualifying grounds); the product is a distributed multi node mesh with one oblique camera; long lie and the hazard inventory are the highest value defensible features; the best channel is operator per bed, not DTC; and reimbursement is structurally foreclosed by the wellness positioning. These rest on primary gait literature, primary FDA and CMS text, primary vendor specs, and dated, named funding deals.
- **HIGH confidence:** the false positive rate is the make or break and the primary kill gate; the clean `Apache-2.0`/`MIT` OSS stack covers almost every subsystem and NVIDIA is optional; the "no raw video leaves" claim is provable only in the qualified form with on sensor inference as the decisive control; the comparables contradict any lean fast DTC timeline.
- **MEDIUM confidence:** the absolute BOM, the approximately $1.8M to $2.0M to G4, the approximately $30M to $45M to breakeven, and the approximately 18K to 28K bed breakeven inflection. These are internally consistent planning models on sourced COGS and cloud costs plus flagged operating assumptions, not an operating plan.
- **WEAKEST (LOW / UNKNOWN):** PERS churn (blocks a hard LTV:CAC), per bed price (blocks precise best channel ARR), and real DTC CAC. All three are Phase 7 open questions carried forward; none was invented.

The load bearing conclusion, HIGH confidence and robust to the weak cells: fund the reshaped B2B product to a staged G4 pilot, sequence non dilutive first, price per bed to operators, and treat the field false positive rate (K1) as the gate that decides whether anything downstream matters. The venture dies first at K1; it dies second if no operator or payer will pay at margin (K2); a DTC led strategy dies at K3 the way Amazon Alexa Together already did. The bulb is already dead.
