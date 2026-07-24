# SENTINEL (Concept A) — Full Compiled Text

Everything for the computer-vision elder monitor in one file: the guide, the two driving briefs, and all ten phases. Generated 2026-07-24.

---

# PART I — DOSSIER AND GUIDE

# Sentinel (Concept A) — Complete Dossier

Everything relating to the computer-vision / passive-sensing elder monitor, in one place: what it is, what the research concluded, the original inputs that drove it, and the exact prompts fed to each research agent.

"Sentinel" is the working name used here for Concept A (Elder Home Monitoring). The formal analysis is the ten files in `research/a/`.

---

## 0. What Sentinel is, in plain language

A passive, easy-install, in-home system that watches an older adult living alone for falls and meaningful changes in daily activity, and tells a remote caregiver when something happens. No wearable to charge, nothing to operate. A conversational layer lets the resident interact and lets the caregiver ask questions about what has been going on. It is positioned as general wellness, not a medical device.

The founder's starting picture was a camera inside a light-bulb form factor. The research tested that picture and rejected the bulb, keeping the mission.

---

## 1. The headline answer

**Recommendation: FUND to a staged G4 pilot, conditional on one kill gate, sold B2B to senior-living operators, built as a distributed sensor mesh, not a light bulb and not direct-to-consumer.**

The four load-bearing conclusions:

1. **The light bulb dies.** It fails on two independent grounds. Switched power (turn the light off and the monitor is dead) has no fix that does not make the bulb redundant. And the ceiling-down viewing angle makes the flagship gait metrics geometrically unmeasurable (foreshortening degrades accuracy up to ~60%, with no published validation of nadir-view gait speed). Since you cannot substantiate a measurement claim you cannot make from that angle, the bulb is disqualified at concept stage. See `phase2_architecture.md`.

2. **A distributed sensor mesh survives.** PIR and door-contact backbone (~$13-25 per node) for activity, one 60GHz radar in the bathroom (camera-forbidden, highest fall room), an under-mattress ballistocardiography mat in the bedroom, and one oblique mains-powered camera doing on-sensor (Sony IMX500) inference so raw video never leaves the package. Per-home hardware BOM about $224.50 at 1,000 units. See `phase2_architecture.md`, `phase3_hardware.md`.

3. **The whole business lives or dies on one number: the field false-positive rate (kill criterion K1).** Lab fall-detection accuracy of ~94% collapses to ~57% in real homes. If you cannot drive escalated false positives below roughly one per home per month without gutting sensitivity, stop, because nothing downstream matters. This is provable cheaply in your own home at gate G2. See `phase6_devplan.md`, `phase8_businesscase.md`.

4. **The channel is per-bed to senior-living operators, not consumers.** DTC in this category has a documented graveyard (Amazon Alexa Together shut down May 2025 despite the lowest customer-acquisition cost on earth). The reimbursement money requires the medical-device positioning the wellness lane is defined by avoiding, which is the central strategic tension. See `phase7_market.md`, `phase8_businesscase.md`.

Capital: roughly $1.8M to $2.0M and 3 to 4 elapsed years to a fundable G4, about $3.3M to $4.6M of that potentially non-dilutive (NSF plus NIA SBIR); roughly $30M to $45M total to breakeven at 18,000 to 28,000 beds.

**Highest-value single feature: long-lie detection** (time on the floor after a fall). It drives outcome severity more than fall prediction, and it is trivially defensible as event detection. Second: the environmental-hazard inventory (loose rugs, clutter, poor night lighting), which requires zero inference about the person and is actionable by a caregiver in an afternoon. No competitor emphasizes either.

---

## 2. How the research was driven (the prompt chain)

Three documents drove everything. They are the "original research prompt" you asked for:

1. **`00_framework.md`** (repo root) — the authoritative governing conventions: the wellness claims boundary (the input-versus-inference line), the maturity gates G0 to G6, the cost-model rules, the evidence rules (every number needs a source, URL, date; never invent; mark confidence), the output contract, and the shared technical spine. Every phase inherits it.

2. **`01_concept_a_elder_monitoring.md`** (repo root) — the Concept A brief itself: the concept statement, the seven founder assumptions to validate (not inherit), and the ten phases with their exact required outputs. This is the spine of Sentinel specifically.

3. **`03_claude_code_setup_and_prompt.md`** (repo root) — the setup and kickoff prompt that stood the whole program up (folder layout, model pinning, the researcher subagent, and the master kickoff instruction to read the four files, ask questions, then execute phase by phase).

The execution model: the main analyst session never ran broad web searches itself. Each phase was handed to a bounded research agent with a target and a stop condition. The agent did the primary-source web research, wrote the phase file, and embedded its citations. The analyst verified, committed to git (one commit per phase, the audit trail), and gated the next phase on the last. The exact per-phase agent prompts are reproduced verbatim in Section 4.

One phase, the architecture fork, was decided by four dedicated primary-source fact sheets (cameras and gait viewing angle; mmWave radar and thermal IR; WiFi CSI, PIR, and acoustic; bed and seat ballistocardiography, hubs, and cloud cost). Those fact sheets are synthesized and cited inside `phase2_architecture.md`. Section 5 explains them.

---

## 3. Phase by phase, in plain language

| Phase | File | The question it answered | What it found |
|-------|------|--------------------------|---------------|
| 0 | `phase0_scope.md` | What exactly are we building, and what is even legal to claim? | 6 CORE features, 3 BLOCKED (with in-lane reframings). Object-location memory is the compute hog that would force a hub. The claims matrix draws the line for every feature. |
| 1 | `phase1_markers.md` | What is actually measurable and worth measuring? (markers before sensors) | Long-lie and hazard inventory are the highest value. The v1 shortlist rides a cheap PIR/door mesh, not a camera. Gait speed is real but only from a side view, which foreshadows the bulb problem. |
| 2 | `phase2_architecture.md` | Which sensing architecture, and does the bulb survive? | The bulb dies (switched power + nadir angle). Selected: distributed mesh with on-sensor camera inference (T4 hybrid). Fallback: all-radar, zero cameras. THE pivotal phase. |
| 3 | `phase3_hardware.md` | What does one home cost to build, at volume? | ~$224.50 BOM per home at 1k units; radar node is the top line item; certification is a hard $80k to $210k NRE. Implied retail $299 to $499, competitive with Vayyar and CarePredict. |
| 4 | `phase4_software.md` | Does the software exist, and can we use it? | Pose estimation = MoveNet or RTMPose (Apache-2.0, commercial-clean). NVIDIA lock-in is real but not required. License traps flagged (OpenPose, Ultralytics, YOLO-World). Scene memory is out of v1. |
| 5 | `phase5_privacy.md` | Can we honestly say "no video leaves," and who consents? | Provable only in the qualified on-sensor-inference form, closing 8 leak paths. Hardest case is a cognitively impaired resident who cannot consent. 12-state all-party audio law forces wake-word-only. |
| 6 | `phase6_devplan.md` | How long, how many engineers, how much? | ~$1.8M to $2.0M and 3 to 4 elapsed years to a fundable G4. Critical path is false-positive reduction and certification, not features. The ground-truth problem is severe; the plan solves for it. |
| 7 | `phase7_market.md` | Who buys, through what channel, how big? | Bottom-up SAM ~$840M ceiling, realistic SOM $40M to $80M. Best channel is per-bed to senior-living operators. Alexa Together's shutdown is the instructive DTC failure. Reimbursement requires device positioning. |
| 8 | `phase8_businesscase.md` | What is the P&L, the capital plan, the kill criteria? | ~$30M to $45M to breakeven at 18k to 28k beds. Winning model: per-bed-per-month to operators, PMPM to payers second. K1 kill criterion: field false-positive rate. |
| 9 | `CONCEPT_A_BUSINESS_CASE.md` | The single fund/no-fund document. | FUND to a staged G4 pilot, conditional on K1, B2B operator channel, mesh not bulb. Two-page exec summary, then the case, then appendices. |

---

## 4. The exact prompts that drove each phase

These are the verbatim task prompts handed to each bounded research agent. Every one carried the same standing rules (do real web research, cite everything with source/URL/date, never invent, mark HIGH/MEDIUM/LOW confidence, read license files directly, no em or en dashes, tables over prose, do the work yourself and do not spawn sub-agents). The concept-specific task text follows.

### Phase 0 — Scope
> Produce Concept A Phase 0 (Scope Normalization). Deliver: (1) one-page restatement separating SETTLED from OPEN; (2) the full FEATURE INVENTORY as a numbered list (fall detection, fall notification, gait/sway metrics, step/mobility metrics, ADL patterns, object location memory, conversational check-in, medication reminders, caregiver query interface, trend reporting); (3) classify each feature CORE / DIFFERENTIATOR / LATER / BLOCKED; (4) the CLAIMS MATRIX per framework section 2 (feature, shipping phrasing, data type, permitting guidance/precedent, line-crossing phrasing, FTC validation evidence required); (5) identify every feature whose compute requirement is materially larger than fall detection (object permanence, natural-language scene query), state what each requires, and whether it fits an edge device or forces a hub.

### Phase 1 — Markers (a kill phase)
> Produce Concept A Phase 1. Build the full marker catalog using the brief's seed list (gait/mobility; balance/near-falls/compensation; falls and LONG-LIE detection; spatial behavior/life-space; sleep/circadian incl. interdaily stability, intradaily variability, relative amplitude; toileting; nutrition/kitchen; IADLs; social/communication; speech [research-only]; environmental hazard; physiological; adherence/cognition proxies). For EACH marker a row: Marker | Indication (non-diagnostic) | Evidence (primary lit, effect size, population, design, gold-standard) | Data type | Sensing modality + spec | Baseline | Time-to-signal | Actionability | Defensible framing (exact string) | Validation burden | Verdict. For gait speed establish published thresholds, populations, and the measurement error of camera-derived gait speed versus an instrumented walkway. Required outputs: full table; ranked v1 shortlist by actionability x evidence / sensing cost; the SENSING REQUIREMENT MATRIX (input to Phase 2); the CAREGIVER REPORT SPEC with actual daily and weekly copy readable in 30 seconds; and the explicit list of markers no ceiling camera can observe.

### Phase 2 — Architecture (the pivotal phase)
> Produce Concept A Phase 2 (Sensing Architecture Fork). (1.1) Enumerate sensing modalities (RGB, depth/stereo, thermal/low-res IR, mmWave radar 60/77GHz, WiFi CSI, PIR + door contacts, load/pressure BCG, acoustic, wearable): what each can/cannot detect, resolution, privacy posture, occlusion/lighting, per-room cost, install difficulty, bathroom viability; state honestly whether WiFi CSI is a product or research path. (1.2) Form factor options (E26 bulb, socket adapter, desk/shelf, corner/wall, disguised, smart display, non-camera node): evaluate the bulb on equal terms; RESOLVE the switched-power problem and the viewing-angle problem explicitly, and if a ceiling view makes the claimed metrics unmeasurable, say so plainly. (1.3) Compute topologies T1-T4 with per-node cost, hub cost, cloud cost/user/month, fall-alert latency, bandwidth, what data leaves the home, security surface. (1.4) RECOMMEND one primary architecture and one fallback with a comparison table across >=4 candidates scoring gait fidelity, fall reliability, bathroom coverage, privacy, install difficulty, per-home BOM, consumer acceptability.
>
> [This phase was additionally supplied with four primary-source modality fact sheets; see Section 5.]

### Phase 3 — Hardware and BOM
> Produce Concept A Phase 3 (Hardware and BOM) for the SELECTED mesh architecture only. (2.1) Compute silicon for the camera node and hub (Sony IMX500, Hailo-8L, RK3588/RK3576, Ambarella, Allwinner/SigmaStar/Ingenic, Jetson Orin) on TOPS, power, package cost at each volume tier, availability, toolchain, model fps, thermal in a sealed enclosure. (2.2) Image sensor and optics specified from the gait requirement. (2.3) Everything else (radio, AC-DC, enclosure, thermal, provisioning). (2.4) Non-camera nodes (seat pad, bed mat BCG, radar, PIR/door), stating whether seat/bed BCG is real and accurate. (2.5) Full BOM at 1/100/1k/10k/100k, landed cost, COGS, NRE incl. tooling and certification (a hard line item). Implied retail at target margin versus competing products' actual prices.

### Phase 4 — Software, models, open source
> Produce Concept A Phase 4. (3.1) Vision and pose: evaluate current open-weight pose models (MoveNet, BlazePose, YOLO-Pose, MMPose/RTMPose, ViTPose, OpenPose) with the EXACT SPDX license per model and commercial-use permission; NVIDIA's offerings and whether they lock the BOM to NVIDIA silicon; fall detection real-world false-positive rates; gait extraction validated versus gold standard. (3.2) ADL and pattern detection: say plainly if it is mostly not machine learning. (3.3) Scene memory and object location: specify the room map, object vocabulary, temporal store, retrieval; whether it belongs in v1. (3.4) The assistant layer: wake word, STT, cost per resident per month, and the safety/escalation/refusal envelope for an older adult in distress. (3.5) Caregiver app and whether the system calls emergency services directly (liability). (3.6) Build-vs-buy table for every subsystem.

### Phase 5 — Privacy
> Produce Concept A Phase 5 for the selected mesh architecture. (1) Data-flow table: every hop, store, retention period, per node type. (2) PROVE OR DISPROVE "no video leaves the device": every code path that could violate it (debug, OTA, crash dumps, remote support) and the control that closes each. (3) Consent architecture for a resident who does not want to be watched and for cognitive impairment (who consents on whose behalf). (4) Applicable law: state biometric privacy, wiretap/two-party consent if audio, HIPAA attachment through the channel. (5) Threat model: secure boot, signed firmware, encrypted storage, key management, OTA security, breach scenario. (6) Approved marketing claim language.

### Phase 6 — Development plan
> Produce Concept A Phase 6. (1) WBS to each gate G1-G6 (firmware, CV, backend, mobile, hardware, industrial design, certification, QA, ops). (2) Timeline and cost at 1/2/3/4 engineers with discipline mix and the tradeoff named. (3) AI-assisted velocity multiplier, cited, low/mid/high. (4) Critical path (likely certification or false-positive reduction). (5) Comparable ventures: how long they took and raised before each milestone, incl. failures. (6) Test plan by gate and SOLVE the ground-truth problem in a real home where nobody annotates video.

### Phase 7 — Market (a kill phase)
> Produce Concept A Phase 7. (1) BOTTOM-UP market sizing: US adults 65+ living alone, subset with a remote adult child, subset able to pay, subset reachable per channel, x realistic price/penetration; then an analyst TAM check. (2) COMPETITIVE LANDSCAPE profiling SafelyYou, Vayyar Care, CarePredict, Sensi.ai, Cherry Home, Origin Wireless, Emerald Innovations, Tellus, Lively/GreatCall, Medical Guardian, Bay Alarm, Life Alert, Apple Watch fall detection, Alexa Together, Best Buy/Current Health, emphasizing the ones that shut down and why. (3) CHANNEL analysis on CAC, sales cycle, contract size, gross margin. (4) REIMBURSEMENT: RPM/RTM/CCM/PCM codes and the tension that reimbursement requires medical-device positioning. (5) PARTNERS. (6) WILLINGNESS TO PAY and churn.

### Phase 8 — Business case
> Produce Concept A Phase 8. (1) Three scale scenarios small/mid/large: full P&L shape, burn, headcount, capital, months to breakeven. (2) Pricing models each: hardware plus subscription, subsidized hardware, free hardware with long commitment, per-bed-per-month to an operator, PMPM to a payer. (3) Capital plan, non-dilutive first (NIH/NIA SBIR, NSF SBIR), then angel/pre-seed/seed with actual recent aging-in-place deals as evidence. (4) Milestone-to-unlock map per gate. (5) Risk register: technical, regulatory, commercial, existential. (6) Kill criteria stated in advance.

### Phase 9 — Synthesis
> Produce the Concept A business case as a SINGLE document for a funder. (1) Executive summary, no more than two pages: recommendation, core thesis (bulb dies, mesh wins, long-lie and hazard inventory highest value, per-bed channel not DTC, the reimbursement-versus-wellness tension), capital ask, top risks and kill criteria. (2) The case across all phases. (3) Appendices: traceability of key numbers to phases, open questions, risk register summary. Every number traceable to a phase.

---

## 5. The four fact sheets that decided the architecture

Phase 2 was decided by four dedicated primary-source research passes. Their findings are synthesized and cited inside `phase2_architecture.md`; the raw fact sheets were working inputs, not committed as separate files. In brief:

1. **Cameras and gait viewing angle.** Validated gait metrics require a side/oblique view of a 2.5 to 4 meter straight path at 30 fps. Overhead/nadir foreshortens displacement toward zero and self-occludes the feet; up to ~60% accuracy loss; no published nadir gait-speed validation exists. Every shipping E26 bulb camera is a security device, none does health/gait. Edge inference adequate for pose starts around $70 (Sony IMX500 or Hailo-8L). This fact sheet is what killed the bulb.

2. **mmWave radar and thermal IR.** Vayyar Care (60GHz, camera-free, works through bathroom steam, ships to senior living at ~$250/device). TI IWR6843 (~$43 chip, fall detection >90% to 6.5m, gait step-length error 4.5cm versus a gold-standard walkway, long-lie via point-cloud). This is what made radar the bathroom and fall-path answer.

3. **WiFi CSI, PIR, acoustic.** Commodity WiFi is a product path for coarse motion only and a research path for falls/gait (lab numbers collapse cross-environment). Emerald Innovations uses its own radio, not commodity WiFi, and ships only to pharma trials. PIR plus door contacts are mature and cheap (~$13-25) but cannot see a motionless person on the floor. Acoustic fall detection is research-grade only.

4. **Bed/seat BCG, hubs, cloud cost.** Under-mattress ballistocardiography is real and validated (Emfit, Withings, EarlySense, HR within a few bpm of ECG). Seat-pad BCG is a research demo. Raw-video-to-cloud (topology T3) costs ~$16/month/home in egress alone and is the privacy killer; edge inference (T1) keeps fall-alert latency under 100ms versus 10-plus seconds for cloud.

If you want these four raw fact sheets dumped verbatim as their own files, say so and I will commit them.

---

## 6. How to read the full set

- The fastest single read is `CONCEPT_A_BUSINESS_CASE.md` (two-page summary up front).
- The three that decide viability: `phase1_markers.md`, `phase2_architecture.md`, `phase7_market.md`.
- The concatenated `SENTINEL_FULL.md` (if generated) contains the two driving briefs plus all ten phases end to end.
- The evidence trail for any claim lives in `research/registers/` (sources, papers, components, competitors, funding).

---

# PART II — DRIVING INPUT: THE GOVERNING FRAMEWORK (00_framework.md)

# 00_FRAMEWORK.md
## Shared Research and Business Case Framework
### Applies to: Concept A (Elder Home Monitoring) and Concept B (Pregnancy and Parenting Companion)

This file is authoritative. Both concept briefs inherit every convention below. Do not restate these rules in output files. Reference them.

---

## 1. WHAT THESE BRIEFS ARE FOR

Produce a defensible business development case for each concept. A business development case answers, with evidence:

1. What exactly gets built, at what technical specification.
2. What it costs to build one, one hundred, ten thousand.
3. What it costs to develop, over what timeline, with how many engineers.
4. Who buys it, why, at what price, and how big that market is.
5. Who we partner with, who funds it, and what milestone unlocks what.
6. Where it goes after v1.

Anything that does not serve one of those six questions is out of scope.

---

## 2. POSITIONING AND CLAIMS BOUNDARY

Both products are positioned as **general wellness**, not medical devices. This is a settled strategic decision, taken with input from an FDA regulator and a quality expert. The lane is broad and the research must reflect that rather than argue with it.

**Established precedent, to be verified and documented, not relitigated:**
- Consumer wearables ship gait and mobility metrics (walking speed, step length, double support time, walking asymmetry) as wellness features.
- Consumer wearables ship walking steadiness classification with notifications referencing fall likelihood, as wellness features.
- Consumer wearables ship fall detection with automatic emergency service escalation, as wellness features.
- Consumer rings and bands ship illness onset, temperature deviation, and readiness signals as wellness features.

The job of this section is **not** to argue that these features are unavailable. It is to **document exactly why they are available**, with citations, so the position survives investor diligence and payer legal review. That artifact is an asset. Build it.

### The lane, stated precisely
FDA general wellness policy covers claims about maintaining or encouraging a healthy lifestyle. It extends to claims that a healthy lifestyle may help reduce the risk of, or help living well with, certain chronic conditions, where that relationship is well understood and accepted. Software functions intended for maintaining or encouraging a healthy lifestyle, unrelated to diagnosis or treatment, are further carved out of the device definition by statute.

### Comfortably inside the lane
- An event occurred. "A fall was detected in the kitchen."
- A measured metric and its trend. "Walking speed is 18 percent below the 30 day baseline."
- A steadiness or stability classification with a general notification.
- A pattern change. "Bathroom visits are up from 4 to 9 per night this week."
- Encouragement of general healthy behavior, activity, sleep, nutrition.
- Education and normalization. "Resting heart rate typically rises across pregnancy. Here is why."
- Event notification and escalation to a designated contact or emergency service.

### The distinction that actually matters: input versus inference

This is the single most important line in this document. Get it right and almost everything both concepts want to do is available.

**Self report is not a claim.** If the app asks the user how she feels and she answers, storing that answer, trending it, charting it, and showing it back to her is a journal. The app has asserted nothing. Mood journals, symptom logs, sleep diaries, pain scales, and daily check ins are ubiquitous consumer features. The user supplied the data. The app reflected it.

**Measurement is not a claim about disease.** Walking speed, stride length, sway amplitude, sit to stand duration, turn count, resting heart rate, HRV, temperature. These are quantities. Trending them, comparing them to the user's own baseline, and comparing them to a published normative range are all measurement and reference, not diagnosis.

**Inference of a named disease from passive data is a claim.** The output string is what matters. "Your mood scores have been low for 14 straight days, and you flagged this yourself" is reflection. "This pattern is consistent with depression" is a screening result. Same underlying data, different assertion.

### Design rule that follows
Prefer self report for anything affective or cognitive. Prefer measurement and trend for anything physical. Let the user, the caregiver, or the clinician draw the conclusion. The product surfaces the pattern and hands it to a human. That posture is both the safest and, in this category, the better product, because a caregiver who is shown a chart trusts it more than a caregiver who is told a verdict.

### The narrow set that stays outside the lane
Not a list of things to abandon. A list of things that must be engineered a specific way, and that go in the risk register with a mitigation, not a strikethrough.

| Item | Why | Available reframing |
|------|-----|---------------------|
| Outputting a disease name inferred from passive data ("signs of depression," "signs of dementia") | Screening claim on a diagnosable condition | Trend the self reported input. Surface it. Prompt a conversation with a clinician. |
| Administering, scoring, and returning a validated clinical instrument as a result (PHQ-9, EPDS, MoCA, M-CHAT) | The instrument is the clinical tool | Two options to research: (a) present the instrument as an educational self check with the score shown to the user only and routed to her provider, which many consumer apps do, or (b) use a non instrument self report scale of the product's own design. Establish current practice and current enforcement posture. Do not assume either is settled. |
| Interpreting a lab value clinically | Clinical decision support | Display the value with the reference range printed by the lab. Explain what the analyte is. Do not tell her what her result means for her. |
| Instructing a change to treatment or medication | Treatment claim | Reminders and adherence logging are fine. Dose guidance is not. |
| Any output that could cause a user to delay seeking care | Severity, not classification | Hard coded red flag escalation layer. See concept briefs. |

### The second regulator, which is the one people forget
FDA governs whether it is a device. **FTC governs whether the claim is true.** FTC Health Products Compliance Guidance requires competent and reliable scientific evidence behind health related claims, and applies to wellness products with full force. A product that states "walking speed is down 18 percent" is making a measurement claim, and the substantiation question is whether the measurement is accurate against a recognized reference standard.

This converts a regulatory question into a **validation cost**, which lands in the business case at G3 and G4 either way. Research the FTC guidance, research what substantiation looks like for a gait metric derived from a camera, and cost it. This is a real line item, not a footnote, and it is where the money actually goes.

### The second regulator, which is the one people forget
FDA governs whether it is a device. **FTC governs whether the claim is true.** FTC Health Products Compliance Guidance requires competent and reliable scientific evidence behind health related claims, and applies to wellness products with full force. A product that states "walking speed is down 18 percent" is making a measurement claim, and the substantiation question is whether the measurement is accurate against a recognized reference standard.

This converts a regulatory question into a **validation cost**, which lands in the business case at G3 and G4 either way. Research the FTC guidance, research what substantiation looks like for a gait metric, and cost it. Do not treat it as a footnote.

### Required deliverables

**1. Claims matrix**, produced in Phase 0 of each brief. For every intended feature: the shipping phrasing, whether the data is self report or measurement or inference, the specific guidance or precedent that permits it, the phrasing that would cross the line, and the validation evidence required to substantiate it under FTC standards.

**2. `regulatory_precedent_dossier.md`**, produced once. The defensible written record: current FDA general wellness guidance, the statutory software function exclusions, current SaMD and Clinical Decision Support guidance, FTC Health Products Compliance Guidance, and the specific consumer product precedents above, with citations and dates. This is the document handed to a diligence lawyer and to a payer's legal team. It is an asset. Build it properly.

**3. `regulatory_risk_register.md`**, produced once, covering both concepts. Not a list of prohibitions. For each identified risk: description, likelihood, impact, the engineering or product mitigation, the leading indicator that tells us it is materializing, and the cost of the mitigation. Include FDA reclassification risk, FTC substantiation risk, product liability, state biometric and reproductive health privacy law, and the failure to escalate scenario.

Verify all guidance from primary sources. Do not rely on memory. Cite document title, issuing body, and date.

---

## 3. MATURITY GATES

All cost, timeline, and business case output is organized against these gates. Never present a single blended "cost to build the product." Always present cost to reach each gate.

| Gate | Name | Definition | Exit criteria |
|------|------|------------|---------------|
| G0 | Concept | Architecture chosen, BOM estimated, no hardware | Signed off architecture, costed BOM |
| G1 | Bench | Breadboard or dev kit, algorithms running on desk hardware, no enclosure | Core detection works on recorded and live data at stated accuracy |
| G2 | Self test | Founder installs in own home, runs continuously | 30 days continuous uptime, false positive rate characterized |
| G3 | Friends and family | 5 to 15 units, real homes, real users, instrumented | Install time measured, retention measured, failure modes cataloged |
| G4 | Pilot | 50 to 200 units, structured cohort, partner site or paying design partner | Efficacy evidence sufficient for a partner conversation, unit economics measured |
| G5 | Limited commercial | Sellable, manufactured at low volume, support exists, certifications complete | Positive contribution margin per unit or per subscriber |
| G6 | Full commercial | Scaled manufacturing, full feature set, channel established | Target CAC and LTV achieved |

For each gate, output: engineering cost, hardware and tooling cost, certification cost, headcount, elapsed months, cumulative burn, and what the gate unlocks (which conversation, which customer, which funding round).

---

## 4. COST MODEL CONVENTIONS

### Hardware
- Quote **BOM at 5 volume tiers: 1, 100, 1,000, 10,000, 100,000 units.**
- Every line item: part number, function, unit cost at each tier, source, date of quote, whether the price is public list, distributor (Digi-Key, Mouser, LCSC), or an estimated contract manufacturer or Alibaba style quote. Label estimates as estimates.
- Separate BOM from **landed cost**: add assembly, test, packaging, freight, duty, yield loss.
- Separate landed cost from **COGS**: add warranty reserve, returns, support allocation.
- **NRE is separate**: injection mold tooling, PCB spins, certification, firmware bring up.
- **Certification is a hard line item, not a footnote.** For any mains powered device sold in the US, at minimum: FCC Part 15 (and Part 15C intentional radiator if it has a radio), UL or ETL listing, and if it screws into a lamp holder, the safety standard applicable to that lamp form factor. Research the actual applicable standards, do not guess. Certification is frequently the single most underestimated cost in a hardware startup and it lands at G5.

### Software and development
- Model timeline and cost at **1, 2, 3, and 4 engineers.**
- State the loaded engineer cost assumption explicitly (San Diego market, fully loaded including benefits, equipment, overhead). Do not use salary alone.
- Apply an **AI assisted development velocity multiplier.** This multiplier must be justified with cited empirical evidence, not asserted. Search for published data on AI assisted developer productivity. If credible published data shows a range, use the range and run low, mid, and high cases. If the evidence is weak or contested, say so and default to a conservative multiplier. **Do not invent a productivity number.**
- Model **Brooks's law**: adding engineers does not scale linearly. State the coordination overhead assumption and its source.
- Distinguish work that is buy from work that is build. For every "we will develop X," first answer: does an off the shelf or open source X already exist, what does it cost, what does it not do?

### Business
- Unit economics: price, COGS, gross margin, CAC, payback period, churn, LTV, LTV to CAC ratio.
- For subscription concepts, model churn explicitly and separately from acquisition. A product with a naturally bounded lifespan (a pregnancy is finite) must model the churn cliff, not average it away.
- Three scale scenarios per concept: small (hundreds of units or subscribers), mid (thousands), large (tens of thousands or more). For each: revenue, burn, headcount, capital required, months to breakeven.

---

## 5. EVIDENCE RULES

These are non negotiable. A business case built on invented numbers is worse than no business case.

1. **Every number gets a source, a URL, and a date.** No exceptions.
2. **Never invent a price, a lead time, a market size, or a timeline.** If it cannot be found, write `UNKNOWN` and add it to the open questions list.
3. **Mark confidence on every material claim: HIGH, MEDIUM, LOW.** HIGH means primary source, current, directly on point. LOW means inference or analogy.
4. **Flag anything older than 18 months as stale.** Semiconductor pricing, module availability, and reimbursement policy all move fast.
5. **Distinguish list price from quoted price from estimated price at volume.** These differ by multiples.
6. **Market sizing must be bottom up first.** Count the addressable units or subscribers and multiply by realistic price and penetration. Only after a bottom up estimate exists may a top down analyst TAM figure be cited, and it must be labeled as a secondary check, not the primary number.
7. **When two sources disagree, present both and say which is more credible and why.** Do not average them silently.
8. **Distinguish a founder assumption from a research finding.** Anything inherited from the concept description is an assumption until validated. Label it.
9. Prefer primary sources: manufacturer datasheets, distributor pricing pages, FDA guidance documents, CMS fee schedules, SEC filings, published papers. Avoid content marketing, listicles, and SEO blog aggregators.

---

## 6. OUTPUT CONTRACT

Every phase writes exactly one markdown file to `/research/`, named as specified in the concept brief. Every phase output file ends with three mandatory sections:

```
## Open Questions
Things that could not be resolved and that block or weaken the next phase.

## Assumptions Made
Every assumption, explicitly listed. If an assumption was necessary to proceed, it goes here, flagged, with the impact if wrong.

## Confidence Summary
Overall confidence in this phase's output, and which specific findings are weakest.
```

Update `/research/decision_log.md` after every phase: what was decided, what evidence supported it, what was rejected and why.

---

## 7. EXECUTION RULES FOR CLAUDE

- **Execute one phase at a time.** Stop at the end of each phase. Do not begin the next phase without instruction.
- **Ask before assuming.** For any technical specific (component selection, register settings, parameter values, process configuration, price point, market segment), ask rather than assume. If a question blocks progress on one thread but not others, ask it and continue on the unblocked threads.
- **Never guess or fill gaps silently.** Any assumption must be explicitly stated and flagged.
- **Do not spawn broad, open ended research.** Every search has a stated target and a stop condition. If a phase specifies "identify 5 candidate compute modules meeting criteria X," find 5 and stop.
- **Read the framework and prior phase outputs before starting a phase.** Do not re research what a prior phase already established and logged.
- **When something in the concept description is technically contradictory or commercially implausible, say so in the output. Do not build around it quietly.**

### Writing style
- No em dashes, en dashes, or hyphens as punctuation. Hyphens permitted only inside part numbers and proper names.
- C suite engineering leadership tone. Authoritative, precise. No hedging, no filler, no throat clearing.
- Tables over prose for anything comparative.
- Short, blunt, comparative summaries. Not narrative.

---

## 8. SHARED TECHNICAL SPINE

Both concepts are the same underlying system: **passive multimodal sensing, plus a fusion layer, plus a language model interpretation layer, delivered into a care context.** Research that serves both should be done once and shared.

Shared research, do once, write to `/research/shared/`:

| Topic | File |
|-------|------|
| LLM interpretation layer: on device vs API, cost per user per month, latency, privacy posture, model selection | `shared_llm_layer.md` |
| Consumer wearable raw data access: which devices expose raw HR, HRV, SpO2, accelerometer, skin temperature, via what API, under what terms, at what cost, with what rate limits | `shared_wearable_data_access.md` |
| Privacy, security, and data architecture: encryption at rest and in transit, edge versus cloud inference, what triggers HIPAA, what triggers state biometric privacy law (Illinois BIPA, Texas CUBI, Washington My Health My Data), consent architecture | `shared_privacy_security.md` |
| Cloud and inference infrastructure cost per user per month at each scale tier | `shared_infra_cost.md` |
| Capital landscape: relevant VCs, strategic investors, non dilutive funding (NIH SBIR, NSF SBIR, NIA specifically for aging tech), accelerators | `shared_capital_landscape.md` |

On wearable data access, be specific and skeptical. The concept description assumes raw sensor data from a consumer band. Most consumer wearable vendors expose derived metrics only, gate raw data behind research agreements, or prohibit it entirely in their developer terms. Establish what is actually obtainable before any downstream design depends on it. If raw data is not obtainable from a given vendor, identify the alternatives: research grade wearables, white label modules, contract manufactured band, or non wearable substitutes.

On privacy law, note that continuous video of a person's home, and any biometric identifier derived from it, is among the most heavily regulated data categories that exists, and that "we only send metadata, not video" is a claim the architecture must actually enforce, not just intend.

---

## 9. RESEARCH ARTIFACT REGISTERS

Everything found gets saved. The registers are the durable asset of this project. They persist across phases and across both concepts. Append to them continuously. Never let a source be cited in a phase output without also landing in the register.

Write to `/research/registers/`.

| File | Contents |
|------|----------|
| `sources.md` | Running bibliography. Every source consulted, including ones rejected. Title, author or org, URL, date accessed, publication date, one line on what it was used for, and a credibility rating. |
| `papers.md` | Academic and clinical literature. Full citation, DOI, what it establishes, sample size and study design, effect size where relevant, whether it is validated against a gold standard, and which marker or claim it supports. Note replication status. Note when a result is a single lab demo and not a productized capability. |
| `components.md` | Every hardware part evaluated, including rejected ones. Part number, manufacturer, function, key specs, price at each volume tier, distributor and link, lead time, lifecycle status, datasheet URL, and why selected or rejected. |
| `oss.md` | Every open source project, model, dataset, and library evaluated. Name, repo URL, license (exact SPDX identifier), maintenance status, last commit, whether commercial use is permitted, whether it requires specific hardware or runtime, what it does, what it does not do, and the estimated engineering effort to integrate. **License is not optional and is not a guess. Read the license file.** Several widely used vision and pose models carry non commercial or restrictive licenses. Flag every one. |
| `datasets.md` | Datasets usable for training, validation, or benchmarking. Name, size, license, access terms, whether it contains the population of interest (older adults in home settings, pregnant people), and known biases. |
| `markers.md` | The unified trend and marker catalog across both concepts. See the marker phase in each concept brief. |
| `vendors.md` | Every vendor, ODM, CM, lab, content licensor, and potential partner. Contact path, what they supply, minimum order quantity, whether they work with startups, and any published pricing. |
| `competitors.md` | Every company profiled. Product, buyer, price, funding history, current status, and if dead, why. |
| `funding.md` | Every fund, grant program, and accelerator identified, with actual recent deals in the category as evidence of thesis fit. |

Register discipline:
1. A register entry is created the moment a thing is evaluated, not at the end of a phase.
2. Rejected items stay in the register with the rejection reason. The rejected list is as valuable as the selected list, and it prevents re researching the same dead end.
3. Every register entry carries a date and a confidence rating.
4. No register entry is ever deleted. It is superseded, with the superseding entry linked.

---

# PART III — DRIVING INPUT: THE CONCEPT A BRIEF (01_concept_a_elder_monitoring.md)

# 01_CONCEPT_A: ELDER HOME MONITORING
## Phased Research and Business Case Brief

Read `00_framework.md` first. It governs this file.

---

## CONCEPT STATEMENT

A passive, easy install, in home monitoring system for older adults living independently, whose caregiver is remote, busy, or both. The system observes movement, gait, and daily activity patterns without requiring the resident to wear, charge, carry, or operate anything. It notifies designated contacts when an event occurs, and it surfaces changes in daily patterns over time. A conversational assistant layer gives the resident a low friction way to interact with it, and gives the remote caregiver a way to ask questions about what has been happening.

Positioning is general wellness. See framework section 2.

---

## FOUNDER ASSUMPTIONS TO VALIDATE, NOT INHERIT

Each of these came from the concept description. Each is a hypothesis. Treat it as such.

| # | Assumption | Why it may be wrong |
|---|-----------|---------------------|
| A1 | A camera inside a light bulb form factor is the best sensor placement | Ceiling down is a poor viewing angle for gait. Lamp sockets are switched, so power is not guaranteed. Thermal envelope inside a bulb is tight. |
| A2 | Compute happens on the camera, and only derived data leaves it | Some described features (object permanence, scene memory, natural language queries about the home) require far more inference and state than a fall detector. Verify what fits in the thermal and cost envelope. |
| A3 | Vision is the primary modality | mmWave radar, WiFi channel state information, pressure and load sensing, and passive infrared all solve subsets of this problem, some with better privacy posture and lower cost. Vision may be the wrong default. |
| A4 | Raw sensor data is obtainable from a consumer wearable band | Most consumer vendors do not expose raw PPG, accelerometer, or skin temperature to third parties. See `shared_wearable_data_access.md`. |
| A5 | Detecting degradation and predicting falls is in scope | It is not, in the wellness lane. See framework section 2. Route to the claims matrix. |
| A6 | An NVIDIA open source vision model is the right starting point | Verify. There may be better licensed or open weight options for pose estimation and gait analysis, and the model choice cascades directly into the compute requirement, which cascades into the BOM. |
| A7 | The buyer is the adult child, paying a consumer subscription | The money in aging in place is concentrated in payers, providers, and operators. Consumer DTC in this category has a documented history of high CAC and hard churn. |

---

## PHASE 0: SCOPE NORMALIZATION
**Output: `/research/a/phase0_scope.md`**

1. Restate the concept in one page, as understood, separating what is settled from what is open.
2. Produce the **feature inventory**: every capability implied by the concept description, as a numbered list. Include, at minimum: fall detection, fall event notification, gait and sway metrics, step and mobility metrics, activity of daily living patterns (bathroom frequency, kitchen use, sleep location, time in bed, chair transfers), object location memory ("where is my phone"), conversational check in, medication reminder prompts, caregiver query interface, trend reporting.
3. For each feature, classify: **CORE** (v1, without it there is no product), **DIFFERENTIATOR** (v1 if affordable), **LATER** (v2 or v3), **BLOCKED** (cannot exist in the wellness lane).
4. Produce the **claims matrix** per framework section 2.
5. Identify every feature whose compute requirement is materially larger than fall detection. Object permanence and natural language scene query are the obvious two. State what each actually requires: persistent semantic scene graph, object detection across a room map, temporal state store, retrieval. Estimate whether that fits on an edge device or forces a hub.

**Stop. Report. Wait.**

---

## PHASE 1: MARKER AND TREND CATALOG
**Output: `/research/a/phase1_markers.md` and append to `/research/registers/markers.md`**

This phase comes before architecture on purpose. **The markers define the sensing requirement. Do not choose a sensor and then ask what it can see.**

Build the full catalog of observable markers that meaningfully track wellbeing, function, and change in an older adult living alone. For each marker, produce a row:

| Field | Requirement |
|-------|-------------|
| Marker | Name it precisely |
| What it indicates | Plain language, non diagnostic |
| Evidence | Primary literature. Effect size, population, study design, whether validated against a gold standard. Cite. Log in `papers.md`. |
| Data type | Self report, measurement, or inference. See framework section 2. |
| Sensing modality | Which sensor sees it, and what specification it demands (resolution, frame rate, placement, sample rate) |
| Baseline | Is the signal meaningful against the person's own baseline, a published normative range, or both |
| Time to signal | How many days or weeks of data before a change is detectable above noise |
| Actionability | What a caregiver could actually do differently. **A marker with no action is telemetry, not a product.** |
| Defensible framing | The exact string the product would show |
| Validation burden | What it would take to substantiate the measurement under FTC standards |
| Verdict | v1, v2, research only, or reject |

### Seed list. Research every one. Add what is missing.

**Gait and mobility.** Gait speed and its trend. Stride length and cadence. Stride time variability. Step width and lateral sway amplitude. Walking asymmetry and weight bearing asymmetry. Turn duration, turn steps, and turn hesitation. Gait initiation hesitation. Freezing episodes. Dual task gait cost, meaning slowing while talking. Stair ascent and descent time, step through versus step to, handrail use.

Gait speed is described in the geriatrics literature as a vital sign level predictor. Establish the actual published thresholds, the populations they were derived in, and the measurement error of camera derived gait speed versus an instrumented walkway. This determines whether the whole concept is measuring anything real.

**Balance, near falls, and compensation.** Furniture surfing, meaning contact with walls and furniture while ambulating. This is a recognized clinical sign and a camera can see it. Stumbles and recoveries that do not become falls. Postural sway during standing tasks. Sit to stand transition time and the number of attempts. Chair rise without arm use versus with. Sit to stand count per day, as a passive proxy for a chair stand test.

**Falls and post fall.** Fall detection. **Long lie detection, meaning time on the floor after a fall.** Research this specifically. Time on the floor is a major driver of outcome severity, and it is arguably the highest value single feature in the entire product, more valuable than fall prediction. It is also trivially defensible as an event detection. Also: fall location, fall context, and whether the person self recovers.

**Spatial behavior.** Life space within the home, meaning how many rooms are visited and how much of the floor plan is traversed. Contraction of life space is a documented functional marker. Room level dwell time. Transition counts. Pacing and wandering. Time in bed versus time in chair versus time ambulating. Sedentary bout length.

**Sleep and circadian.** Sleep location, meaning bed versus chair. Time in bed. Sleep fragmentation. Night time bathroom trips. Night time wandering. Bed exit events. **Circadian rest activity rhythm metrics from the actigraphy literature: interdaily stability, intradaily variability, relative amplitude, and the timing of least and most active periods.** These are established, quantitative, and derivable from passive activity data. Research them properly. Sliding down in bed, as described in the concept.

**Toileting.** Bathroom visit frequency, day and night. Dwell time. Deviation from personal baseline. Night time frequency change is a well documented general health signal. Bathroom is also the highest fall risk room and the room where cameras are unacceptable. Note the modality consequence.

**Nutrition and kitchen.** Kitchen dwell time. Meal preparation events. Refrigerator and cabinet interactions. Eating duration. Meal frequency and skipped meals. Fluid intake proxies. Research whether refrigerator interaction counts have been validated as a nutrition proxy in the smart home literature.

**Instrumental activities of daily living.** The concept mentions dishes and cleaning. Formalize it. Dishwashing events. Laundry events. Tidying behavior. Mail and package retrieval. Plant and pet care. Bathing and shower frequency. Dressing. Change in the frequency of habitual tasks is a functional decline signal and it is exactly what a remote adult child notices on a visit and cannot see from a distance.

**Social and communication.** Front door events and visitor counts. Time spent in conversation. Phone use. Outgoing trips from the home and their duration. Voice interaction volume with the assistant itself. Social isolation is a documented mortality risk factor and it is measurable passively.

**Speech and interaction.** Speech rate. Pause length and frequency. Word finding hesitation. Lexical diversity. Response latency to a prompt. This is an active research area for cognitive change. Treat it as **research only for v1**, log it, and do not ship an output string from it. It is the highest scientific upside and the highest claim risk in the catalog.

**Environmental hazard.** Loose rugs. Clutter in walking paths. Poor lighting in transit areas at night. Obstructed stairs. Missing handrails. A camera can inventory these. **This is a fall prevention feature that requires zero inference about the person, is completely defensible, is actionable by the caregiver in an afternoon, and no competitor emphasizes it.** Research it seriously.

**Physiological.** From a wearable, if raw access exists. From contactless sensing, if it does not. Resting heart rate trend. HRV trend. Respiratory rate. SpO2. Skin temperature. The seat pad and bed mat ballistocardiography path. Establish which of these are obtainable and at what accuracy.

**Adherence and cognition proxies.** Pill organizer interaction. Medication reminder response rate. Object misplacement frequency, which the phone finding feature generates as a byproduct. Repeated questions to the assistant. Stove and appliance left on. Door left open. Note that object misplacement frequency is a self generating cognitive signal and also the most claim sensitive item in this list. Log it, do not output a conclusion from it.

### Required outputs of this phase

1. The full marker table.
2. **A ranked shortlist for v1**, ordered by actionability multiplied by evidence strength divided by sensing cost. Not by how interesting the marker is.
3. **The sensing requirement matrix**: for each v1 marker, the minimum sensor specification required to observe it. This matrix is the input to Phase 2. It is the deliverable that prevents building a camera that cannot see what the product claims to see.
4. **The caregiver report specification**: what the remote adult child actually receives, daily and weekly, and what a change in it would cause them to do. Write the actual report copy. If the report is not something a busy person would read in 30 seconds, redesign it.
5. Explicit identification of markers that no camera can observe from a ceiling, and markers that require a modality the concept has not budgeted for.

**Stop. Report. Wait.**

---

## PHASE 2: SENSING ARCHITECTURE FORK
**Output: `/research/a/phase2_architecture.md`**

Input: the sensing requirement matrix from Phase 1. Every architecture is scored against its ability to observe the v1 marker shortlist. An architecture that cannot see the shortlist is rejected regardless of cost.

This is the most important phase in the brief. Everything downstream is a consequence of it. Do not shortcut it.

### 1.1 Enumerate the sensing modalities

For each, establish from primary sources: what it can and cannot detect, spatial resolution, privacy posture, occlusion and lighting behavior, per room cost, install difficulty, and whether it works in a bathroom (the highest fall risk room and the one where a camera is least acceptable).

| Modality | Must research |
|----------|---------------|
| RGB camera | Low light performance, IR illumination, frame rate needed for gait |
| Depth or stereo camera | Cost delta, whether depth materially improves gait metrics |
| Thermal or low resolution IR array | Privacy advantage, resolution floor for fall detection |
| mmWave radar (60GHz, 77GHz) | Vayyar, TI IWR and xWR families, Infineon. Through wall, bathroom viable, no image |
| WiFi channel state information sensing | The MIT and Emerald Innovations line of work. What is actually reproducible outside a lab. Router access requirements. |
| Passive infrared and door contacts | Cheapest baseline. What Care.coach class and legacy PERS systems already do |
| Load and pressure sensing | Seat pad, bed mat, floor mat. Ballistocardiography for HR without a wearable |
| Acoustic | Fall sound signature, distress speech, voice interface |
| Wearable | Only if raw data access is real. See A4. |

For WiFi CSI specifically: find the actual papers, identify whether commodity routers expose CSI, identify which chipsets do, and state honestly whether this is a product path or a research path today. Do not assume the MIT result is productizable because a paper exists.

### 1.2 Enumerate the form factor options

The concept assumes a light bulb. Evaluate it against the alternatives on equal terms.

| Form factor | Must research |
|-------------|---------------|
| Screw in bulb (E26) | Thermal envelope, switched power problem, viewing angle from ceiling, applicable safety standard, existing products in this form factor and why they did or did not work |
| Bulb socket adapter with pass through | Solves nothing about the switch |
| Desk or shelf camera (the NexiGo class reference) | Cheapest, best angle, worst aesthetics and stigma |
| Corner or wall mounted, hardwired or battery | Best angle for gait, hardest install |
| Disguised in a household object | Consent and trust implications. Note that covert monitoring of an adult raises legal and ethical problems distinct from any technical ones |
| Smart display or existing device | Piggyback on installed base |
| Non camera node (radar or pressure) | Eliminates the aesthetic and privacy objection entirely |

**Resolve the switched power problem explicitly.** If a resident turns off the light, the monitor is dead, and the caregiver may not know. Options: multi bulb redundancy, supercapacitor holdup with a last gasp radio message, a companion mains node, or abandoning the bulb. Cost each.

**Resolve the viewing angle problem explicitly.** Determine, from published gait analysis literature, what camera placement and what minimum frame rate and resolution are required to extract the specific metrics claimed: stride length, cadence, gait speed, lateral sway amplitude, weight bearing asymmetry, sit to stand transition time. A ceiling down view may make several of these unmeasurable. If so, say so plainly. This finding either kills or reshapes the bulb concept, and it is better to know at G0 than at G3.

### 1.3 Enumerate the compute topologies

| Topology | Description |
|----------|-------------|
| T1 | Full inference on the sensor node. Only derived events and metrics leave the device. No video ever leaves. |
| T2 | Sensor node does lightweight detection and streams compressed features to an in home hub. Hub does heavy inference. Nothing leaves the house except events and summaries. |
| T3 | Sensor node streams to cloud. Cloud does inference. |
| T4 | Hybrid. Node handles latency critical events (fall detection). Hub or cloud handles the assistant, the scene memory, and trend analysis. |

For each topology: per node cost, hub cost if any, cloud cost per user per month, latency for a fall alert, bandwidth, what data physically leaves the home, security surface, and the marketing claim it supports.

Note the tension: T1 has the strongest privacy story and is what the concept description wants. The assistant and object memory features push toward T2 or T4. Cost each honestly. The right answer is probably a T1 fall path plus a T2 assistant path, but prove it.

### 1.4 Recommend

Recommend one primary architecture and one fallback, with the specific evidence that decided it. Produce a comparison table across at least four candidate architectures scoring: gait metric fidelity, fall detection reliability, bathroom coverage, privacy posture, install difficulty, per home BOM, and consumer acceptability.

**Stop. Report. Wait.**

---

## PHASE 3: HARDWARE AND BOM
**Output: `/research/a/phase3_hardware.md`**

Only for the architecture selected in Phase 2. Do not cost architectures that were rejected.

### 2.1 Compute silicon

Derive the requirement from the model selected in Phase 4, or if ordering forces it, derive a requirement envelope first and validate it in Phase 3. State clearly which you did.

Candidates to evaluate. Do not stop at the ones named here, but do not omit them either.

- **NVIDIA Jetson Orin Nano and Orin NX.** Capable, expensive, thermally hungry. Establish real module price at volume, not dev kit price.
- **Hailo-8L and Hailo-10.** Accelerator, needs a host.
- **Sony IMX500.** Inference inside the image sensor. Directly relevant to the "no video ever leaves" claim, because the pixel data never leaves the sensor package. Investigate carefully.
- **Ambarella CV2x and CV5 family.** Purpose built for exactly this.
- **Rockchip RK3588 and RK3576.** Cheap, NPU on board, strong Chinese supply chain.
- **Allwinner, Amlogic, SigmaStar.** The low cost IP camera SoCs that the entire Alibaba camera module ecosystem is actually built on. This is where the cost floor lives.
- **STM32N6.** ST's NPU capable MCU. Relevant given existing ST relationships.
- **Kneron, Synaptics Katana, Analog Devices MAX78000.** Ultra low power vision.
- **Nordic nRF54.** Radio and low power MCU. Not a vision processor. Correct role is the radio and sensor hub, not the inference engine. State this rather than evaluating it as a vision candidate.
- **Arduino.** Not a candidate for anything in this system. Say so once and move on.

For each viable candidate: TOPS or equivalent, power at load, package cost at each volume tier, availability and lead time, toolchain maturity, whether the selected model actually runs on it and at what frame rate, and thermal dissipation in a sealed enclosure.

### 2.2 Image sensor and optics

Specify from the gait requirement, not from a spec sheet wish. Resolution, frame rate, field of view, low light sensitivity, IR sensitivity, and IR illuminator requirement. Then find the cheapest sensor and module that meets it. Search the actual module supply: Alibaba, Made in China, Chinese ODM camera module houses, and Western distribution. Compare a $4 module against a $40 module on the specific requirement, not on general quality.

### 2.3 Everything else

Radio (WiFi, Thread, BLE, and whether the assistant needs a microphone and speaker), power supply and the AC to DC stage, enclosure, thermal management, microphone array if voice is in scope, indicator LED, and any pairing or provisioning hardware.

### 2.4 Non camera nodes

Cost the seat pad, bed mat, radar node, and any other sensor node in the recommended architecture. For the seat pad specifically: ballistocardiography derived HR from a load cell or piezo array. Establish whether that is a real, buildable, accurate measurement or a research demo. Cite.

### 2.5 Output

Full BOM at 1, 100, 1k, 10k, 100k. Landed cost. COGS. NRE including tooling and certification. Explicit statement of what a single complete home system costs to build at each tier, where a home is defined as a stated number of nodes covering a stated number of rooms.

Then state the implied retail price at a target gross margin, and compare it to the actual price of every competing product on the market.

**Stop. Report. Wait.**

---

## PHASE 4: SOFTWARE, MODELS, AND OPEN SOURCE
**Output: `/research/a/phase4_software.md`**

The governing question for every item: **does this already exist, and can we use it?** Build is the last resort, not the first.

### 3.1 Vision and pose

- Human pose estimation: evaluate the current open weight options. Verify licenses. Several widely used pose models carry licenses that prohibit or complicate commercial use. This is a real risk and it must be checked per model, not assumed.
- NVIDIA's offerings specifically: what is actually released, under what license, requiring what runtime, and whether it locks the BOM to NVIDIA silicon. The concept description assumes NVIDIA. Test that assumption.
- Fall detection: published approaches, published accuracy, and the false positive problem. A fall detector that cries wolf twice a week gets unplugged in month two. Find real world false positive rates, not benchmark numbers.
- Gait metric extraction from pose keypoints: what is published, what is validated against gold standard (instrumented walkway, motion capture), and what the error bars actually are.

### 3.2 Activity of daily living and pattern detection

Room level occupancy, transition counting, duration in state. This is mostly not machine learning. Say so if true. Cheap, reliable, and boring beats a model.

### 3.3 Scene memory and object location

The "where is my phone" feature. Requires: a persistent room map, room naming during onboarding, object detection over a vocabulary of household objects, a temporal store of last known object location, and a retrieval interface. Specify each. Estimate the model, the storage, and the compute. Determine which topology from Phase 2.3 it forces. This feature is likely the single largest driver of compute cost in the system. Establish whether it belongs in v1.

### 3.4 The assistant layer

See `shared/shared_llm_layer.md`. Concept specific questions: wake word, on device speech to text versus cloud, latency tolerance for conversation, cost per resident per month, and the safety envelope. The assistant talks to an older adult who may be lonely, confused, or in distress. Define the escalation behavior and the refusal behavior. Define what happens when the resident says something that suggests a medical emergency, and define it in a way that survives the wellness positioning.

### 3.5 Caregiver application

Mobile and web. Notification delivery, escalation ladder, emergency contact tree, and the decision about whether the system ever calls emergency services directly. That decision has liability consequences. Research what existing PERS providers do and what their terms of service say.

### 3.6 Build versus buy table

Every subsystem. Open source option, license, commercial option, cost, gap analysis, and the estimated engineering weeks to close the gap.

**Stop. Report. Wait.**

---

## PHASE 5: DATA, PRIVACY, AND SECURITY ARCHITECTURE
**Output: `/research/a/phase5_privacy.md`**

Inherits `shared/shared_privacy_security.md`. Concept specific work:

1. Data flow diagram for the recommended architecture. Every hop, every store, every retention period.
2. Prove or disprove the claim "no video leaves the device." Identify every code path that could violate it, including debug, OTA, crash dumps, and remote support.
3. Consent architecture. The resident is the data subject. The caregiver is the buyer and the user. These are different people with different interests. Design for the case where the resident does not want to be watched. Design for cognitive impairment and the question of who can consent on whose behalf. This is not a legal footnote, it is a product design constraint and a market objection.
4. Applicable law: state biometric privacy statutes, wiretap and two party consent statutes if audio is recorded, and the conditions under which HIPAA attaches (it attaches through the customer, not the product, so a home health agency channel changes everything).
5. Threat model. A camera in a bedroom is a high value target. Specify: secure boot, signed firmware, encrypted storage, key management, OTA security, and what happens when the company is breached.
6. What the architecture allows us to say in marketing, stated as approved claim language.

**Stop. Report. Wait.**

---

## PHASE 6: DEVELOPMENT PLAN, COST, AND TIMELINE
**Output: `/research/a/phase6_devplan.md`**

Per framework section 4.

1. Work breakdown structure to each gate G1 through G6. Firmware, computer vision, backend, mobile, hardware, industrial design, certification, QA, and operations.
2. Timeline and cost at 1, 2, 3, and 4 engineers. State the discipline mix at each headcount. One engineer cannot do embedded vision, iOS, and cloud infrastructure well. Name the tradeoff.
3. AI assisted velocity multiplier, cited and justified. Low, mid, high cases.
4. Critical path. Name the longest pole. It is probably certification or false positive rate reduction, not feature development.
5. Comparable ventures. Find companies that built something similar. Establish how long it actually took them and how much they actually raised before each milestone. Use funding announcements, press, and filings. This is the single best sanity check on any internal estimate, and it is the section most likely to contradict the founder's timeline.
6. Test plan by gate. G2 is the founder's own home. G3 is family and friends. Specify the instrumentation: what is logged, what constitutes a false positive, what the ground truth is, and how ground truth is established in a real home where nobody is annotating video.

The ground truth problem is severe and under appreciated. Design for it now.

**Stop. Report. Wait.**

---

## PHASE 7: MARKET, COMPETITION, AND CHANNEL
**Output: `/research/a/phase7_market.md`**

1. **Bottom up market sizing.** Count. US adults 65 and over living alone. Subset with a remote adult child. Subset with the income or the family income to pay. Subset reachable through each channel. Multiply by realistic price and realistic penetration. Then, and only then, cite an analyst TAM as a check.
2. **Competitive landscape.** At minimum, research and profile: SafelyYou, Vayyar Care, CarePredict, Sensi.ai, Cherry Home, Origin Wireless, Emerald Innovations, Tellus, Lively and GreatCall, Medical Guardian, Bay Alarm Medical, Life Alert, Apple Watch fall detection, Amazon Alexa Together and its fate, Best Buy Health and Current Health and its fate. For each: what they sell, to whom, at what price, how much they raised, current status. **Pay particular attention to the ones that shut down or were wound down. The failures in this category are more informative than the successes.**
3. **Channel analysis.** Compare, on CAC, sales cycle, contract size, and gross margin: direct to consumer, Medicare Advantage supplemental benefits, home health and home care agencies, senior living and assisted living operators, health systems and ACOs, long term care insurers, and hardware retail.
4. **Reimbursement.** Research current CPT codes for remote physiologic monitoring and remote therapeutic monitoring, chronic care management, and principal care management. Establish what a wellness positioned product can and cannot bill for, and what would have to change for it to bill. Note that reimbursement generally requires the medical device positioning the concept is trying to avoid. Name that tension. It is the central strategic tension of this business.
5. **Partners.** Camera and module ODMs, contract manufacturers, silicon vendors with startup programs, PERS monitoring call centers (do not build a 24/7 call center, buy it), wearable vendors, senior living operators willing to host a pilot, and academic gait labs for validation.
6. **Willingness to pay.** Find published data on what families actually pay for aging in place technology and what the churn looks like.

**Stop. Report. Wait.**

---

## PHASE 8: BUSINESS CASE AND CAPITAL
**Output: `/research/a/phase8_businesscase.md`**

1. Three scale scenarios, small, mid, large, per framework section 4. Full P&L shape, burn, headcount, capital required, months to breakeven.
2. Pricing model options: hardware plus subscription, hardware subsidized with subscription, hardware free with a long subscription commitment, per bed per month to an operator, per member per month to a payer. Model each.
3. Capital plan. What raises when, against which gate. Non dilutive first: NIH and NIA SBIR is directly relevant to aging in place technology and should be researched by name, along with NSF SBIR. Then angel, pre seed, seed. Identify actual funds and actual partners who have written checks in this category in the last 24 months, with the specific deals as evidence. Do not produce a generic list of aging tech VCs.
4. Milestone to unlock map. For each gate: what this gate proves, who cares that it is proven, what conversation it opens, and what it is worth in valuation or contract terms.
5. Risk register. Technical, regulatory, commercial, and existential. For each: likelihood, impact, mitigation, and the leading indicator that tells us it is happening.
6. Kill criteria. State, in advance, what finding would make this not worth building. A business case without kill criteria is a pitch, not an analysis.

**Stop. Report. Wait.**

---

## PHASE 9: SYNTHESIS
**Output: `/research/a/CONCEPT_A_BUSINESS_CASE.md`**

Single document. Executive summary of no more than two pages, then the case, then the appendices. Written for a reader who will decide whether to fund it. Every number traceable to a phase output. Every open question surfaced, not buried.

---

## PRIORITY ORDER IF TIME OR BUDGET IS CONSTRAINED

Phase 1 (markers), Phase 2 (architecture), and Phase 7 (market and channel) are the three that can kill the concept. Do them first and do them well. Phase 3 and Phase 6 tell you what it costs. Phases 4, 5, and 8 are execution detail that only matters if the first three survive.

---

# PART IV — THE TEN PHASE OUTPUTS


===================================================================
# (phase0_scope.md)
===================================================================

# CONCEPT A, PHASE 0: SCOPE NORMALIZATION

Governed by `00_framework.md`. Positioning is general wellness per framework section 2. This file scopes only. It does not choose sensors, silicon, or price. Those are Phase 1 and later.

---

## 1. ONE PAGE RESTATEMENT: SETTLED versus OPEN

### Concept, as understood
A passive, easy install, in home system for an older adult living alone whose caregiver is remote. It observes movement, gait, and daily activity without the resident wearing, charging, or operating anything. It notifies designated contacts on an event. It surfaces changes in daily patterns over time. A conversational layer lets the resident interact and lets the caregiver ask questions about the home. Positioning is general wellness, not a medical device.

### SETTLED (strategic decisions, not to be relitigated)
| # | Settled item | Basis |
|---|--------------|-------|
| S1 | General wellness positioning, not a medical device | Framework section 2. Decided with FDA regulator and quality input. |
| S2 | The product surfaces patterns to a human. It does not output a diagnosis. Input versus inference is the governing line. | Framework section 2. |
| S3 | Event detection plus escalation to a designated contact or emergency service is inside the lane | FDA General Wellness policy; Apple Watch fall detection precedent. |
| S4 | Measured metrics with trend against the user's own baseline are inside the lane | FDA General Wellness policy; Apple mobility metrics precedent. |
| S5 | The buyer and the data subject are different people (caregiver buys, resident is observed) | Concept statement. Consent architecture consequence deferred to Phase 5. |
| S6 | Two regulators bind, not one. FDA governs device status; FTC governs claim truth and converts each measurement claim into a validation cost | Framework section 2; FTC Health Products Compliance Guidance. |

### OPEN (hypotheses to validate in later phases, do not treat as decided)
| # | Open item | Founder assumption ref | Phase that resolves |
|---|-----------|------------------------|---------------------|
| O1 | Camera in a light bulb form factor is the right sensor placement | A1 | Phase 2 |
| O2 | Full inference on the camera node, only derived data leaves | A2 | Phase 2, Phase 3 |
| O3 | Vision is the primary modality (versus radar, WiFi CSI, pressure, PIR) | A3 | Phase 2 |
| O4 | Raw sensor data is obtainable from a consumer wearable band | A4 | shared_wearable_data_access |
| O5 | An NVIDIA open source vision model is the right starting point | A6 | Phase 4 |
| O6 | The buyer is the adult child paying a consumer subscription | A7 | Phase 7 |
| O7 | A ceiling down view can actually measure the claimed gait metrics | A1 | Phase 1, Phase 2 |
| O8 | The object memory and natural language query features fit v1 economics | A2 | this phase (compute), Phase 3 (cost) |

The single scope hazard already visible: the concept bundles a cheap event detector (fall) with two features (object permanence, natural language scene query) whose compute envelope is materially larger. Section 5 below quantifies that split. It is the most important finding of Phase 0.

---

## 2. FEATURE INVENTORY (numbered)

Every capability implied by the concept description. Classification in the next section.

1. Fall detection (event: a fall occurred)
2. Fall event notification and escalation to designated contact or emergency service
3. Long lie detection (time on the floor after a fall)
4. Gait metrics (walking speed, stride length, cadence)
5. Sway and balance metrics with a walking steadiness classification
6. Step and mobility metrics, including life space within the home (rooms visited, floor traversed)
7. ADL: bathroom visit frequency, day and night
8. ADL: kitchen use and meal preparation events
9. ADL: sleep location (bed versus chair)
10. ADL: time in bed
11. ADL: chair transfers (sit to stand events and duration)
12. Object location memory ("where is my phone")
13. Conversational check in with the resident
14. Medication reminder prompts and adherence logging
15. Caregiver query interface (natural language questions over the home history)
16. Trend reporting (daily and weekly caregiver report)
17. Environmental hazard inventory (loose rugs, clutter in paths, poor night lighting, obstructed stairs)
18. Red flag emergency escalation layer (hard coded, prevents delayed care)
19. Fall risk prediction score (predictive likelihood output)
20. Cognitive decline inference (from object misplacement frequency, repeated questions, speech)
21. Mood or depression inference (from passive behavioral data)

Items 19 through 21 are included because the concept description implies them (object misplacement is a "self generating cognitive signal," speech is flagged as highest claim risk). They are inventoried so they are explicitly classified, not silently dropped.

---

## 3. CLASSIFICATION: CORE / DIFFERENTIATOR / LATER / BLOCKED

CORE means v1, no product without it. DIFFERENTIATOR means v1 if affordable. LATER means v2 or v3. BLOCKED means it cannot ship as a stated output in the wellness lane; the reframing (not the raw feature) may still ship.

| # | Feature | Class | Rationale |
|---|---------|-------|-----------|
| 1 | Fall detection | CORE | The event that justifies the system. Defensible as event detection. |
| 2 | Fall notification and escalation | CORE | Without escalation the detection is inert. |
| 3 | Long lie detection | CORE | Highest value single signal per framework, trivially defensible as event detection, low incremental compute over fall. |
| 6 | Step, mobility, and life space patterns | CORE | Cheap, reliable, mostly not machine learning. Carries the "changes over time" value proposition. |
| 16 | Trend reporting | CORE | The surfaced output the caregiver actually consumes. Product is invisible without it. |
| 18 | Red flag escalation layer | CORE | Safety requirement. Prevents the delayed care scenario that is the category's core liability. |
| 4 | Gait metrics | DIFFERENTIATOR | Strong precedent (Apple ships these as wellness). Conditional on viewing angle (O7); may be unmeasurable from ceiling. |
| 5 | Sway and steadiness classification | DIFFERENTIATOR | Precedent exists (Apple walking steadiness with fall likelihood notification). Same viewing angle risk. |
| 7 | Bathroom frequency | DIFFERENTIATOR | High value general health signal. Camera unacceptable in bathroom; forces a non camera modality. Cost consequence, not a claims problem. |
| 8 | Kitchen use | DIFFERENTIATOR | Nutrition proxy, defensible as activity count. Validation of the proxy is open (Phase 1). |
| 9 | Sleep location | DIFFERENTIATOR | Defensible as location classification. |
| 10 | Time in bed | DIFFERENTIATOR | Measurement, defensible. |
| 11 | Chair transfers | DIFFERENTIATOR | Passive proxy for a chair stand test. Defensible as measurement. |
| 13 | Conversational check in | DIFFERENTIATOR | Adds engagement and retention. Pushes compute topology (section 5). Safety envelope required. |
| 14 | Medication reminders | DIFFERENTIATOR | Reminders and adherence logging are explicitly inside the lane. Low cost, retention positive. Dose guidance is out. |
| 17 | Environmental hazard inventory | DIFFERENTIATOR | Zero inference about the person, fully defensible, actionable in an afternoon, no competitor emphasizes it. Strong wedge. |
| 12 | Object location memory | LATER | Largest compute driver in the system (section 5). Forces a hub or cloud. Weak clinical value relative to cost. Defer to v2. |
| 15 | Caregiver natural language query | LATER | Requires the same VLM plus retrieval stack as object memory. Ship a structured (non natural language) caregiver report in v1; defer free form query. |
| 19 | Fall risk prediction score | BLOCKED | Predictive risk output on a diagnosable outcome. Reframe: ship the steadiness classification with a general notification (feature 5), which precedent permits. Do not ship a "you are likely to fall" score. |
| 20 | Cognitive decline inference | BLOCKED | Screening claim on a diagnosable condition (dementia). Reframe: trend the self generating signal, surface the pattern, prompt a clinician conversation. Research only for speech metrics. No output string. |
| 21 | Mood or depression inference | BLOCKED | Screening claim. Reframe: self report journal, surface the trend, let a human conclude. |

Counts: CORE 6, DIFFERENTIATOR 10, LATER 2, BLOCKED 3.

---

## 4. CLAIMS MATRIX (per framework section 2)

Columns per the framework required deliverable. Data type is self report, measurement, or inference. Validation evidence is what FTC competent and reliable scientific evidence would demand to substantiate the measurement.

| Feature | Shipping phrasing (inside lane) | Data type | Guidance or precedent that permits it | Phrasing that crosses the line | FTC validation evidence required |
|---------|---------------------------------|-----------|---------------------------------------|--------------------------------|----------------------------------|
| Fall detection | "A fall was detected in the kitchen at 3:42 pm." | Measurement (event) | FDA General Wellness policy; Apple Watch hard fall detection ships as consumer wellness | "You are at high risk of falling." (prediction) | Detection sensitivity and specificity against annotated ground truth falls; characterized false positive rate |
| Fall notification and escalation | "We alerted your contact and, after no response, emergency services." | Measurement (event) plus action | Apple Watch automatic Emergency SOS after unresponsive hard fall | Any claim the system prevents falls | Escalation reliability, time to alert, delivery confirmation |
| Long lie detection | "A person has been on the floor for 12 minutes." | Measurement (event plus duration) | Event detection, same basis as fall | "Prolonged floor time indicates [named condition]." | Time on floor accuracy versus ground truth; immobility discrimination |
| Gait metrics | "Walking speed is 18 percent below the 30 day baseline." | Measurement | Apple ships walking speed, step length, double support time, walking asymmetry as wellness (iOS mobility metrics) | "Your gait indicates Parkinson's / neurological decline." | Camera derived gait speed error versus an instrumented walkway or motion capture reference standard. This is the central Phase 1 measurement validation. |
| Sway and steadiness | "Walking steadiness is classified Low this week." | Measurement plus classification | Apple Walking Steadiness ships an OK / Low / Very Low classification with a notification referencing fall likelihood | "This means you will fall." | Classification agreement against a reference balance measure; false classification rate |
| Life space and mobility | "3 of 6 rooms visited today, down from a typical 5." | Measurement | Activity and location counting, non diagnostic pattern change | "Room contraction is a sign of dementia." | Room occupancy and transition accuracy versus ground truth logs |
| Bathroom frequency | "Night time bathroom visits rose from 4 to 9 this week." | Measurement (pattern change) | Framework: a pattern change is inside the lane | "This indicates a urinary tract infection." | Visit count accuracy from the chosen non camera modality |
| Kitchen use | "Meal preparation events dropped from 3 to 1 per day." | Measurement | Activity count, non diagnostic | "You are malnourished." | Event detection accuracy; validity of the count as a nutrition proxy (open) |
| Sleep location | "Slept in the chair 4 of the last 7 nights." | Measurement (classification) | Location classification, non diagnostic | "Chair sleeping indicates heart failure." | Location classification accuracy |
| Time in bed | "Time in bed averaged 11 hours, up from 8." | Measurement | Duration measurement | "You are depressed." | Duration accuracy versus ground truth |
| Chair transfers | "Sit to stand now takes 2.4 seconds, up from 1.6." | Measurement | Measurement plus trend versus own baseline | "You have sarcopenia." | Transition time accuracy versus a timed chair stand reference |
| Conversational check in | "How are you feeling today?" then stores and trends the answer | Self report | Self report is not a claim; mood and symptom journals are ubiquitous consumer features | Assistant asserting a diagnosis from the conversation | Substantiation not required for reflecting self report; the escalation logic (feature 18) does require validation |
| Medication reminders | "Time to take your morning medication." Logs taken or not. | Self report plus action | Reminders and adherence logging are inside the lane per framework | "Increase your dose." / "Skip this pill." (treatment claim) | Reminder delivery reliability; adherence log accuracy |
| Trend reporting | Charts of the above metrics against the person's own baseline | Measurement plus self report | Trending measurement and reference to normative range is measurement, not diagnosis | Any report field that names a disease as a conclusion | Inherits the validation burden of each metric it displays |
| Environmental hazard inventory | "A loose rug is present in the hallway walking path." | Measurement (of the environment) | Zero inference about the person; object detection of a static hazard | "This hazard will cause a fall." | Hazard detection accuracy versus labeled ground truth |
| Object location memory | "Your phone was last seen on the kitchen counter." | Measurement (object state) | Object detection plus last seen location; a convenience feature, not a health claim | Inferring cognitive state from misplacement frequency | Object recognition and last seen location accuracy |
| Caregiver query | Answers factual questions over stored, already validated metrics | Measurement (retrieval) | Retrieval over data already permitted above | Generating a diagnostic conclusion in the answer | Inherits the validation of the underlying metrics; retrieval faithfulness |
| Fall risk prediction (BLOCKED) | Do not ship as a predictive score | Inference | None. Reframe to steadiness classification. | "Your fall risk score is 82 / 100." | Not applicable; blocked |
| Cognitive inference (BLOCKED) | Do not ship an output string | Inference | None. Research only. Reframe to self report trend plus clinician prompt. | "Signs of dementia detected." | Not applicable; blocked |
| Mood inference (BLOCKED) | Do not ship an output string | Inference | None. Reframe to self report journal. | "This pattern is consistent with depression." | Not applicable; blocked |

Cross cutting FTC note: every measurement row converts into a validation cost that lands at G3 and G4. The most expensive single line is camera derived gait speed accuracy against an instrumented walkway, because gait speed is the metric the concept most wants to trend and the one with the largest reference standard gap. Cost it in Phase 6, not as a footnote.

---

## 5. COMPUTE DELTA: FEATURES MATERIALLY LARGER THAN FALL DETECTION

### Baseline: fall detection
Fall and long lie detection are pose keypoint extraction plus a short temporal classifier, or a low resolution motion classifier. They run in real time on a low cost camera SoC or a small NPU. Only an event and a timestamp leave the node. This is the compute floor of the system and it fits topology T1 (full inference on the sensor node). Gait, sway, ADL counts, and hazard inventory sit within roughly the same order of magnitude; hazard inventory can run periodically (batched), not real time.

### The two features that break the envelope
| Feature | What it actually requires | Model class | Memory pressure | Fits edge? | Forces |
|---------|---------------------------|-------------|-----------------|------------|--------|
| Object location memory (feature 12) | Persistent semantic scene graph of the home; open vocabulary object detection over a room map; temporal state store of last known location per tracked object; a retrieval interface | Open vocabulary detector plus a scene graph store plus retrieval; VLM to resolve free form object references | Detector plus persistent graph plus continuous per object state; grows with object vocabulary and home size | No, not on a low cost camera SoC | A hub (Jetson Orin NX 16GB class) or cloud |
| Caregiver natural language query (feature 15) and conversational assistant (feature 13) | Speech to text; a language model for the dialog; retrieval over the temporal store and scene graph; text to speech | VLM plus LLM plus STT plus TTS | A capable VLM needs materially more than a camera node carries. LLaVA-OneVision-7B needs about 16GB in fp16 for weights alone; Jetson Orin Nano 8GB runs efficient VLMs (for example VILA-2.7B) only with aggressive 4 bit quantization; the 16GB Orin NX is the practical floor for an 8 bit VLM | No, not on a camera node | A hub or cloud |

### Interpretation
Object permanence and natural language scene query share one stack: a persistent scene representation plus open vocabulary perception plus a language model over retrieval. Academic home robot systems that do this (GraphEQA, EmbodiedLGR) run the VLM plus memory pipeline locally, but on robot class compute, not on a light bulb. The camera node cannot host it. This confirms founder assumption A2 is wrong as stated: the described features do not all fit "compute happens on the camera."

### Consequence for architecture (flagged for Phase 2, not decided here)
The system splits into two compute tiers:
- A T1 fall and metrics path on the camera node, which preserves the "no video ever leaves" claim for the safety critical function.
- A T2 or T4 assistant and memory path on an in home hub (or cloud), which the object memory and natural language features require.

This is a hub bearing architecture, not a single node one, the moment features 12, 13, and 15 enter v1. That is the primary reason those three are classed LATER (12, 15) or conditional DIFFERENTIATOR (13): they change the bill of materials and the data exit story, not merely the software scope. Object location memory (feature 12) is the single largest compute driver in the system.

---

## Register Entries

Not written to `/research/registers/` per instruction (this phase writes only its own file). Staged for the register owner to append.

Sources (for `sources.md`):
| Source | Org, date | Used for | Credibility |
|--------|-----------|----------|-------------|
| General Wellness: Policy for Low Risk Devices | FDA, updated 2026-01-06 (supersedes 2019) | Wellness lane definition; low risk test | HIGH, primary |
| Section 520(o)(1)(B) FD&C Act, 21st Century Cures Act (2016-12-13) | US statute | Software function device exclusion | HIGH, primary |
| Health Products Compliance Guidance | FTC, 2022-12-20 | Competent and reliable scientific evidence standard; RCT expectation | HIGH, primary |
| Measuring Walking Quality Through iPhone Mobility Metrics | Apple, 2022-05 | Precedent: walking speed, step length, double support, asymmetry ship as wellness | HIGH, primary vendor |
| Measure your walking steadiness (support.apple.com/102504) | Apple | Precedent: steadiness OK/Low/Very Low classification with notification | HIGH, primary vendor |
| Use Fall Detection with Apple Watch (support.apple.com/108896) | Apple | Precedent: hard fall detection plus automatic emergency call escalation | HIGH, primary vendor |
| Symptom Radar | Oura, 2024 launch | Precedent: temperature and readiness deviation ships as wellness with tiered signal | HIGH, primary vendor |
| Getting Started with Edge AI on NVIDIA Jetson (LLMs, VLMs) | NVIDIA / Edge AI and Vision Alliance, 2026-01 | Edge VLM memory tiers; Orin Nano vs NX vs AGX | MEDIUM, vendor technical |
| GraphEQA: 3D Semantic Scene Graphs for Real time Embodied QA | arXiv 2412.14480 | Scene graph plus VLM for home QA runs on robot class compute | MEDIUM, preprint |
| EmbodiedLGR: Lightweight Graph Representation and Retrieval | arXiv 2604.18271 | Local VLM plus semantic graph plus time based retrieval; confirms stack shape | MEDIUM, preprint |

Competitors / precedents noted this phase (for `competitors.md`, full profiling in Phase 7): Apple (Watch fall detection, iPhone mobility metrics, Walking Steadiness) as the dominant wellness precedent; Oura (Symptom Radar) as the deviation signal precedent. Both are precedent assets, not direct competitors to the passive in home concept.

---

## Open Questions
1. Can a ceiling down or bulb mounted camera actually measure gait speed, stride length, and sway to a standard that survives FTC substantiation against an instrumented walkway? Blocks the gait and sway DIFFERENTIATOR classification. (O7, Phase 1 and 2)
2. What non camera modality covers the bathroom (feature 7), and at what added BOM? The bathroom is both the highest fall risk room and the room where a camera is unacceptable. (Phase 2)
3. Does refrigerator or cabinet interaction count have published validation as a nutrition proxy (feature 8)? Marked UNKNOWN. (Phase 1)
4. Is the 2026-01-06 FDA General Wellness revision materially different from the 2019 version in any way that narrows the lane for passive home monitoring? Full text not yet read; flagged for the precedent dossier. UNKNOWN pending primary read.
5. Exact incremental compute of long lie detection over fall detection assumed negligible; not yet measured. (Phase 3, Phase 4)
6. Whether a v1 caregiver report can deliver value with structured query only, deferring natural language query (feature 15) to v2 without losing the core value proposition. (Phase 1 report spec)

## Assumptions Made
1. Long lie detection is low incremental compute over fall detection and therefore CORE. Impact if wrong: it moves to DIFFERENTIATOR and the CORE count drops to 5. Confidence MEDIUM.
2. Life space and ADL counting are "mostly not machine learning" and cheap, per framework section 3.2, justifying feature 6 as CORE. Impact if wrong: cost rises, but classification holds. Confidence MEDIUM.
3. Medication reminders are treated as inside the lane (reminders and adherence only, no dose guidance). Founder assumption, consistent with framework. Confidence HIGH.
4. The three inference features (19, 20, 21) are inventoried as implied by the concept even though the concept does not name them as products, because object misplacement and speech are explicitly flagged in the brief. If the founder never intended them as outputs, they simply confirm as BLOCKED with no loss. Confidence HIGH.
5. Edge VLM memory figures (LLaVA 16GB fp16, Orin Nano 8GB needs 4 bit, Orin NX 16GB floor) are drawn from vendor and preprint sources, not benchmarked on the exact model this product will use. Directionally sound, not final. Confidence MEDIUM.
6. Concept description inputs (form factor, modality, buyer) remain founder assumptions, not findings, per framework rule 8. Carried as OPEN, not settled.

## Confidence Summary
Overall confidence HIGH on the scope structure, the classification logic, and the compute split conclusion, which is the load bearing finding of this phase. The regulatory precedent is grounded in primary sources (FDA, FTC) and primary vendor documentation (Apple, Oura) and is HIGH. The weakest elements are: (a) the gait and sway DIFFERENTIATOR classifications, which hinge on an unresolved measurement feasibility question (Open Question 1) and could move to LATER if a ceiling view cannot meet FTC substantiation; (b) the precise edge versus hub compute thresholds, which are MEDIUM pending a model specific benchmark in Phase 3 and Phase 4; and (c) the assumption that the 2026 FDA revision does not narrow the lane, which is UNKNOWN until the primary text is read for the precedent dossier. None of these weaken the central conclusion that object permanence and natural language scene query force a hub and belong to a later version.


===================================================================
# (phase1_markers.md)
===================================================================

# Concept A, Phase 1: Marker and Trend Catalog

Governed by `00_framework.md` (sections 2, 5, 6, 9) and `01_concept_a_elder_monitoring.md` (Phase 1). Positioning is general wellness. Every row below is written to the input versus inference rule in framework section 2: physical quantities are measured and trended, affective and cognitive states are self reported, and no disease name is inferred from passive data.

This phase defines the sensing requirement. No sensor was chosen first. Phase 2 scores architectures against the v1 shortlist and the Sensing Requirement Matrix in this document.

Citation keys `[P#]` resolve in the Register Entries papers table at the end. Confidence tags are HIGH, MEDIUM, LOW per framework section 5.

---

## 1. Full Marker Catalog

Columns follow the Phase 1 row spec. Evidence is stated in brief with the load bearing number; full effect size, population, design, and gold standard status live in the papers register. "Own" = own rolling baseline, "Norm" = published normative range, "Both" = both apply.

### 1.1 Gait and mobility

| Marker | What it indicates (non diagnostic) | Evidence | Data type | Sensing modality + spec demanded | Baseline | Time to signal | Actionability | Defensible framing (exact string) | Validation burden (FTC) | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Usual gait speed and trend | Global function and reserve. A vital sign level correlate of survival and disability | HIGH. Pooled 34,485 adults 65+, 0.8 m/s tracks median life expectancy, each +0.1 m/s raises survival [P1]. Meaningful change 0.05 m/s, substantial 0.10 m/s [P2]. Camera RMSE 0.04 m/s vs pressure walkway [P3b], Kinect ICC 0.81 to 0.98 vs GAITRite [P3a] | Measurement | Camera with pose estimation. Side or oblique view, unobstructed straight path 2.5 to 4 m in frame, 15 to 30 fps min. Nadir ceiling view degrades it (see section 5) | Both | 2 to 4 weeks to establish baseline, then a 0.10 m/s sustained drop is above measurement noise | Prompt a PT referral or a clinic gait assessment. A sustained drop is the strongest single trend trigger in the catalog | "Walking speed is 0.72 m/s, down 14 percent from the 30 day baseline of 0.84 m/s." | Bench study of camera derived speed vs an instrumented walkway (GAITRite or equivalent) across placements and lighting, reporting bias and 95 percent limits of agreement | v1 |
| Stride length and cadence | Components of gait speed. Localize whether a speed drop is shorter steps or slower cadence | MEDIUM. Markerless motion capture stride length RMSE 0.05 to 0.08 m, cadence RMSE 2.3 steps/min vs pressure walkway [P3b] | Measurement | Camera, same spec as gait speed. Stride length needs a calibrated ground plane | Both | 2 to 4 weeks | Adds interpretation to a speed change, not independently actionable | "Average step length 0.51 m." | Same bench study as gait speed | v2 |
| Stride time variability (CV) | Rhythm instability. A prospective fall predictor independent of speed | HIGH. 52 adults 70+, stride time variability 106 ms in future fallers vs 49 ms in non fallers, ~5x fall likelihood [P4] | Measurement | Camera pose or floor sensing. Requires many consecutive strides at ~30 fps; single short in home paths may not yield enough strides | Own | 4 to 8 weeks (needs many gait bouts) | Elevated variability supports a fall risk conversation and hazard review | "Stride timing is more irregular than the 60 day baseline." | Bench study vs force sensitive insoles or instrumented walkway; establish minimum stride count for a stable CV | v2 |
| Lateral sway amplitude, step width | Dynamic balance during walking | LOW to MEDIUM. Step width variability associated with fall risk at faster speeds [P4 related, see register] | Measurement | Camera, frontal or oblique view. Nadir view cannot resolve lateral sway reliably | Own | 4 to 8 weeks | Supports fall risk context | "Side to side sway during walking has increased." | Bench validation vs motion capture (Vicon class) | v2 |
| Walking and weight bearing asymmetry | Unilateral problem, pain, or post event change | LOW. Shipped as a wellness metric on consumer wearables (precedent, framework section 2). In home camera validation UNKNOWN | Measurement | Camera, oblique view. Nadir view cannot resolve reliably | Own | 4 to 8 weeks | Prompts a check for a new limp or pain | "Walking asymmetry has increased week over week." | Camera derived asymmetry vs motion capture. Currently UNKNOWN | v2 |
| Turn duration, turn steps, hesitation | Balance and executive control during direction change | MEDIUM. Turning slowness and step count associated with fall risk and cognitive load (see register) | Measurement | Camera, overhead or oblique both workable for turn detection | Own | 4 to 8 weeks | Supports fall risk context | "Turns are taking longer than baseline." | Bench validation vs motion capture | v2 |
| Gait initiation hesitation, freezing | Basal ganglia motor control (parkinsonian pattern), non diagnostic | LOW for in home camera. Research grade only | Measurement | Camera, high frame rate | Own | UNKNOWN | Prompts clinician conversation | "Pauses before starting to walk have increased." | Not substantiable at v1 | research only |
| Dual task gait cost | Cognitive motor interference. Slowing while talking tracks cognitive load | MEDIUM. Higher dual task cost correlates with cognitive decline across the spectrum; meta analytic support in MCI [P6]. Requires a controlled secondary task, not passively inducible | Measurement plus prompt | Camera plus the assistant issuing a standardized verbal task. Not a purely passive metric | Own | UNKNOWN passively | Prompts cognitive conversation with clinician. Claim sensitive | "Walking slowed more than usual while talking." | Would require a validated in home dual task protocol. Not available | research only |
| Stair ascent/descent time, step pattern, handrail use | Lower limb strength, confidence, safety behavior | LOW. Clinically recognized, in home camera validation UNKNOWN. Many target homes are single story | Measurement plus inference | Camera on the stair, oblique. Not a ceiling bulb view | Own | UNKNOWN | Prompts handrail install or PT | "Uses the handrail on the stairs more than before." | High. Not substantiable at v1 | v2 |

### 1.2 Balance, near falls, and compensation

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Furniture surfing (contact with walls and furniture while walking) | Balance impairment and reduced confidence. A recognized early clinical sign | LOW as primary literature. Clinically described as an early warning sign [P18]; no quantified in home effect size found | Inference | Camera, room level, oblique. Needs furniture map and hand/body proximity detection | Own | 2 to 4 weeks | Prompts a balance assessment and a walker or grab bar conversation. High face validity to a caregiver | "Reaching for furniture or walls for support while walking." | High. This is an inference and needs a quantified concurrent validity study vs observation | v2 |
| Stumbles and recoveries (near falls that do not become falls) | Instability events short of a fall. Higher frequency precedes falls | LOW quantified for camera. Conceptually strong | Inference | Camera, room level | Own | 2 to 6 weeks | Prompts fall risk review before a fall occurs | "A near fall was detected, no fall followed." | High | v2 |
| Sit to stand transition time and attempts | Lower limb strength and power. A passive proxy for the five times sit to stand test | HIGH for the clinical test. FTSS above 15 s predicts recurrent falls in community adults 65+ [P5]; cut points 12 to 16 s across cohorts. Passive in home camera derivation validation UNKNOWN | Measurement | Camera, oblique view of the chair. Nadir view can time a rise but cannot see arm use well | Both | 2 to 4 weeks | A slowing rise or new arm use prompts strength and PT conversation | "Standing up from a chair is taking longer than the 30 day baseline." | Bench study of camera timed sit to stand vs a stopwatch administered FTSS | v1 |
| Chair rise with vs without arm use | Compensation for lower limb weakness | MEDIUM (arm use is part of FTSS scoring). Camera detection of arm use validation UNKNOWN | Inference | Camera, oblique. Nadir view weak | Own | 2 to 4 weeks | Supports the strength conversation | "Now using the armrests to stand up." | High (inference) | v2 |
| Sit to stand count per day | Passive activity and lower limb use volume | MEDIUM. Face valid activity proxy; specific validation UNKNOWN | Measurement | Camera or seat pad load sensor | Own | 1 to 2 weeks | Low activity prompts encouragement and a check for a new problem | "Stood up from sitting 9 times today vs a typical 22." | Moderate | v1 |

### 1.3 Falls and post fall

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Fall event detection | A fall occurred | HIGH clinical need. Real world detector performance is the risk: lab sensitivity 94 percent collapses to 57 percent on real falls, and false alarm burden is high [P17]. This is an engineering problem, not an evidence gap | Measurement (event) | Camera with pose or fall classifier, or mmWave radar, or thermal array. Frame rate 15 to 30 fps. Bathroom needs a non camera modality | Event | Immediate | Notify designated contact and escalate. Core product event | "A fall was detected in the kitchen at 2:14 pm." | Bench and field false positive rate characterization (framework gate G2). A detector that cries wolf gets unplugged | v1 |
| Long lie detection (time on floor after a fall) | Duration on the floor, the dominant driver of post fall outcome severity | HIGH. In adults 90+, 80 percent could not get up after at least one fall, 30 percent lay 1 hour or more; long lie associated with hospitalization, injury, and move to long term care [P7]. A long lie over 1 hour is associated with roughly doubled mortality (secondary sources, see register) | Measurement (event plus duration) | Any presence and posture modality that detects a person immobile on the floor over time. Camera, radar, thermal, or floor sensing. Must cover bathroom via non camera node | Event | Immediate to minutes | Immediate escalation. This is the single highest value feature in the product and the most defensible event detection | "A person has been on the floor of the bathroom for 22 minutes." | Lower than gait. It is event and duration detection, not a physiological measurement claim. Characterize floor detection sensitivity and false positive rate | v1 |
| Fall location and context | Where and around what activity a fall happened | MEDIUM. Bathroom is the highest fall risk room [P10 related]. Context aids caregiver response | Inference | Room level presence plus event modality | Event | Immediate | Targets the hazard review to the room | "Fall occurred in the bathroom near the tub." | Moderate | v1 |
| Self recovery after a fall | Whether the person got up unaided | MEDIUM | Inference | Same as long lie | Event | Minutes | Distinguishes a check in from an escalation | "A fall was detected and the person got up within 90 seconds." | Moderate | v1 |

### 1.4 Spatial behavior and life space

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| In home life space (rooms visited, floor plan traversed) | Functional mobility and engagement. Contraction is a documented decline marker | HIGH for life space construct. A 10 point LSA decline over 6 months raised 6 month mortality odds by 72 percent; LSA at or below 40 marks high risk [P9]. The published instrument is neighborhood scale; in home adaptation is ours to validate | Inference | Room level presence. PIR plus door contacts suffice, no camera needed. Camera optional | Own | 1 to 2 weeks | A contracting footprint prompts a wellness check and a conversation | "Time is now spent almost entirely in 2 of 5 rooms, down from 4." | Moderate. This is a behavior count, not a physiological claim. Validate room attribution accuracy | v1 |
| Room level dwell time | Where time is spent | MEDIUM. Component of life space | Measurement | Room level presence (PIR) | Own | 1 week | Feeds the life space and sleep location signals | "8 hours in the bedroom during the day, up from 3." | Low | v1 |
| Room to room transition count | Ambulation volume and activity | MEDIUM | Measurement | PIR plus door contacts | Own | 1 week | Low transitions prompt an activity check | "12 room transitions today vs a typical 34." | Low | v1 |
| Pacing and wandering | Agitation or restlessness (non diagnostic) | LOW quantified. Behaviorally recognized | Inference | Room level presence over time | Own | 2 to 4 weeks | Prompts a caregiver conversation | "Repeated back and forth walking at night." | Moderate | v2 |
| Sedentary bout length, time ambulating vs sitting vs in bed | Activity distribution and immobility | MEDIUM. Sedentary time and immobility track poor outcomes (see register) | Measurement plus inference | PIR plus seat and bed presence | Own | 1 to 2 weeks | Prolonged sedentary bouts prompt encouragement | "Longest sitting stretch today was 6 hours." | Low | v1 |

### 1.5 Sleep and circadian

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Sleep location (bed vs chair) | Sleeping in a chair signals dyspnea, edema, or bed access difficulty | LOW quantified, high clinical face validity | Inference | Bed presence (mat) plus seat presence. Bedroom camera unacceptable | Own | 1 to 2 weeks | Prompts a health check | "Slept in the recliner 4 of the last 7 nights." | Moderate | v1 |
| Time in bed and rough time asleep | Sleep opportunity and gross sleep amount | MEDIUM. Under mattress contactless HR and breathing validated vs polysomnography in older adults [P15] | Measurement | Under mattress ballistocardiography mat or radar. Not a camera | Own | 1 to 2 weeks | Large shifts prompt a conversation | "Time in bed averaged 11 hours this week, up from 8." | Moderate. Validate against actigraphy or PSG for sleep claims | v1 |
| Sleep fragmentation, bed exit events | Disrupted sleep, nocturia, restlessness | MEDIUM. Bed exit and breathing disturbance detectable contactlessly [P15] | Measurement | Under mattress mat or radar | Own | 1 to 2 weeks | Feeds nocturia and fall risk signals | "Got out of bed 5 times last night vs a typical 2." | Moderate | v1 |
| Circadian rest activity rhythm: interdaily stability (IS), intradaily variability (IV), relative amplitude (RA), L5/M10 timing | Robustness of the 24 hour activity rhythm. Degradation tracks cognitive decline and mortality | HIGH. In older men, lower IS and RA and higher IV predicted incident cognitive impairment [P8]; UK Biobank low RA raised dementia risk [P8]; +1 SD IS reduced mortality risk 26 percent [P8] | Measurement (derived) | Any continuous activity stream: PIR occupancy, camera activity, or bed/seat sensing. No wearable required | Own | 2 to 4 weeks minimum for stable nonparametric metrics | A degrading rhythm prompts a sleep, light, and routine conversation and a clinician flag. Non diagnostic | "Your daily activity rhythm is less regular than last month." | Moderate. Validate the passive activity derived IS/IV/RA against wrist actigraphy derived values | v1 |
| Sliding down in bed | Weakness, positioning difficulty | LOW. No quantified evidence found | Inference | Under mattress pressure array or radar | Own | UNKNOWN | Prompts a positioning aid conversation | "Repositioning lower in the bed overnight." | High | research only |

### 1.6 Toileting

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Nighttime bathroom trip frequency (nocturia proxy) | Sleep disruption, cardiac, renal, prostate, diabetes, and fall risk signal | HIGH. Nocturia 3+ voids associated with ~2x mortality; 2+ vots associated with 1.8x hip fracture risk; high prevalence in 80+ [P10] | Measurement (count) | Bathroom door contact plus PIR, or mmWave radar. No camera in the bathroom | Both | 1 to 2 weeks | A rise from baseline prompts a medication review and clinician conversation. Directly linked to fall risk | "Nighttime bathroom visits rose from 2 to 6 per night this week." | Low. This is an event count, not a physiological claim | v1 |
| Daytime bathroom frequency | Hydration, urinary, or GI change | MEDIUM | Measurement | Bathroom door plus PIR | Own | 1 to 2 weeks | Prompts a conversation | "Daytime bathroom visits up 60 percent." | Low | v1 |
| Bathroom dwell time | Difficulty, fall, or immobility in the highest risk room | MEDIUM | Measurement plus inference | Bathroom PIR or radar. No camera | Own | 1 to 2 weeks | Long dwell prompts a check | "Spent 40 minutes in the bathroom, well above baseline." | Moderate | v1 |

### 1.7 Nutrition and kitchen

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Kitchen use and meal preparation events | Whether the person is preparing and eating meals | MEDIUM. Sensor observation shows MCI adults spend more time looking in the fridge and cabinets; kitchen activity recognition can separate MCI from normal cognition (n=19) [P13] | Inference | Kitchen PIR plus appliance/cabinet contacts, or camera. Refrigerator door sensor | Own | 1 to 2 weeks | A drop in meal prep events prompts a nutrition check and meal support | "Kitchen meal preparation events dropped from 3 to 1 per day." | Moderate. Validate that detected events correspond to actual meals | v1 |
| Refrigerator and cabinet interaction count | Food access proxy | LOW quantified as a nutrition endpoint. Widely proposed, not validated against intake [P13 related] | Measurement | Door contact sensors | Own | 1 to 2 weeks | Feeds the nutrition signal | "Refrigerator opened 2 times today vs a typical 8." | High to validate as a nutrition claim | v2 |
| Eating duration and meal frequency, skipped meals | Appetite and routine | LOW quantified for passive sensing | Inference | Kitchen and dining presence, appliance events | Own | 2 to 4 weeks | Prompts a nutrition conversation | "Appears to have skipped the midday meal 4 days this week." | High | v2 |
| Fluid intake proxy | Hydration | LOW. No validated passive proxy found | Inference | Kettle, tap, or cup interactions | Own | UNKNOWN | Prompts hydration reminder | "Fewer drink preparation events than usual." | High | research only |

### 1.8 Instrumental activities of daily living

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Change in frequency of habitual IADL tasks (dishwashing, laundry, tidying) | Functional decline. IADL loss precedes ADL loss and predicts dementia and mortality | MEDIUM to HIGH for the construct. IADL limitation predicts progression to dementia and is a mortality risk factor [P16]. Passive per task detection validation UNKNOWN | Inference | Appliance use sensors, camera activity recognition | Own | 2 to 4 weeks | A drop in habitual tasks is exactly what a visiting adult child notices. Prompts support services | "Dishwashing and tidying activity is below the monthly baseline." | High. Each task detector needs concurrent validation | v2 |
| Bathing and shower frequency | Self care maintenance | LOW quantified. Bathroom is camera prohibited | Inference | Bathroom water or humidity sensor, or radar | Own | 2 to 4 weeks | Prompts a self care conversation | "Showering less often than the monthly baseline." | High | v2 |
| Mail and package retrieval, outings | Engagement and routine | LOW quantified | Inference | Door contact plus outdoor absence detection | Own | 2 to 4 weeks | Feeds social and function signals | "No trips outside the home for 6 days." | Moderate | v2 |
| Plant and pet care, dressing | Fine grained self care and routine | LOW. Not reliably observable | Inference | Camera activity recognition | Own | UNKNOWN | Weak | Not shown | High | reject (v1) |

### 1.9 Social and communication

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Out of home trips and duration | Social and community engagement. Isolation is a mortality risk | HIGH for the isolation construct. Social isolation OR 1.29, living alone OR 1.32 for mortality [P11] | Inference | Door contact plus absence detection. Camera not required | Own | 1 to 2 weeks | A drop prompts a wellness and social support conversation | "No trips outside the home this week, down from a typical 4." | Moderate | v1 |
| Front door events and visitor counts | Social contact volume | MEDIUM. Proxy for the isolation construct [P11] | Measurement | Door contact, optional camera at entry | Own | 1 to 2 weeks | Low visitor counts prompt outreach | "2 visitors this week vs a typical 6." | Moderate | v1 |
| Voice interaction volume with the assistant | Engagement and, indirectly, mood or loneliness | LOW quantified | Measurement | The assistant subsystem itself | Own | 2 to 4 weeks | Feeds engagement signal | "Talked with the assistant less this week." | Moderate | v2 |
| Time in conversation, phone use | Social contact | LOW. Requires audio, raises two party consent | Inference | Microphone. Unbudgeted, consent heavy | Own | UNKNOWN | Prompts outreach | "Fewer or shorter conversations detected." | High plus legal | research only |
| Self reported mood and loneliness check in | How the person feels | HIGH as a design pattern (self report is not a claim, framework section 2) | Self report | The assistant prompts, the person answers | Own | Immediate per entry | Low scores prompt a caregiver call. Safest affective signal | "You told us you felt lonely on 4 days this week." | None as a measurement claim. It is a journal | v1 |

### 1.10 Speech and interaction (research only for v1)

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Speech rate, pause frequency and length, word finding, lexical diversity, response latency | Cognitive change (non diagnostic). Highest scientific upside and highest claim risk in the catalog | MEDIUM as science. Acoustic and linguistic models separate MCI and dementia from controls at AUC 0.76 to 0.94 [P14]; non semantic voice features detect MCI in Framingham [P14]. Not a productized in home capability | Inference | Microphone array. Unbudgeted by the concept. Two party consent implications | Own | UNKNOWN in home | None at v1. Log only. Do not ship an output string | Not shown at v1 | Very high. Inference of cognitive state from passive audio is the highest FTC and FDA exposure item here | research only |

### 1.11 Environmental hazard

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Home fall hazard inventory (loose rugs, clutter in paths, low light in transit areas, obstructed stairs, missing handrails) | Modifiable environmental fall risk. Zero inference about the person | HIGH. Home fall hazard reduction cut fall rate 26 percent overall (RaR 0.74) and 38 percent in higher risk people (RaR 0.62), 12 RCTs, 5293 participants, Cochrane [P12] | Inference (about the environment, not the person) | Camera, one time or periodic scene scan. Any placement that images floors and paths. Lowest frame rate and resolution demand of any camera task | Norm (hazard checklist) | Immediate (one time scan) | The caregiver fixes it in an afternoon. Completely defensible, requires no inference about the resident, and no competitor emphasizes it | "3 potential trip hazards found: a loose rug in the hallway, a cord across the bedroom path, and a dim stair landing." | Low to moderate. Validate hazard detection precision and recall against a human home safety assessment. No person level claim | v1 |

### 1.12 Physiological

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Resting heart rate and HRV trend | Cardiovascular and illness onset signal | MEDIUM. Shipped as wellness on consumer wearables (precedent). Raw wearable access unresolved (assumption A4). Contactless bed HR validated vs PSG ECG in older adults [P15] | Measurement | Wearable (if raw access real) or under mattress BCG mat or radar. Not a camera | Both | 1 to 2 weeks | A sustained shift prompts a health check | "Resting heart rate up 8 bpm from baseline." | Moderate. Contactless HR needs validation vs ECG in the target population | v1 (bed mat path), pending A4 for wearable |
| Respiratory rate | Respiratory or cardiac change | MEDIUM. Contactless breathing rate validated vs PSG in older adults [P15] | Measurement | Under mattress mat or radar | Both | 1 to 2 weeks | Prompts a health check | "Breathing rate at night is elevated vs baseline." | Moderate | v1 (bed mat path) |
| SpO2, skin temperature | Oxygenation and illness or infection onset | LOW to MEDIUM. Wearable precedent exists; raw access unresolved. Not contactlessly available at home accuracy | Measurement | Wearable only. Gated by A4 | Both | 1 to 2 weeks | Prompts a health check | "Skin temperature is above your baseline." | Moderate to high | v2, gated by A4 |

### 1.13 Adherence and cognition proxies

| Marker | What it indicates | Evidence | Data type | Sensing modality + spec | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Medication reminder response rate | Adherence behavior | MEDIUM. Adherence logging is a settled consumer feature | Measurement | The reminder subsystem, optional instrumented pill organizer | Own | 1 to 2 weeks | Missed responses prompt a caregiver nudge | "Responded to 3 of 7 medication reminders this week." | Low. Logging, not dose guidance | v1 |
| Pill organizer interaction | Whether the organizer was opened | LOW quantified | Measurement | Instrumented organizer (unbudgeted) or camera | Own | 1 to 2 weeks | Prompts a nudge | "Pill organizer not opened on 2 days." | Moderate | v2 |
| Appliance or stove left on, door left open | Safety and, indirectly, memory | MEDIUM safety value | Measurement (event) | Stove current sensor, door contact | Event | Immediate | Immediate safety notification | "The stove has been on for 90 minutes with no one in the kitchen." | Low (event) | v1 (as safety event), cognition inference research only |
| Object misplacement frequency (byproduct of the find my phone feature) | Memory behavior. The most claim sensitive item in the catalog | LOW quantified. Self generating signal | Inference | Object detection and scene memory (heavy compute, see Phase 0/4) | Own | UNKNOWN | Log only. Do not output a cognitive conclusion | Not shown as a cognitive claim | Very high. Do not ship an inference | research only |
| Repeated questions to the assistant | Memory behavior | LOW | Inference | The assistant subsystem | Own | UNKNOWN | Log only | Not shown as a conclusion | Very high | research only |

---

## 2. Ranked v1 Shortlist

Ordered by (actionability x evidence strength) / sensing cost, per the Phase 1 instruction. Not by scientific interest. Sensing cost is the marginal cost of the modality required to observe the marker: door contacts and PIR are cheapest, a shared camera is moderate, a bed or seat mat is moderate, a wearable or radar is higher.

| Rank | Marker | Actionability | Evidence | Sensing cost | Why it ranks here |
|---|---|---|---|---|---|
| 1 | Long lie detection | Highest (immediate escalation) | HIGH [P7] | Shared with fall path | Highest value single feature. Event and duration detection, lowest claim risk, directly changes an outcome |
| 2 | Fall event detection | Highest (immediate escalation) | HIGH need, engineering risk on false positives [P17] | Shared sensor | Core. Without it there is no product. Value gated by real world false positive rate |
| 3 | Nighttime bathroom frequency (nocturia proxy) | High (med review, fall risk) | HIGH [P10] | Lowest (door + PIR) | Strong evidence, trivial sensing, direct action, tied to falls |
| 4 | Life space contraction and room transitions | High (wellness check) | HIGH construct [P9] | Lowest (PIR + door) | Strong construct, cheapest sensing, exactly what a remote child cannot see |
| 5 | Gait speed trend | High (PT referral) | HIGH [P1][P2], camera validated [P3] | Moderate (camera) | Vital sign level evidence and camera measurable, but needs the right view (section 5) |
| 6 | Home fall hazard inventory | High (fix in an afternoon) | HIGH [P12] | Low (one time camera scan) | RCT backed, zero person inference, defensible, uncontested by competitors |
| 7 | Circadian rest activity rhythm (IS, IV, RA) | Medium to high (clinician flag) | HIGH [P8] | Low (rides on PIR/activity) | Free rider on occupancy data already collected, strong evidence |
| 8 | Sit to stand time and count | High (strength, PT) | HIGH for the clinical test [P5] | Moderate (camera or seat pad) | Passive proxy for a validated test, actionable |
| 9 | Out of home trips and visitor counts | Medium to high (social outreach) | HIGH construct [P11] | Low (door contact) | Cheap, strong construct, addresses isolation mortality |
| 10 | Sleep location, time in bed, bed exits | Medium (health check) | MEDIUM [P15] | Moderate (bed mat) | Adds the bedroom without a camera |
| 11 | Contactless resting HR and respiratory rate | Medium (health check) | MEDIUM [P15] | Moderate (bed mat) | Physiological trend without a wearable, pending validation |
| 12 | Kitchen meal preparation events | Medium (nutrition support) | MEDIUM [P13] | Low to moderate | Nutrition and cognition proxy, needs event validation |
| 13 | Self reported mood and loneliness check in | High (call) | HIGH as design pattern | Near zero (software) | Safest affective signal, pure self report |
| 14 | Medication reminder response rate | Medium (nudge) | MEDIUM | Near zero (software) | Settled feature, logging only |
| 15 | Stove or appliance left on, door left open | High as safety event | MEDIUM | Low (current + door sensor) | Immediate safety value |

Everything below the line is v2 or research only per the catalog verdicts.

---

## 3. Sensing Requirement Matrix (input to Phase 2)

For each v1 marker, the minimum sensor specification. Phase 2 must reject any architecture that cannot observe this set. Note the recurring theme: the highest evidence markers do not all want a camera, and the two rooms with the most signal (bathroom, bedroom) forbid one.

| v1 Marker | Minimum sensor spec | Placement | Bathroom / bedroom viable | Camera required |
|---|---|---|---|---|
| Long lie detection | Presence plus floor level posture over time. Camera pose at 15+ fps, OR 60/77 GHz mmWave radar, OR thermal array, OR floor pressure. Immobility timer | Every high risk room including bathroom | Needs a non camera node in the bathroom | No, if radar or thermal used |
| Fall event detection | Same modalities as long lie, 15 to 30 fps for a vision classifier. Latency to alert under seconds | Living area, kitchen, bathroom, bedroom | Bathroom and bedroom need non camera | No |
| Nighttime bathroom frequency | Binary presence and entry/exit timing. PIR plus door contact, or radar | Bathroom door and interior | Yes (this is a no camera room) | No |
| Life space and room transitions | Room level occupancy and transitions. One PIR per room plus door contacts | One node per room | Yes | No |
| Gait speed trend | Pose estimation over a calibrated straight path 2.5 to 4 m, side or oblique view, 15 to 30 fps, adequate low light or IR. Nadir ceiling view is inadequate (section 5) | Hallway or long sightline room, wall or corner height, not ceiling nadir | No (needs the main circulation path) | Yes |
| Home fall hazard inventory | Still or low rate imaging of floors and paths, moderate resolution. Lowest frame rate demand of any camera task | Any view that images floor and walking paths | Camera prohibited in bathroom, so hazard scan there is manual | Yes (except bathroom) |
| Circadian rest activity rhythm (IS, IV, RA) | Any continuous activity time series at minute resolution. Rides on PIR occupancy, camera activity, or bed/seat sensing | Whole home aggregate | Yes | No |
| Sit to stand time and count | Camera oblique view of primary seating, 15 to 30 fps, OR seat pad load sensor for count and rough timing | Living area seating | n/a | Camera for arm use, seat pad for count |
| Out of home trips and visitor counts | Entry door state and occupancy. Door contact plus interior PIR | Entry door | n/a | No |
| Sleep location, time in bed, bed exits | Under mattress load or ballistocardiography mat, OR bedroom radar. No camera | Bed | Bedroom viable without camera | No |
| Contactless resting HR and respiratory rate | Under mattress ballistocardiography mat sampling adequate for cardiac and respiratory band, OR radar. Validate vs ECG/PSG | Bed | Yes | No |
| Kitchen meal preparation events | Kitchen PIR plus refrigerator and cabinet door contacts and/or appliance current sensing. Camera optional | Kitchen | n/a | No |
| Self reported mood and loneliness | Software prompt and response via the assistant | n/a | n/a | No |
| Medication reminder response rate | Software prompt and response, optional instrumented organizer | n/a | n/a | No |
| Stove or appliance left on, door left open | Current clamp or smart plug on the appliance, door contact | Kitchen, exterior doors | n/a | No |

Headline for Phase 2: a single ceiling camera cannot deliver the v1 set. The evidence rich, low cost markers (nocturia, life space, circadian rhythm, out of home trips, sleep) want a distributed low cost PIR, door contact, and bed mat mesh. The camera earns its place for gait speed, hazard inventory, sit to stand, and as one option for the fall and long lie path. This is a multi node architecture, not a bulb.

---

## 4. Caregiver Report Specification

Design constraint: the remote adult child is busy. If it is not readable in 30 seconds it does not get read. Default state is a single green line. Detail is pull, not push. Escalations interrupt, trends do not.

### 4.1 Daily digest (push once, or silent if all normal). Target read time 10 seconds.

```
Mom, Tuesday                                    [ All normal ]

Up at 6:40, active day, in bed 10:15pm.
No falls. 2 bathroom trips overnight (normal).
Walking speed steady. Ate lunch and dinner.

Nothing needs your attention today.
```

Changed day variant:

```
Mom, Tuesday                                    [ 1 thing to note ]

No falls. Good activity.
> Up 5 times overnight for the bathroom, usually 2.
  Third night in a row. Worth a mention at her next appointment.

[ See week ]        [ Call Mom ]
```

### 4.2 Immediate alert (interrupts). This is the product.

```
FALL DETECTED
Bathroom, 2:14pm. Still on the floor (4 min).

[ Call Mom ]   [ Call 911 ]   [ I'm handling it ]
```

Auto escalates to the next contact and, per the escalation policy set in Phase 5, to emergency services if unacknowledged and the person remains down.

### 4.3 Weekly summary (push Sunday). Target read time 30 seconds.

```
Mom, this week                          Overall: steady, 1 trend to watch

WHAT CHANGED
> Nighttime bathroom trips up: 2 to 5 per night. New this week.
  What you can do: mention it to her doctor, it affects sleep and falls.

STEADY
  Walking speed 0.83 m/s, flat vs last month.
  No falls, no near falls detected.
  Active in all rooms, normal daily rhythm.
  Meals prepared every day.

ONE FIX AROUND THE HOUSE
  Loose rug in the hallway is a trip hazard. 10 minute fix on your next visit.

[ Full detail ]     [ Adjust what I get alerted about ]
```

Rules embedded in the copy above:
- Every trend line pairs the change with the specific action. A trend with no action is deleted from the report, not shown. This enforces the framework rule that a marker with no action is telemetry, not a product.
- Numbers are shown as own baseline comparisons, never as a diagnosis. Framing matches the Defensible framing column exactly.
- The hazard item is the one uncontested, zero inference, high trust line and it appears every week until fixed.

---

## 5. Markers No Ceiling Camera Can Observe, and Markers Needing an Unbudgeted Modality

### 5.1 No ceiling (nadir) camera can observe these, regardless of resolution

| Marker | Why the ceiling view fails | What it actually needs |
|---|---|---|
| Stride length, lateral sway, weight bearing and walking asymmetry | Nadir geometry foreshortens the sagittal and frontal planes where these live. A top down view cannot resolve step length or sway amplitude reliably | Wall or corner mounted oblique or side view camera |
| Gait speed at stated accuracy | Achievable only over a calibrated straight path viewed side on or obliquely. A single overhead cone sees a short, angularly distorted path | Oblique or side view along a circulation path |
| Sit to stand with arm use detection | Vertical rise under the camera is hard to time and arm use is occluded from directly above | Oblique view of the chair |
| Furniture surfing, stumbles, chair rise mechanics | Require limb and posture detail the nadir view flattens | Oblique room view |
| Nighttime and daytime bathroom activity, dwell, nocturia | Cameras are unacceptable in the bathroom, the single highest fall risk room | PIR plus door contact, or mmWave radar |
| Sleep location, time in bed, fragmentation, bed exit | Cameras are unacceptable in the bedroom | Under mattress mat or bedroom radar |
| Contactless HR, HRV, respiratory rate | Not derivable from a ceiling RGB image at clinical accuracy | Under mattress ballistocardiography mat, radar, or a wearable |

### 5.2 Markers requiring a modality the concept has not budgeted for (the concept budgeted a bulb camera only)

| Marker | Unbudgeted modality required | Note |
|---|---|---|
| Contactless resting HR, HRV, respiratory rate | Under mattress ballistocardiography mat (load cell or piezo) or mmWave radar | Validated vs PSG in older adults [P15]. Adds a bed node to the BOM |
| SpO2, skin temperature | Wearable with raw data access | Gated by assumption A4, unresolved. See `shared_wearable_data_access.md` |
| Nocturia, bathroom dwell, bathroom falls and long lie | Bathroom node: mmWave radar or PIR plus door contact | No camera permitted. Radar is the only modality that gets fall and long lie coverage in the bathroom |
| Sleep and bed exit | Under mattress mat or bedroom radar | No camera permitted |
| Speech and cognitive proxies | Microphone array | Research only. Two party consent and high claim risk. Do not ship an output |
| Time in conversation, phone use | Microphone | Research only, consent heavy |
| Stove left on | Current clamp or smart plug | Cheap add, high safety value |
| Pill organizer interaction, meal prep detail | Instrumented organizer, appliance current or contact sensors | Cheap adds, moderate value |
| Whole home life space, circadian rhythm at low cost | Distributed PIR mesh, one per room | The evidence rich markers ride on this cheap mesh, not the camera |

Strategic consequence for Phase 2, stated plainly: the concept's single bulb camera cannot see most of the highest evidence, lowest cost, most defensible markers. The product the evidence points to is a low cost PIR and door contact mesh, plus a bed mat, plus one well placed oblique camera for gait, hazard inventory, and one fall path. The bulb form factor is the wrong default. This is the finding to carry into the Phase 2 architecture fork.

### 5.3 Gait speed and camera measurement error (the concept critical question)

The Phase 1 brief asks whether camera derived gait speed measures anything real. Answer: yes, for trend and substantial change detection, with one placement caveat.

- Published thresholds: 0.8 m/s tracks median life expectancy for adults 65+ and is the widely used frailty and mobility cut point [P1]. Meaningful change is 0.05 m/s, substantial change is 0.10 m/s [P2], and a 0.1 m/s annual decline predicts mortality [P2].
- Camera measurement error: markerless motion capture reports gait speed RMSE 0.04 m/s vs a pressure sensitive walkway [P3b], and Kinect based systems agree with GAITRite at ICC 0.81 to 0.98 [P3a]. Smartphone single camera apps are weaker (ICC 0.53) [P3a].
- Verdict: camera error of ~0.04 m/s sits below the substantial change threshold of 0.10 m/s and at the edge of the 0.05 m/s minimal meaningful change. Gait speed survives as a trend and substantial change signal. It does not survive as a single reading precise to the minimal clinically important difference. Critically, this holds only for a side or oblique calibrated view. A nadir ceiling bulb view has no published validation and is expected to be materially worse. The bulb kills the metric, the metric does not kill the product.

---

## Register Entries

### Papers (for `papers.md`, framework section 9 columns)

| Key | Full citation | DOI / ID | What it establishes | Sample size and design | Effect size | Validated vs gold standard | Marker / claim supported | Replication / status |
|---|---|---|---|---|---|---|---|---|
| P1 | Studenski S et al. Gait Speed and Survival in Older Adults. JAMA 2011;305(1):50-58 | 10.1001/jama.2010.1923 | Gait speed is a vital sign level survival predictor; 0.8 m/s tracks median life expectancy | Pooled 9 cohorts, 34,485 adults 65+, 6 to 21 yr follow up | Each +0.1 m/s associated with higher survival; large absolute survival spread across speed range | Reference is directly measured gait speed | Gait speed trend | Landmark, widely replicated |
| P2 | Perera S et al. Meaningful change and responsiveness in common physical performance measures in older adults. JAGS 2006;54(5):743-749 | 10.1111/j.1532-5415.2006.00701.x | Meaningful change 0.05 m/s, substantial 0.10 m/s; 0.1 m/s/yr decline predicts mortality | Multi cohort, observational plus RCT data | 0.05 m/s small meaningful, 0.10 m/s substantial | Anchor and distribution based | Gait speed change thresholds | Widely cited standard |
| P3a | Ferraris C et al (and related). Using New Camera-Based Technologies for Gait Analysis in Older Adults in Comparison to the Established GAITRite System. Sensors 2020;20(1):125 | 10.3390/s20010125 | Camera gait analysis agrees with instrumented walkway in older adults | 44 adults 65+ | Kinect ICC 0.81 to 0.98 vs GAITRite; smartphone app ICC 0.53 | Yes, GAITRite instrumented walkway | Camera gait speed validity | Single study, older adult population |
| P3b | Portable motion capture cameras accurately characterize gait metrics vs a pressure-sensitive walkway. Scientific Reports 2024 | 10.1038/s41598-024-68402-x | Markerless camera gait metrics match a pressure walkway | Validation cohort vs pressure walkway | Speed RMSE 0.04 m/s; cadence 2.3 steps/min; stride length RMSE 0.05 to 0.08 m; r>0.9 | Yes, pressure sensitive walkway | Camera gait speed measurement error | Recent, single study |
| P4 | Hausdorff JM et al. Gait variability and fall risk in community-living older adults: a 1-year prospective study. Arch Phys Med Rehabil 2001;82(8):1050-1056 | 10.1053/apmr.2001.24893 | Stride time variability prospectively predicts falls | 52 adults 70+, 1 yr prospective | Fallers 106+/-30 ms vs non fallers 49+/-4 ms; ~5x fall likelihood | Force sensitive insoles | Stride time variability | Landmark, replicated |
| P5 | Buatois S et al. Five Times Sit to Stand Test is a Predictor of Recurrent Falls in Healthy Community-Living Subjects Aged 65 and Older. JAGS 2008;56(8):1575-1577 | 10.1111/j.1532-5415.2008.01777.x | FTSS above 15 s predicts recurrent falls | Community adults 65+ | >15 s marks higher recurrent fall risk; other cohorts 12 to 16 s cut points | Reference is timed FTSS | Sit to stand time | Replicated, standard clinical test |
| P6 | Bishnoi A, Hernandez ME et al. Dual task walking costs in older adults with MCI: systematic review and meta-analysis. Aging Ment Health / related 2021 | see register | Higher dual task gait cost tracks cognitive decline | Meta analysis, MCI vs controls | Consistent higher DTC in MCI; magnitude varies | Neuroimaging and cognitive tests | Dual task gait cost (research only) | Meta analytic, heterogeneous |
| P7 | Fleming J, Brayne C. Inability to get up after falling, subsequent time on floor, and summoning help: prospective cohort study in people over 90. BMJ 2008;337:a2227 | 10.1136/bmj.a2227 | Long lie is common and predicts serious outcomes | Prospective cohort, adults 90+ | 80% could not get up after >=1 fall; 30% lay >=1 hr; long lie associated with hospitalization and LTC move | Observed, self report validated | Long lie detection | Landmark for long lie |
| P8 | Rogers-Soeder TS et al. Nonparametric Parameters of 24-Hour Rest-Activity Rhythms and Cognitive Decline in Older Men (MrOS); plus UK Biobank RAR-dementia; plus Como Vai cohort mortality | PMID 34558603; JMIR PH 2024 e55211; PMC10871497 | Degraded rest-activity rhythm predicts cognitive decline, dementia, and mortality | MrOS (older men, longitudinal); UK Biobank (large cohort); Como Vai (older adults) | Lower IS/RA and higher IV predict incident cognitive impairment; +1 SD IS reduces mortality risk 26% | Wrist actigraphy | Circadian IS/IV/RA | Multiple cohorts, consistent direction |
| P9 | Kennedy RE et al. Life-Space Mobility Change Predicts 6-Month Mortality. JAGS / PMC5826722; plus UAB LSA normative data PMC7741046 | PMC5826722 | Life-space decline predicts short term mortality | UAB Study of Aging, 1000 Medicare beneficiaries 65+ | 10 point LSA decline over 6 mo raised 6 mo mortality odds 72%; LSA <=40 high risk | LSA instrument (self report reference) | In home life space contraction | Replicated across cohorts (SOF, MrOS) |
| P10 | Nocturia reviews and cohorts: Association of nocturia with cardiovascular and all-cause mortality (PMC10768185); nocturia falls and fracture literature | PMC10768185 | Nocturia frequency predicts mortality and fracture; high prevalence in elderly | Prospective cohort up to 31 yr; review data | >=3 voids ~2x mortality; >=2 voids >2x fall/fracture trauma, 1.8x hip fracture | Voiding diaries | Nighttime bathroom frequency | Consistent across sources |
| P11 | Holt-Lunstad J et al. Loneliness and Social Isolation as Risk Factors for Mortality: A Meta-Analytic Review. Perspect Psychol Sci 2015;10(2):227-237 | 10.1177/1745691614568352 | Social isolation and living alone raise mortality risk | Meta analysis, studies 1980-2014 | Isolation OR 1.29, loneliness OR 1.26, living alone OR 1.32 | Self report and objective network measures | Out of home trips, social contact | Landmark, 2024 meta reconfirms |
| P12 | Clemson L et al. Environmental interventions for preventing falls in older people living in the community. Cochrane Database Syst Rev 2023 | 10.1002/14651858.CD013258.pub2 | Home fall hazard reduction reduces fall rate | 22 RCTs, 8463 participants | RaR 0.74 overall (12 studies, 5293); RaR 0.62 in higher risk (9 studies, 1513); moderate certainty | RCT fall outcomes | Home hazard inventory | High quality systematic review |
| P13 | Kitchen activity and MCI: HAR from kitchen activities detecting MCI (medRxiv 2025.05.24.25328107); smart kitchen AAL (PMC3926629) | medRxiv 2025.05.24.25328107 | Kitchen behavior separates MCI from normal cognition; fridge/cabinet dwell elevated in MCI | 19 age-matched older adults (8 NC, 11 MCI); plus prior lab work | Detectable classification difference; small n | Neuropsych reference | Kitchen meal prep events | Small n, lab grade, not productized |
| P14 | Speech biomarkers: Framingham non-semantic acoustic voice features detect MCI (PMC11377909); systematic reviews of speech-based cognitive decline detection (npj Digit Med 2025) | PMC11377909 | Acoustic and linguistic speech features separate MCI/dementia from controls | Framingham cohort; multiple review corpora | AUC 0.76 to 0.94 across studies | Clinical cognitive diagnosis | Speech markers (research only) | Research grade, not productized in home |
| P15 | Contactless bed sensing: Reliable Contactless Monitoring of Heart Rate, Breathing Rate and Breathing Disturbance During Sleep in Aging (medRxiv 2023.10.13.23296936 / PMC11387924); load-cell BCG HR (Sensors 2019;19(6):1451) | PMC11387924; 10.3390/s19061451 | Under-mattress BCG measures HR, breathing, and bed exit vs PSG in older adults | 35 community older adults 65-83, PSG lab plus 7-14 d home | Validated vs PSG ECG and respiratory plethysmography | Yes, polysomnography | Contactless HR/RR, sleep, bed exit | Emerging, product-adjacent |
| P16 | IADL prediction literature: IADL limitation predicts progression to dementia (BMC Public Health 2025; ScienceDirect 48-mo follow up); IADL-mortality links | 10.1186/s12889-025-22788-z | IADL limitation predicts dementia onset, disability, mortality; precedes ADL loss | Population longitudinal cohorts (8-yr and 48-mo) | Significantly higher dementia onset with IADL limitation, amplified with concurrent MCI | Functional and clinical reference | IADL frequency change | Consistent, construct-level |
| P17 | Real-world fall detection accuracy: Bagalà F et al. Evaluation of Accelerometer-Based Fall Detection Algorithms on Real-World Falls. PLoS One 2012;7(5):e37062; plus long-term false alarm studies | 10.1371/journal.pone.0037062 | Lab fall-detection accuracy collapses on real-world falls; false alarms are the failure mode | 13 algorithms on real-world falls; long-term elderly monitoring | Real-world sensitivity ~57% (vs ~94% lab); false alarms 3 to 85 per day in some settings | Annotated real falls | Fall event detection (false positive risk) | Robust cross-study finding |
| P18 | Furniture walking as an early balance/fall-risk sign (clinical/PT sources; AFP mobility assistive device use 2021) | AFP 2021;103(12):737 | Furniture walking recognized as an early balance-impairment and fall-risk sign | Clinical review, no quantified in-home effect | Qualitative | No | Furniture surfing | LOW, no primary effect size |

### Markers (for `markers.md`)

All rows in section 1 are the marker register entries: 40+ markers across 13 clusters, each with data type, sensing modality, baseline, time to signal, actionability, defensible framing, validation burden, and verdict. v1 verdicts: gait speed, sit-to-stand, fall detection, long lie, fall location/self-recovery, life space, room dwell/transitions, sedentary bouts, sleep location, time in bed, bed exits, circadian IS/IV/RA, nighttime and daytime bathroom frequency, bathroom dwell, kitchen meal prep, out-of-home trips, visitor counts, self-reported mood, contactless HR/RR (bed mat), medication reminder response, stove/door safety events, home hazard inventory. Research-only: speech markers, object misplacement, repeated questions, dual-task gait, gait initiation/freezing, fluid intake, sliding in bed, cognition inference from any proxy. Reject at v1: plant/pet care, dressing detection.

### Sources (for `sources.md`)

| Source | Org / venue | URL | Credibility | Used for |
|---|---|---|---|---|
| Studenski 2011 | JAMA | https://pmc.ncbi.nlm.nih.gov/articles/PMC3080184/ | HIGH | Gait speed survival thresholds |
| Perera 2006 | JAGS | https://pmc.ncbi.nlm.nih.gov/articles/PMC5992037/ | HIGH | Meaningful change thresholds |
| Ferraris/Sensors 2020 | MDPI Sensors | https://pmc.ncbi.nlm.nih.gov/articles/PMC6983253/ | HIGH | Camera vs GAITRite in older adults |
| Sci Rep 2024 markerless | Nature Sci Rep | https://www.nature.com/articles/s41598-024-68402-x | HIGH | Camera gait speed RMSE |
| Hausdorff 2001 | Arch Phys Med Rehabil | https://pubmed.ncbi.nlm.nih.gov/11494184/ | HIGH | Stride time variability and falls |
| Buatois 2008 | JAGS | https://agsjournals.onlinelibrary.wiley.com/doi/10.1111/j.1532-5415.2008.01777.x | HIGH | FTSS fall prediction |
| Dual-task meta | PLOS / RG | https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0317365 | MEDIUM | Dual-task gait cost |
| Fleming & Brayne 2008 | BMJ | https://pmc.ncbi.nlm.nih.gov/articles/PMC2590903/ | HIGH | Long lie prevalence and outcomes |
| Rogers-Soeder MrOS 2021 | J Gerontol | https://pmc.ncbi.nlm.nih.gov/articles/PMC8824593/ | HIGH | Rest-activity rhythm and cognition |
| UK Biobank RAR 2024 | JMIR Public Health | https://publichealth.jmir.org/2024/1/e55211 | HIGH | RAR and dementia risk |
| Como Vai cohort | PMC | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10871497/ | MEDIUM | IS and mortality |
| Life-space 6-mo mortality | JAGS / PMC | https://pmc.ncbi.nlm.nih.gov/articles/PMC5826722/ | HIGH | Life-space decline and mortality |
| UAB LSA normative | PMC | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7741046/ | HIGH | Life-space instrument norms |
| Nocturia mortality cohort | PMC | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10768185/ | HIGH | Nocturia and mortality/fracture |
| Holt-Lunstad 2015 | Perspect Psychol Sci | https://journals.sagepub.com/doi/full/10.1177/1745691614568352 | HIGH | Social isolation mortality |
| Clemson Cochrane 2023 | Cochrane | https://www.cochranelibrary.com/cdsr/doi/10.1002/14651858.CD013258.pub2/full | HIGH | Home hazard fall reduction |
| Kitchen MCI HAR 2025 | medRxiv | https://www.medrxiv.org/content/10.1101/2025.05.24.25328107.full.pdf | MEDIUM | Kitchen behavior and MCI |
| Framingham voice MCI | PMC | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11377909/ | MEDIUM | Speech markers of cognition |
| Speech XAI review 2025 | npj Digit Med | https://www.nature.com/articles/s41746-025-02105-z | MEDIUM | Speech markers, AUC range |
| Contactless sleep aging 2023 | medRxiv / PMC | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11387924/ | MEDIUM | Bed BCG HR/RR vs PSG |
| Bed BCG load cell 2019 | MDPI Sensors | https://pmc.ncbi.nlm.nih.gov/articles/PMC6470700/ | MEDIUM | BCG HR feasibility |
| IADL dementia prediction | BMC Public Health | https://bmcpublichealth.biomedcentral.com/articles/10.1186/s12889-025-22788-z | MEDIUM | IADL decline and dementia |
| Bagala 2012 real-world falls | PLOS One | https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0037062 | HIGH | Real-world fall detection accuracy |
| Furniture walking sign | AFP / clinical | https://www.aafp.org/pubs/afp/issues/2021/0615/p737.html | LOW | Furniture surfing as a sign |

---

## Open Questions

1. Nadir ceiling camera gait accuracy is UNKNOWN. No published validation of gait speed, stride length, or sway from a top down bulb view exists. All camera gait validation cited uses side or oblique views. This must be bench tested in Phase 2 or the bulb form factor is unsubstantiated for its headline metric.
2. In home life space has no validated instrument. The LSA is neighborhood scale and self reported. Room level sensor derived life space is a reasonable analog but its correlation with the validated LSA and with outcomes is UNKNOWN and needs a validation study.
3. Passive circadian IS/IV/RA is validated from wrist actigraphy, not from PIR occupancy or camera activity. The transfer of the nonparametric metrics to a non wearable activity stream is plausible but UNVALIDATED. Time to signal for stable IS/IV/RA in a home stream is UNKNOWN.
4. Contactless HR/RR accuracy in real bedrooms (multiple occupants, pets, movement) versus the sleep lab is UNKNOWN. Cited validation is largely single occupant.
5. Long lie floor detection false positive and false negative rates in real homes are UNKNOWN. The clinical value of the feature is HIGH but its engineering reliability is unproven, exactly as with fall detection [P17].
6. Kitchen meal prep event detection has only small n lab evidence (n=19). Whether detected events map to actual meals and to nutritional status is UNKNOWN.
7. Camera measurement error of 0.04 m/s is from research grade markerless capture. Whether a low cost single sensor node hits the same error is UNKNOWN and cost dependent (Phase 3).
8. Effect sizes for furniture surfing, stumbles, and several IADL detectors are UNKNOWN as quantified in home literature. These are LOW confidence until validated.

## Assumptions Made

1. The report copy assumes the caregiver is a remote adult child, per assumption A7 in the brief. If the buyer is a payer or operator (A7 flags this as likely), the report audience and format change and section 4 must be revisited.
2. Sensing cost rankings in section 2 assume PIR and door contacts are materially cheaper than a camera node and a bed mat, which is standard but is priced in Phase 3, not here.
3. The Sensing Requirement Matrix assumes bathrooms and bedrooms forbid cameras. This is treated as a hard product and market constraint per the brief, not a preference.
4. Verdicts assume the wellness lane per framework section 2. Any marker whose only value is a disease inference is placed research only regardless of scientific strength (speech, object misplacement, cognition proxies).
5. Time to signal estimates are engineering judgments anchored to each metric's day to day variance, not measured in this product. They are flagged where UNKNOWN.
6. Where a cited number came from a review or secondary summary rather than the primary article (long lie mortality doubling, some nocturia ratios), it is labeled and the primary is listed for verification in Phase 2 follow up.

## Confidence Summary

Overall confidence: HIGH on the marker evidence base and the v1 shortlist ranking, MEDIUM on the in home realizability of the top markers.

- HIGHEST confidence findings: gait speed as a vital sign level marker with defined thresholds [P1][P2]; long lie as the highest value, lowest claim risk feature [P7]; nocturia, life space, social isolation, circadian rhythm, and home hazard evidence [P8][P9][P10][P11][P12]. These are settled literature.
- Camera gait speed survives measurement error for trend and substantial change detection [P3], with the firm caveat that this holds for oblique or side views only, not a nadir ceiling bulb view.
- WEAKEST findings, carried as Open Questions: nadir camera gait accuracy (unvalidated), in home life space validity (analog only), passive circadian metric transfer from actigraphy (unvalidated), long lie and fall detection real world reliability (engineering unproven), and kitchen and IADL event detection (small n or absent).
- The load bearing strategic conclusion, HIGH confidence: the single bulb camera the concept assumes cannot observe most of the highest evidence, lowest cost, most defensible markers. The evidence points to a distributed low cost sensor mesh plus a bed mat plus one oblique camera, not a bulb. This is the primary input to the Phase 2 architecture fork.


===================================================================
# (phase2_architecture.md)
===================================================================

# Concept A, Phase 2: Sensing Architecture Fork

Governed by `00_framework.md` (sections 2, 5, 6, 8, 9) and `01_concept_a_elder_monitoring.md` (Phase 2). Inputs consumed and not re researched: the Sensing Requirement Matrix and v1 shortlist in `research/a/phase1_markers.md`, the feature classification and compute split in `research/a/phase0_scope.md`, and the edge versus cloud and consent posture in `research/shared/shared_privacy_security.md`.

Governing rule for this phase, inherited from Phase 1: every architecture is scored against its ability to observe the v1 marker shortlist. An architecture that cannot see the shortlist is rejected regardless of cost. The load bearing Phase 1 finding stands as the premise here: a single ceiling camera cannot deliver the v1 set, gait speed is validated only from a side or oblique view, and the highest evidence lowest cost markers (nocturia, life space, circadian rhythm, sleep, out of home trips) want a distributed low cost mesh, not a bulb.

Confidence tags are HIGH, MEDIUM, LOW per framework section 5. Prices are labeled list, distributor, retail, or estimate. Citation keys `[S#]` and `[P#]` resolve in the Register Entries tables.

---

## 1.1 Sensing Modality Enumeration

The v1 shortlist demands five things at once: a fall and long lie path in every high risk room including the bathroom, an oblique gait view on a circulation path, a bedroom sleep and vitals path with no camera, a whole home occupancy stream for life space and circadian metrics, and cheap event contacts for doors and appliances. No single modality serves all five. The table below scores each modality on what Phase 1 actually requires.

| Modality | Detects (v1 relevant) | Cannot detect | Spatial resolution | Privacy posture | Occlusion / lighting | Per room cost | Install | Bathroom viable | Product vs research |
|---|---|---|---|---|---|---|---|---|---|
| RGB camera | Fall, long lie, gait speed (oblique), sit to stand, life space, hazard inventory, ADL recognition | Anything in a no camera room; vitals at clinical accuracy | High. Full pose keypoints at 30 fps [S12][S13] | Worst. Identifiable video is the most regulated home data category (`shared_privacy_security`) | Fails in darkness without IR illuminator; occluded by furniture; gait needs unobstructed 2.5 to 4 m path | Module $5 to $25 [S9]; node BOM est $30 to $70 | Moderate (needs placement, power) | No. Unacceptable in bath and bedroom | Product (mature) |
| Depth / stereo camera | Same as RGB plus metric depth for stride length and sway | Same no camera rooms | High plus depth. But most depth sensors cap at 30 Hz, below the 60 to 100 Hz motion capture standard for fine lower limb kinematics [S12] | Same as RGB. Depth map is still a body scan | IR projector aids low light; sunlight washes out active stereo | RealSense D435 retail approx $300+ [S11]; adds material cost over RGB | Moderate | No | Product, but cost delta not justified (see 1.4) |
| Thermal / low res IR array | Presence, coarse fall (blob on floor), room occupancy | Gait metrics, identity, fine posture, vitals | Very low. Grid-EYE 8x8, MLX90640 32x24 [S6] | Strong. Thermal blob, no identifiable image | Works in darkness. CAUTION: thermal contrast degrades in bathroom steam and humidity (LWIR physics); no primary bathroom validation found [S6] | Sensor $37 to $40 [S6]; node est $50 to $80 | Moderate | Marginal. Steam degrades it, unlike radar | Product for presence; research for fall |
| mmWave radar 60/77 GHz (Vayyar, TI IWR6843, Infineon BGT60TR13C) | Fall, long lie, presence, room mobility, gait speed and step length, respiration and HR, bed exit, nocturia | Identity, fine hand detail, hazard inventory (no image of the scene) | No image. Point cloud plus posture. Gait step length error 4.5 cm and 8.3 percent vs Zeno walkway, ICC 0.91, gait speed error approx 0.02 m/s [P19]; HR rel error approx 1.96 percent, resp approx 1.33 percent [P20] | Strong. No camera, no image, no mic | Works in pitch darkness and through steam. Bathroom viable [S1] | TI IWR6843 chip approx $43 single [S2]; Infineon BGT60TR13C approx $19.72 [S3]; node BOM est $30 to $120/room [S2][S3]; Vayyar retail approx $250/device [S4] | Moderate (wall or ceiling mount, mains) | Yes. The only whole room modality that gets fall and long lie in the bathroom [S1] | Product (Vayyar shipping B2C and B2B); TI/Infineon are build paths |
| WiFi CSI (commodity) | Coarse motion and presence only, whole home | Fall, gait, posture, vitals at product reliability | Whole home, no localization at room precision reliably | Strong (no image) | Through wall; highly sensitive to environment and device changes | Uses existing router plus nodes; low incremental | Low (software on existing WiFi) if it worked | Yes in principle | Product path for motion/presence ONLY; research path for fall and gait |
| WiFi CSI (research grade) | Lab fall 90 to 94 percent, gait, breathing | Cross user, cross environment, cross device generalization; needs firmware patched NICs | n/a | Strong | n/a | Requires Intel 5300 / Atheros / Nexmon / ESP32 patched hardware, not a product [S5] | Research only | n/a | Research path. Not productizable today |
| Emerald Innovations (MIT/Katabi RF) | Gait speed, mobility, sleep stages, respiration, location, falls, through wall | n/a for our channel | High (proprietary) | Strong (no image) | Through wall, own low power radio approx 1000x below WiFi | Not for sale to consumer | n/a | Yes | Research/clinical only. Customer is pharma trials (BlueRock/Bayer, Aspen, Verge), no consumer FDA clearance, not buyable [S7] |
| PIR + door / window contacts | Room occupancy, transitions, life space, circadian stream, nocturia (night motion plus door), out of home trips, kitchen and appliance events | Falls, gait, posture, a motionless person on the floor (PIR needs movement) | Room level binary | Strong (no image) | Works in darkness; PIR blind to a still person | Aqara Motion P1 approx $13 to $25, contact approx $13 to $20 [S8] | Lowest. Peel and stick, needs a hub | Yes (this is the no camera room modality for occupancy) | Product (mature) |
| Load / pressure: under mattress BCG mat | Time in bed, bed exit, sleep fragmentation, resting HR and respiratory rate | Anything off the bed; gait; falls | Bed level. Validated resting HR and sleep onset vs PSG; poor sleep stage classification [P15][S10] | Strong (no image, no mic) | Placement dependent, multi occupant degrades it | Emfit QS retail $299, no subscription [S10]; OEM mat est $40 to $90 | Low (slides under mattress) | Bedroom viable without a camera | Product (Emfit shipping) |
| Load / pressure: seat pad BCG | Sit to stand count, seat occupancy, resting HR while seated | Gait, falls, off chair activity | Chair level. Prototype only: 9 subjects, 95.1 percent HR accuracy, motion artifact limited [P21] | Strong | Motion artifact dominated when the person shifts | Est $20 to $60 | Low | n/a | Research/prototype. HR while seated is a demo, not a product |
| Acoustic (mic array) | Fall sound signature, distress speech, voice interface | Reliable fall discrimination; anything visual | Room level | Worst after camera. All party consent wiretap exposure (`shared_privacy_security` 4.4) | Works in darkness; confounded by household noise | Mic array est $5 to $30 | Low | Yes physically, but consent blocks it | Research path for fall (lab 91 to 100 percent but approx 5 false alarms/hr [S14]); product only as the assistant voice interface |
| Wearable | Resting HR, HRV, SpO2, skin temp, fall (on device), steps | Anything the resident does not wear; the concept is explicitly no wear | On body | Moderate | n/a | Device cost varies | Requires the resident to wear and charge | Yes if worn | Gated by assumption A4 (raw data access unresolved). Contradicts the no wear premise |

### Modality findings that decide the architecture

1. Radar is the only whole room modality that delivers fall and long lie in the bathroom, the highest fall risk room and a hard no camera room [S1][P19]. This is not optional. Any architecture that claims fall coverage must place a non camera node in the bath. Radar is that node. HIGH.
2. The camera earns its place for exactly four tasks that no cheap modality does: gait speed and step length from an oblique view, sit to stand mechanics, home hazard inventory (which requires an actual image of the floor and paths), and one optional living area fall path. It earns nothing in the bath or bedroom. HIGH.
3. The evidence rich, lowest cost markers ride on a PIR and door contact mesh: life space, room transitions, circadian IS/IV/RA, nocturia, out of home trips, kitchen events. This mesh is approx $13 to $25 per node [S8] and is the true backbone of the product. HIGH.
4. The bedroom sleep and contactless vitals path is a bed mat, not a camera and not (necessarily) a radar. Emfit class BCG is shipping and validated for resting HR and bed exit, weaker for sleep staging [P15][S10]. MEDIUM.
5. WiFi CSI is a research path for the features this product needs. Stated honestly: commodity routers do not expose CSI through any API; extraction requires firmware patched Intel 5300, Atheros, Nexmon, or ESP32 hardware [S5]. Shipping commodity WiFi products (Xfinity WiFi Motion, Plume, Origin/Hex Home) detect motion and presence only, not falls or gait, and lab fall numbers of 90 to 94 percent collapse across users, environments, and devices. IEEE 802.11bf WLAN Sensing published 2025-09-26 but silicon and products lag ratification by years. Do not budget WiFi CSI for fall or gait in v1. HIGH.
6. Emerald is the existence proof that RF can do gait and falls contactlessly, but it is not a component we can buy. Its customer is pharma clinical trials, not consumers, and it has no consumer FDA clearance [S7]. It informs the roadmap, not the BOM. HIGH.
7. Acoustic fall detection stays research only. The false alarm rate (approx 5/hr even after height filtering) and two party consent wiretap exposure both disqualify it as a v1 fall modality [S14]. The microphone survives only as the assistant voice interface with on device wake word and no retained audio, per `shared_privacy_security` 4.4. HIGH.

---

## 1.2 Form Factor Options

The concept assumes a camera inside an E26 bulb. Evaluated on equal terms below. Two problems decide it: the switched power problem and the viewing angle problem. Both are resolved explicitly and both point the same way.

| Form factor | Best for | Fatal or limiting issue | Cost posture | Verdict |
|---|---|---|---|---|
| Screw in E26 bulb camera | Zero new wiring, uses an existing socket | Switched power (dies when the light is off); ceiling nadir viewing angle kills gait and sit to stand metrics; tight thermal envelope; UL lamp safety standard applies. Every shipping E26 bulb camera today is a security device (Sengled Snap $129.99, Amaryllo Zeus $249.99, LaView L2 approx $20 to $50 [S18]); none does health or gait, and none is a fixed nadir mount | Module cheap, but the redundancy or holdup needed to survive switched power adds cost (below) | Reject as the primary sensor. See 1.2.1 and 1.2.2 |
| Bulb socket adapter with pass through | Keeps the bulb, adds a tap | Solves nothing about the switch; the socket is still switched | Low | Reject. Cosmetic only |
| Desk / shelf camera (NexiGo class) | Cheapest, best oblique angle, always on mains via USB or barrel jack | Aesthetics and stigma; must be placed and aimed | Node BOM est $30 to $70; adequate edge pose compute starts approx $70 (IMX500) [S16] | Recommended camera form factor for the one gait node |
| Corner / wall mount, hardwired or battery | Best angle for gait and whole room fall | Hardest install (drilling, or battery service) | Higher install cost | Viable alternative for the gait/fall node where aesthetics matter |
| Disguised in a household object | Aesthetics | Covert monitoring of a competent adult is a distinct legal and ethical problem (`shared_privacy_security` 5.2). A visible, dignified active indicator is required, which defeats disguise | n/a | Reject on ethics and consent, independent of cost |
| Smart display or existing device (Nest Hub, Echo Show) | Piggyback on installed base for the assistant | Wrong placement for gait; camera on a display is still a camera in a living space. Piggyback on the sensors is blocked: Nest Hub Soli radar and Echo Show expose no third party passive health sensor SDK; Alexa Together caregiver monitoring was discontinued approx 2025-05 and replaced by Emergency Assist ($7.99/mo, response only, no activity feed) [S22] | Low incremental | Viable host for the assistant voice/UI only, not the sensor |
| Non camera node (radar or PIR or bed mat) | Eliminates the aesthetic and privacy objection entirely | Cannot do gait or hazard inventory | Radar est $30 to $120/room [S2][S3]; PIR approx $13 to $25 [S8]; DIY bed mat BOM est $15 to $30 [S21] | Recommended for bath, bedroom, and the occupancy mesh |

Applicable safety and radio standards for a bulb camera, for the record (bulb reject stands regardless): the LED end product falls under UL 1993 (self ballasted lamps) with UL 8750 for the LED components; the radio and electronics fall under FCC Part 15 Subpart B (unintentional radiator) plus Subpart C (intentional radiator, WiFi). No camera specific UL standard applies; the lamp standard is the anchor. UL 2089 (cited loosely in some places) is for vehicle battery adapters and does not apply. Sealed E26 envelopes already trap LED driver heat (flicker, buzz, yellowing, thermal shutdown, fire risk on non enclosed rated bulbs); adding a multi watt camera SoC and WiFi radio compounds this, and no vendor publishes a camera plus LED derating. This is an additional, independent strike against the bulb. [S19] HIGH on standards, LOW on the unpublished thermal margin.

### 1.2.1 The switched power problem, resolved with costs

If the resident turns off the light, a bulb monitor is dead and the caregiver may not know. This is a safety defect, not an inconvenience. Four options, each costed:

| Option | How it works | Added BOM / cost | Does it actually solve it | Verdict |
|---|---|---|---|---|
| Multi bulb redundancy | Put the monitor in several bulbs per room | Nx the node cost | No. When the wall switch is off, every bulb on that circuit is off together. Redundancy across bulbs on one switch is no redundancy | Reject |
| Supercap holdup plus last gasp radio | A supercapacitor holds the node up for seconds after power loss; the node sends a "I lost power" packet before it dies [S15] | Supercap plus PMIC est $1 to $3 BOM [S15] | Partial. It notifies the caregiver that the eye went dark, but the room is then unmonitored. It converts a silent failure into a known gap, nothing more | Insufficient alone |
| Companion mains node | Add a separate always powered node (wall outlet) that carries the sensing; the bulb becomes a light again | The node cost, which is the whole sensor cost | Yes, fully. But the moment an always powered node exists, the bulb is redundant. This is the tell | This is the real answer, and it abandons the bulb |
| Abandon the bulb | Put the sensor on mains via a shelf/corner node or a radar node | No holdup circuitry needed | Yes | Recommended |

Conclusion: the only robust fix for switched power is a continuously powered node, and a continuously powered node is not a bulb. The supercap last gasp is worth adding to any mains node as cheap insurance against outages (est $1 to $3), but it does not rescue the bulb form factor. HIGH.

### 1.2.2 The viewing angle problem, resolved against the Phase 1 gait finding

Phase 1 established, from published gait validation, that camera derived gait speed and step length are validated only from a side or oblique view over a calibrated 2.5 to 4 m path, and that a nadir ceiling view has no published validation and is expected to be materially worse [P3a][P3b, via Phase 1 section 5.3]. This phase confirms the general camera requirement: markerless gait analysis uses a monocular camera at 800x600 and 30 fps as a practical clinical standard, with fine lower limb kinematics wanting 60 to 100 Hz [S12][S13].

Mapping the v1 camera markers to a ceiling nadir bulb view:

| v1 camera marker | Ceiling nadir bulb view | Oblique wall/shelf view |
|---|---|---|
| Gait speed and trend | Fails. Foreshortened, short angularly distorted path, no published validation | Works (RMSE approx 0.04 m/s from side/oblique, Phase 1 [P3]) |
| Step length, lateral sway, asymmetry | Fails. Nadir geometry flattens the sagittal and frontal planes | Works from oblique |
| Sit to stand time and arm use | Weak. Vertical rise under the lens is hard to time, arm use occluded from directly above | Works from oblique |
| Home hazard inventory | Partial. Sees the floor but from a distorted top down angle | Works |
| Fall / long lie | Workable (a body on the floor is detectable from above), but the bathroom and bedroom still forbid a camera, so a nadir camera cannot be the fall path anyway | Workable, same room limits |

The published gait placement literature is unambiguous: validated metrics require a side, oblique, or sagittal view of a 2.5 to 4 m straight walking path at 30 fps and 720p to 1080p [S12][S13][S23]. An overhead nadir view is geometrically hostile: horizontal displacement foreshortens toward zero directly under the lens, the feet self occlude, steep vertical angles degrade accuracy by up to 60 percent, and there is no published validation of nadir view gait speed at all [S23]. Sit to stand, a vertical motion, is even less observable from overhead. Monocular RGB from the correct oblique angle reaches clinically acceptable spatiotemporal agreement, so a depth camera is not strictly required for speed, stride, and cadence [S12][S13]; depth adds cost ($300 to $700) mainly for fine kinematics the product does not claim.

Stated plainly, per the Phase 2 instruction: a ceiling bulb view makes the concept's headline gait and sit to stand metrics unmeasurable. The bulb does not merely place the camera badly; it places it where the product's flagship measurement claim cannot be substantiated under FTC standards. This reshapes the concept: the camera must move to an oblique wall or shelf position on a circulation path, and it becomes one node among several, not the whole system. HIGH.

### 1.2.3 Does the bulb survive

No, not as the primary sensor. It fails on two independent grounds, either of which is disqualifying: switched power (a safety defect with no fix short of adding a mains node that makes the bulb redundant) and viewing angle (the nadir view cannot measure the flagship gait and sit to stand metrics). A bulb could at most host a non camera radio or a nightlight plus PIR, but even there the switched power problem persists and a $13 to $25 mains or battery PIR does the job without it [S8]. The founder assumption A1 is disproven. The product is a distributed multi node system.

---

## 1.3 Compute Topologies

Topologies scored on per node cost, hub cost, cloud cost per user per month, fall alert latency, bandwidth, what data leaves the home, security surface, and the marketing claim supported. The Phase 0 compute split governs: fall and long lie are the compute floor and run on the node (T1); the assistant, object memory, and natural language query break the node envelope and force a hub or cloud (T2/T4).

| Topology | Description | Per node cost | Hub cost | Cloud cost/user/mo | Fall alert latency | Bandwidth off home | What leaves the home | Security surface | Marketing claim supported |
|---|---|---|---|---|---|---|---|---|---|
| T1 On node full inference | Node runs detection; only events and metrics leave | Higher node (needs an NPU, e.g. IMX500 on chip inference approx $70 [S16], or a camera SoC) | None | Lowest. Events are KB to MB/day, effectively under $0.10/mo bandwidth [S24] | Lowest. Edge fall inference approx 15 to 98 ms (YOLOv5 on RPi 98 ms) [S24] | Tiny (events, KB/day) | Only derived events and metrics. No video ever | Smallest attack surface; per home, not central | "Video is processed on the device. Raw video is not sent to our servers." (strongest privacy claim) |
| T2 Node plus in home hub | Node does light detection; streams features to a hub doing heavy inference | Lower node | Hub: RK3588 SBC tier est $80 to $230, or Jetson Orin NX 16GB tier est $300 to $700, plus approx $30 to $60 case/PSU [S20] | Low (summaries only), same near zero bandwidth as T1 | Low, local hub | Low (features/summaries) | Events and summaries only | Hub is a local high value target; still no cloud corpus | "Nothing leaves your home except events and summaries." |
| T3 Node to cloud | Node streams raw to cloud; cloud infers | Lowest node | None | Highest and prohibitive. 1080p H.264 at approx 5 Mbps is approx 180 GB/mo/stream (H.265 approx 90 GB); AWS egress at $0.09/GB is approx $16/mo egress alone per home plus S3 storage at $0.023/GB-mo plus cloud GPU inference [S24] | Cloud round trip 50 to 200+ ms; cloud centric fall pipelines can exceed 10 s, unacceptable for falls [S24]; fails on connectivity loss | High (continuous video) | Raw video and audio leave the home | Largest. A cloud breach exposes the entire base at once (`shared_privacy_security` 2) | Weakest privacy story. Contradicts the concept |
| T4 Hybrid | Node handles latency critical events (fall) locally; hub or cloud handles the assistant, scene memory, and trend analysis on already derived features | Node as T1 for the fall path | Hub optional (if object memory is in v1) | Medium. Assistant LLM tokens per resident (deferred to `shared_llm_layer.md`); sensing bandwidth near zero | Lowest for falls (local edge, under approx 3 s end to end for the alert [S24]); relaxed for the assistant | Low (derived features plus assistant turns) | Events, summaries, and assistant dialogue on stripped features. No raw video | Split surface; the safety path is local and offline capable | "Fall detection runs on the device and works even if the internet is down. The assistant runs in the cloud on data with no video." |

### Topology findings

1. The fall and long lie path must be T1. It is latency critical and safety critical, and `shared_privacy_security` 2 requires the safety path to run locally and survive a connectivity drop. A cloud dependent fall alert is unacceptable. HIGH.
2. T3 (stream raw to cloud) is rejected outright. It breaks the "no video leaves" claim the concept is built on, maximizes breach exposure, and carries the highest recurring cost via continuous video egress (est 10 to 20 GB/day/camera) and cloud GPU inference. HIGH.
3. The assistant, object memory, and natural language query cannot run on a camera node (Phase 0 section 5). They force a hub (T2) or cloud (T4) on already derived, non reconstructable features. Since Phase 0 classes object memory and free form query as LATER, v1 does not need the hub for those; it needs cloud only for the assistant LLM, on stripped features. HIGH.
4. The right v1 answer is T4 hybrid with a T1 fall path: local on node fall and long lie and metric extraction (no video out), plus a cloud assistant and trend layer on derived features only. This is exactly the split `shared_privacy_security` recommends and the one the Phase 2 brief predicted. It preserves the strongest defensible privacy claim while enabling the assistant. HIGH.
5. On node inference is cheapest to operate and strongest on privacy, but pushes silicon cost into the node (an NPU or a capable camera SoC; the Sony IMX500 is directly relevant because pixels never leave the sensor package, approx $70 at the Raspberry Pi AI Camera reference [S16]). The precise silicon selection is Phase 3. MEDIUM.

Precise cloud cost per user per month for the assistant LLM is deferred to `shared_llm_layer.md` and `shared_infra_cost.md` and is not invented here. The transport and storage cost of a T1/T4 events only design is near zero; the recurring cost is the assistant tokens, not the sensing.

---

## 1.4 Recommendation

Five candidate architectures scored against the Phase 1 v1 shortlist. A home is defined as a 2 bedroom single resident dwelling: living area, kitchen, hallway, bedroom, bathroom (5 zones). Scores are 1 (poor) to 5 (excellent). BOM ranges are node estimates at low volume, hardware only, to be firmed in Phase 3.

| Architecture | Gait fidelity | Fall reliability | Bathroom coverage | Privacy posture | Install difficulty (5 = easy) | Per home BOM (est, hardware) | Consumer acceptability | Verdict |
|---|---|---|---|---|---|---|---|---|
| A0 Single ceiling E26 bulb camera (founder concept) | 1 (nadir view kills gait) | 2 (no bath/bedroom; dies when light off) | 1 (camera prohibited, and switched off) | 2 (camera in living space, video) | 4 (screw in) | approx $40 to $90 | 2 (camera stigma, switched power) | REJECT. Cannot see the shortlist |
| A1 Distributed mesh: PIR+door mesh (all rooms) + bed mat (bedroom) + radar (bathroom, +optional bedroom) + one oblique mains camera (living/hall) | 4 (oblique camera, validated view) | 5 (radar in bath, camera+radar in living, mat bed exit) | 5 (radar) | 4 (camera only in one shared living space; none in bath/bedroom; T1 fall path, no video out) | 3 (multi node, mostly peel and stick; one camera to place; one radar to mount) | approx $180 to $360 | 4 (no camera in private rooms; visible, explainable) | PRIMARY |
| A2 All radar + PIR/door mesh, no camera anywhere | 3 (radar gait speed and step length good [P19], but no hazard inventory, no sit to stand arm use) | 5 (radar every room) | 5 (radar) | 5 (no camera at all) | 3 (radar nodes need mains and mounting) | approx $250 to $600 (radar per room) | 5 (zero camera objection) | FALLBACK |
| A3 Oblique cameras in living areas + radar in bath/bedroom | 5 (best gait and sit to stand) | 5 | 5 (radar) | 2 (multiple cameras in living spaces) | 2 (several cameras to place and power) | approx $300 to $600 | 2 (multiple cameras, high stigma) | Reject for v1 (privacy and cost) |
| A4 WiFi CSI whole home (+ optional camera) | 1 (research path) | 1 (research path, collapses cross env) | 3 (in principle) | 5 (no image) | 5 (software) | Low | 4 | REJECT. Not productizable for fall/gait today [S5] |

### Primary: A1, the distributed mesh with one oblique camera

A1 is the only architecture that observes the full v1 shortlist at defensible cost while keeping cameras out of the two private rooms. Composition:

- PIR plus door/window contact mesh, one node per zone (approx $13 to $25 each [S8]): delivers life space, room transitions, circadian IS/IV/RA, nocturia, out of home trips, kitchen and appliance events, sedentary bouts. This is the evidence rich backbone, ranks 3, 4, 7, 9, 12, 15 on the Phase 1 shortlist, at the lowest sensing cost.
- One 60 GHz radar node in the bathroom (est $30 to $120 [S2][S3], or Vayyar class approx $250 [S4]): the only way to get fall, long lie, dwell, and nocturia in the highest fall risk no camera room [S1][P19]. Optionally a second radar in the bedroom for sleep and vitals if the bed mat is not chosen.
- One under mattress BCG mat in the bedroom: time in bed, bed exit, sleep fragmentation, resting HR and respiratory rate, no camera. Ranks 10 and 11. Under mattress BCG is a real, validated, shipping modality: Emfit QS (HR limits of agreement +/-4.4 bpm vs ECG, approx CA$420, no subscription [S10]), Withings Sleep Analyzer ($199.95, validated in adults 65 to 83, HR within 2 bpm, apnea approx 88 percent [S21]), and the clinical EarlySense (Baxter/Hillrom, FDA 510(k) K180079, HR 96.1 percent, RR 93.3 percent [S21]). A DIY load cell or piezo node is est $15 to $30 at low volume [S21]. Sleep staging is the weak axis across all of them; resting HR, respiration, and bed exit are solid.
- One oblique, mains powered camera node in the living area or hallway on a circulation path (est $30 to $70 [S9]), running T1 on node inference (IMX500 class so pixels never leave the sensor [S16]): gait speed, sit to stand, home hazard inventory, and a living area fall path. Ranks 5, 6, 8. Never a ceiling bulb; never in the bath or bedroom.
- Compute: T4 hybrid. Fall and long lie and metric extraction on node (T1, no video out); assistant and trend layer in the cloud on derived features only.

A1 scores 4 or 5 on gait, fall, bathroom, and privacy, the four dimensions that can kill the concept, and keeps the per home hardware BOM in the approx $180 to $360 range at low volume. It is more nodes than a bulb, but every node is cheap and each is justified by a specific high evidence marker the bulb cannot see.

### Fallback: A2, all radar, no camera

If consumer research shows that any camera anywhere is a hard adoption blocker (a real possibility in this population), fall back to A2: radar in every room plus the PIR/door mesh, zero cameras. A2 keeps fall, long lie, bathroom coverage, and radar derived gait speed and step length [P19], and scores a perfect 5 on privacy and camera acceptability. What it loses: the home hazard inventory (which needs an actual image of the floor, the one uncontested zero inference wedge from Phase 1 rank 6), sit to stand arm use detection, and the richest gait detail. It also costs more, because radar per room is pricier than PIR per room. A2 is the privacy maximal, higher cost, slightly narrower product. It is a genuine fallback, not a downgrade, because it preserves the two highest value features (long lie and fall) and the bathroom.

### The decisive evidence

Three findings decide it. First, Phase 1 and the gait literature establish that the flagship gait and sit to stand metrics are measurable only from an oblique view, not a nadir ceiling view [P3, S12, S13], which kills the bulb as the sensor. Second, the bathroom is both the highest fall risk room and a hard no camera room, and radar is the only whole room modality that covers it in darkness and steam [S1][P19], which forces a non camera node the bulb concept never budgeted. Third, the highest evidence lowest cost markers (nocturia, life space, circadian rhythm, sleep) do not want a camera at all and ride on a $13 to $25 PIR/door mesh [S8], which makes the single expensive camera the wrong center of gravity. The camera survives, once, obliquely, in one shared room. The bulb does not survive.

---

## Register Entries

### Components (for `components.md`)

| Part / product | Manufacturer | Function | Key spec | Price (label) | Source | Confidence |
|---|---|---|---|---|---|---|
| IWR6843 | Texas Instruments | 60 to 64 GHz FMCW radar SoC (DSP+MCU) | Fall demo >90% to 6.5 m; HR within approx 5 bpm; long lie via point cloud + posture; no image | approx $43 single (1ku quote gated) [S2] | ti.com IWR6843 datasheet | HIGH spec / MEDIUM price |
| IWR6843ISK-ODS | Texas Instruments | Radar EVM, overhead/ceiling optimized | Evaluation module | approx $188 to $230 [S2] | Digikey | MEDIUM |
| IWRL6432AOP | Texas Instruments | Low power 57 to 64 GHz radar, antenna in package | Presence, motion, gesture; low power modes | approx $11.19 at 1ku [S17] | ti.com part details | MEDIUM |
| BGT60TR13C | Infineon | 58 to 63.5 GHz radar, antenna in package, 1Tx/3Rx | Range 0.2 to 15 m; presence + vitals; approx 5 mW low power modes | approx $19.72 [S3] | Infineon part page | HIGH spec / MEDIUM price |
| Vayyar Care | Vayyar | 60 GHz 4D imaging radar node (shipping) | FOV 140 az x 70 el, range approx 13 ft; camera free; bathroom viable; auto fall + long lie | approx $250/device retail, +$20/mo monitoring [S4] | Amazon, Ctech | HIGH specs / LOW published accuracy |
| AMG8833 Grid-EYE | Panasonic | 8x8 thermal IR array | 60 deg FOV, approx 7 m, +/-2.5 C | approx $18 to $40 [S6] | Digikey, Mouser | HIGH |
| MLX90640 | Melexis | 32x24 thermal IR array | 55x35 or wide 110x75 deg FOV | approx $37 to $70 [S6] | Melexis, Mouser | HIGH |
| Sony IMX500 (RPi AI Camera) | Sony | 12 MP image sensor with on chip inference | Inference in sensor package; only metadata leaves; supports "no image leaves" claim | $70 retail [S16] | raspberrypi.com, Sony | HIGH |
| Emfit QS | Emfit Ltd | Under mattress BCG mat (shipping) | HR LoA +/-4.4 bpm vs ECG; HRV, respiration, bed exit; no subscription; weak sleep staging | approx CA$420 retail [S10] | emfit.com, JMIR [P15] | HIGH price / MEDIUM accuracy |
| Withings Sleep Analyzer | Withings | Under mattress BCG mat (shipping) | Validated adults 65 to 83; HR within 2 bpm; apnea approx 88% | $199.95 retail [S21] | PMC11387924, PMC8314651 | HIGH |
| EarlySense (bed sensor) | Baxter / Hillrom | Clinical under mattress piezo | FDA 510(k) K180079; HR 96.1%, RR 93.3% | Clinical (not consumer priced) [S21] | PMC5337599 | HIGH |
| Jetson Orin NX 16GB / RK3588 SBC | NVIDIA / Rockchip | Optional in home hub (T2/T4, VLM/memory) | Orin NX approx 157 TOPS; RK3588 approx 6 TOPS | Orin NX approx $599 @1ku; RK3588 SBC $60 to $229 [S20] | arrow, radxa | HIGH / MEDIUM |
| Aqara Motion Sensor P1 | Aqara | Zigbee PIR occupancy | approx 5 yr CR2450 battery | approx $13 to $25 [S8] | distributor | HIGH |
| Aqara / Third Reality contact sensor | Aqara / Third Reality | Zigbee door/window contact | approx 1 to 2 yr battery | approx $13 to $20 [S8] | distributor | HIGH |
| Intel RealSense D435 | Intel | RGB + stereo depth camera | Depth to 10 m; most depth sensors cap 30 Hz | approx $300+ retail [S11] | Intel store, Digikey | MEDIUM |
| Low cost IP camera module | Various (Allwinner/SigmaStar SoC) | RGB camera module for the gait node | 1080p, H.265, on board NPU (e.g. V831 0.2 TOPS) | module approx $5 to $25 [S9] | Alibaba | MEDIUM |
| Supercap + PMIC (dying gasp) | CAP-XX / TI | Holdup + last gasp radio on mains node | Seconds of holdup, sends power loss packet | est approx $1 to $3 BOM [S15] | CAP-XX, TI app note SLVAG21 | MEDIUM |

### Vendors (for `vendors.md`)

| Vendor | Supplies | Channel / note | Confidence |
|---|---|---|---|
| Vayyar | Shipping 60 GHz radar fall detection nodes (B2C and B2B senior living/PERS) | Buy or partner; proven bathroom fall node; own accuracy not public | HIGH |
| Texas Instruments | mmWave radar silicon (IWR6843, IWRL6432) + reference designs (TIDEP-01000/01010) | Build path; EVMs available now; existing ST relationship noted for MCU side | HIGH |
| Infineon | 60 GHz radar (BGT60TR13C) for presence + vitals | Build path; lower cost, best for presence/vitals not whole room fall | HIGH |
| Panasonic / Melexis | Thermal IR arrays | Build path; privacy friendly presence; steam caution | MEDIUM |
| Sony (AITRIOS) | IMX500 on sensor inference | Directly supports "no video leaves" claim; Phase 3 silicon candidate | HIGH |
| Emfit Ltd | Under mattress BCG sleep/vitals mat | Shipping product and OEM path for the bedroom node | MEDIUM |
| Aqara / Third Reality | Zigbee PIR and contact sensors | Cheap mature mesh backbone; needs a hub | HIGH |
| Emerald Innovations | Contactless RF gait/fall (MIT/Katabi) | NOT a component vendor for consumer; pharma trials only; roadmap reference | HIGH |

### Sources (for `sources.md`)

| Key | Source | URL | Date | Used for | Credibility |
|---|---|---|---|---|---|
| S1 | Vayyar Care technology and bathroom coverage | https://vayyar.com/care-pages/how/ | 2026 access | Radar bathroom fall/long lie, works in darkness and steam | HIGH (vendor) |
| S2 | TI IWR6843 datasheet + Digikey EVM pricing | https://www.ti.com/product/IWR6843 ; https://www.digikey.com/en/products/detail/texas-instruments/IWR6843ISK-ODS/10434600 | 2026 access | Radar chip and EVM price, fall demo | HIGH |
| S3 | Infineon BGT60TR13C part page | https://www.infineon.com/part/BGT60TR13C | 2026 access | 60 GHz radar spec and price | HIGH spec / MEDIUM price |
| S4 | Vayyar Care Amazon listing + Ctech | https://www.amazon.com/Vayyar-Care-Touchless-Detection-Subscription/dp/B09JXV82Z6 ; https://www.calcalistech.com/ctechnews/article/rj0cnyqiq | 2022 to 2026 | Retail price approx $250/device, +$20/mo | HIGH price / LOW accuracy |
| S5 | CSIKit / Nexmon CSI / WiFi CSI surveys | https://github.com/Gi-z/CSIKit ; https://github.com/seemoo-lab/nexmon_csi ; https://dhalperi.github.io/linux-80211n-csitool/ | 2026 access | Commodity routers do not expose CSI; patched hardware only; research path | HIGH |
| S6 | Grid-EYE AMG8833 and MLX90640 datasheets/pricing | https://www.digikey.com/en/products/detail/panasonic-electronic-components/AMG8833/5825302 ; https://www.melexis.com/en/product/mlx90640/far-infrared-thermal-sensor-array | 2026 access | Thermal array resolution and price | HIGH |
| S7 | Emerald Innovations (MIT/Katabi) | https://emeraldinno.com/publications/ ; https://www.technologyreview.com/2018/09/12/140293/ | 2016 to 2026 | Contactless RF gait/fall; pharma trial customer, not consumer | HIGH |
| S8 | Aqara/Third Reality PIR and contact sensor pricing (coordinator fact sheet) | vendor listings | 2026 access | PIR/door mesh cost | HIGH |
| S9 | Low cost IP camera module / SoC pricing | https://www.alibaba.com/showroom/ip-camera-allwinner.html ; https://www.cnx-software.com/2020/04/28/allwinner-v831-ai-full-hd-camera-soc/ | 2026 access | Camera module BOM approx $5 to $25 | MEDIUM |
| S10 | Emfit QS product + validation | https://emfit.com/ ; https://biomedeng.jmir.org/2020/1/e16620 | 2026 access | Bed BCG price $299, validated resting HR, weak sleep staging | HIGH price / MEDIUM accuracy |
| S11 | Intel RealSense D435 store/spec | https://store.intelrealsense.com/buy-intel-realsense-depth-camera-d435.html | 2026 access | Depth camera price and 30 Hz cap context | MEDIUM |
| S12 | Markerless gait pose estimation review | https://pmc.ncbi.nlm.nih.gov/articles/PMC10384445/ ; https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10295566/ | 2023 | 800x600/30 fps clinical standard; 60 to 100 Hz for fine kinematics | HIGH |
| S13 | Markerless gait via single camera and CV | https://www.sciencedirect.com/science/article/abs/pii/S0021929024001040 | 2024 | Single RGB camera gait, low cost/low rate limits | HIGH |
| S14 | Acoustic fall detection research | https://pubmed.ncbi.nlm.nih.gov/19163747/ ; https://link.springer.com/chapter/10.1007/978-981-96-9805-9_42 | 2009 to 2025 | Lab 91 to 100%, approx 5 false alarms/hr, research path | MEDIUM |
| S15 | Supercap dying gasp design | https://www.ti.com/lit/an/slvag21/slvag21.pdf ; https://www.cap-xx.com/news/cap-xx-launches-ultra-small-5mm-cylindrical-supercapacitor-to-power-iot-devices | 2026 access | Last gasp holdup cost and behavior | MEDIUM |
| S16 | Sony IMX500 Raspberry Pi AI Camera | https://www.raspberrypi.com/products/ai-camera/ ; https://www.aitrios.sony-semicon.com/edge-ai-devices/raspberry-pi-ai-camera | 2026 access | On sensor inference, $70, pixels never leave sensor | HIGH |
| S17 | TI IWRL6432AOP 1ku price | https://www.ti.com/product/IWRL6432AOP | 2026 access | Low power radar chip approx $11.19 at 1ku | MEDIUM |
| S18 | Shipping E26 bulb cameras | https://www.amazon.com/dp/B01MSRZCWC (Sengled) ; https://www.amazon.com/dp/B083183ZBF (Amaryllo Zeus) ; https://www.microcenter.com/product/686742 (LaView) | 2026 access | All shipping bulb cameras are security devices, none health/gait; prices | HIGH |
| S19 | E26 thermal envelope + UL/FCC standards | bulbbasics.com LED enclosed fixture guide ; UL 1993 / UL 8750 (globalspec) ; FCC Part 15 Subpart B/C (f2labs) | 2026 access | Sealed bulb heat trapping; applicable lamp and radio standards | HIGH std / LOW thermal margin |
| S20 | Hub compute pricing (Jetson, RK3588) | https://www.arrow.com (Jetson Orin NX 900-13767-0000-000) ; https://radxa.com ; jetsonhacks.com | 2026 access | Hub tier prices for T2/T4 | HIGH / MEDIUM |
| S21 | BCG bed mats (Withings, EarlySense) + DIY BOM | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11387924/ ; PMC8314651 ; EarlySense FDA 510(k) K180079 ; JMIR PMC8204244 | 2020 to 2026 | Validated bed BCG products; DIY mat BOM | HIGH |
| S22 | Smart display closed SDK + Alexa Together end | research.google contactless sleep sensing ; safewise Alexa Together ; tomsguide Alexa Emergency Assist | 2025 to 2026 | Piggyback blocked; Alexa Together discontinued, replaced by Emergency Assist $7.99/mo | HIGH |
| S23 | Gait viewing angle degradation | https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6375625/ ; arXiv 2507.11037 (FootGait3D) ; PMC12431465 | 2019 to 2025 | Nadir view foreshortening, up to 60% degradation, no nadir validation | HIGH placement / MEDIUM-HIGH nadir |
| S24 | Cloud vs edge cost and latency | dacast video bandwidth ; AWS egress/S3 pricing ; Springer 978-3-032-02831-0_40 ; arXiv edge-cloud | 2026 access | T3 approx 180 GB/mo, approx $16/mo egress; edge fall 15 to 98 ms vs cloud >10 s | HIGH / MEDIUM |

### Papers (for `papers.md`)

| Key | Citation | What it establishes | Design / n | Effect size | Gold standard | Supports | Status |
|---|---|---|---|---|---|---|---|
| P19 | mmWave radar in home gait validation (PMC10891707, 2024; PMC9784666, 2022) | Radar gait speed and step length match instrumented walkway | In home cohorts | Step length error 4.5 cm / 8.3% vs Zeno, ICC 0.91; gait speed error approx 0.02 m/s | Zeno Walkway | Radar as a gait modality | HIGH, recent |
| P20 | Contactless mmWave vitals (Nature s41598-024-77683-1, 2024) | Radar HR and respiration accuracy | Validation study | HR rel error approx 1.96%, resp approx 1.33% | ECG / reference | Radar contactless vitals | HIGH |
| P21 | Zero effort seat cushion BCG HR (JMIR Rehabil Assist Technol 2021, PMC8204244) | Seat pad BCG HR is a prototype | 9 subjects | 95.1% HR accuracy, motion artifact limited | ECG | Seat pad HR (research/demo) | LOW (prototype, small n) |
| P15 | Emfit QS BCG vs PSG (JMIR Biomed Eng 2020; Ranta JCSM 2022) [carried from Phase 1] | Under mattress BCG measures resting HR and bed exit; poor sleep staging | 31 older adults (avg 84) + PSG cohorts | Good resting HR and sleep onset; low sleep stage agreement | PSG | Bedroom vitals/sleep node | MEDIUM |

Note: P3a, P3b (camera gait validation, side/oblique only), P7 (long lie), P10 (nocturia), P17 (real world fall false positives) are carried from `research/a/phase1_markers.md` and cited here without re logging.

---

## Open Questions

1. Nadir versus oblique camera gait accuracy remains formally UNVALIDATED as a bench result for this product (carried from Phase 1 Open Question 1). The architecture assumes the oblique node hits the approx 0.04 m/s error the literature reports; a low cost single node may not. Bench test in Phase 3/G1. MEDIUM impact: if the low cost oblique node cannot hit the error floor, gait speed weakens to a coarse trend and A2 (radar gait, error approx 0.02 m/s [P19]) becomes more attractive.
2. Vayyar and radar vendors do not publish sensitivity and specificity for fall and long lie; only marketing multipliers ("4X"). The real world false positive rate of any fall modality is the make or break number (Phase 1 [P17]) and is UNKNOWN per vendor. Must be characterized at G2.
3. Radar gait fidelity versus an oblique camera is not settled for the specific in home geometry (short paths, furniture, multi person). P19 is promising but from controlled cohorts. If radar gait proves equal in home, the camera loses its last unique job except hazard inventory, and A2 could become primary.
4. Thermal array bathroom viability is unconfirmed: LWIR thermal contrast degrades in steam and no primary bathroom validation exists [S6]. Thermal is therefore not a bathroom fall candidate; radar is. Retained as an occupancy option only.
5. Precise cloud cost per resident per month for the assistant (T4) is deferred to `shared_llm_layer.md` and `shared_infra_cost.md`, unread in this phase. The sensing transport cost is near zero; the recurring cost is assistant tokens.
6. Per home node count and therefore BOM depend on the target home size and the buyer (A7). The 5 zone, single resident model here is an assumption; a payer or operator channel may standardize a different kit. Phase 3 and Phase 7.
7. Whether the bedroom vitals node should be a bed mat (Emfit, Withings, or a DIY load cell node at est $15 to $30 [S21]) or a second radar is unresolved. The mat is cheaper and shipping but weak on sleep staging; radar adds fall coverage in the bedroom at higher cost. Decide in Phase 3 against the marker value.
8. Exact on node silicon for the T1 camera path (IMX500 vs a camera SoC with NPU vs a small accelerator) is Phase 3, driven by the Phase 4 model choice.

## Assumptions Made

1. A home is a 2 bedroom, single resident dwelling with 5 sensing zones. If homes are larger or multi resident, node count and BOM scale and the mesh cost rises. Confidence MEDIUM.
2. PIR and door contacts are treated as materially cheaper than radar or camera nodes, consistent with the coordinator fact sheet pricing [S8]. Firmed in Phase 3.
3. The bathroom and bedroom are hard no camera rooms, per Phase 1 and the market/consent constraint in `shared_privacy_security` 5. Treated as non negotiable, not a preference.
4. The T4 hybrid assistant path processes only derived, non reconstructable features in the cloud, never raw video, per `shared_privacy_security` 2. The "no video leaves" claim is assumed enforceable and is scoped for proof in Phase 5.
5. Radar node BOM of approx $30 to $120/room is an estimate built from the TI and Infineon chip prices plus typical module overhead [S2][S3]; the Vayyar approx $250 is a finished retail node [S4]. A custom node should land between. Confidence MEDIUM.
6. Object memory and natural language query are LATER (Phase 0), so v1 does not require an in home hub; the T4 cloud assistant runs on derived features. If either moves into v1, a T2 hub (Jetson Orin NX 16GB class, est $150 to $400) is added. Confidence HIGH on the split, MEDIUM on the hub price.
7. Seat pad BCG is a research prototype [P21] and is not budgeted for v1; sit to stand count comes from the camera or a simple seat occupancy sensor, not seated HR. Confidence HIGH.

## Confidence Summary

Overall confidence: HIGH on the architecture decision, MEDIUM on the specific node BOM and on radar versus camera gait parity.

- HIGHEST confidence: the bulb fails on both switched power and viewing angle and does not survive as the primary sensor; the bathroom forces a non camera radar node; the evidence rich low cost markers ride on a PIR/door mesh, not a camera; WiFi CSI is a research path for fall and gait and a product path for coarse motion only; the fall path must be T1 local and T3 raw to cloud is rejected. These are grounded in primary vendor specs, primary gait literature, and the Phase 1 matrix.
- HIGH confidence: A1 (distributed mesh with one oblique camera) is the only architecture that observes the full v1 shortlist while keeping cameras out of private rooms; A2 (all radar) is a genuine privacy maximal fallback that keeps the two highest value features and the bathroom at the cost of hazard inventory and sit to stand detail.
- MEDIUM confidence, carried as Open Questions: per node BOM at low volume, real world fall false positive rates per modality (vendor accuracy not public), radar versus oblique camera gait parity in real homes, and the bed mat versus bedroom radar choice.
- The single load bearing conclusion, HIGH confidence: the product is a distributed multi node system, T4 hybrid with a T1 local fall path, primary A1 with fallback A2. The camera survives once, obliquely, in one shared room. The E26 bulb does not survive.


===================================================================
# (phase3_hardware.md)
===================================================================

# Concept A, Phase 3: Hardware and BOM

Governed by `00_framework.md` (sections 4, 5, 6, 9) and `01_concept_a_elder_monitoring.md` (Phase 3). Costs only the architecture selected in Phase 2: A1, the distributed mesh. Rejected architectures (A0 bulb, A2 all radar, A3 multi camera, A4 WiFi CSI) are not costed. Builds on the Phase 2 component prices `[S2][S3][S8][S9][S10][S16][S20][S21]` and extends them with new distributor and CM sourcing. New citation keys are `[H#]`; Phase 2 keys `[S#]` and `[P#]` are reused and resolve in that file.

Confidence tags are HIGH, MEDIUM, LOW per framework section 5. Prices are labeled list, distributor, retail, CM, or estimate. Estimates are built from sourced component prices plus standard PCBA and assembly overhead; they are labeled estimate and are not to be read as quotes.

## The system being costed

A home is a 2 bedroom, single resident dwelling with 5 sensing zones (living area, kitchen, hallway, bedroom, bathroom), carried from Phase 2. The A1 node set:

| Qty | Node | Zone | Modality | Power | Radio |
|---|---|---|---|---|---|
| 5 | PIR occupancy node | one per zone | pyroelectric PIR | battery | Thread or Zigbee |
| 4 | Door and window contact | front door, bathroom door, refrigerator, one cabinet | reed or Hall | battery | Thread or Zigbee |
| 1 | 60 GHz radar node | bathroom | FMCW mmWave | mains | WiFi |
| 1 | Under mattress BCG mat | bedroom | piezo or PVDF | mains or battery | Thread or WiFi |
| 1 | Oblique camera node | living area or hallway | RGB plus IR, on node inference | mains | WiFi |
| 1 | Hub and assistant | central | Thread and Zigbee border router, WiFi gateway, microphone array, speaker | mains | WiFi, Thread, BLE |

Total 13 devices covering 5 rooms. The 9 piece PIR and contact mesh is the evidence rich, low cost backbone. The three mains nodes (radar, camera, hub) carry most of the cost, most of the certification burden, and all of the thermal risk.

---

## 2.1 Compute silicon

### Requirement basis: envelope, not model

Phase 4 (software and model selection) is not yet produced. Per the Phase 3 instruction, the compute requirement here is a derived envelope, to be validated against the actual model in Phase 4 and on the bench at G1. Stated explicitly so it is not mistaken for a model derived figure.

Two on node inference jobs drive silicon selection, both on the camera node. No cloud silicon is in scope here (the assistant LLM cost lives in `shared_infra_cost.md` and `shared_llm_layer.md`).

| Job | Envelope requirement | Basis |
|---|---|---|
| Gait metric extraction | Single person 2D human pose, 13 to 17 keypoints, 30 fps at 720p to 1080p, oblique view, followed by lightweight temporal math for speed, cadence, step length, sit to stand | Phase 1 sensing matrix and Phase 2 gait finding (30 fps, 720p to 1080p, oblique) [S12][S13] |
| Living area fall and long lie | Frame level fall classifier plus a floor dwell timer on the same pose stream | Phase 1 rank 1 (long lie) and fall path |

Real time single person pose at 30 fps and 720p sits at roughly 1 to 4 effective INT8 TOPS for the current open pose models (MoveNet, RTMPose, YOLO pose class), or is delivered by an in sensor detector that runs one small network and hands keypoints to a cheap host. The bathroom and bedroom fall paths do not use this silicon at all: the radar node runs its own fall detection on its on chip DSP, and the bed mat runs threshold logic on a microcontroller. Only the one camera node needs a vision inference engine.

### Candidate evaluation

Prices are the best available at 2026-07-10. Volume tier prices for silicon are frequently gated behind NDA; where a tier is not published it is marked UNKNOWN and estimated from analogous parts, labeled estimate.

| Candidate | Effective AI perf | Power at load | Package cost (label) | Runs the pose envelope at 30 fps | Thermal in sealed enclosure | Toolchain | Availability | Verdict for the camera node |
|---|---|---|---|---|---|---|---|---|
| Sony IMX500 (in sensor) | On sensor NPU, one small network, approx 8 MB in package | Approx 0.2 to 0.5 W added to the sensor | $70 retail as the Raspberry Pi AI Camera reference module [S16]; bare IMX500 sensor est $20 to $35 at volume, Sony gated (UNKNOWN published) | Marginal alone: runs a detector or a lightweight keypoint net in the sensor; full multi joint gait math runs on a cheap host. This is the point, pixels never leave the sensor package | Trivial. Fanless, sealed viable | Sony AITRIOS, Ultralytics export path; constrained to models that fit the in package memory | In production to at least Jan 2028 [S16] | PRIMARY. The only option that keeps pixel data inside the sensor package, which is the load bearing privacy claim |
| Ambarella CV25 or CV22 | CVflow, pose plus activity demoed on device | Approx 1 to 2 W (CV25), higher (CV22) | NDA. Est $10 to $18 (CV25), $20 to $35 (CV22) at volume, labeled estimate; single unit UNKNOWN | Yes, purpose built for camera pose and activity at 4MP30 (CV25) or 8MP (CV22) | Manageable with a small heatsink | Ambarella CVflow SDK, closed, design house typically required | Through Ambarella and camera design houses; not stocked at distributors | ALTERNATIVE. Cleanest single chip image plus CV path, but NDA pricing and a closed toolchain lock the BOM to Ambarella |
| Rockchip RK3576 | 6 TOPS NPU | Approx 3 to 5 W | Chip est $15 to $25 at volume (labeled estimate); reference board $103 [H1] | Yes, with headroom | Needs a heatsink and vent; sealed fanless is marginal | RKNN toolkit, maturing | Strong Chinese supply chain | ALTERNATIVE (cost down). Pixels enter the SoC, still no video leaves the home, but not the in package claim |
| Rockchip RK3588 | 6 TOPS NPU, 8 core | Approx 5 to 8 W | Chip est $30 to $50 at volume (labeled estimate); SBC $150 to $180 [H1][S20] | Yes, large headroom | Poor. 5 to 8 W in a sealed elder home node needs active cooling or a large heatsink | RKNN, mature | Strong | REJECT for the node (thermal and cost); candidate for the hub upgrade path only |
| Hailo-8L accelerator | 13 TOPS | Approx 1.5 to 2.5 W | M.2 module approx $70 retail in the Raspberry Pi AI Kit [H2]; chip est $20 to $30 at volume, labeled estimate | Yes, large headroom | Manageable, but it is an accelerator that still needs a host SoC and its own board area | Hailo Dataflow Compiler, good | Mouser, DigiKey [H2] | REJECT for the node. Needs a host, doubling silicon; overkill for single person pose |
| STMicroelectronics STM32N657 | Neural ART NPU, 600 GOPS, 3 TOPS per W | Sub 1 W | $10.85 tape and reel at MOQ 3000, up to $20.62 by variant [H3] | Partial. Fine for a detector or a small keypoint net; not full multi person pose at 30 fps 1080p | Excellent, sub 1 W, sealed viable | ST Edge AI, STM32Cube.AI; existing ST relationship noted in the brief | DigiKey in stock [H3] | ALTERNATIVE for a stripped camera node or as the radar and mesh host MCU. Under specified for the full gait model |
| Allwinner V851 or V853, SigmaStar SSC338Q, Ingenic T31 | 0.2 to 1 TOPS NPU (Allwinner); small NPUs on SigmaStar and Ingenic | Approx 0.5 to 1.5 W | Chip est $4 to $8 (Allwinner, SigmaStar, Ingenic), labeled estimate; some Alibaba listings quote far lower and are not credible for a genuine part [S9][H4] | Detection yes, credible full pose at 30 fps no. Correct role is the low cost host that pairs with the IMX500 | Good, low power | Vendor BSPs, thin; camera ODM support | The entire Alibaba camera module ecosystem, deep supply [S9][H4] | SELECTED as the host SoC beneath the IMX500 (aggregation, gait math, WiFi, OTA). Not the inference engine |
| NVIDIA Jetson Orin Nano 8GB | 67 TOPS (Super) | 7 to 25 W | Module approx $299 retail and small qty [H5]; 1ku UNKNOWN, est $200 to $260, labeled estimate | Far more than needed | Not viable in a sealed node. Requires active cooling | JetPack, CUDA, mature | Arrow, Seeed, Connect Tech [H5] | REJECT for the node. Overpowered, hot, expensive. Hub upgrade path only |
| NVIDIA Jetson Orin NX 16GB | 100 to 157 TOPS | 10 to 40 W | Module $399 to $599 at 1ku [H6] | Far more than needed | Not viable sealed | JetPack, CUDA | Arrow, CDW [H6] | REJECT for v1. Only justified if an on premises vision language model or object memory moves into scope, which Phase 0 classes LATER |
| Kneron, Synaptics Katana, ADI MAX78000, Nordic nRF54, Arduino | Ultra low power vision or radio MCU | Sub 1 W | Various, not sourced this phase | No, all under the 30 fps pose envelope | n/a | n/a | n/a | Not evaluated as the vision engine. Per the brief: the nRF54 class part is the radio and sensor hub, not the inference engine; Arduino is not a candidate for anything here |

### Camera node silicon decision

Primary: Sony IMX500 in sensor inference paired with a low cost Allwinner or SigmaStar host SoC. Rationale, in priority order:

1. The IMX500 is the only path where pixel data never leaves the sensor package, which is the strongest form of the concept privacy claim and directly supports the "no video ever leaves" positioning [S16]. Every other option moves raw pixels into a general purpose SoC (still inside the home, still T1, but a weaker claim).
2. Thermal. The camera node is a sealed, fanless, mains device in a living space. The IMX500 adds a few hundred milliwatts; the host SoC runs 1 to 2 W. This fits a sealed enclosure. RK3588 and any Jetson do not.
3. Cost. IMX500 sensor plus a sub $8 host is materially cheaper than a Hailo plus host or any Jetson.

The IMX500 constraint is model fit: it runs one small network in the sensor. If Phase 4 selects a pose model that does not fit the in package memory, the fallback is the Ambarella CV25 (single chip, purpose built, thermal and cost acceptable, at the price of a closed toolchain and NDA pricing) or the RK3576 (flexible, cheap, but pixels enter the SoC). This is Open Question 1.

### Hub silicon decision

The hub is a Thread and Zigbee border router, a WiFi gateway, and the voice front end for the assistant. The heavy assistant LLM runs in the cloud (Phase 2 T4, `shared_infra_cost.md`), so the hub does not need a large NPU in v1. An RK3566 class SoC (chip from $10.31 at LCSC [H7]) runs the border router, local wake word, on device speech to text buffering, and event aggregation with room to spare. The Jetson Orin Nano or NX is the hub upgrade path only if on premises object memory or an on premises vision language model moves from LATER into scope; it is not in the v1 hub.

---

## 2.2 Image sensor and optics

Specified from the gait requirement, not from a spec sheet wish. The requirement, from Phase 1 and Phase 2: oblique view of a 2.5 to 4 m walking path, 30 fps, 720p to 1080p, usable in low light (hallway at night is a primary gait capture location), therefore IR sensitivity and an IR illuminator, with a mechanical IR cut filter so daytime color and night IR both work.

The $4 versus $40 comparison, on this specific requirement:

| Option | Part | Resolution and low light | IR | Meets the gait requirement | Module cost (label) |
|---|---|---|---|---|---|
| The $4 module | OV2640 based module | 2 MP, poor low light, rolling shutter | Weak without an added illuminator | No. Fails the night hallway low light case; noise at low lux destroys keypoint stability | Approx $3 to $5 [H4] |
| The right part | SC2336 or Sony IMX307 STARVIS, 2 MP StarLight class | 2 MP, strong low light (starlight class), clean at low lux | IR sensitive, pairs with an 850 nm illuminator and an IR cut switch | Yes. This is the correct floor for night gait | Bare MIPI module est $8 to $15; integrated USB with ISP est $17 to $30 [H4] |
| The $40 module | Integrated IMX335 5 MP USB module with ISP, IR cut, and illuminator | 5 MP, strong low light | Full IR path integrated | Yes, and over specified. 5 MP is more than 1080p gait needs | Approx $30 to $40 [H4] |
| The privacy anchor | Sony IMX500 (as above) | 12 MP sensor, on chip inference | Add an external 850 nm illuminator and IR cut | Yes, plus it keeps pixels in the sensor package | Sensor est $20 to $35 at volume; $70 as the RPi AI Camera reference [S16] |

Finding: the gait requirement is met by a roughly $10 to $15 StarLight class 2 MP module (SC2336 or IMX307), not by the $4 OV2640 (fails low light and IR) and not requiring the $40 5 MP module (over specified). The $40 premium buys resolution the product does not claim. In the selected architecture the camera node uses the IMX500 for the in sensor inference privacy claim, at an est $20 to $35 sensor cost plus an $850 nm illuminator (est $0.50 to $1.50) and an IR cut filter mechanism (est $1 to $3). If Phase 4 forces a camera SoC path, the SC2336 or IMX307 StarLight module at $10 to $15 is the correct sensor, not the OV2640 and not the 5 MP part. HIGH on the requirement, MEDIUM on the volume module prices (Alibaba CM range, not firm quotes).

Optics: a fixed focus lens, roughly 90 to 110 degree horizontal field of view to frame a 2.5 to 4 m path from a shelf or corner, M12 mount, est $1 to $4. No autofocus, no zoom.

---

## 2.3 Everything else on the mains nodes

| Subsystem | Selection | Function | Cost (label) | Confidence |
|---|---|---|---|---|
| Radio, mesh nodes | ESP32-C6 module or an nRF52 or ESP32-H2 class part | WiFi 6, BLE 5, and 802.15.4 (Thread and Zigbee) in one part; the mesh uses the 802.15.4 side, the mains nodes use WiFi | ESP32-C6-MINI module from $2.96, bare SoC from $2.18 at LCSC [H8] | HIGH |
| Radio, hub | ESP32-C6 or a dedicated Thread and Zigbee coordinator alongside the RK3566 WiFi | Border router plus WiFi gateway | As above plus SoC WiFi | HIGH |
| Microphone array (hub only) | 2 to 4 MEMS microphones plus a codec | Wake word and assistant voice capture; on device wake word, no retained raw audio, per Phase 2 and `shared_privacy_security` 4.4 | Mics est $0.50 to $1.00 each, codec est $1 to $2 | MEDIUM |
| Speaker and amplifier (hub only) | Small speaker plus a class D amp | Assistant voice output | Est $1 to $3 | MEDIUM |
| Power, AC to DC (mains nodes) | External UL listed wall adapter, 5 V, 2 A | Offloads mains safety certification to the pre listed adapter | Retail $6 to $10; OEM CM est $2 to $4 at volume [H9] | MEDIUM |
| Holdup, dying gasp (mains nodes) | Supercapacitor plus PMIC | Sends a power loss packet before the node dies, per Phase 2 1.2.1 | Est $1 to $3 BOM [S15] | MEDIUM |
| Enclosure | Injection molded ABS or PC, two part | Housing, mount, light pipe | Per part est $0.30 to $1.50 at volume plus tooling NRE (below) | MEDIUM |
| Indicator LED and provisioning | RGB status LED plus a pairing button; provisioning over BLE from the app | Visible active indicator (required for consent, Phase 2) and setup | Est $0.30 to $0.80 | HIGH |

Design note on the AC to DC stage: using an external pre listed wall adapter rather than an internal mains supply is a deliberate cost and certification choice. It moves the mains isolation safety burden onto a component that is already UL or ETL listed, and it reduces the device itself to a low voltage DC product, which shrinks its own safety scope to UL 62368-1 at low voltage. This is the standard consumer IoT approach and it materially lowers certification NRE.

---

## 2.4 Non camera nodes

### PIR and door contact mesh

The cheapest and highest evidence nodes. Retail reference: Aqara Motion Sensor P1 approx $13 to $25, contact sensor approx $13 to $20 [S8]. As an own build the BOM is far lower because the retail price carries brand margin and channel.

| Node | Key parts | BOM 1 | BOM 1k | BOM 100k | Confidence |
|---|---|---|---|---|---|
| PIR node | Pyroelectric PIR sensor and Fresnel lens (est $0.30 to $1.00), ESP32-C6 or nRF52 radio ($2 to $3 [H8]), PCB, battery holder plus CR123 or 2x AA, enclosure, LED, button | est $14 | est $6.50 | est $4 | MEDIUM |
| Contact node | Reed or Hall sensor and magnet (est $0.20 to $0.60), radio SoC ($2 [H8]), PCB, coin cell, enclosure | est $10 | est $4.50 | est $2.80 | MEDIUM |

These are estimates built from the sourced radio price plus standard PIR, PCB, battery, and enclosure costs. Firm CM quotes are an Open Question.

### 60 GHz radar node (bathroom)

The single most expensive sensing node and the one that makes the bathroom fall claim possible. Build path is the TI IWR6843 (on chip DSP and MCU, runs the fall and long lie detection itself, no host inference SoC needed) [S2], or the lower cost TI IWRL6432AOP (approx $11.19 at 1ku [S17], lower power, weaker for whole room fall) or Infineon BGT60TR13C (approx $19.72, presence and vitals, needs a host MCU [S3]). The finished Vayyar Care node is approx $250 retail [S4] and sets the buy versus build ceiling.

| Node | Key parts | BOM 1 | BOM 1k | BOM 100k | Confidence |
|---|---|---|---|---|---|
| Radar node (IWR6843 build) | IWR6843 ($43 single, est $28 at 1k, est $24 at 100k [S2]), antenna on PCB, PMIC, ESP32-C6 WiFi ($3 [H8]), supercap holdup ($2 [S15]), AC to DC adapter ($2 to $4 [H9]), enclosure, test | est $145 | est $62 | est $42 | MEDIUM |

The IWR6843 volume pricing is estimated from the $43 single unit price and typical TI volume curves; TI 1ku pricing is quote gated (UNKNOWN published). A custom node landing between the raw chip cost and the $250 Vayyar retail node is credible. MEDIUM.

### Under mattress BCG mat (bedroom)

Is it real and accurate: yes for resting heart rate, respiration, and bed exit; weak for sleep staging. This is a shipping, validated modality, not a research demo. Emfit QS reports heart rate limits of agreement of plus or minus 4.4 bpm versus ECG [S10][P15]; Withings Sleep Analyzer is validated in adults aged 65 to 83 with heart rate within 2 bpm and apnea detection around 88 percent [S21]; the clinical EarlySense holds FDA 510(k) K180079 with heart rate 96.1 percent and respiratory rate 93.3 percent [S21]. Sleep stage classification is the weak axis across all under mattress BCG products [P15]. The seat pad BCG, by contrast, is a research prototype only (9 subjects, motion artifact limited [P21]) and is not in the v1 BOM; sit to stand count comes from the camera, not from a seat sensor.

Shipping product prices: Emfit QS approx $299 (CA$420) [S10], Withings Sleep Analyzer $199.95 [S21]. Own build BOM:

| Node | Key parts | BOM 1 | BOM 1k | BOM 100k | Confidence |
|---|---|---|---|---|---|
| Bed mat BCG | Piezo or PVDF film strip ($5 to $10), charge amp and AFE ($2 to $4), MCU plus radio ESP32-C6 ($3 [H8]), PCB, mat substrate and enclosure ($4 to $8), cable | est $45 | est $20 | est $13 | MEDIUM |

Buy versus build: at low volume, licensing an Emfit or Withings OEM path may beat an own build once validation and firmware effort are counted; at high volume the own build wins on unit cost. Decided in Phase 6.

---

## 2.5 Full BOM, landed cost, COGS, and NRE

### Per node BOM at each volume tier (hardware BOM, USD, estimate)

| Node | 1 | 100 | 1k | 10k | 100k |
|---|---|---|---|---|---|
| PIR node | 14 | 9 | 6.50 | 5 | 4 |
| Contact node | 10 | 6.50 | 4.50 | 3.50 | 2.80 |
| Radar node | 145 | 85 | 62 | 50 | 42 |
| Bed mat BCG | 45 | 28 | 20 | 16 | 13 |
| Camera node (IMX500 plus host) | 110 | 70 | 52 | 42 | 34 |
| Hub | 75 | 52 | 40 | 33 | 28 |

### Full home system BOM (5 PIR, 4 contact, 1 radar, 1 bed mat, 1 camera, 1 hub)

| Line | 1 | 100 | 1k | 10k | 100k |
|---|---|---|---|---|---|
| 5x PIR | 70 | 45 | 32.50 | 25 | 20 |
| 4x contact | 40 | 26 | 18 | 14 | 11.20 |
| 1x radar | 145 | 85 | 62 | 50 | 42 |
| 1x bed mat | 45 | 28 | 20 | 16 | 13 |
| 1x camera | 110 | 70 | 52 | 42 | 34 |
| 1x hub | 75 | 52 | 40 | 33 | 28 |
| System hardware BOM | 485 | 306 | 224.50 | 180 | 148 |

### Landed cost and COGS (per home system)

Landed adds assembly, functional test, packaging, freight, and duty, plus yield loss, at approx 35 percent at 1 unit falling to approx 22 percent at 100k as assembly automates and yield matures. COGS adds warranty reserve, returns, and support allocation at approx 11 to 12 percent.

| Metric | 1 | 100 | 1k | 10k | 100k |
|---|---|---|---|---|---|
| Hardware BOM | 485 | 306 | 224.50 | 180 | 148 |
| Landed cost | 655 | 404 | 292 | 227 | 181 |
| COGS | 730 | 452 | 327 | 254 | 201 |

Reading: a complete 13 device home system costs approximately $327 in COGS at 1,000 systems and approximately $201 at 100,000 systems. The three mains nodes (radar, camera, hub) are approximately 68 percent of the system BOM at 1k ($154 of $224.50); the 9 piece mesh that carries the highest evidence markers is only approximately $50. The single largest line item at every tier is the radar node, followed by the camera node.

### NRE (one time, hardware only)

Software and firmware development is costed in Phase 6 and is not double counted here. FTC gait measurement substantiation (framework sections 2 and 4) is a validation cost that lands at G3 and G4 and is Phase 6, not a hardware NRE line; it is flagged, not costed here.

| NRE item | Basis | Estimate |
|---|---|---|
| Injection mold tooling, 5 enclosures | Aluminum molds for mid volume run $2,000 to $5,000 each; steel for high volume $5,000 to $30,000 each [H10]. Shared enclosure platform across the battery nodes reduces count | $25,000 to $80,000 |
| PCB spins, 6 boards at 2 to 3 spins | Layout, fab, assembly of prototype runs | $10,000 to $25,000 |
| Certification, FCC Part 15 B and C | Camera, radar, and hub are intentional radiators. WiFi integrated device FCC certification $6,500 to $12,000 each; using pre certified radio modules cuts 60 to 80 percent [H11]. The 60 GHz radar is the costly one (band and antenna testing). Battery mesh nodes use a pre certified radio module, so modular FCC only | $20,000 to $45,000 across SKUs |
| Certification, UL or ETL listing | Mains devices to UL 62368-1 at low voltage (external adapter is separately pre listed). ETL is 20 to 30 percent below UL; UL runs $5,000 to $50,000 per product [H11]. Three mains SKUs (camera, radar, hub) | $24,000 to $60,000 |
| Certification, ongoing UL or ETL mark and factory inspection | Quarterly mark fee plus inspection [H11] | $3,000 to $8,000 per year, recurring |
| Hardware NRE total (excl. recurring) | | approx $80,000 to $210,000 |

Certification is the most underestimated line and it lands at G5 per the framework. The 60 GHz radar intentional radiator testing and the three way UL or ETL listing are the drivers. Using an external pre listed AC to DC adapter and pre certified radio modules is the single biggest lever to hold this down.

### Implied retail versus competitors

At a 50 percent hardware gross margin (retail equals 2x COGS), the implied one time hardware retail price is approximately $650 at 1k systems, approximately $510 at 10k, and approximately $400 at 100k. In this category hardware is typically sold near cost and the margin is taken in a recurring subscription (`shared_infra_cost.md` establishes the recurring cost structure), so a hardware retail of $299 to $499 with a monthly service fee is the realistic posture, matching the market below.

| Product | What it sells | Hardware price | Recurring | Note |
|---|---|---|---|---|
| This system (A1) | 13 device mesh: falls, long lie, gait, vitals, ADL, assistant | Implied $400 to $650 at margin; realistic $299 to $499 subsidized | Service TBD (`shared_infra_cost.md`) | Far richer feature set than any single competitor below |
| Vayyar Care | Single modality 60 GHz fall node | $250 per device, approx 3 per home ($750) [S4] | $20 per month [S4] | Falls only, no gait, no ADL, no vitals |
| CarePredict @Home | Wearable plus environment kit | $499 upfront [competitor scan] | $69.99 per month after a 45 day trial | Wearable based; the resident must wear it |
| Envoy at Home | 8 sensor passive kit | $399 one time [competitor scan] | $99 per month | PIR and contact class, AI reports, passive fall |
| People Power Presence | Gateway plus 2 contact plus 3 motion | Subscription bundled [competitor scan] | Subscription | Mesh only, no camera, no radar |
| Butlr Care | Anonymous thermal presence | B2B, per sensor annual | Approx a couple hundred dollars per sensor per year [competitor scan] | Senior living channel, thermal only |
| Amazon Alexa Emergency Assist | Response service on Echo | Uses existing Echo | $7.99 per month [S22] | Response only; Alexa Together caregiver monitoring was discontinued approx 2025-05 [S22] |
| Medical alert with fall (benchmark) | Pendant plus base | $199 to $450 [competitor scan] | $25 to $40 per month | Single function reference point |

Positioning read: the A1 system COGS of approximately $201 to $327 at volume supports a $299 to $499 subsidized hardware price, which is competitive with the CarePredict and Envoy multi sensor kits and undercuts three Vayyar nodes at $750, while delivering a materially broader marker set (falls plus long lie plus gait plus contactless vitals plus ADL plus assistant) than any single competitor. The cost of that breadth is concentrated in two nodes, the radar and the camera; the rest of the system is cheap. The strategic question the business case must answer (Phase 7 and Phase 8) is whether the added breadth justifies the added hardware cost against a market that has repeatedly failed to sustain consumer hardware plus subscription in this category.

---

## Register Entries

### Components (for `components.md`)

| Part / product | Manufacturer | Function | Price by tier (label) | Source | Confidence |
|---|---|---|---|---|---|
| IMX500 (RPi AI Camera) | Sony | In sensor inference image sensor; pixels stay in package | $70 retail module; bare sensor est $20 to $35 at volume, 1ku UNKNOWN | [S16] | HIGH spec / MEDIUM volume price |
| RK3576 | Rockchip | 6 TOPS NPU SoC, camera node alternative | Chip est $15 to $25 volume; board $103 | [H1] | MEDIUM |
| RK3588 | Rockchip | 6 TOPS NPU SoC, hub upgrade | Chip est $30 to $50; SBC $150 to $180 | [H1][S20] | MEDIUM |
| RK3566 | Rockchip | Quad A55 SoC, selected hub | From $10.31 chip at LCSC | [H7] | HIGH |
| Hailo-8L | Hailo | 13 TOPS M.2 accelerator | Module approx $70 retail; chip est $20 to $30 volume | [H2] | HIGH spec / MEDIUM volume price |
| STM32N657 | STMicroelectronics | 600 GOPS NPU MCU; radar/mesh host or stripped camera | $10.85 T&R at MOQ 3000 to $20.62 by variant | [H3] | HIGH |
| Ambarella CV25 / CV22 | Ambarella | CVflow camera SoC, pose and activity; camera node alternative | NDA; est $10 to $18 (CV25), $20 to $35 (CV22) volume | [competitor/vendor scan] | LOW price / HIGH spec |
| Allwinner V851 / V853 | Allwinner | Low cost camera SoC, selected IMX500 host | Chip est $4 to $8 | [S9][H4] | MEDIUM |
| SigmaStar SSC338Q, Ingenic T31 | SigmaStar, Ingenic | Low cost camera SoCs, host alternatives | Chip est $4 to $8 | [S9][H4] | MEDIUM |
| Jetson Orin Nano 8GB | NVIDIA | 67 TOPS module, hub upgrade only | Approx $299 module; 1ku UNKNOWN, est $200 to $260 | [H5] | MEDIUM |
| Jetson Orin NX 16GB | NVIDIA | 100 to 157 TOPS module, hub upgrade only | $399 to $599 at 1ku | [H6] | HIGH |
| SC2336 / IMX307 StarLight module | SmartSens / Sony | 2 MP low light IR sensitive gait sensor (SoC path) | Bare MIPI est $8 to $15; USB integrated est $17 to $30 | [H4] | MEDIUM |
| IMX335 5 MP module | Sony | Over specified low light module | Approx $30 to $40 | [H4] | MEDIUM |
| OV2640 module | OmniVision | Low cost 2 MP; fails low light and IR requirement | Approx $3 to $5 | [H4] | MEDIUM |
| ESP32-C6-MINI / WROOM | Espressif | WiFi 6, BLE 5, Thread, Zigbee radio | Module from $2.96; SoC from $2.18 at LCSC | [H8] | HIGH |
| IWR6843 | Texas Instruments | 60 GHz radar with on chip fall detection | $43 single; est $28 at 1k, $24 at 100k, 1ku UNKNOWN | [S2] | HIGH spec / MEDIUM price |
| IWRL6432AOP | Texas Instruments | Low power 60 GHz radar | Approx $11.19 at 1ku | [S17] | MEDIUM |
| BGT60TR13C | Infineon | 60 GHz radar, presence and vitals | Approx $19.72 | [S3] | HIGH spec / MEDIUM price |
| Emfit QS | Emfit | Under mattress BCG, validated HR and bed exit | Approx $299 (CA$420) retail | [S10][P15] | HIGH price / MEDIUM accuracy |
| Withings Sleep Analyzer | Withings | Under mattress BCG, validated in 65 to 83 | $199.95 retail | [S21] | HIGH |
| Piezo / PVDF bed mat (own build) | Various | Bedroom BCG node | BOM est $45 (1) to $13 (100k) | [S21][H8] | MEDIUM |
| AC to DC wall adapter, 5 V 2 A, pre listed | Various | Mains power, offloads safety cert | Retail $6 to $10; OEM CM est $2 to $4 | [H9] | MEDIUM |
| Injection molded enclosure | CM | Node housing | Per part est $0.30 to $1.50; tooling $2k to $30k per mold | [H10] | MEDIUM |

### Vendors (for `vendors.md`)

| Vendor | Supplies | Note | Confidence |
|---|---|---|---|
| Sony (AITRIOS) | IMX500 in sensor inference | Load bearing for the pixels never leave the sensor claim; volume pricing gated | HIGH |
| Rockchip | RK3566 hub SoC, RK3576/RK3588 camera and hub alternatives | Strong Chinese supply, RKNN toolkit | MEDIUM |
| Ambarella | CV25/CV22 camera SoC | Purpose built pose and activity; closed SDK, NDA pricing, design house route | MEDIUM |
| Allwinner, SigmaStar, Ingenic | Low cost camera host SoCs | The Alibaba camera module cost floor; selected as IMX500 host | MEDIUM |
| Espressif | ESP32-C6 radio | WiFi 6, Thread, Zigbee, BLE in one part; LCSC stocked | HIGH |
| Texas Instruments | IWR6843, IWRL6432 radar plus reference designs | Radar build path with on chip fall detection | HIGH |
| Infineon | BGT60TR13C radar | Lower cost presence and vitals radar | HIGH |
| Emfit, Withings | Under mattress BCG products and OEM path | Bedroom node buy option | MEDIUM |
| NVIDIA | Jetson Orin Nano/NX modules | Hub upgrade path only, not v1 | HIGH |
| A UL or ETL recognized test lab (ACB, TUV, Intertek class) | FCC and UL/ETL certification | Certification NRE; select at G4 to G5 | MEDIUM |

### Sources (for `sources.md`)

| Key | Source | URL | Date | Used for | Credibility |
|---|---|---|---|---|---|
| H1 | RK3576 and RK3588 deep dive and board pricing | https://bliiot.com/info-detail/rk3576-deep-dive-6-tops-npu-meets-unbeatable-cost-performance-in-aiot ; https://rockchips.net/product/rk3588/ | 2026 access | RK3576/RK3588 NPU, power, board price | MEDIUM (vendor/secondary) |
| H2 | Hailo-8L at Mouser and DigiKey | https://www.mouser.com/new/hailo/hailo-hailo-8l-m2-ai-acceleration-modules/ ; https://www.digikey.com/en/product-highlight/r/raspberry-pi/ai-kit | 2026 access | 13 TOPS accelerator, module price | HIGH |
| H3 | STM32N657 at DigiKey | https://www.digikey.com/en/products/detail/stmicroelectronics/STM32N657X0H3Q/25675974 | 2026 access | Neural ART MCU price and specs | HIGH |
| H4 | Low light and IR camera module pricing | https://knightli.com/en/2026/05/01/sony-imx-camera-module-guide/ ; https://www.alibaba.com/product-detail/IMX307-IMX335-IMX415-IMX-334-sensor_1600669537778.html ; https://www.cnx-software.com/2022/10/06/allwinner-v851s-v851se-low-cost-camera-soc-embeds-64mb-ddr2-a-0-5-tops-npu/ | 2026 access | SC2336/IMX307/IMX335/OV2640 module prices; Allwinner host SoC | MEDIUM (CM listings) |
| H5 | Jetson Orin Nano 8GB module pricing | https://www.arrow.com/en/products/900-13767-0030-000/nvidia.html ; https://www.seeedstudio.com/NVIDIA-JETSON-ORIN-NANO-8GB-Module-p-5552.html | 2026 access | Orin Nano module price | MEDIUM |
| H6 | Jetson Orin NX 16GB module pricing | https://www.arrow.com/en/products/900-13767-0000-000/nvidia.html ; https://forums.developer.nvidia.com/t/pricing-and-availability-information/278065 | 2026 access | Orin NX 1ku price $399 to $599 | HIGH |
| H7 | RK3566 at LCSC | https://www.lcsc.com/product-detail/Microcontroller-Units-MCUs-MPUs-SOCs_Rockchip-RK3566_C2943786.html | 2026 access | Hub SoC chip price from $10.31 | HIGH |
| H8 | ESP32-C6 at LCSC | https://www.lcsc.com/product-detail/C5364646.html ; https://www.lcsc.com/product-detail/C5736265.html | 2026 access | Radio module and SoC pricing | HIGH |
| H9 | AC to DC 5 V 2 A adapter pricing | https://www.jameco.com/c/AC-to-DC-Wall-Adapters.html ; https://www.digikey.com/en/products/filter/ac-dc-desktop-wall-power-adapters/130 | 2026 access | Mains adapter retail and OEM cost | MEDIUM |
| H10 | Injection mold tooling cost | https://formlabs.com/blog/injection-molding-cost/ ; https://www.rapiddirect.com/blog/injection-molding-costs/ | 2026 access | Mold tooling NRE by volume | MEDIUM |
| H11 | FCC Part 15 and UL/ETL certification cost | https://www.jettest.net/blog/explained-what-is-fcc-certification-cost-breakdown-2026 ; https://factoryfollow.com/en/ul-certification-guide.html ; https://www.komaspec.com/about-us/blog/ul-vs-etl-vs-csa-certification/ | 2026 access | FCC 15B/15C and UL/ETL listing costs | MEDIUM to HIGH |
| H12 | Competitor hardware and subscription pricing | https://www.carepredict.com/ ; https://www.envoyathome.com/ ; https://www.butlr.com/solutions/care ; Vayyar and Alexa per Phase 2 [S4][S22] | 2026 access | CarePredict $499 plus $69.99/mo; Envoy $399 plus $99/mo; Butlr per sensor annual | MEDIUM |

### Papers (for `papers.md`)

Carried from Phase 2 without re logging: P15 (Emfit BCG vs PSG), P19 (radar gait validation), P20 (radar vitals), P21 (seat pad BCG prototype). No new papers added this phase; Phase 3 is a costing phase.

---

## Open Questions

1. Camera node model fit on the IMX500. The IMX500 runs one small network in the sensor package. Whether the Phase 4 pose model fits its in package memory at 30 fps is UNVALIDATED. If it does not, the fallback is the Ambarella CV25 (closed toolchain, NDA price) or the RK3576 (pixels enter the SoC, weaker privacy claim). This decision changes the camera node BOM by roughly plus or minus $15 and changes the strength of the privacy claim. Resolve at G1 with the Phase 4 model.
2. TI IWR6843 1ku and 100k pricing is quote gated (UNKNOWN published). The radar node BOM uses estimates from the $43 single unit price. The radar is the single largest line item, so this estimate carries the most BOM risk. Obtain a TI or distributor volume quote.
3. Ambarella CV25/CV22 pricing is NDA (UNKNOWN). The alternative camera path cost is estimated only.
4. CM assembly, test, packaging, freight, duty, and yield percentages are modeled (35 percent falling to 22 percent), not quoted. A real CM quote at 1k, 10k, and 100k is needed to firm landed cost.
5. Bed mat buy versus build (Emfit or Withings OEM versus own piezo build) is unresolved and depends on validation and firmware effort counted in Phase 6.
6. Node count per home assumes the 5 zone, single resident model. A payer or operator channel may standardize a different kit (fewer or more nodes), which moves the system BOM materially. Phase 7 and Phase 8.
7. Certification scope assumes an external pre listed adapter and pre certified radio modules. If the design integrates a mains supply or a bare radio, UL and FCC scope and cost rise sharply.
8. FTC gait measurement substantiation cost (framework sections 2 and 4) is flagged but not costed here; it is a Phase 6 validation line at G3 to G4, not a hardware NRE.

## Assumptions Made

1. The compute requirement is an envelope (single person pose at 30 fps 720p to 1080p, roughly 1 to 4 effective TOPS, plus a fall classifier), not a model derived figure, because Phase 4 is not yet produced. If the actual model is heavier, the IMX500 primary fails and the node moves to a CV25 or RK3576, raising node cost and lowering the privacy claim. Impact: MEDIUM.
2. The home is 13 devices over 5 zones. Larger or multi resident homes scale node count and BOM. Impact: MEDIUM.
3. Per node BOM figures are estimates built from sourced component prices plus standard PCBA and assembly overhead, not CM quotes. Impact on system BOM: MEDIUM.
4. The radar node runs its fall detection on the IWR6843 on chip DSP, so no separate inference SoC is budgeted in the radar node. If a host SoC is required, add approximately $8 to $15 to the radar node. Impact: LOW to MEDIUM.
5. The bed mat is an own build in the BOM. If an OEM license path is chosen, unit cost rises at low volume and falls slower at high volume. Impact: LOW.
6. Landed adds 35 to 22 percent and COGS adds 11 to 12 percent. These are standard hardware ratios, not quoted. Impact: MEDIUM.
7. The 50 percent hardware gross margin is illustrative; the category norm is hardware near cost with margin in subscription. The implied retail is therefore an upper reference, and the realistic $299 to $499 subsidized price is the operative figure. Impact: LOW on the analysis, HIGH on the go to market, deferred to Phase 8.
8. Certification is scoped to FCC Part 15 B and C plus UL or ETL to UL 62368-1 at low voltage, using a pre listed external adapter. This is the standard consumer IoT scope and is assumed correct; a mains integrated design would change it. Impact: MEDIUM.

## Confidence Summary

Overall confidence: HIGH on the silicon selection logic and the certification framing, MEDIUM on the absolute BOM figures.

- HIGHEST confidence: the camera node should use in sensor inference (IMX500) for the privacy claim and thermal envelope, and the Jetson and RK3588 are wrong for a sealed node (too hot, too expensive); the radar node runs its own fall detection on chip; the seat pad BCG is a research prototype and out of v1, while the under mattress BCG is real and validated for HR, respiration, and bed exit; certification is a hard NRE line dominated by the 60 GHz radar intentional radiator testing and the three way UL or ETL listing. These rest on primary distributor and vendor data and on the Phase 2 findings.
- HIGH confidence: the system cost structure, that the three mains nodes are approximately 68 percent of the BOM and the radar node is the single largest line, and that the cheap PIR and contact mesh carries the highest evidence markers.
- MEDIUM confidence, carried as Open Questions: the absolute per node BOM estimates (radar 1ku pricing gated, Ambarella NDA, CM overhead modeled not quoted), the IMX500 model fit, and the bed mat buy versus build.
- The load bearing conclusion, HIGH confidence: a complete 13 device home system costs approximately $327 in COGS at 1,000 systems and approximately $201 at 100,000, supporting a $299 to $499 subsidized hardware price that is competitive on price with CarePredict and Envoy and cheaper than three Vayyar nodes, while delivering a broader marker set than any single competitor. The cost is concentrated in the radar and camera nodes; the mesh backbone is cheap.


===================================================================
# (phase4_software.md)
===================================================================

# Concept A, Phase 4: Software, Models, and Open Source

Governed by `00_framework.md` (sections 2, 5, 6, 8, 9) and `01_concept_a_elder_monitoring.md` (Phase 4). Inputs consumed and not re researched: the selected architecture A1 (distributed mesh, one oblique T1 camera, T4 hybrid compute) in `research/a/phase2_architecture.md`; the v1 marker shortlist and gait validation numbers in `research/a/phase1_markers.md`; the feature classification and compute split (object memory and free form query are LATER) in `research/a/phase0_scope.md`; and the LLM topology decision in `research/shared/shared_llm_layer.md`.

Governing question for every item, per the Phase 4 brief: does this already exist, and can we use it? Build is the last resort. Every license below was read from the actual LICENSE file, not inferred from a README, per framework section 9. Confidence tags are HIGH, MEDIUM, LOW. Citation keys `[S#]` and `[P#]` resolve in the Register Entries tables. Papers P1 to P21 carried from Phase 1 and Phase 2 are cited without re logging.

The load bearing license finding, stated up front: two of the most cited pose libraries are commercially poisoned. OpenPose is CMU non commercial only. Ultralytics YOLO Pose is AGPL-3.0, which forces either open sourcing the entire product or buying an Enterprise License. The clean, commercially usable, silicon agnostic options are MoveNet, MediaPipe BlazePose, and RTMPose, all Apache-2.0. NVIDIA is not required and its stack locks the BOM to NVIDIA silicon.

---

## 3.1 Vision and Pose

### 3.1.1 Pose estimation, exact license per model

License read from the LICENSE file in each case. "Commercial" is the plain answer to whether a closed source, sold, commercial product may use it without a separate paid agreement.

| Model | Owner | License (SPDX, from LICENSE file) | Commercial use | Runtime / silicon | Note | Confidence |
|---|---|---|---|---|---|---|
| MoveNet (Lightning / Thunder) | Google | `Apache-2.0` [S30] | YES, unrestricted | TFLite / TF.js / ONNX; any CPU, NPU, or GPU; runs on IMX500 class, Hailo, Rockchip | Single person, edge optimized, 2 model sizes; the cheapest clean option | HIGH |
| MediaPipe BlazePose (Pose Landmarker) | Google | `Apache-2.0` [S26] | YES, unrestricted | TFLite / MediaPipe graph; mobile and edge; any silicon | 33 3D landmarks, on device, mobile grade; model card adds no field of use restriction beyond Apache | HIGH |
| RTMPose / RTMO (in MMPose) | OpenMMLab (Shanghai AI Lab) | `Apache-2.0` [S27] | YES, unrestricted | ONNX / TensorRT / ncnn / OpenVINO; any silicon | Current SOTA accuracy per compute for real time; top tier and clean license | HIGH |
| ViTPose | ViTAE-Transformer / OpenMMLab | `Apache-2.0` [S28] | YES, unrestricted | PyTorch / ONNX; heavier, GPU leaning | Highest accuracy class, transformer, heavier than needed for edge | HIGH |
| YOLO-Pose (YOLOv8-pose / YOLO11-pose) | Ultralytics | `AGPL-3.0` [S25] | NO, not without a paid Enterprise License | ONNX / TensorRT / TFLite; any silicon | AGPL network copyleft forces open sourcing the entire product, or buy the Enterprise License. Community report approx $5,000/yr for a sole developer, custom otherwise [S31] | HIGH |
| OpenPose | Carnegie Mellon University | Custom CMU academic / non commercial license [S29] | NO, prohibited. Commercial requires a separate CMU agreement | CUDA leaning, heavy | "Noncommercial internal research purposes" only; explicitly forbids sale, sublicense, and third party access. Do not ship it | HIGH |
| BodyPoseNet / BodyPose3DNet / TRTPose | NVIDIA | NVIDIA model license (TAO / NGC terms) [S33][S34] | YES for the model, but see silicon lock below | TensorRT / DeepStream; NVIDIA GPU or Jetson ONLY | Commercially usable weights, but the deployment runtime is NVIDIA only. This is the lock, see 3.1.2 | HIGH license / HIGH lock |

Findings.

1. Two widely used models are commercially unusable as shipped. OpenPose (CMU non commercial) and Ultralytics YOLO Pose (AGPL-3.0) are the two the Phase 4 brief warned about. AGPL is the more insidious of the two because it is often mistaken for a permissive open license. Under AGPL, offering the product over a network obligates disclosure of the entire corresponding source, which is incompatible with a closed source commercial product. The escape is the Ultralytics Enterprise License, a real recurring cost line [S31]. HIGH.
2. The clean set is MoveNet, MediaPipe BlazePose, RTMPose/RTMO, and ViTPose, all `Apache-2.0`, all commercial with no field of use restriction. For the single oblique edge camera in architecture A1, MoveNet or RTMPose is the recommended pose backbone: both run on non NVIDIA silicon (IMX500, Hailo, Rockchip NPU) and both preserve the T1 "no video leaves the node" claim. RTMPose is the accuracy leader per unit compute; MoveNet is the lightest. HIGH.
3. Model weights carry their own license separate from code. For all four clean models the published weights are released under the same Apache-2.0 terms, unlike several detectors below where the weights diverge from the code. HIGH.

### 3.1.2 NVIDIA specifically, and the silicon lock test (founder assumption A6)

The concept assumes an NVIDIA open source vision model is the right starting point (A6). Tested against primary NVIDIA documentation:

| Question | Finding | Consequence |
|---|---|---|
| Does NVIDIA release usable pose models? | Yes. BodyPoseNet (2D multi person), BodyPose3DNet (3D), and TRTPose, plus PeopleNet for detection, are on the NGC catalog and are marked ready for commercial use [S33][S34] | The models are not the problem |
| What runtime do they require? | TAO trained models deploy through TensorRT and DeepStream, which are NVIDIA only. Deployment targets are Jetson (Orin Nano/NX/AGX) or discrete NVIDIA GPUs [S32][S33] | The runtime is the lock |
| Do they lock the BOM to NVIDIA silicon? | YES. The optimized runtime path (TensorRT engine, DeepStream pipeline) runs only on NVIDIA GPUs and Jetson modules. Choosing NVIDIA's software offering forces an NVIDIA compute node into the BOM | This is the lock the brief asked us to test |
| Is NVIDIA required to do pose at all? | NO. MoveNet, MediaPipe, and RTMPose run on Sony IMX500, Hailo-8L, Rockchip RK3588 NPU, and generic ARM via ONNX/TFLite | NVIDIA is optional, not necessary |

Verdict on A6: disproven. NVIDIA offers commercially usable pose models, but adopting NVIDIA's model stack locks the compute node to Jetson class silicon, which Phase 2 and the Phase 3 BOM direction (Sony IMX500 at approx $70, on sensor inference, pixels never leave the package [S16]) explicitly avoid. A Jetson Orin NX 16GB tier node is approx $300 to $700 versus approx $70 for the IMX500 reference [S20][S16]. The correct choice is an Apache-2.0 model on non NVIDIA edge silicon. NVIDIA silicon belongs only in the optional in home hub if object memory enters a later version (Phase 2 T2 path), never in the always on camera node. HIGH.

### 3.1.3 Fall detection: published approaches, accuracy, and the real world false positive problem

The Phase 4 brief is explicit: a fall detector that cries wolf twice a week gets unplugged in month two. Benchmark numbers and real world numbers are different animals. Both are recorded.

| Approach | Reported lab accuracy | Real world reality | Source |
|---|---|---|---|
| Accelerometer / wearable algorithms (13 algorithms benchmarked) | Sensitivity approx 94% on scripted falls | Collapses to approx 57% sensitivity on real world falls; false alarms 3 to 85 per day in some settings | [P17] carried from Phase 1 |
| Wearable device, real deployment (older adults) | n/a | 84 fall alarms recorded, 83 were false; 42% of false alarms during normal device use | [S35] |
| Accelerometer sensor, long term elderly | Sensitivity 80% (12 of 15 real falls) | 0.049 false alarms per usage hour, reduced to 0.025 per hour after tuning. At 0.025/hr that is still approx 0.6 nuisance alarms per day per node | [S36] |
| Vision RGB pose based | High on scripted datasets | RGB inherently higher false alarm rate: lying down deliberately, sitting abruptly, and floor exercises are confused with falls | [S37] survey |
| Thermal (TaFall, balance informed) | n/a | Claimed overall false alarm rate 0.00126% (single study, lab grade, not an in home deployment number) | [S37] |

The arithmetic that decides the feature: even a 2% per event false positive rate translates to dozens of unnecessary alerts per day in continuous deployment [S37]. A detector at 0.025 false alarms per hour is approx one nuisance alert every other day per node; across a five node home that is multiple per day. This is the "unplugged in month two" failure mode, quantified.

Engineering consequences for v1, consistent with Phase 2 architecture A1:

1. Do not ship a single modality vision fall classifier as the sole fall path. The real world false positive rate of RGB pose fall detection alone is unacceptable [S37][P17]. HIGH.
2. Gate on immobility and long lie duration, not on the fall impact event alone. Phase 1 established long lie (time on the floor) as the highest value, lowest claim risk feature [P7]. A person on the floor for 60 or more seconds who does not self recover is a far higher precision trigger than a sub second impact signature. Duration gating is the single most effective false positive suppressor. HIGH.
3. Use modality confirmation. Architecture A1 places radar in the bathroom and bedroom and a camera in the living area. Where two modalities overlap, require agreement before escalating. This is the multi stage confirmation pattern the recent literature converges on [S37]. HIGH.
4. Real world false positive rate per modality is UNKNOWN per vendor (Vayyar and radar vendors publish only marketing multipliers, Phase 2 Open Question 2). It must be characterized at gate G2 (founder's own home, 30 days) before any pilot. This is a critical path item, not a footnote. HIGH.

### 3.1.4 Gait metric extraction from pose keypoints, validated vs gold standard, with error bars

Two distinct claims must be separated: spatiotemporal gait metrics (speed, cadence, step length) versus joint angle kinematics (hip, knee, ankle angles). They validate very differently.

| Metric class | Best open pipeline | Validation vs gold standard, with error bars | Verdict for v1 |
|---|---|---|---|
| Gait speed, cadence, step length (spatiotemporal) | Pose keypoints (MoveNet/RTMPose) plus a calibrated ground plane; or OpenCap | Camera gait speed RMSE approx 0.04 m/s vs pressure walkway [P3b]; Kinect ICC 0.81 to 0.98 vs GAITRite [P3a]; cadence RMSE approx 2.3 steps/min; step length RMSE 0.05 to 0.08 m [P3b]. Holds for side or oblique view only | v1 as a trend and substantial change signal. Error 0.04 m/s sits below the 0.10 m/s substantial change threshold [P2] |
| Joint angle kinematics (knee/hip/ankle flexion) | OpenCap (open source, `Apache-2.0` class, Stanford) | Overall RMSE approx 5.8 degrees, peak error up to 11.3 degrees vs marker based mocap in healthy gait; 3.2 to 16.4 degrees across gait types; worse for pathological gait; transverse plane and ankle poorly captured [S24b] | NOT v1. Above the 2 to 5 degree clinical threshold, and needs 2 cameras plus cloud processing |

Findings.

1. The product does not claim joint angle kinematics, so the OpenCap 5.8 degree error is not disqualifying; it simply confirms that fine kinematics are out of reach for a single low cost node. What the product claims (gait speed trend) is the spatiotemporal metric, which validates to approx 0.04 m/s from an oblique view [P3b]. HIGH.
2. OpenCap is a real, validated, open source reference but is a two camera plus cloud biomechanics pipeline [S24b], not an edge single node design. Use it as the validation reference and the bench comparator at G1, not as the shipped runtime. MEDIUM.
3. The unresolved risk carried from Phase 1 and Phase 2 stands: whether a single low cost oblique node hits the 0.04 m/s error floor is UNKNOWN and must be bench tested at G1. If it cannot, gait speed degrades to a coarse trend and the all radar fallback A2 (radar gait speed error approx 0.02 m/s [P19]) becomes more attractive. MEDIUM.

---

## 3.2 Activity of Daily Living and Pattern Detection

Stated plainly, per the Phase 4 instruction: the ADL and pattern layer is mostly NOT machine learning. It is deterministic state machines and signal processing over cheap binary sensor streams. This is a feature, not a limitation. Cheap, reliable, and boring beats a model that drifts and needs retraining.

| Capability | Method | Machine learning required? | Why |
|---|---|---|---|
| Room occupancy | Last PIR to fire per zone, with a debounce timer | No | A PIR event plus a timeout is a rule, not a model |
| Room to room transition counting | Ordered PIR/door event sequence over a home topology graph | No | Graph traversal over timestamped events |
| Duration in state (dwell time, sedentary bouts, time in bed) | Interval accumulation between state changes | No | Arithmetic over state transitions |
| Life space (rooms visited, floor traversed) | Set of zones entered per day over the home graph | No | Set cardinality per window |
| Nocturia count (nighttime bathroom trips) | Bathroom door plus PIR events within a night window | No | Event counting with a time gate |
| Circadian IS / IV / RA, L5 / M10 | Nonparametric statistics on the minute level activity time series | No (signal processing, not ML) | Established actigraphy formulas [P8], deterministic |
| Kitchen meal preparation events | Appliance current plus cabinet/fridge contact plus kitchen PIR, rule combined | Mostly no; a light classifier optional | Event co occurrence rules; a small classifier only if disambiguation is needed [P13] |
| Baseline and anomaly ("up from 2 to 6") | Rolling per resident baseline plus a robust deviation threshold (for example median plus k times MAD) | No (classical statistics) | Personal baseline deviation, not a trained model |

Findings.

1. The entire ADL, spatial behavior, sleep timing, toileting, and circadian layer, which is the evidence rich backbone of the product (Phase 1 shortlist ranks 3, 4, 7, 9, 10, 12, 15), runs on rule based logic and classical statistics over a PIR, door contact, and bed mat mesh. Zero neural inference. HIGH.
2. The only ML in the sensing layer is pose estimation for gait, sit to stand, and hazard inventory (3.1) and the fall classifier (gated by duration, 3.1.3). Everything else is a state machine. This keeps the compute envelope small and the failure modes debuggable, and it means most of the product is not exposed to model drift or dataset license risk at all. HIGH.
3. Engineering effort here is integration and tuning of an event pipeline (a home state model, a rules engine, a per resident baseline store), not model development. This is weeks of backend work, not a research program. MEDIUM.

---

## 3.3 Scene Memory and Object Location ("where is my phone")

Phase 0 classed object location memory (feature 12) as LATER and identified it as the single largest compute driver in the system. Phase 4 specifies the stack and confirms the verdict.

### 3.3.1 What it actually requires

| Component | What it is | Open option and license | Model / storage / compute |
|---|---|---|---|
| Persistent room map | A spatial map of the home with named zones | SLAM or a manual onboarding room layout; no heavy model needed for a fixed camera set | Small; a static map per home |
| Room naming (onboarding) | Human labels rooms once | UI plus the assistant; trivial | Negligible |
| Open vocabulary object detection | Detect arbitrary household objects (phone, keys, glasses, remote, wallet) by name, not a fixed class list | Grounding DINO `Apache-2.0` [S39]; OWL-ViT `Apache-2.0` [S38]; Detic `Apache-2.0` code [S40]; YOLO-World `GPL-3.0` (avoid) [S41] | A detector plus a text encoder; hundreds of MB to a few GB in memory; GPU or a strong NPU |
| Temporal object store | Last known location per tracked object over time | A time indexed database (SQLite/Postgres plus a small vector store); build | Grows with object vocabulary and home size; modest storage, continuous write |
| Retrieval interface | Resolve a free form query to the store | The assistant LLM over the store (VLM optional) | Reuses the assistant layer (3.4) |

### 3.3.2 License trap in the detectors

The open vocabulary detector is where a license mistake hides. YOLO-World is `GPL-3.0` [S41], the same copyleft failure mode as the AGPL pose trap: it forces source disclosure of derivatives. The clean choices are Grounding DINO and OWL-ViT, both `Apache-2.0`. Detic code is `Apache-2.0` but some Detic weights are trained on ImageNet-21K and inherit that dataset's non commercial research restriction, so the weights must be selected carefully even though the code is clean [S40]. This is exactly the code versus weights split framework section 9 warns about. HIGH.

### 3.3.3 Compute, storage, topology, and the v1 decision

| Question | Answer |
|---|---|
| Model class | Open vocabulary detector (Grounding DINO / OWL-ViT class) plus a language model for retrieval; optionally a VLM to resolve ambiguous references |
| Memory pressure | The detector plus text encoder does not fit a low cost camera SoC. Consistent with Phase 0: an 8 bit VLM wants the 16GB Orin NX class as the practical floor |
| Which topology (Phase 2.3) does it force | It forces T2 (in home hub) or T4 cloud on derived features. It cannot run on the T1 camera node. This adds a hub (Jetson Orin NX 16GB class, est $300 to $700) to the BOM the moment it enters v1 [S20] |
| Storage | Modest (a time indexed object store per home), continuous small writes |
| Does it belong in v1 | NO |

Verdict: scene memory does NOT belong in v1. It is the single largest compute driver, it forces a hub into the BOM that v1 otherwise avoids, it carries the most claim sensitive byproduct in the catalog (object misplacement frequency as a cognitive signal, which Phase 1 marks research only, do not output), and its clinical value is low relative to its cost. Its consumer appeal is real but it is a convenience feature, not a safety feature. Defer to v2, where a hub may be justified by other features. This confirms the Phase 0 classification and founder assumption A2 (compute happens on the camera) is wrong for this feature. HIGH.

---

## 3.4 The Assistant Layer

Inherits the LLM decision in `shared/shared_llm_layer.md`: a hybrid, sensitivity routed layer, a quantized 4B edge model (`Qwen3-4B` Apache-2.0 or `Phi-4-mini` MIT) for routine narration and anything touching raw context, and a small to mid cloud tier (Claude Haiku 4.5 or Sonnet 5 for safety aligned output) for RAG grounded education and safety escalation phrasing, at roughly under $1 per resident per month at medium volume. Concept specific components below.

### 3.4.1 Wake word

| Option | License (from source) | Commercial | Note | Confidence |
|---|---|---|---|---|
| openWakeWord | Code `Apache-2.0`; pre trained models `CC-BY-NC-SA-4.0` (non commercial) [S42] | Code yes; bundled models NO | Must train custom wake word models for commercial shipment (the framework and tooling are free); do not ship the bundled models | HIGH |
| Picovoice Porcupine | Repo `Apache-2.0`, but optimizer output and custom keywords require a paid Picovoice agreement [S43] | Paid for production custom wake words | Commercial engine with an open shell; predictable licensing, paid | HIGH |

Recommendation: openWakeWord framework (`Apache-2.0`) with a custom trained wake model, or Porcupine if a supported commercial SLA is preferred. Either way the wake word runs on device, always local, no audio retained. MEDIUM.

### 3.4.2 On device vs cloud speech to text

| Engine | License (from LICENSE file) | Commercial | Runtime | Latency | Note | Confidence |
|---|---|---|---|---|---|---|
| whisper.cpp | `MIT` [S44 via shared] | YES | CPU / Metal / CUDA / Vulkan; ARM and Raspberry Pi | approx 0.5 to 2 s behind live speech | The cross platform embedded choice; runs the OpenAI Whisper weights (also `MIT`) with no Python | HIGH |
| Vosk | `Apache-2.0` [S45] | YES | Kaldi based; CPU, Raspberry Pi, mobile, embedded | Very low, streaming | Lighter and lower latency than Whisper, less accurate on accented/noisy speech | HIGH |
| Moonshine | Code `MIT`; English models `MIT`; non English models Moonshine Community License (non commercial under $1M rev) [S46] | English YES; non English gated | Python, iOS, Android, Pi, MCU, DSP, wearables | Very low, streaming, optimized for live | Highest accuracy per size at the top end; English models fully commercial | HIGH |

Recommendation: on device STT, not cloud. The resident's speech is raw in home audio, the most consent heavy stream in the system (Phase 2 acoustic finding, two party consent exposure). Keeping STT local removes the audio egress question entirely, matching `shared_llm_layer.md` section 6 and the Phase 2 rule that the microphone survives only as a local wake plus on device transcription path with no retained audio. Moonshine (English, `MIT`) or whisper.cpp (`MIT`) for accuracy; Vosk (`Apache-2.0`) if latency and footprint dominate. HIGH.

### 3.4.3 Latency and cost per resident per month

Carried from `shared_llm_layer.md`: interactive chat needs sub 2 s first token; an edge 4B model meets first token but is slow on long throughput (12 to 20 s for 100 tokens on ARM class), so long answers stream from the cloud tier. Cost per resident per month at medium volume (150 interactions) is approx $0.04 (GPT-5 Nano) to $0.64 (Claude Haiku 4.5), dropping toward approx $1.30 to $1.60 for Haiku at high volume with caching and batch, and approximately $0 marginal for the edge path (capitalized in the BOM, not metered). Sub $1 per resident per month is readily achievable. HIGH (Claude pricing primary), MEDIUM (edge throughput, generic benchmarks).

### 3.4.4 The safety, escalation, and refusal envelope (must survive wellness positioning)

The assistant talks to an older adult who may be lonely, confused, or in distress. This is the highest liability surface in the software. The envelope is defined to hold inside the general wellness lane (framework section 2): the product surfaces patterns and events to a human, it does not diagnose or treat.

| Resident utterance class | Required assistant behavior | Why it survives wellness positioning |
|---|---|---|
| Explicit medical emergency ("I fell", "I can't breathe", "chest pain", "help") | Deterministic hard coded escalation. Trigger the same event and escalation path as a detected fall (contact tree, then emergency services per policy). Do NOT let the LLM improvise the decision | This is event detection and escalation, which framework section 2 places inside the lane (Apple Watch precedent). It is not diagnosis |
| Distress or self harm language | Deterministic escalation to a human contact plus surfacing of crisis resources from a vetted, hard coded resource list | Routing a person to a human is not a clinical claim |
| Request for medical advice, diagnosis, dose change ("should I take more of my pill", "do I have an infection") | REFUSE the clinical judgment. Do not diagnose, do not alter treatment. Log the question, offer to notify the caregiver or clinician, provide general education only from the RAG corpus | Refusing diagnosis and treatment is exactly what keeps the product a wellness device. Dose guidance is out (Phase 0 claims matrix) |
| Health education / normalization | Answer only from the vetted RAG corpus, never from parametric memory | FTC substantiation (framework section 2) requires a citable source; RAG converts it to a content licensing line, not a model gamble |
| Affective / loneliness ("I feel so alone") | Reflect, store as self report, trend, and surface to the caregiver if a threshold is crossed. Empathetic, non clinical | Self report is not a claim; a mood journal is a ubiquitous consumer feature (Phase 0) |
| Routine chit chat, reminders | Handle on device; medication reminders and adherence logging only, never dose guidance | Reminders and logging are inside the lane |

Rules that make the envelope auditable and safe:

1. The emergency and escalation decision is a hard coded template and rule, never generative. `shared_llm_layer.md` section 4 requires safety critical escalation phrasing to be deterministic and auditable, not model improvisation. The LLM may phrase the reassurance to the resident, but the decision to escalate is code. HIGH.
2. Refusal is a first class behavior. The assistant must refuse to diagnose, to interpret a symptom clinically, and to change a medication. This refusal is not a product weakness; it is the mechanism that keeps the product a general wellness device rather than software as a medical device. HIGH.
3. Offline resilience. The safety path (detected fall, "help") must function with no network, on the local node, per Phase 2 (T1 fall path is offline capable) and `shared_privacy_security`. A cloud dependent escalation is unacceptable. HIGH.
4. No audio retention. Wake word and STT are local; the assistant works on transcribed text and derived features, never retained raw audio, per 3.4.2. HIGH.

---

## 3.5 Caregiver Application

Mobile and web. Notification delivery, an escalation ladder, an emergency contact tree, and the load bearing liability decision: does the system ever call emergency services directly.

### 3.5.1 What existing PERS providers actually do

| Practice | Finding | Source |
|---|---|---|
| Who dispatches | The signal goes to a professional monitoring center. A trained operator speaks to the resident, works a list of emergency caregiver contacts, and connects 911 only if a contact cannot be reached or the situation is life threatening. 911 is generally not the first action | [S47] |
| Direct to 911 without a human in the loop | Standard PERS deliberately routes through a trained operator first, precisely to filter false alarms before emergency services are dispatched | [S47] |
| Apple Watch (the exception) | Auto calls emergency services after approx one minute of detected immobility following a hard fall, then messages emergency contacts. No human operator in the loop | [S48] |
| Liability posture in the ToS | Broad limitation of liability. Providers disclaim liability for loss or injury "regardless of whether caused by negligent performance", and cap total liability at a fixed sum (a representative cap is $2,500) | [S47] |

### 3.5.2 Escalation ladder and the 911 decision for this product

Recommended v1 design, consistent with Phase 1 alert copy and Phase 5 (escalation policy is owned there):

1. Event detected (fall plus long lie, or resident says "help"). Node fires locally.
2. Tier 1: push alert to the primary caregiver with Call, Call 911, and "I am handling it" actions (Phase 1 alert copy). Interrupts.
3. Tier 2: if unacknowledged within a set window and the person remains down, escalate to the next contact in the tree.
4. Tier 3: if the contact tree is exhausted and the person remains down, escalate to emergency services via a bought professional monitoring center (the PERS pattern), not a homegrown 911 auto dialer.

The 911 decision, stated as a recommendation with its rationale:

| Option | Liability exposure | Recommendation |
|---|---|---|
| System auto dials 911 directly (Apple Watch style) | High. The company becomes the decision maker on emergency dispatch, owns false dispatch cost and duty of care, and is exposed for missed and delayed calls | Do NOT build this in house for v1 |
| System escalates to a bought PERS monitoring center that dispatches | Contained. The monitoring center carries the trained operator, the dispatch relationship, and the established liability framework (with its caps and disclaimers) | RECOMMENDED. Buy the monitoring, do not build a 24/7 call center (Phase 7 partner note) |
| System notifies contacts only, never escalates to services | Low technical liability but a product and ethical gap for the long lie scenario | Insufficient alone for a safety product |

Rationale: do not build a 24/7 call center and do not become the entity that decides to dispatch emergency services. Partner with an existing PERS monitoring provider, inherit their operator workflow and their liability framework, and keep the product's own escalation to notification plus handoff. The company's ToS must carry the same class of limitation of liability and disclaimer the incumbent PERS providers use [S47], drafted in Phase 5 and Phase 8. Whether the product ever auto dials 911 with no human is a policy decision with direct liability consequences and is deferred to Phase 5 with this phase's strong recommendation against an in house auto dialer. HIGH.

---

## 3.6 Build versus Buy, per Subsystem

Every subsystem. OSS option with exact license, commercial option, cost, gap, and engineering weeks to close the gap. Weeks are engineering estimates at the loaded San Diego rate assumption carried from the framework; they are effort to integrate and harden, not to invent. Confidence MEDIUM on week counts (they are estimates), HIGH on the buy versus build direction.

| Subsystem | OSS option (SPDX license) | Commercial option | Approx cost | Gap to close | Eng weeks | Direction |
|---|---|---|---|---|---|---|
| Pose estimation | MoveNet `Apache-2.0`; RTMPose `Apache-2.0` | Ultralytics Enterprise (approx $5k/yr+) [S31]; NVIDIA TAO (silicon lock) | OSS free | Port to edge silicon (IMX500/Hailo), tune for oblique view | 4 to 8 | BUILD on OSS (MoveNet/RTMPose) |
| Fall + long lie detection | Pose plus a duration gated classifier on OSS pose; radar vendor SDK | Vayyar Care node (approx $250 + $20/mo) [S4] | OSS free; Vayyar recurring | Achieve acceptable real world FP rate; fuse camera + radar | 10 to 20 | BUILD detection, BUY radar node |
| Gait metric extraction | Pose keypoints + calibration; OpenCap as reference | none needed | OSS free | Single node accuracy to 0.04 m/s floor; bench validate | 6 to 12 | BUILD on OSS |
| ADL / occupancy / transitions | Rules engine over PIR/door events (no ML); Home Assistant class stack (`Apache-2.0`) | Any Zigbee hub SDK | OSS free | Home state model, per resident baseline, anomaly thresholds | 6 to 10 | BUILD (mostly not ML) |
| Circadian IS/IV/RA | Nonparametric actigraphy formulas (open, `pyActigraphy` MIT class) | none | OSS free | Adapt actigraphy math to a PIR/activity stream; validate transfer | 3 to 5 | BUILD on OSS |
| Scene memory / object location (LATER) | Grounding DINO `Apache-2.0` / OWL-ViT `Apache-2.0`; avoid YOLO-World `GPL-3.0` | Cloud detection APIs | OSS free; hub adds $300 to $700 | Persistent map, temporal store, retrieval, VLM; forces a hub | 16 to 30+ | DEFER to v2 |
| Wake word | openWakeWord code `Apache-2.0` (models `CC-BY-NC-SA`, retrain) | Porcupine (paid custom) | OSS free + training | Train a custom commercial wake model | 2 to 4 | BUILD on OSS or BUY Porcupine |
| Speech to text (on device) | whisper.cpp `MIT`; Vosk `Apache-2.0`; Moonshine `MIT` (English) | Cloud STT (rejected on privacy) | OSS free | Integrate on device, tune for older adult speech, noise | 3 to 6 | BUILD on OSS, on device |
| Assistant LLM | Qwen3-4B `Apache-2.0` / Phi-4-mini `MIT` (edge) | Claude Haiku/Sonnet API (cloud) | approx <$1/resident/mo (see 3.4.3) | Hybrid routing, safety envelope, RAG corpus | 8 to 16 | BUY API + BUILD edge (hybrid) |
| Safety / escalation logic | none (must be bespoke, hard coded) | none | build | Deterministic escalation state machine, auditable | 4 to 8 | BUILD (bespoke, safety critical) |
| RAG health content corpus | none clean | Licensed medical content | UNKNOWN (content license) | Source, license, and vet a substantiable corpus (framework §2) | UNKNOWN | BUY content, BUILD retrieval |
| Emergency monitoring / dispatch | none (do not build) | PERS monitoring center (per seat/mo) | per contract | Integration, SLA, liability framework | 4 to 8 (integration) | BUY (do not build a call center) |
| Caregiver mobile + web app | Standard app frameworks (React Native, Flutter, permissive) | none | OSS free | Notification, escalation UI, contact tree, report rendering | 12 to 24 | BUILD on OSS frameworks |

Cross cutting build versus buy findings.

1. Almost every perception subsystem has a clean `Apache-2.0` or `MIT` OSS option that runs on non NVIDIA silicon. The two traps to route around are AGPL (Ultralytics YOLO Pose) and GPL/non commercial (YOLO-World, OpenPose, openWakeWord bundled models, Detic ImageNet-21K weights). None of these is necessary; a clean substitute exists for each. HIGH.
2. The correct buys are the radar node (Vayyar or a TI/Infineon build), the assistant cloud API for the few turns that need frontier reasoning, the RAG health content, and the PERS emergency monitoring. Everything else is integration of permissively licensed OSS. HIGH.
3. The single largest deferrable cost is scene memory. Deferring it to v2 keeps the hub out of the v1 BOM and removes 16 to 30+ engineering weeks from the v1 critical path. HIGH.
4. The bespoke, safety critical, cannot buy items are the fall duration gating logic and the escalation state machine. These are where engineering rigor, not model selection, decides whether the product is safe and whether it survives the "unplugged in month two" false positive test. HIGH.

---

## Register Entries

### oss (for `oss.md`) — exact SPDX license and commercial-use flag

| Name | Source | SPDX license (from LICENSE file) | Commercial use | Runtime / hardware | Does | Does not | Confidence |
|---|---|---|---|---|---|---|---|
| MoveNet | Google (TF Hub / Kaggle) [S30] | `Apache-2.0` | YES, unrestricted | TFLite/ONNX; any silicon incl. IMX500/Hailo/Rockchip | Fast single person pose, edge | Multi person crowd, 3D | HIGH |
| MediaPipe BlazePose | Google [S26] | `Apache-2.0` | YES, unrestricted | TFLite/MediaPipe; mobile/edge | 33 3D landmarks on device | Heavy multi person | HIGH |
| RTMPose / RTMO (MMPose) | OpenMMLab [S27] | `Apache-2.0` | YES, unrestricted | ONNX/TensorRT/ncnn/OpenVINO; any silicon | SOTA accuracy per compute, real time | n/a | HIGH |
| ViTPose | ViTAE-Transformer [S28] | `Apache-2.0` | YES, unrestricted | PyTorch/ONNX; GPU leaning | Highest accuracy class | Cheap edge | HIGH |
| YOLO-Pose (YOLOv8/11-pose) | Ultralytics [S25] | `AGPL-3.0` | NO without paid Enterprise License | ONNX/TensorRT/TFLite; any silicon | Strong pose + detect | Closed source use without paying | HIGH |
| OpenPose | CMU [S29] | Custom CMU non commercial | NO, prohibited (separate CMU license required) | CUDA leaning | Multi person 2D pose | Any commercial use | HIGH |
| NVIDIA BodyPoseNet / BodyPose3DNet / TRTPose | NVIDIA [S33][S34] | NVIDIA model/NGC license | YES (model), but runtime is NVIDIA only | TensorRT/DeepStream; Jetson/NVIDIA GPU ONLY | Commercial pose on NVIDIA | Run off NVIDIA silicon | HIGH |
| Grounding DINO | IDEA-Research [S39] | `Apache-2.0` | YES | PyTorch/ONNX; GPU/strong NPU | Open vocabulary detection | Edge on a camera SoC | HIGH |
| OWL-ViT | Google Research [S38] | `Apache-2.0` | YES | HF/Scenic; GPU | Open vocabulary detection | Edge | HIGH |
| Detic | Meta [S40] | Code `Apache-2.0`; some weights inherit ImageNet-21K non commercial | Code YES; check weights | GPU | Large vocabulary detection | Ship ImageNet-21K weights commercially | HIGH code / MEDIUM weights |
| YOLO-World | Tencent AILab [S41] | `GPL-3.0` | NO in closed source (copyleft) | ONNX; edge capable | Real time open vocab detection | Proprietary product without source disclosure | HIGH |
| OpenCap | Stanford [S24b] | `Apache-2.0` class (open source) | YES | 2 cameras + cloud | Reference biomech/gait validation | Single node edge runtime | MEDIUM |
| openWakeWord | dscripka [S42] | Code `Apache-2.0`; bundled models `CC-BY-NC-SA-4.0` | Code YES; models NO (retrain) | On device | Wake word framework | Ship bundled models commercially | HIGH |
| Picovoice Porcupine | Picovoice [S43] | Repo `Apache-2.0`; production custom keywords paid | Paid for production | On device | Enterprise wake word | Free custom production keywords | HIGH |
| whisper.cpp (+ Whisper weights) | ggml-org / OpenAI [shared] | `MIT` | YES | CPU/Metal/CUDA/Vulkan; ARM/Pi | On device STT | Real time on tiny MCU | HIGH |
| Vosk | Alphacephei [S45] | `Apache-2.0` | YES | Kaldi; CPU/Pi/mobile/embedded | Low latency streaming STT | High accuracy on noisy/accented | HIGH |
| Moonshine | Moonshine AI [S46] | Code `MIT`; English models `MIT`; non English Community License (non comm <$1M) | English YES; non English gated | Python/iOS/Android/Pi/MCU | Low latency STT | Non English commercial without registration | HIGH |
| Qwen3-4B (edge assistant) | Alibaba [shared] | `Apache-2.0` | YES | llama.cpp/Ollama; ~3 GB Q4 | Edge narration/chat | Frontier reasoning | MEDIUM (license from search) |
| Phi-4-mini (edge assistant) | Microsoft [shared] | `MIT` | YES | llama.cpp/Ollama; ~3 GB Q4 | Best small reasoner @8 GB | Vision | MEDIUM |

### papers (for `papers.md`)

| Key | Citation | What it establishes | Design / n | Effect / error | Gold standard | Supports | Status |
|---|---|---|---|---|---|---|---|
| P17 (carried) | Bagalà F et al., PLoS One 2012;7(5):e37062, plus long term false alarm studies | Lab fall accuracy collapses on real falls; false alarms are the failure mode | 13 algorithms on real falls | Real world sens approx 57% vs approx 94% lab; 3 to 85 false alarms/day in some settings | Annotated real falls | Fall detection real world FP | Robust, cross study |
| P3a/P3b (carried) | Sensors 2020;20(1):125; Sci Rep 2024 s41598-024-68402-x | Camera gait speed valid vs walkway from oblique view | 44 adults 65+; validation cohort | Speed RMSE 0.04 m/s; ICC 0.81 to 0.98; cadence 2.3 steps/min; stride 0.05 to 0.08 m | GAITRite / pressure walkway | Gait speed from pose | Recent, single studies |
| P19 (carried) | mmWave in home gait (PMC10891707, PMC9784666) | Radar gait speed/step length match walkway | In home cohorts | Step length error 4.5 cm / 8.3%, ICC 0.91; speed error approx 0.02 m/s | Zeno Walkway | Radar gait fallback | HIGH |
| NEW: OpenCap validation | Validation of OpenCap, J Biomech 2024/2025 (S0021929024002781; arXiv 2409.03766) [S24b] | Markerless joint kinematics error above clinical threshold | Healthy + pathological gait cohorts | Overall RMSE approx 5.8 deg, peak up to 11.3 deg; 3.2 to 16.4 deg range; worse pathological | Marker based mocap | Joint kinematics NOT v1 grade | HIGH |
| NEW: wearable real world FP | Real World Accuracy and Use of a Wearable Fall Detection Device, PMC4662041 [S35] | Real deployment false alarm dominance | Older adults, field | 84 alarms, 83 false; 42% during normal use | Observed | Fall FP failure mode | HIGH |
| NEW: long term fall sensor FP | Sensitivity and False Alarm Rate of a Fall Sensor, PubMed 25138139 [S36] | Real world sensitivity and FP rate | Long term elderly | Sens 80% (12/15); 0.049 to 0.025 false alarms/hr | Observed real falls | Fall FP quantification | HIGH |

### sources (for `sources.md`)

| Key | Source | URL | Date | Used for | Credibility |
|---|---|---|---|---|---|
| S25 | Ultralytics LICENSE (AGPL-3.0) | https://github.com/ultralytics/ultralytics/blob/main/LICENSE | 2026-07-10 | YOLO-Pose AGPL-3.0, commercial requires Enterprise | HIGH (primary license file) |
| S26 | MediaPipe LICENSE (Apache-2.0) | https://github.com/google-ai-edge/mediapipe/blob/master/LICENSE | 2026-07-10 | BlazePose Apache-2.0 | HIGH (primary) |
| S27 | MMPose LICENSE (Apache-2.0) | https://github.com/open-mmlab/mmpose/blob/main/LICENSE | 2026-07-10 | RTMPose/RTMO Apache-2.0 | HIGH (primary) |
| S28 | ViTPose LICENSE (Apache-2.0) | https://github.com/ViTAE-Transformer/ViTPose/blob/main/LICENSE | 2026-07-10 | ViTPose Apache-2.0 | HIGH (primary) |
| S29 | OpenPose LICENSE (CMU non commercial) | https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/LICENSE | 2026-07-10 | OpenPose non commercial only | HIGH (primary) |
| S30 | MoveNet model card / license | https://www.kaggle.com/models/google/movenet ; https://www.tensorflow.org/hub/tutorials/movenet | 2026-07-10 | MoveNet Apache-2.0, commercial | HIGH |
| S31 | Ultralytics Enterprise License + pricing discussion | https://www.ultralytics.com/license ; https://github.com/orgs/ultralytics/discussions/7440 | 2026-07-10 | AGPL vs paid Enterprise, approx $5k/yr sole dev report | MEDIUM (page 403; pricing from community) |
| S32 | NVIDIA DeepStream + TAO deployment docs | https://docs.nvidia.com/tao/tao-toolkit/text/ds_tao/deepstream_tao_integration.html | 2026-07-10 | TAO models deploy via TensorRT/DeepStream on NVIDIA only | HIGH (vendor) |
| S33 | NVIDIA BodyPoseNet NGC + docs | https://catalog.ngc.nvidia.com/orgs/nvidia/teams/tao/models/bodyposenet ; https://docs.nvidia.com/tao/archive/5.3.0/text/bodypose_estimation/bodyposenet.html | 2026-07-10 | NVIDIA pose commercial ready, Jetson/GPU target | HIGH (vendor) |
| S34 | NVIDIA TAO commercial licensing forum + PeopleNet | https://forums.developer.nvidia.com/t/understanding-tao-models-commercial-licensing/281977 | 2026-07-10 | TAO models commercial use readiness | MEDIUM (vendor forum) |
| S35 | Real World Accuracy of a Wearable Fall Detection Device | https://pmc.ncbi.nlm.nih.gov/articles/PMC4662041/ | 2026-07-10 | 83 of 84 alarms false in real deployment | HIGH |
| S36 | Sensitivity and False Alarm Rate of a Fall Sensor, long term elderly | https://pubmed.ncbi.nlm.nih.gov/25138139/ | 2026-07-10 | Real world sens 80%, 0.049 to 0.025 false/hr | HIGH |
| S37 | Fall detection surveys + TaFall + lightweight AI real time | https://pmc.ncbi.nlm.nih.gov/articles/PMC7805655/ ; https://arxiv.org/pdf/2604.09693 ; https://link.springer.com/article/10.1007/s00607-026-01651-y | 2026-07-10 | RGB higher FP; 2% FP → dozens/day; thermal TaFall 0.00126% (lab); multi stage confirmation | MEDIUM to HIGH |
| S24b | OpenCap validation studies | https://www.sciencedirect.com/science/article/abs/pii/S0021929024002781 ; https://arxiv.org/pdf/2409.03766v2 ; https://www.mdpi.com/2673-7078/5/4/88 | 2026-07-10 | Markerless kinematics RMSE 5.8 deg (peak 11.3), above clinical threshold | HIGH |
| S38 | OWL-ViT license (Apache-2.0) | https://github.com/google-research/scenic ; HF google/owlvit-base | 2026-07-10 | Open vocab detector Apache-2.0 | MEDIUM to HIGH |
| S39 | Grounding DINO LICENSE (Apache-2.0) | https://github.com/IDEA-Research/GroundingDINO/blob/main/LICENSE | 2026-07-10 | Grounding DINO Apache-2.0 | HIGH (primary) |
| S40 | Detic LICENSE (Apache-2.0) + weight caveat | https://github.com/facebookresearch/Detic/blob/main/LICENSE | 2026-07-10 | Code Apache-2.0; ImageNet-21K weights non commercial caveat | HIGH code / MEDIUM weights |
| S41 | YOLO-World LICENSE (GPL-3.0) | https://github.com/AILab-CVC/YOLO-World/blob/master/LICENSE | 2026-07-10 | Open vocab detector GPL-3.0, copyleft | HIGH (primary) |
| S42 | openWakeWord LICENSE + README | https://github.com/dscripka/openWakeWord/blob/main/LICENSE | 2026-07-10 | Code Apache-2.0; bundled models CC-BY-NC-SA-4.0 | HIGH (primary) |
| S43 | Picovoice Porcupine license | https://github.com/Picovoice/porcupine ; https://picovoice.ai/products/voice/wake-word/ | 2026-07-10 | Repo Apache-2.0; production custom keywords paid | HIGH |
| S44 | whisper.cpp license (MIT) | https://github.com/ggml-org/whisper.cpp | 2026-07-10 | On device STT MIT | HIGH |
| S45 | Vosk COPYING (Apache-2.0) | https://github.com/alphacep/vosk-api/blob/master/COPYING | 2026-07-10 | Vosk Apache-2.0 | HIGH (primary) |
| S46 | Moonshine LICENSE (MIT + Community) | https://github.com/moonshine-ai/moonshine/blob/main/LICENSE | 2026-07-10 | Code/English MIT; non English Community License | HIGH (primary) |
| S47 | PERS monitoring + escalation + liability practice | https://www.medicalcarealert.com/monitoring-agreement/ ; https://www.cbsnews.com/news/how-medical-alert-systems-work/ ; https://en.wikipedia.org/wiki/Medical_alarm | 2026-07-10 | Operator dispatch, contacts before 911, liability cap approx $2,500, broad disclaimer | HIGH |
| S48 | Apple Watch fall detection escalation | https://support.apple.com/en-us/108896 | 2026-07-10 | Auto 911 after approx 1 min immobility, then messages contacts | HIGH (vendor primary) |

---

## Open Questions

1. Real world false positive rate per fall modality is UNKNOWN (carried from Phase 2 Open Question 2). Vendors publish marketing multipliers, not sensitivity/specificity. Vision RGB fall FP is documented as high [S37][P17]; radar FP is unpublished. This is the make or break number and must be characterized at G2. HIGH impact.
2. Whether a single low cost oblique camera node hits the 0.04 m/s gait speed error floor is UNKNOWN (carried from Phase 1/2). Published 0.04 m/s is research grade markerless capture; OpenCap joint kinematics show error rises on cheaper/pathological cases [S24b]. Bench test at G1. If it fails, gait weakens to a coarse trend and radar fallback A2 gains. MEDIUM impact.
3. Ultralytics Enterprise License pricing is not published; the approx $5k/yr sole developer figure is a community report [S31] and the `ultralytics.com/license` page returned 403. Since the recommendation is to avoid AGPL entirely by using MoveNet/RTMPose, this is not on the critical path, but the exact number is UNKNOWN if the founder insists on YOLO Pose.
4. Detic model weight licensing (ImageNet-21K non commercial inheritance) needs a per checkpoint read before any commercial use [S40]. Only relevant if scene memory enters v1, which is not recommended.
5. RAG health content corpus for FTC substantiable education is unscoped (carried from `shared_llm_layer.md`): source, license cost, and update cadence are UNKNOWN and are a real line item.
6. Exact PERS monitoring partner terms, per seat pricing, and integration API are UNKNOWN pending Phase 7 vendor conversations. The decision to buy (not build) monitoring is HIGH confidence; the price is not yet known.
7. Whether the product ever auto dials 911 with no human in the loop is a policy and liability decision deferred to Phase 5. This phase recommends against an in house auto dialer and for PERS handoff, but the final call has legal consequences owned by Phase 5 and Phase 8.

## Assumptions Made

1. Licenses were read from the LICENSE file for Ultralytics, OpenPose, MediaPipe, MMPose, ViTPose, Grounding DINO, Detic, YOLO-World, Vosk, Moonshine, and openWakeWord (primary). MoveNet and OWL-ViT licenses are from model cards and repository metadata, not a fetched LICENSE file (MEDIUM to HIGH). Qwen3 and Phi-4-mini licenses are carried from `shared_llm_layer.md`, where direct license file reads were blocked (open item in that file).
2. Engineering week estimates in 3.6 are integration and hardening estimates at the framework's loaded rate, not build from scratch. They are MEDIUM confidence and are inputs to Phase 6, not final.
3. The safety envelope (3.4.4) assumes the deterministic hard coded escalation path and the refusal behavior are sufficient to keep the assistant inside the general wellness lane. This is consistent with framework section 2 and `shared_llm_layer.md`, but the final claims review is owned by Phase 5 and the precedent dossier.
4. The recommendation to buy PERS monitoring rather than build a call center assumes a monitoring partner will integrate with a third party device, consistent with the Phase 7 partner note. Confidence MEDIUM on availability, HIGH on the direction.
5. Scene memory is treated as LATER (Phase 0). If the founder insists it enters v1, the hub cost (Jetson Orin NX 16GB class, est $300 to $700) and 16 to 30+ engineering weeks re enter the v1 plan, and the "no hub in v1" BOM assumption from Phase 2 breaks.
6. Fall detection is assumed to require duration gating plus modality confirmation to reach an acceptable FP rate. This is a design assumption grounded in the FP literature [S35][S36][S37][P17], not a measured result on this product.

## Confidence Summary

Overall confidence: HIGH on the license findings and the build versus buy direction, MEDIUM on the engineering week estimates and the not yet measured false positive and single node gait accuracy numbers.

- HIGHEST confidence, from primary license files: OpenPose is non commercial and unusable as shipped; Ultralytics YOLO Pose is AGPL-3.0 and requires a paid Enterprise License for a closed source product; MediaPipe BlazePose, RTMPose/RTMO, ViTPose, MoveNet, Grounding DINO, Vosk, and Moonshine (English) are clean and commercially usable; YOLO-World is GPL-3.0 and openWakeWord bundled models are CC-BY-NC-SA (retrain required). These were read from the LICENSE file.
- HIGH confidence: NVIDIA is not required for pose and its stack (TensorRT/DeepStream) locks the compute node to Jetson class silicon, contradicting the Phase 2/3 IMX500 direction. Founder assumption A6 is disproven. The recommended pose backbone is MoveNet or RTMPose (`Apache-2.0`) on non NVIDIA edge silicon.
- HIGH confidence: fall detection real world false positive rate, not benchmark sensitivity, is the feature's make or break, and the fix is duration gated long lie plus modality confirmation, not a better single classifier. The ADL/pattern layer is deterministic rules and classical statistics, not machine learning. Scene memory forces a hub, is the largest compute driver, and does not belong in v1.
- HIGH confidence: existing PERS providers route through a trained operator that tries contacts before 911 and carry broad liability disclaimers with low caps; the product should escalate to a bought monitoring partner and must not build an in house 911 auto dialer or a 24/7 call center.
- WEAKEST elements, carried as Open Questions: per modality real world fall FP rate (UNKNOWN, vendor accuracy not public), single low cost node gait accuracy (UNVALIDATED), the RAG content corpus (unscoped), and PERS partner pricing (UNKNOWN). None weakens the central conclusion: clean `Apache-2.0`/`MIT` OSS covers almost every subsystem, NVIDIA is optional and locks silicon, and the two hard build items are the fall duration gating and the escalation state machine.


===================================================================
# (phase5_privacy.md)
===================================================================

# Concept A, Phase 5: Data, Privacy, and Security Architecture

Governed by `00_framework.md` (sections 2, 5, 6, 8, 9) and `01_concept_a_elder_monitoring.md` (Phase 5). Inherits `research/shared/shared_privacy_security.md` in full and does not repeat it. This phase does concept specific work only, against the architecture selected in `research/a/phase2_architecture.md`: primary A1, a distributed mesh (PIR and door contact mesh in every zone, an under mattress BCG mat in the bedroom, a 60 GHz radar node in the bathroom and optionally the bedroom, and one oblique mains powered camera node in a shared living area running on node inference), compute topology T4 hybrid with a T1 local fall path. Object memory and natural language query are LATER (Phase 0), so v1 carries a mesh gateway, not an inference hub.

Inherited baselines applied without restatement: encryption floor AES 256 at rest and TLS 1.3 in transit (`shared` section 1.3); edge versus cloud data minimization posture (`shared` section 2); HIPAA attaches through the channel, not the product (`shared` section 3); BIPA, CUBI, and MHMDA comparison with MHMDA as the binding constraint (`shared` section 4); all party consent wiretap regime for audio (`shared` section 4.4); the surrogate consent pattern skeleton (`shared` section 5.2); approved claim posture (`shared` section 7).

Confidence tags HIGH, MEDIUM, LOW per framework section 5. Citation keys `[S#]` resolve in Register Entries. Legal claims carry source, URL, date, and the named authority.

---

## 1. DATA FLOW: EVERY HOP, EVERY STORE, EVERY RETENTION PERIOD

The architecture has six node types plus a mesh gateway plus a cloud tier plus two application clients (resident and caregiver). The governing rule from `shared` section 2 holds throughout: raw sensitive modality (video, audio, radar point cloud, load cell waveform) is processed at the edge; only derived, non reconstructable features and events transit off the home.

### 1.1 Per node data lineage

| Node type | Raw signal captured | Processing location | What leaves the node | Where it goes next | On node store and retention | Off node store and retention |
|---|---|---|---|---|---|---|
| Camera node (oblique, living area), T1 on sensor (IMX500 class) | RGB frames | Inference inside the sensor package; pixels do not reach the application SoC | Pose keypoints, gait metrics, sit to stand timing, fall and long lie events, periodic hazard inventory labels. No frame, no image | Mesh gateway, then cloud | Rolling frame buffer inside the sensor die only, overwritten continuously, never persisted to disk. Derived metrics buffered on the node SoC less than 24 h until gateway ack | Derived metrics and events in cloud, see 1.2 |
| Radar node (bathroom, optional bedroom) | 60 GHz point cloud and range Doppler | On node classifier | Presence, fall, long lie, dwell, nocturia count, coarse gait speed, respiration and resting HR values. No point cloud raw stream | Mesh gateway, then cloud | Point cloud held in RAM only for the classification window, not persisted. Derived events buffered less than 24 h until ack | Events and vitals values in cloud |
| BCG bed mat (bedroom) | Ballistocardiography load waveform | On node or gateway feature extraction | Time in bed, bed exit, sleep fragmentation, resting HR, respiratory rate. No waveform | Mesh gateway, then cloud | Waveform in RAM only during extraction, not persisted. Nightly summary buffered until ack | Nightly summaries in cloud |
| PIR and door and window contacts | Binary motion and open close | Native, no inference | Timestamped occupancy and transition and open close events | Mesh gateway (Zigbee or Thread), then cloud | Battery node, event pushed immediately, minimal local buffer | Event stream in cloud, aggregated to life space, circadian, ADL |
| Microphone (assistant, camera node or a dedicated voice node) | Audio | On device wake word only; no audio retained until wake | After wake word: utterance transcribed. Design target is on device speech to text; if cloud STT is used, the utterance audio transits under explicit consent | Cloud assistant | No audio persisted pre wake; post wake utterance held only for the turn, not stored, unless the resident opts into transcript retention | Transcript text only, not audio, retention per 1.2 |
| Mesh gateway (home) | None of its own; aggregation and transport | Buffering, encryption, backhaul | Encrypted batch of derived events and metrics over TLS 1.3 | Cloud ingest | Encrypted local store of derived events, rolling 7 to 30 days as offline resilience buffer, then purged after cloud ack | n/a |
| Cloud assistant and trend tier | None captured; receives derived features only | LLM interpretation on stripped features; trend analytics | Caregiver report, assistant replies, notifications | Resident app, caregiver app, escalation path | n/a | See 1.2 retention schedule |

### 1.2 Cloud stores and retention schedule (product policy, design decision)

Retention is a product policy input, not a legal constant. The schedule below is set to MHMDA data minimization and the BIPA destroy on purpose completion or three year floor (`shared` section 4.1), and is a recommendation to be confirmed per launch state. Confidence MEDIUM on the exact windows, HIGH on the direction (minimize).

| Cloud store | Contents | Retention | Basis |
|---|---|---|---|
| Event log | Falls, long lie, bed exit, door events, escalations | 13 months rolling, then aggregate and purge raw events | Enables year over year trend while bounding the compellable and breachable corpus |
| Derived metric time series | Gait speed, sit to stand, nocturia count, life space, circadian indices, resting HR, respiration | 13 months rolling; downsample to weekly aggregates thereafter | MHMDA minimization; trend value preserved at coarser grain |
| Assistant transcripts (text) | Resident and caregiver dialogue turns | 30 days default, off by default for retention beyond the turn, resident opt in for longer | All party consent and MHMDA; audio never stored |
| Account and role graph | Identities, roles, capacity flags, consent grants and revocations | Life of account plus statutory tail, then delete | Consent auditability; deletion right honored |
| Backups | Encrypted snapshots of the above | Match primary retention; deletion propagates to backups within a defined window | `shared` section 6.3 deletion including backups |
| Raw video, raw audio, raw point cloud, raw waveform | None. These never reach the cloud in v1 | Not stored | The load bearing minimization claim |

Every deletion request purges primary and backup within the stated window. No raw modality is ever a cloud store row, which is the fact that makes section 2 provable and section 7 sayable.

---

## 2. PROVE OR DISPROVE: "NO VIDEO LEAVES THE DEVICE"

The claim is provable in the qualified form the shared file permits ("Raw video is processed on the device and is not sent to our servers"), and only if every code path below is affirmatively closed and audited. The absolute form ("your video never leaves your home") is not defensible, because residual paths (a crash dump, a compromised device) cannot be reduced to a mathematical zero. This matches `shared` section 7: state the enforced claim, not the absolute.

The architectural enabler is on sensor inference (Sony IMX500 class, `phase2_architecture` S16): pixels are consumed inside the sensor package and only a metadata tensor crosses to the application SoC. That removes the frame from the application processor entirely, which collapses most exfiltration paths at the hardware level rather than the policy level. This is the single most important control in the whole phase.

### 2.1 Every code path that could violate the claim, and the control that closes it

| # | Code path | How it could leak video | Control that closes it | Residual risk | Confidence |
|---|---|---|---|---|---|
| 1 | Normal inference path | App SoC reads a frame buffer to run the model | On sensor inference (IMX500 class): frames never leave the sensor die; app SoC receives only the metadata tensor. No frame buffer is exposed to application code | Near zero by construction | HIGH |
| 2 | Developer and debug builds | A debug build enables a frame dump, a live preview, or logs raw frames for tuning | Production signed image has no frame egress path compiled in; frame access is a debug only capability gated behind a hardware fuse or secure debug that is blown or disabled before shipment; separate firmware variants for lab and field | Low; depends on build hygiene and fuse discipline | MEDIUM |
| 3 | OTA update | A future signed update quietly adds a frame capture and upload capability | Signed firmware and signed OTA (section 5); a documented policy that no OTA may enable raw modality egress without a re consent event; code review gate on any camera pipeline change; reproducible builds so the shipped image is auditable | Low; this is a governance control, not a hardware one, so it is only as strong as the review process | MEDIUM |
| 4 | Crash dumps and telemetry | A core dump or diagnostic snapshot captures a frame buffer resident in RAM | With on sensor inference there is no frame in app SoC RAM to capture; additionally, crash dumps exclude any camera memory region and are scrubbed before upload; telemetry is schema allowlisted to derived fields only | Low; the IMX500 architecture removes the frame from the dumpable region | MEDIUM to HIGH |
| 5 | Remote support and live view | A support engineer requests a live camera view or a stored clip to diagnose an install | No remote video access capability is built. Support sees derived events and device health only. Any on device diagnostic image is viewable on device by the resident, never streamed off | Low; a deliberately absent feature cannot be abused, provided it is never added | HIGH |
| 6 | Local verification clip for false positive reduction | A short pre and post event clip is buffered to let a human or model confirm a fall, and that clip is uploaded | Design decision: no clip is uploaded. If a verification clip is buffered at all, it stays on device, encrypted to the secure element, auto deleted on a short timer, and is never a network payload. Preferred v1 posture: no clip buffer, radar plus pose event fusion for confirmation instead | Medium if a clip buffer is introduced; the safest build has none | MEDIUM |
| 7 | Model improvement data collection | Raw frames are harvested to retrain the detector | No raw frame collection. Model improvement uses on device metrics, synthetic data, or a separate explicit opt in program with its own consent and its own store, never the production telemetry path | Low if the no raw collection rule holds | MEDIUM |
| 8 | Physical device compromise | An attacker with the device extracts frames from memory or storage | Secure boot, encrypted storage, no persisted frames (section 5). Even a rooted device yields at most the in sensor rolling buffer, not a history | Low for history; a live compromised device is a single home exposure, not a corpus | MEDIUM |

### 2.2 Verdict

Provable, conditionally. "Raw video is processed on the device and raw video is not transmitted to our servers or our support staff" is true and defensible if and only if paths 1 through 8 are closed as specified and audited before any marketing uses the claim. The strongest single move is on sensor inference, which converts the promise from a policy assertion (path 4, 5) into a hardware property (path 1). The weakest links are the governance paths (OTA path 3, debug path 2), which no hardware can close and which require process discipline and code review as the control. The absolute unqualified claim is prohibited per `shared` section 7. Confidence HIGH on the verdict, MEDIUM on the field enforcement of the governance paths.

---

## 3. CONSENT ARCHITECTURE: THE RESIDENT IS NOT THE BUYER

This is a product design constraint and a market objection, not a compliance footnote. The resident is the data subject. The caregiver (adult child) is the buyer and the day to day user. Their interests diverge: the caregiver wants visibility, the resident may not want to be watched, and the resident may have fluctuating or diminished capacity to consent at all. A product that treats the buyer as the account owner and the resident as an object of that account is both legally exposed (covert or non consented surveillance of a competent adult) and commercially fragile (the resident unplugs it, or refuses it, which is the dominant churn and refusal mode in this category).

### 3.1 The design stance

The product implements a role and capacity model, not a single owner account. The resident is a first class principal with visibility and control, even when the caregiver pays. This is engineering work at G0 and G1, per `shared` section 5.2, restated here as a build requirement, not a policy document.

### 3.2 Four consent states the product must handle

| State | Who consents | Product behavior | Basis |
|---|---|---|---|
| Competent resident, willing | Resident, informed opt in | Full function. Resident sees what is captured and what is shared, and can pause or revoke. Visible active indicator on every sensing node | BIPA, CUBI, MHMDA consent runs to the data subject (`shared` 4); wiretap consent for audio (section 4) |
| Competent resident, unwilling or ambivalent | Resident controls scope | Resident can decline the camera and keep the mesh, decline audio, or decline sharing specific categories with the caregiver. The caregiver cannot override. Covert operation is not an available configuration | Covert monitoring of a competent adult is a distinct legal and ethical exposure (`shared` 5.2); MHMDA granular consent |
| Resident with diminished or fluctuating capacity | Resident assent plus surrogate consent | Solicit resident assent and show a visible, dignified active indicator even where legal consent flows through a surrogate. Capacity is presumed until shown otherwise and can fluctuate; the product must not assume the buyer can consent for the resident | Surrogate consent doctrine; MHMDA; ethical assent standard (`shared` 5.2) |
| Resident lacks capacity | Legally authorized representative | Consent flows through a surrogate in a defined priority order (see 3.3). The surrogate must follow the resident's known wishes and values, and absent those, the resident's best interest | State surrogate decision maker statutes (see 3.3) |

### 3.3 Who can consent for a cognitively impaired adult (the hardest case, verified)

Surrogate consent for a consumer monitoring product is not identical to clinical treatment consent, and the exact enforceable order is state specific and, for a non clinical consumer product, partly untested. The clinical and statutory hierarchy is the correct model to build to, because it is the order courts and states already recognize. Confidence MEDIUM on direct applicability to a consumer product, HIGH on the hierarchy itself.

| Priority | Surrogate | Authority | Source | Confidence |
|---|---|---|---|---|
| 1 | Agent under a health care power of attorney (durable POA for health care) | Designated in advance by the resident while competent | Arizona Rev. Stat. 36-3231 (surrogate decision makers, priorities), azleg.gov, accessed 2026-07-10; general default surrogate framework, Merck Manual "Default Surrogate Decision Making," merckmanuals.com, accessed 2026-07-10 | HIGH |
| 2 | Court appointed guardian of the person (where appointed for health decisions, may outrank the agent for its express purpose) | Court order | Illinois Health Care Surrogate Act priority order, Illinois Legal Aid Online, illinoislegalaid.org, accessed 2026-07-10 | HIGH |
| 3 | Spouse or domestic partner | Default statutory next of kin | Illinois Health Care Surrogate Act; Merck Manual default surrogate list, accessed 2026-07-10 | HIGH |
| 4 | Adult child | Default statutory next of kin | Same | HIGH |
| 5 | Parent | Default statutory next of kin | Same | HIGH |
| 6 | Adult sibling | Default statutory next of kin | Same | HIGH |

Named authorities: Arizona Rev. Stat. 36-3231 sets an explicit statutory priority (agent under health care POA first, then court appointed health care guardian, then spouse, adult child, parent, sibling). Illinois Health Care Surrogate Act sets a parallel order (guardian of the person, spouse, adult child, parent, sibling). The uniform decision standard across states: the surrogate must follow the resident's expressed wishes and known values, and where unknown, act in the resident's best interest. Sources: azleg.gov/ars/36/03231.htm (accessed 2026-07-10); illinoislegalaid.org healthcare surrogate (accessed 2026-07-10); merckmanuals.com default surrogate decision making (accessed 2026-07-10). Confidence HIGH on the hierarchy, MEDIUM on whether a consumer wellness product may rely on it directly without a clinical nexus, which is untested and belongs in the launch state legal review.

Build consequence: onboarding must capture the resident's role and capacity status and, where capacity is absent, the surrogate's authority basis (POA document, guardianship order, or attested next of kin standing in priority order), and must record which principal granted consent for what, revocably and auditable. A single "owner buys and controls everything" account is a defect, not a simplification.

### 3.4 The market objection stated plainly

The resident who does not want to be watched is not an edge case; the resident is the person the product lives or dies with. The architecture already answers this: the two private rooms have no camera (bathroom radar, bedroom mat or radar), the camera sits obliquely in one shared room with a visible active indicator, and no raw video leaves. The consent model turns that architecture into an adoption argument: the resident can see and control what is captured and shared, which is the difference between a product an older adult accepts and one an older adult unplugs. Confidence HIGH on the principle.

---

## 4. APPLICABLE LAW, APPLIED TO CONCEPT A

Inherits the full statutory analysis in `shared` section 4. Applied to this product's specific data (gait and whole body movement signatures, home activity patterns, contactless vitals, and an audio assistant) below.

### 4.1 State biometric and consumer health privacy law, applied

| Statute | Does it reach this product's data | Applied finding | Confidence |
|---|---|---|---|
| Illinois BIPA (740 ILCS 14) | Enumerated identifiers are face, voice, fingerprint, hand and iris geometry. A gait or whole body movement signature is not enumerated. A voiceprint from the assistant could be, if the product builds one | Gait likely outside BIPA's enumerated list; a voiceprint would be inside it. Do not build a voice template. Confirm gait non applicability before relying on it (`shared` Open Question 2) | MEDIUM |
| Texas CUBI (Bus. & Com. Code 503.001) | Same enumerated set as BIPA; AG only enforcement | Same as BIPA; no private right of action lowers acute litigation risk but not the compliance duty | MEDIUM |
| Washington MHMDA (RCW 19.373) | "Consumer health data" sweeps in home activity patterns, sleep, gait decline, nocturia, and any inference of health status, regardless of whether it is a biometric identifier | Binding constraint. This product's derived markers are consumer health data. Design to MHMDA opt in, separate sharing consent, minimization, and deletion, and BIPA and CUBI are cleared by margin (`shared` 4.3) | HIGH |

Net, unchanged from the shared file: MHMDA governs. The product's home activity and health inference data is squarely "consumer health data," so the whole consent and minimization architecture is built to MHMDA whether or not gait is a biometric identifier.

### 4.2 Audio triggers a separate regime: all party consent wiretap law

The assistant captures audio in a home where visitors, aides, and family members also speak. Recording a private conversation without the consent of all parties is a crime in the all party consent states. As of 2026, twelve states apply an all party (two party) consent rule: California, Connecticut, Delaware, Florida, Illinois, Maryland, Massachusetts, Montana, New Hampshire, Oregon, Pennsylvania, and Washington. Illinois is a felony; Washington is a gross misdemeanor (`shared` 4.4). Source: Recording Law, "Two Party Consent States for Recording (2026 Guide)," recordinglaw.com, accessed 2026-07-10; corroborated by worldpopulationreview.com two party consent states 2026. Confidence HIGH on the twelve state set, HIGH on Illinois and Washington penalties (primary statutes cited in `shared` 4.4).

Product consequence, restated as a build constraint: on device wake word processing with no pre wake audio retention; no ambient always on recording; post wake utterances not stored by default; explicit onboarding consent and a visible indicator; and a design that does not record a third party (an aide, a visitor) without a lawful basis. A device that silently records the household cannot lawfully operate in twelve states. This makes "no retained audio, wake word only" a national design floor, not a per state toggle. Confidence HIGH.

### 4.3 When HIPAA attaches: the channel decides

Restating `shared` section 3 applied to this product. HIPAA does not attach because the product touches health data; it attaches because of who the customer is.

| Channel | HIPAA status | BAA required | Effect on this product | Confidence |
|---|---|---|---|---|
| Direct to consumer (adult child buys for a parent) | Not a covered entity, not a business associate. HIPAA does not attach | No | FTC Health Breach Notification Rule plus MHMDA and state law govern. This is the base case | HIGH |
| Sold through or integrated by a home health agency, hospital, or health plan, handling data on their behalf | Business associate | Yes, before any PHI is exchanged | Full HIPAA Security Rule, BAA, and breach notification under 45 CFR 164.400 to 414 attach. Changes the compliance baseline entirely | HIGH |
| Reimbursed by a payer where the product performs a regulated function for the payer | Likely business associate | Yes | Same as above; analyze per deal | MEDIUM |

Strategic note carried from the concept brief and confirmed against primary sources in `shared` 3.3: a home health agency channel converts the product into a business associate and imposes the full Security Rule from day one. The DTC base case is governed by FTC HBNR (2024 amendments, effective 2024-07-29, `shared` 3.4) plus MHMDA, not by nothing. There is no unregulated state.

### 4.4 PERS emergency dispatch: liability and terms of service (concept specific, verified)

The concept escalates events to a designated contact and, in some designs, to emergency services. That escalation decision carries liability distinct from any privacy question, and it is the reason the concept brief (Phase 4 section 3.5, Phase 7 section 5) says do not build a 24 7 call center, buy it. Findings:

| Finding | Detail | Source | Confidence |
|---|---|---|---|
| A PERS provider that assumes the emergency response function assumes a duty of care | Courts have found subscribers rely on a PERS provider's representation that emergency response will be at least as good as calling 911 directly; a monitoring failure that delayed EMS created a triable duty of care question and summary judgment for the provider was denied | SDM Magazine, "Summary Judgement Denied: A Death Leads to a Cautionary PERS Saga," sdmmag.com, accessed 2026-07-10 (fetch 403 blocked; content via search extraction); Kirschenbaum & Kirschenbaum PERS legal guidance, kirschenbaumesq.com | MEDIUM |
| Monitoring failures during a live event drive the worst outcomes | A documented case: operator called 911 but did not relay that the subscriber was home alone behind locked doors and that contact was lost, delaying treatment by at least 18 minutes; the subscriber died | SDM Magazine (as above), accessed 2026-07-10 | MEDIUM |
| Limitation of liability clauses are standard and generally enforceable, but do not cover gross negligence or willful or wanton misconduct | Providers cap damages (a common cap is a nominal sum, for example $2,500), disclaim liability even for their own ordinary negligence, and require the subscriber to indemnify; under Georgia law such clauses are valid unless they purport to relieve gross negligence or willful or wanton misconduct | Medical Care Alert monitoring agreement, medicalcarealert.com (fetch 403; terms via search extraction), accessed 2026-07-10; SDM Magazine, "Limited Liability Clause Would Have Helped in Wrongful Death Lawsuit," sdmmag.com, accessed 2026-07-10 | MEDIUM |
| PERS is contractually positioned as not a substitute for 911 and not a lifesaving or medical device | Monitoring agreements state the service is not 100 percent reliable, is not a replacement for emergency services, and is not certified for emergency response | GeoArm and Medical Care Alert PERS monitoring terms, geoarm.com and medicalcarealert.com, accessed 2026-07-10 | MEDIUM |

Product consequence: the decision to call emergency services directly should sit with a licensed, insured monitoring center partner operating under its own terms of service and limitation of liability, not with the product company. This aligns the liability with the party that carries the insurance and the enforceable contract, and it keeps the product's own escalation to a notify the designated contact function plus a hard coded red flag layer (Phase 0 feature 18). The product's own terms must mirror the PERS posture: not a substitute for 911, not a medical device, not a guaranteed lifesaving system, with a limitation of liability clause that survives everything short of gross negligence. Note the tension: an automated fall alert with no human in the loop that dispatches 911 on a false positive imports the monitoring center's liability without the monitoring center's insurance, which is why the human verified partner path is preferred. Confidence MEDIUM (secondary sources; primary contract text was 403 blocked to the fetcher, same site side blocking noted in the shared file, and the substance is corroborated across multiple extractions).

---

## 5. THREAT MODEL: A BEDROOM OR BATHROOM SENSOR IS A HIGH VALUE TARGET

A sensing node in a private room of an older adult's home is among the highest value physical targets a consumer device can be. The bedroom and bathroom nodes in this architecture are non camera by design (radar, mat), which removes the image from the target, but a compromised radar or mat still exposes presence, sleep, vitals, and toileting patterns, and a compromised living area camera node is the crown jewel. The architecture's data minimization (no raw modality leaves, no cloud video corpus) means the worst case cloud breach exposes derived metrics, not video, and the worst case device breach exposes one home, not the base. That is the whole point of the edge posture. The controls below make it real.

### 5.1 Controls

| Control | Specification | Purpose | Confidence |
|---|---|---|---|
| Secure boot | Hardware root of trust; boot ROM verifies a signed bootloader, which verifies signed firmware, chain anchored in fuses. A device will not run an unsigned or modified image | Prevents persistent implant and rooted firmware that could add a frame egress path (section 2 path 8) | HIGH (standard practice), MEDIUM (per silicon feasibility, Phase 3) |
| Signed firmware and signed OTA | Every image and every update is signed; the device verifies the signature and rejects unsigned or downgraded images (anti rollback). Reproducible builds so the shipped image is auditable | Closes section 2 path 3; prevents a malicious or coerced update from enabling raw egress | HIGH |
| Encrypted storage | On device storage encrypted AES 256 (`shared` 1.3), keys held in a secure element, not in plaintext on flash. No raw frames, audio, point clouds, or waveforms persisted (section 1) | A stolen device yields no history, only what is in volatile memory | HIGH |
| Key management | Per device identity keys provisioned at manufacture into the secure element; per home or per tenant data keys; envelope encryption with a cloud KMS or HSM; documented rotation; keys never on the edge device in plaintext (`shared` 1.3) | Limits blast radius of a single device compromise to one home | MEDIUM |
| Transport security | TLS 1.3 device to cloud with certificate pinning; mutual authentication so a spoofed cloud cannot harvest a node | Prevents interception and node hijack | HIGH |
| Mesh security | Zigbee or Thread network with encrypted links; the gateway authenticates each node; no unauthenticated node joins | Prevents a rogue node injecting false events or eavesdropping the mesh | MEDIUM |
| Debug lockdown | Secure debug (JTAG, UART) fused off or authenticated before shipment; no production frame or audio egress capability compiled in (section 2 paths 2, 5) | Removes the developer path to raw modality | MEDIUM |
| Patch cadence | An SLA for security patching over signed OTA across the fleet; a device that cannot be patched is the weak point (`shared` section 2) | The edge posture's operational cost; edge is harder to keep patched than cloud | MEDIUM |

### 5.2 The breach scenario, and why the architecture bounds it

| Breach vector | What an attacker gets | Why it is bounded | Notification obligation |
|---|---|---|---|
| Cloud tier breach | Derived metrics, events, transcripts (text), account and consent graph for the whole base | No raw video, audio, point cloud, or waveform exists in the cloud to steal. Encryption to NIST standards renders the store unusable if key material is not also taken, engaging breach safe harbor (`shared` 1.3, 3.4) | DTC: FTC Health Breach Notification Rule (`shared` 3.4). Covered channel: HIPAA breach notification 45 CFR 164.400 to 414 |
| Single device compromise | One home's live derived stream, and at most an in sensor rolling buffer, not a history | Per home blast radius by key design; no persisted raw modality; secure boot limits persistence | Same regime as above, scoped to affected individuals |
| Mesh eavesdrop | Encrypted derived events for one home | Encrypted links; derived not raw | Same |
| Insider or support abuse | Derived data and device health; no video or audio access exists to abuse (section 2 path 5) | The remote video capability is deliberately absent | Same |

The breach story the architecture permits is materially better than a cloud video product: the company cannot leak video it never received, and cannot leak a corpus it never assembled. The residual exposure is a derived metrics breach, which is real and still notifiable, but is not the catastrophic home video exposure the category is known for. Confidence HIGH on the bounding logic, MEDIUM on the per silicon control feasibility (Phase 3).

---

## 6. APPROVED MARKETING CLAIM LANGUAGE

Per `shared` section 7: every privacy claim maps to an enforced control and a proven code path, or it is not said. A privacy promise the architecture does not enforce is an FTC deceptive practice. The table states what this architecture permits.

| Approved claim (permitted because the architecture enforces it) | Enforcing control | Prohibited or high risk version | Why |
|---|---|---|---|
| "There is no camera in your bedroom or bathroom." | Architecture: bathroom radar, bedroom mat or radar, no camera in private rooms | "Total privacy in every room." | Specific and true; absolutes invite a counterexample |
| "Raw video is processed on the device. Raw video is not sent to our servers." | On sensor inference (IMX500 class) plus section 2 paths closed and audited | "Your video never leaves your home." | The absolute cannot survive a crash dump or a compromised device (section 2 verdict); the qualified claim can |
| "Our staff cannot see a live video or a video clip from your home." | No remote video access capability built (section 2 path 5) | "No one can ever access your camera." | True as an absent feature; the absolute overreaches |
| "Encrypted in transit and at rest using AES 256 and TLS 1.3." | Section 5 controls, `shared` 1.3 | "Military grade encryption." | Specific and verifiable versus puffery FTC disfavors |
| "You decide what is captured and what your family can see, and you can change it at any time." | Role and capacity model, granular revocable consent (section 3) | "Fully HIPAA compliant" (in the DTC channel) | HIPAA does not attach DTC; claiming it misleads (`shared` 7) |
| "We do not sell your health data." | No sale, no broker path; MHMDA sale authorization not sought | "We will never share your data with anyone." | Lawful process can compel disclosure; an absolute never is false |
| "Fall detection runs on the device and works even if the internet is down." | T1 local fall path (`phase2_architecture` topology finding 1) | "Guaranteed to detect every fall" or "a lifesaving device" | Detection is not 100 percent reliable; and a lifesaving or medical claim exits the wellness lane and imports PERS liability (section 4.4) |
| "This is a wellness product, not a medical device, and not a replacement for calling 911." | Positioning (framework section 2); PERS posture (section 4.4) | Any implied emergency response guarantee | Mirrors the enforceable PERS terms of service posture |

Rule, restated: if a control does not enforce it and a code path does not prove it, it is not a claim. Confidence HIGH.

---

## Register Entries

Per framework section 9, sources land in `research/registers/sources.md`. This phase does not edit the registers (instructed scope limit). Staged for append below, including the site side 403 blocks noted (same automated fetcher blocking documented in `shared_privacy_security.md`; substance obtained via search extraction, primary URLs cited for the human reader).

### Sources consulted (stage into registers/sources.md)

| Source | Org | URL | Date accessed | Used for | Credibility |
|---|---|---|---|---|---|
| Two Party Consent States for Recording (2026 Guide) | Recording Law | recordinglaw.com/party-two-party-consent-states | 2026-07-10 | Full 12 state all party consent set for the audio assistant | MEDIUM (secondary, current) |
| Two Party Consent States 2026 | World Population Review | worldpopulationreview.com/state-rankings/two-party-consent-states | 2026-07-10 | Corroboration of the 12 state set | LOW (aggregator, corroborating) |
| Surrogate decision makers; priorities; limitations, Ariz. Rev. Stat. 36-3231 | Arizona Legislature | azleg.gov/ars/36/03231.htm | 2026-07-10 | Statutory surrogate priority order (POA agent, then guardian, then next of kin) | HIGH (primary statute) |
| Health Care Surrogate legal questions (Illinois Health Care Surrogate Act) | Illinois Legal Aid Online | illinoislegalaid.org/legal-information/healthcare-surrogate-legal-questions | 2026-07-10 | Illinois surrogate priority order | MEDIUM (secondary, on primary law) |
| Default Surrogate Decision Making | Merck Manual | merckmanuals.com/home/fundamentals/legal-and-ethical-issues/default-surrogate-decision-making | 2026-07-10 | General default surrogate hierarchy and best interest standard | MEDIUM (secondary, authoritative) |
| Summary Judgement Denied: A Death Leads to a Cautionary PERS Saga | SDM Magazine | sdmmag.com/articles/102697 | 2026-07-10 | PERS duty of care; monitoring failure delayed EMS 18 min; summary judgment denied | MEDIUM (trade press; fetch 403, via extraction) |
| Limited Liability Clause Would Have Helped in Wrongful Death Lawsuit | SDM Magazine | sdmmag.com/articles/93960 | 2026-07-10 | Enforceability of limitation of liability clauses in monitoring contracts | MEDIUM (trade press; fetch 403, via extraction) |
| PERS / Medical Alert / Personal Emergency Response | Kirschenbaum & Kirschenbaum | kirschenbaumesq.com/article/pers-medical-alert-personal-emergency-response | 2026-07-10 | PERS provider liability and contract protections | MEDIUM (law firm; fetch 403, via search snippet) |
| Monitoring Agreement | Medical Care Alert | medicalcarealert.com/monitoring-agreement | 2026-07-10 | Liability cap, not a substitute for 911, not a medical device language | MEDIUM (primary vendor terms; fetch 403, via extraction) |
| Medical Alert PERS Alarm Monitoring Services terms | GeoArm Security | geoarm.com/medical-alert-pers-alarm-monitoring-services.html | 2026-07-10 | PERS not 100 percent reliable, not certified emergency response | MEDIUM (vendor) |

### Sources rejected

| Source | Reason rejected |
|---|---|
| Various 911 dispatcher immunity articles (Texas, New Mexico, Alaska wrongful death) | About government 911 dispatcher sovereign immunity, not private PERS provider liability; off point for a commercial monitoring partner |
| Nimitai, ConvertAudioToText, getnextphone call recording law blogs | SEO aggregators; superseded by Recording Law and the primary statutes cited in `shared` 4.4 |
| Dementia end of life surrogate decision academic papers (Oxford, PMC clusters) | Clinical end of life decision literature; not consumer product consent authority |

Note: sdmmag.com, kirschenbaumesq.com, and medicalcarealert.com returned HTTP 403 to the automated fetcher (site side bot blocking, consistent with the pattern documented in `shared_privacy_security.md`, not an organization policy denial). Substance was obtained via search engine extraction of those same pages and corroborated across sources. Direct machine fetch of the full contract and case text is an open item.

## Open Questions

1. Whether a consumer wellness product (no clinical or HIPAA nexus in the DTC channel) may rely on the clinical and statutory surrogate consent hierarchy directly, and the exact enforceable order per launch state. The hierarchy is confirmed; its application to a non clinical consumer monitoring product is untested and belongs in launch state legal review. Does not block the architecture.
2. Whether a gait or whole body movement signature qualifies as a biometric identifier under BIPA or CUBI (carried from `shared` Open Question 2). Likely outside the enumerated list; MHMDA captures it regardless. Do not build a voice template, which would be inside BIPA. Confirm before relying on non applicability.
3. Field enforcement of the governance code paths in section 2 (OTA path 3, debug path 2) depends on process discipline and code review, which no hardware closes. The audit procedure that certifies the "no raw video leaves" claim before marketing uses it is a G2 to G3 deliverable, not settled here.
4. Whether v1 ships any local verification clip buffer at all (section 2 path 6). The safest build has none and confirms falls by radar plus pose fusion. If false positive rate at G2 forces a clip, the claim language must be requalified. Decide at G2 against the measured false positive rate.
5. Per silicon feasibility of secure boot, secure element, and fused debug lockdown on the selected camera and radar nodes is Phase 3, driven by the Phase 4 model and Phase 3 silicon choice.
6. Exact retention windows in section 1.2 are a product policy recommendation set to MHMDA minimization and the BIPA 3 year floor; confirm per launch state before G4.
7. Primary contract and case text for the PERS liability findings (section 4.4) was 403 blocked to the fetcher; verify the SDM cases and the Medical Care Alert terms against primary text before any partner contract negotiation.
8. Whether the emergency dispatch function is outsourced to a licensed monitoring center (recommended) or built. If built, the product imports PERS duty of care and liability without a monitoring center's insurance. Resolve in Phase 4 section 3.5 and Phase 7 section 5.

## Assumptions Made

1. Assumed the architecture is A1 as selected in Phase 2 (mesh, one oblique camera, T4 hybrid, T1 fall path, no in home inference hub in v1). If the A2 all radar fallback is adopted, the camera code paths in section 2 fall away entirely and the "no video leaves" question is moot, which strengthens the privacy posture. Impact if wrong: section 2 narrows, sections 5 and 6 unchanged.
2. Assumed on sensor inference (IMX500 class) is the camera node design, which is what makes section 2 path 1 a hardware property. If the camera node instead exposes frames to an application SoC, the "no raw video leaves" claim weakens from a hardware property to a policy assertion and section 2 paths 4 and 8 reopen. Impact if wrong: the headline privacy claim degrades. Confidence MEDIUM (silicon selection is Phase 3).
3. Assumed DTC as the base channel, with the home health agency and payer channels as variants that attach HIPAA (section 4.3). Impact if wrong (primary channel is a covered entity): HIPAA Security Rule and BAA become baseline from day one, raising compliance cost, which is the safe direction to plan for.
4. Assumed the assistant uses on device wake word with no retained audio and, preferably, on device speech to text. If cloud STT is used, the utterance audio transits and the all party consent and MHMDA analysis tightens. Impact if wrong: audio becomes a transiting sensitive modality, expanding section 2 and section 4.2 scope.
5. Assumed retention windows in section 1.2 as a minimization aligned recommendation, not a legal constant. Impact if wrong: windows adjust per launch state; direction (minimize) holds.
6. Assumed the emergency dispatch function, if offered, is outsourced to a licensed monitoring center partner under its own ToS. Impact if wrong (built in house): the product carries PERS duty of care and liability directly (section 4.4).
7. Legal findings assumed current as of 2026-07-10. The 12 state all party consent set, the surrogate hierarchy, and the PERS liability posture are stable; the two time sensitive items flagged in `shared` (HIPAA Security Rule NPRM, reproductive rule) do not bear on Concept A.

## Confidence Summary

Overall confidence: HIGH on the load bearing conclusions, MEDIUM on the specifics that depend on Phase 3 silicon and G2 field data.

- HIGH: the data flow minimization design (no raw modality leaves, no cloud video corpus); the verdict that "no raw video leaves the device" is provable only in the qualified form and only if the section 2 code paths are closed, with on sensor inference as the decisive control; MHMDA as the binding privacy constraint applied to this product's derived health data; the 12 state all party consent floor forcing a no retained audio, wake word only design nationally; HIPAA attaching through the channel not the product; the breach scenario bounding logic; the approved claim language mapping to enforced controls.
- MEDIUM: the exact surrogate consent order's direct applicability to a non clinical consumer product (open question 1); field enforcement of the governance code paths (open question 3); the PERS liability findings, which rest on trade press and vendor terms that were 403 blocked to the fetcher and corroborated via extraction (section 4.4); per silicon security control feasibility (Phase 3); the specific retention windows.
- LOW / weakest: whether gait qualifies as a biometric identifier (carried open question); whether v1 ships any local verification clip, which if introduced requalifies the headline claim.
- The single load bearing conclusion, HIGH confidence: the architecture makes the strongest privacy claim in the category defensible, because the company cannot leak video it never receives and cannot leak a corpus it never assembles, but only if on sensor inference is the camera design and every code path in section 2 is affirmatively closed and audited before the claim is marketed.


===================================================================
# (phase6_devplan.md)
===================================================================

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


===================================================================
# (phase7_market.md)
===================================================================

# PHASE 7: MARKET, COMPETITION, AND CHANNEL
## Concept A: Elder Home Monitoring
Output file. Governed by `00_framework.md` (sections 5 evidence rules, 9 registers) and `01_concept_a_elder_monitoring.md` Phase 7.

Positioning under evaluation: general wellness, consumer subscription, remote adult child as buyer (founder assumption A7, flagged for challenge).

Date of analysis: 2026-07-10. Currency USD.

---

## 1. BOTTOM-UP MARKET SIZING

Method per framework section 6: count addressable units, apply realistic price and penetration, then check against an analyst TAM. The funnel below sizes the **direct-to-consumer (DTC) segment** first, because that is the buyer the concept assumes. Channel-specific reachable populations are treated separately in section 1.3, because the reachable count is a function of channel, not of the total.

### 1.1 The funnel

| Step | Population | Multiplier | Result | Confidence | Source / basis |
|------|-----------|-----------|--------|-----------|----------------|
| 1 | US adults 65+ living alone, community-dwelling | baseline | **16.2M** | HIGH | ACL 2023 Profile of Older Americans / Census CPS 2023: ~28% of community-dwelling 65+ live alone; 5.7M men + 10.5M women = 16.2M |
| 2 | Have at least one living adult child | x 0.80 | 13.0M | MEDIUM | Assumption. Childlessness among current 65+ cohort ~20%. The buyer in the concept is an adult child; elders with no child fall out of the DTC thesis |
| 3 | Nearest child is "remote" (not within ~20 minutes) | x 0.25 | 3.25M | MEDIUM | AARP/NAC Caregiving in the US 2020: 75% of caregivers live with or within 20 min of the recipient; ~25% are farther; 11% are 1hr+. Used as proxy for the share whose child cannot simply drop by |
| 4 | Household able and willing to fund ~$30-50/mo discretionary | x 0.60 | **1.95M** | LOW-MEDIUM | Assumption. Elders living alone are lower income (median individual income $29,740, 2022; 17.7% in poverty). Ability to pay sits with the adult child. 60% is a judgment call, flagged |

**Addressable DTC households (SAM population): ~1.95M, round to ~2.0M.**

### 1.2 Price and penetration to revenue

Product economics assumed for sizing (validated downstream in Phase 3 / Phase 8, here used only to convert units to dollars):
- Hardware: $200-400 one-time (comparable to CarePredict @Home kit $449.99, Vayyar ~$250/device x3).
- Subscription: $30-40/mo, i.e. ~$360-480/yr. Anchored to PERS market actual pricing (section 6), midpoint $420/yr used.

| Layer | Households | x annual subscription | Result | Note |
|-------|-----------|----------------------|--------|------|
| TAM (all living-alone 65+, theoretical ceiling) | 16.2M | $420 | **~$6.8B/yr** | Ignores buyer, ability to pay, competition. Not a real target |
| SAM (remote-child, able to pay) | 2.0M | $420 | **~$840M/yr** | The defensible DTC ceiling for this product |
| SOM at 5% penetration of SAM | 100,000 | $420 | **~$42M/yr ARR** | Realistic mature DTC outcome. PERS 65+ penetration is 9% and flat (section 6); a pricier, more complex product should assume less |
| SOM at 10% penetration of SAM | 195,000 | $420 | **~$82M/yr ARR** | Optimistic DTC case |

Add-in hardware revenue at SOM 5%: 100,000 units x $300 blended = ~$30M one-time, recurring only on replacement/new adds.

**Headline: the realistic DTC SAM is ~$840M/yr of subscription revenue; a well-executed DTC-only business captures $40-80M ARR at maturity. That is a real business but not a venture-scale outcome on DTC alone. This is the single most important number in the phase and it corroborates founder assumption A7's warning that DTC in this category is CAC- and churn-bound.**

### 1.3 Reachable population by channel (the count changes with the channel)

The framework requires "subset reachable per channel." Reachable universe differs by go-to-market:

| Channel | Reachable universe | Basis | Confidence |
|---------|-------------------|-------|-----------|
| DTC | ~2.0M households (funnel above) | derived | LOW-MEDIUM |
| Senior living / assisted living operators | ~1.0M residents across ~30,600-33,000 communities, ~1.2M licensed beds | NCHS / NIC / A Place for Mom 2024 | HIGH |
| Home health / home care agencies | Clients of ~11,500 Medicare-certified home health agencies plus a larger fragmented non-medical home care base | CDC NCHS 2023 (11,506 HHAs); Definitive tracks 17,300+ active | MEDIUM |
| Medicare Advantage supplemental benefit | ~34M+ MA enrollees, but only ~14.5% of plans ever offered PERS and that is contracting in 2025 | KFF; ATI Advisory | MEDIUM |

Note: institutional channels reach fewer total elders than the DTC funnel but reach them in aggregated, higher-contract-value units. See section 3.

### 1.4 Analyst TAM check (secondary only)

| Source | Figure | Scope | Read |
|--------|--------|-------|------|
| Laurie Orlov, Aging & Health Technology Watch, Market Overview 2024 | **$9.1B (2024)**, aging-in-place technology | All aging-in-place tech, not just monitoring | Our DTC SAM ($840M/yr) is ~9% of this broad category. Plausible |
| AARP + Consumer Technology Association (Jan 2025) | **$120B by 2030**, "aging technology" | Very broad (all agetech incl. mobility, hearing, telehealth) | Too broad to anchor on. Marketing-grade |
| Mordor Intelligence / Grand View | **$10.2-10.8B (2025-26)** medical alert / PERS market | Global PERS, the closest comparable | Our product is one entrant in a ~$10B global PERS market. $40-80M ARR SOM is a ~0.5-0.8% share. Credible |

The bottom-up and the PERS-specific analyst figure agree in order of magnitude. The broad "agetech" TAMs are not usable as a target and are cited only to show the concept does not contradict them.

---

## 2. COMPETITIVE LANDSCAPE

Full profiles. Register rows in section 9. Failures emphasized per brief.

### 2.1 Master table

| Company | What they sell | Buyer / channel | Price (list vs actual) | Raised / ownership | Status 2025-26 | Conf. |
|---------|---------------|-----------------|------------------------|--------------------|----------------|-------|
| **SafelyYou** | Ceiling camera + "Safety AI" fall detection/prevention, memory-care focus | B2B senior living / memory care operators | Per-bed monthly subscription (undisclosed); 15-bed minimum; install ~$200/bed | ~$100M+ total; $43M Series C Jan 2025 (Touring Capital) | Operating, scaling | HIGH status / LOW price |
| **Vayyar Care** | 60GHz mmWave radar, camera-free/wearable-free fall detection | DTC (Amazon), senior living, UK councils, care-software partners | List ~$250/device (~3/home) + $20/mo emergency calling; bulk undisclosed | Parent Vayyar Imaging ~$308M total ($108M Series E 2021, Koch) | Operating (product line) | HIGH price / MEDIUM attribution |
| **CarePredict** | "Tempo" AI wrist wearable + room beacons; activity, behavior, fall, location | Senior living + aging-in-place @Home | @Home kit ~$449.99 hardware + monthly subscription; facility undisclosed | ~$42-46M; $29M Series A-3 Jul 2023 | Operating; KamiCare partnership Nov 2025 | HIGH status / MEDIUM raise |
| **Sensi.ai** | Acoustic/audio AI "virtual care agent", no cameras/wearables, 100+ insights | B2B home care agencies | Custom B2B subscription by agency size (undisclosed) | ~$98M+; $45M Series C Oct 2025 (Qumra); $31M Series B 2024 (Insight) | Operating, high growth (~400% YoY claimed) | HIGH status / LOW price |
| **Cherry Home / Cherry Labs** | Wall camera + computer vision (skeletonized, local); falls, gait, inactivity | Home care agencies + families (DTC) | Historical list ~$1,600 (2-room) to $2,000 (6-room) + monitoring; current unknown | ~$6M total ($5.2M Dec 2018, GSR) | Dormant / low-traction; no funding or news since 2018-19 | MEDIUM status / LOW price |
| **Origin Wireless / Origin AI** | WiFi/RF "AI Sensing"; motion, presence, fall, breathing; 200+ patents | Licensing/OEM to carriers, ISPs, security (Verizon, Alarm.com) | Licensing/embedded (undisclosed) | ~$52M raised | **ACQUIRED by ADT for $170M cash, announced Feb 24 2026** | HIGH |
| **Emerald Innovations** | MIT (Katabi) spinout; contactless RF through-wall movement, breathing, HR, sleep, falls | Pharma (drug trials) + research | B2B/research contracts (undisclosed) | Bootstrapped / employee-owned; $1.1M grant 2023 | Operating, profitable, pharma-focused | HIGH status / MEDIUM raise |
| **Tellus (fka Tellus You Care)** | Bedroom radar, contactless HR/respiration/sleep/gait/falls | B2B eldercare; heavy Japan pilots | Undisclosed | Seed-stage only | ACQUIRED by AIP Healthcare ~Oct 2024 (terms undisclosed) | MEDIUM |
| **Lively / GreatCall** | Jitterbug phones, Lively Mobile PERS, Urgent Response | DTC + Best Buy retail; seniors + caregivers | Device from ~$79.99; plans from $14.99/mo; health/safety tiers layered | **Best Buy acquired for $800M, closed Oct 1 2018** (~900k subs) | Active as Lively from Best Buy Health; retained after Current Health divestiture | HIGH |
| **Medical Guardian** | PERS in-home + mobile + MGMove smartwatch | DTC online/phone | Monitoring from $27.95/mo; range to ~$46.95; fall detection +$10/mo; device $149.95-$199.95 | $100M growth (Water Street, 2020); acquired MobileHelp May 2024 | Active, growing via M&A | HIGH |
| **Bay Alarm Medical** | PERS (SOS Home, Micro, All-in-One, Smartwatch) | DTC online/phone | From $27.95/mo (landline) to ~$64.95; cellular $34.95/mo | Family-owned (Westphal); no outside funding | Active | HIGH |
| **Life Alert** | PERS ("I've fallen and I can't get up"), no fall detection | DTC, heavy TV/telemarketing | $49.95-$89.95/mo (well above ~$29 avg) + ~$197 setup; mandatory 36-month contract | Private; ownership/raise UNKNOWN | Active but reputationally strained (2,300+ FTC complaints 2020-25) | HIGH price / LOW ownership |
| **Apple Watch fall detection** | Consumer smartwatch wellness/safety feature (not monitored PERS) | Retail; mainstream consumers, auto-enabled 55+ | Hardware $249 (SE) to ~$799 (Ultra); **no monthly fee** | Apple Inc. (feature) | Active, expanding (satellite SOS) | HIGH |
| **Amazon Alexa Together** | Elder-monitoring subscription: caregiver activity feed, remote Alexa mgmt, 24/7 Urgent Response, 3rd-party fall detection | Amazon; adult-child caregivers | $19.99/mo or $199/yr, 6-mo free trial | Amazon (in-house) | **DISCONTINUED May 21 2025** (launched Dec 7 2021); emergency piece folded into Alexa Emergency Assist | HIGH |
| **Best Buy Health / Current Health** | Care-at-home / RPM platform + hospital-at-home | B2B enterprise sales to health systems | Enterprise/contract (undisclosed) | **Best Buy acquired Current Health for ~$400M, closed Nov 2 2021** | **DIVESTED late June 2025**, sold back to co-founder McGhee; preceded by $475M goodwill impairment + 161 layoffs | HIGH |

### 2.2 The failures, which are the instructive part

**Amazon Alexa Together (dead, May 2025). The most instructive failure in the set.**
A $19.99/mo subscription from the company with the lowest customer acquisition cost on earth (installed Alexa base, Prime relationship, zero-cost distribution) still could not sustain a bundled elder-monitoring product. Amazon unbundled it and kept only the one feature with genuine willingness to pay, professional emergency response, migrating it into the cheaper Alexa Emergency Assist and discarding the caregiver activity-monitoring layer entirely. Lesson: the caregiver "activity feed / dashboard" layer that this concept centers on is precisely the layer Amazon found people would not pay for. If the entity with the best distribution in the world could not make the monitoring-dashboard subscription work, a startup paying real CAC should not assume it can. This directly stress-tests the concept's core value proposition.

**Best Buy Health / Current Health (bought $400M 2021, written down $475M and divested 2025, under 4 years).**
Enterprise B2B care-at-home / RPM sold to health systems. Best Buy took a $475M goodwill impairment (business worth far less than paid), 161 layoffs, and sold it back to its founder. The enterprise-clinical market "did not scale as originally forecasted." Meanwhile Best Buy **kept** Lively, the consumer PERS subscription that fit its retail channel. Lesson: channel-fit dominates. The provider-side clinical sale is slow, complex, and did not scale even for a $40B retailer; the consumer subscription with retail distribution survived.

**Tellus You Care (soft landing ~2024) and Cherry Home (dormant since 2019).**
Two sensing startups that never cleared senior-living CAC and reimbursement hurdles on seed capital. Tellus pivoted to Japan (better demographics), then was quietly absorbed by AIP Healthcare. Cherry Home (camera-based in-home vision for seniors, the closest architectural analog to this concept's default) raised $6M in 2018-19 and has shown no funding, pricing, or product news since: effectively dead. Lesson: in-home camera vision for elders faces privacy resistance and family CAC that a lightly funded company cannot outrun. This is a direct warning to the concept's camera-in-a-bulb default (assumption A1/A3).

**Origin AI (exit, not failure, but instructive).** WiFi-sensing never became a standalone senior product; the durable value was the RF-sensing IP, monetized by embedding it in ADT's installed base ($170M, Feb 2026). Lesson: component-layer sensing tech monetizes better inside a distribution giant than sold direct. Relevant if this concept's real asset turns out to be an algorithm rather than a product.

**Synthesis:** The winners in this category are (a) simple monitored PERS with retail/DTC distribution (Lively, Medical Guardian, Bay Alarm), (b) B2B sensing sold per-bed into operators who already carry liability for falls (SafelyYou, Sensi.ai), and (c) IP licensors (Origin). The losers are consumer monitoring **dashboards** (Alexa Together) and enterprise clinical platforms bought by non-clinical parents (Current Health). The concept as framed (consumer dashboard + in-home camera) sits closest to the two failure archetypes.

---

## 3. CHANNEL ANALYSIS

Compared on CAC, sales cycle, contract size, and gross margin. Hard CAC and margin figures for this specific category are largely private; cells are marked with confidence and basis. Directional ranking is HIGH confidence even where individual cells are LOW.

| Channel | CAC | Sales cycle | Contract size | Gross margin | Verdict |
|---------|-----|-------------|---------------|--------------|---------|
| **DTC (consumer subscription)** | HIGH: $150-400+ blended (paid search/TV/affiliate). Generic subscription CAC avg ~$72 is a floor this category exceeds due to trust-heavy, considered purchase | Short (days-weeks) | Small: ~$420/yr sub + $200-400 hardware | MEDIUM: hardware-subsidized; PERS margins under commoditization pressure, ~40-60% blended vs 78% pure SaaS | Fast but CAC/churn-bound; the Alexa Together graveyard. LOW confidence this scales to venture size alone |
| **Medicare Advantage supplemental benefit (PMPM)** | LOW per-member once contracted; the sale is to the plan | Long (12-24 mo; annual bid cycle) | Large (PMPM x thousands of members) | HIGH if software-led | Attractive economics but **contracting in 2025** (UnitedHealthcare dropped Lifeline PERS as core benefit; only ~14.5% of plans ever offered PERS). Timing risk |
| **Home health / home care agencies** | MEDIUM (sell to ~11,500 agencies, fragmented) | Medium (3-9 mo) | Medium (per-client or per-agency SaaS) | HIGH (software/analytics margins) | Sensi.ai's proven lane. Agency carries the care relationship and some liability. Fragmentation is the tax |
| **Senior living / assisted living operators (per-bed)** | MEDIUM-LOW (concentrated: ~1,000 operators control most of 1.2M beds) | Medium-long (6-12 mo, pilot-gated) | Large (per-bed/mo x 100s of beds per deal) | HIGH (per-bed software) | SafelyYou's proven lane. Operator buys because it **owns fall liability**. Best margin+contract combination |
| **Health systems / ACOs** | HIGH (enterprise clinical sale) | Very long (12-24+ mo) | Large but slow | MEDIUM | Current Health's graveyard. Requires medical-device positioning + clinical evidence. Contradicts the wellness lane |
| **LTC insurers** | MEDIUM | Long (12-18 mo) | Medium-large | HIGH | Insurer funds monitoring to defer claims (delayed institutionalization). Small number of carriers; underdeveloped but rational buyer |
| **Hardware retail (Best Buy, Amazon)** | Shifts CAC to channel (slotting/margin share) | Medium to get on shelf | Small unit, high volume | LOW (retail margin share erodes it) | Distribution, not a buyer. Works for simple SKUs (Lively). Poor fit for install-heavy multi-node systems |

**Best channel by CAC-to-margin: senior living / assisted living operators, per-bed.** Concentrated buyer base (low CAC per bed), high gross margin on per-bed software, large multi-bed contracts, and the buyer has a hard financial reason to pay (it carries fall liability and insurance exposure). This is exactly where SafelyYou raised $100M+ and where the concept's fall-detection and long-lie-detection features have a buyer who is legally and financially motivated. Home care agencies (Sensi.ai's lane) are a close second. DTC and health-system/ACO are the two channels the failure record most strongly warns against.

This finding directly challenges founder assumption A7's implied DTC default and confirms its explicit warning: the money is in operators and payers, not the consumer.

---

## 4. REIMBURSEMENT

### 4.1 Code families and current payment

| Code | Covers | ~2025 national avg Medicare | Device requirement | Conf. |
|------|--------|----------------------------|--------------------|-------|
| **RPM 99453** | Device setup + patient education (once/device) | ~$19.73 | Must be FDA 201(h) device | HIGH code / MEDIUM $ |
| **RPM 99454** | Device supply + transmission; **≥16 days data / 30** | ~$43.03 | Must be FDA 201(h) device | HIGH / MEDIUM |
| **RPM 99457** | First 20 min/mo clinical management + 1 interactive contact | ~$47.87-51.77 | — | HIGH / MEDIUM |
| **RPM 99458** | Each additional 20 min/mo (add-on) | ~$38.49 | — | HIGH / MEDIUM |
| **RTM 98975/76/77** | Setup; respiratory device; musculoskeletal device (≥16 days/30) | ~$19 / ~$50 / ~$43 | Must be FDA 201(h) device | HIGH / MEDIUM |
| **RTM 98980/81** | First 20 min / additional 20 min management | ~$48 / ~$38 | — | HIGH / MEDIUM |
| **CCM 99490 / 99439** | Non-complex, first / additional 20 min; **≥2 chronic conditions** | ~$60.49 / ~$45.93 | No device required | HIGH / MEDIUM |
| **CCM 99487 / 99489** | Complex CCM, first 60 min / additional 30 min | ~$130 (LOW) / ~$70.52 | No device | MEDIUM/LOW |
| **PCM 99424 / 99426** | Physician / clinical-staff time, first 30 min; **exactly 1 complex chronic condition** | ~$88 / ~$68 | No device | MEDIUM |
| **PCM 99425 / 99427** | Each additional 30 min (add-on) | UNKNOWN / ~$48.45 | No device | LOW/MEDIUM |

2026 note: CMS finalized shorter-duration RPM/RTM codes effective 1/1/2026 (e.g. 99445 device supply for 2-15 days, priced ~$52; 99470 first 10 min management ~$26), lowering the data-day threshold. Source: CMS CY2026 PFS Final Rule (CMS-1832-F).

### 4.2 What a wellness-positioned product can and cannot bill. The central tension.

**Cannot bill RPM or RTM.** The logic chain is airtight from primary sources:
1. CMS requires the RPM/RTM monitoring device to meet the FDA definition of a "medical device" under **Section 201(h) of the FD&C Act** (established CY2019/2020 PFS policy).
2. The 21st Century Cures Act (Dec 2016, section 3060) amended the FD&C Act to **remove** general-wellness software "intended for maintaining or encouraging a healthy lifestyle **unrelated to the diagnosis, cure, mitigation, prevention, or treatment of a disease**" from the 201(h) device definition. FDA's own general-wellness guidance states such products are not regulated as devices.
3. Therefore a product that is, by design and by claim, a general-wellness product is **excluded from 201(h)** and cannot serve as the qualifying device for RPM (99453/99454) or RTM (98975-98977). Note: 201(h) status does not require FDA clearance, but it does require a disease-related intended use, which is exactly what the wellness positioning forbids.

**Cannot directly bill CCM or PCM either, though for a different reason.** CCM and PCM are time/service codes that pay a **clinician** for care-coordination time and require **no device**. A wellness product could be a workflow tool *supporting* a clinician's CCM/PCM delivery, but the payment goes to the clinician for documented time, not to the product vendor. There is no code that pays a non-device wellness product.

**The tension, stated plainly:** Reimbursement is the largest and most durable revenue pool in aging-in-place, and every device-paying code (RPM, RTM) is gated behind FDA medical-device status. The concept's settled strategic decision (framework section 2) is to be a general-wellness product, which is *defined by exclusion from* that device status. **The concept cannot simultaneously be a general-wellness product and bill RPM/RTM. This is the central strategic tension of the business.** The routes out are all costly: (a) build a separate cleared medical-device SKU for the reimbursed channel (adds regulatory cost, contradicts the lane), (b) partner with a clinician/RPM vendor who supplies the qualifying device and sell the wellness layer as adjacent software, or (c) forgo reimbursement entirely and live on DTC + operator per-bed + payer PMPM, none of which require device status. Option (c) is the only one consistent with the current positioning, and it removes the single largest revenue pool from the model.

---

## 5. PARTNERS

Grouped by function per Phase 7 item 5. Detailed vendor rows in section 9.

| Function | Candidate partners | Rationale | Conf. |
|----------|-------------------|-----------|-------|
| Camera / module ODMs | Chinese IP-camera module houses (Allwinner/Rockchip/SigmaStar-based), Western distribution for validated modules | Cost floor for vision node; detailed BOM in Phase 3 | MEDIUM |
| Contract manufacturers | Regional CMs for low-volume G3-G5; Asian CM at G6 | Standard hardware scaling path | LOW |
| Silicon vendors w/ startup programs | NVIDIA (Jetson / Inception), Ambarella, Hailo, ST (STM32N6) | Compute for pose/fall; validate against wellness lane in Phase 3-4 | MEDIUM |
| PERS monitoring call centers (buy, do not build) | Existing 24/7 monitoring centers (the infrastructure Lively/Medical Guardian/Bay Alarm rely on) | Framework/brief: do not build a call center. White-label the escalation layer | MEDIUM |
| Radar / contactless sensing | Vayyar (60GHz modules), TI IWR/xWR, Infineon | Bathroom-viable, no-image modality; addresses camera privacy objection (assumption A3) | MEDIUM |
| Wearable vendors | Only if raw-data access is real (assumption A4, see shared register) | Most vendors expose derived metrics only | LOW |
| Senior living operators (pilot hosts) | Large operators controlling concentrated bed counts | Best channel (section 3); pilot host + design partner | MEDIUM |
| Home care agencies (channel + pilot) | Large multi-site agencies (Sensi.ai's customer profile) | Second-best channel | MEDIUM |
| Academic gait labs (validation) | University gait/biomechanics labs with instrumented walkways | Required to substantiate gait metrics under FTC standards (framework section 2) | MEDIUM |
| RPM vendor (reimbursement bridge) | An FDA-device RPM platform vendor | The only compliant route to touch reimbursement without abandoning the wellness lane (section 4.2 option b) | LOW |

---

## 6. WILLINGNESS TO PAY AND CHURN

### 6.1 What families actually pay (DTC, published)

| Item | Value | Conf. | Source |
|------|-------|-------|--------|
| PERS / medical alert monthly, overall avg 2025 | ~$37/mo (band $25-50) | MEDIUM-HIGH | NCOA; SeniorLiving.org 2026 |
| In-home base unit | $20-40/mo | MEDIUM | NCOA / AgingInPlace |
| Mobile / GPS | $30-50/mo | MEDIUM | same |
| Fall detection add-on | +~$10/mo | MEDIUM | same |
| Equipment / activation one-time | $50-350 device; activation up to ~$200 | MEDIUM | SeniorLiving.org |
| Family caregiver total out-of-pocket (context) | ~$7,200/yr avg | HIGH | AARP/NAC Caregiving in the US 2025 |

The willingness-to-pay ceiling for the monitoring subscription is anchored hard at ~$25-50/mo by an entrenched PERS market. A new product priced above that band fights both the anchor and the incumbents' distribution.

### 6.2 Demand signal and churn

| Metric | Value | Conf. | Source |
|--------|-------|-------|--------|
| 65+ currently using PERS/medical alert | **9%, flat vs 2023** | MEDIUM | The Senior List 2026 Usage Report |
| Adult children who discussed PERS with parent | 26% | MEDIUM | same |
| Purchase intent among adult children | **fell 39% (2023) to 22% (2026)** | MEDIUM | same |
| 65+ reporting a fall since turning 65 | 44% | MEDIUM | same |
| **PERS-specific churn / retention** | **UNKNOWN** — no public figure; held in private filings | — | Open Question |
| Annual plans reduce churn vs monthly | ~51% reduction | LOW (general) | subscription benchmark, not PERS-specific |
| MA plans offering PERS as supplemental benefit | rose 1.2% (2017) to 14.5% (2019), **contracting 2025** | MEDIUM | ATI Advisory |

**Read:** Penetration is stuck at 9% and adult-child purchase intent is falling (39% to 22% in three years) despite 44% of elders having fallen. This is a market with real need but softening discretionary demand and a hard price anchor. It is a demand-softness signal, not a demand vacuum, and it argues against a DTC-led, premium-priced entry. Churn is the single most important number the model needs and it is not publicly available; this is a material open question, not a value to assume.

---

## Register Entries

Per framework section 9. To be appended by the register-maintaining process; reproduced here for the phase record. (This phase does not edit `research/registers/` directly per instruction.)

### 9.1 competitors.md (Product | Buyer | Price | Funding | Status | If dead, why)

| Company | Product | Buyer | Price | Funding/ownership | Status | If dead, why |
|---------|---------|-------|-------|-------------------|--------|--------------|
| SafelyYou | Ceiling camera fall-detection AI | Senior living operators | Per-bed sub (undisclosed) + ~$200/bed install | ~$100M+; $43M Series C 2025 | Operating | - |
| Vayyar Care | 60GHz radar fall detection | DTC + operators | ~$250 device + $20/mo | Parent ~$308M | Operating | - |
| CarePredict | AI wearable + beacons | Senior living + @Home | ~$449.99 kit + sub | ~$42-46M | Operating | - |
| Sensi.ai | Acoustic AI monitoring | Home care agencies | Custom B2B | ~$98M+ | Operating | - |
| Cherry Home | Camera CV monitoring | Agencies + families | ~$1,600-2,000 + sub (historical) | ~$6M | Dormant | No traction; camera privacy resistance + family CAC on seed capital |
| Origin AI | WiFi/RF sensing IP | OEM/licensing | Licensing (undisclosed) | ~$52M | Acquired by ADT $170M Feb 2026 | - (exit) |
| Emerald Innovations | Contactless RF health sensing | Pharma / research | B2B contract | Bootstrapped; $1.1M grant | Operating | - |
| Tellus You Care | Bedroom radar | Eldercare (Japan) | Undisclosed | Seed only | Acquired by AIP Healthcare ~2024 | Sub-scale; soft landing after failing to clear CAC/reimbursement on seed |
| Lively/GreatCall | Jitterbug + PERS | DTC + retail | Device $79.99+; $14.99/mo+ | Best Buy $800M 2018 | Active | - |
| Medical Guardian | PERS + smartwatch | DTC | $27.95-46.95/mo + device | $100M growth 2020 | Active | - |
| Bay Alarm Medical | PERS | DTC | $27.95-64.95/mo | Family-owned | Active | - |
| Life Alert | PERS | DTC/TV | $49.95-89.95/mo + $197 setup; 36-mo contract | Private, UNKNOWN | Active | - |
| Apple Watch | Fall detection wellness feature | Retail consumers | $249-799 hardware, no fee | Apple | Active | - |
| Amazon Alexa Together | Caregiver monitoring subscription | Adult-child caregivers | $19.99/mo or $199/yr | Amazon | **Dead May 21 2025** | Dashboard layer had no willingness-to-pay; only emergency response valued, folded into Emergency Assist |
| Best Buy Health / Current Health | RPM / care-at-home platform | Health systems | Enterprise (undisclosed) | Best Buy $400M 2021 | **Divested June 2025** | Enterprise-clinical did not scale; $475M impairment; channel mismatch with retailer parent |

### 9.2 sources.md (additions this phase)

| Source | Org | URL | Pub date | Used for | Credibility |
|--------|-----|-----|----------|----------|-------------|
| 2023 Profile of Older Americans | ACL | acl.gov/sites/default/files/Profile%20of%20OA/ACL_ProfileOlderAmericans2023_508.pdf | 2024 | 65+ living-alone count | HIGH (gov) |
| Living Arrangements Varied Across Age Groups | US Census | census.gov/library/stories/2024/05/living-arrangements.html | 2024-05 | Living-alone shares | HIGH |
| Caregiving in the US 2020 | AARP/NAC | aarp.org/pri/topics/ltss/family-caregiving/caregiving-in-the-united-states/ | 2020 | Long-distance caregiver share | HIGH |
| Caregiving in the US 2025 | AARP/NAC | aarp.org/press/releases/2025-07-24... | 2025-07 | Family OOP spend | HIGH |
| Market Overview: Technology for Aging 2024 | L. Orlov / Aging & Health Tech Watch | ageinplacetech.com/files/aip/Market%20Overview%202024%20Final%20January-2024.pdf | 2024-01 | Analyst TAM check | MEDIUM |
| Aging tech $120B by 2030 | AARP + CTA | aarp.org/press/releases/2025-1-8... | 2025-01 | Broad TAM (context only) | LOW-MEDIUM |
| PERS market report | Mordor Intelligence | mordorintelligence.com/industry-reports/medical-alert-system-personal-emergency-response-system-market | 2025-26 | PERS market size | MEDIUM |
| Medical Alert Systems Market | Grand View Research | grandviewresearch.com/industry-analysis/medical-alert-personal-emergency-response-system-pers-market | 2024-25 | PERS market size | MEDIUM |
| 2026 Medical Alert Device Usage Report | The Senior List | theseniorlist.com/research/medical-alert-device-consumer-usage-study/ | 2026 | Penetration, intent, churn context | MEDIUM |
| Medical alert cost | NCOA | ncoa.org/product-resources/medical-alert-systems/medical-alert-systems-cost/ | 2025 | DTC pricing | MEDIUM-HIGH |
| RPM CPT quick guide | Prevounce / OpenLoop | blog.prevounce.com/quick-guide-remote-patient-monitoring-rpm-cpt-codes-to-know | 2025 | RPM codes + 16-day rule | MEDIUM |
| Billing for RPM | HHS Telehealth | telehealth.hhs.gov/providers/best-practice-guides/telehealth-and-remote-patient-monitoring/billing-remote-patient | 2025 | RPM billing rules | HIGH (gov) |
| General Wellness: Policy for Low Risk Devices | FDA | fda.gov/regulatory-information/search-fda-guidance-documents/general-wellness-policy-low-risk-devices | rev. 2026-01 | 201(h) exclusion | HIGH (gov) |
| CY2026 PFS Final Rule (CMS-1832-F) | CMS | cms.gov/newsroom/fact-sheets/calendar-year-cy-2026-medicare-physician-fee-schedule-final-rule-cms-1832-f | 2025 | 2026 RPM/RTM codes | HIGH (gov) |
| CCM 2025 rates | SignalLamp / ChartSpan | signallamphealth.com/2025-medicare-cpt-code-reimbursements-for-chronic-care-management-ccm/ | 2025 | CCM payment | MEDIUM |
| PCM 2025 codes | ThoroughCare / RHIhub | thoroughcare.net/blog/2025-principal-care-management-pcm-cpt-codes-billing-and-reimbursements | 2025 | PCM payment | MEDIUM |
| CY2025 MA market trends | ATI Advisory | atiadvisory.com/resources/cy-2025-medicare-advantage-market-trends-first-look/ | 2024 | MA supplemental PERS trend | MEDIUM |
| Medicare Advantage 2024 Spotlight | KFF | kff.org/medicare/medicare-advantage-2024-spotlight-first-look/ | 2024 | MA plan counts | HIGH |
| Assisted living statistics | A Place for Mom / NCHS / NIC | aplaceformom.com/senior-living-data/articles/assisted-living-statistics | 2024 | Bed/community counts | MEDIUM-HIGH |
| Home Health Care FastStats | CDC NCHS | cdc.gov/nchs/fastats/home-health-care.htm | 2023 | HHA counts | HIGH (gov) |
| Best Buy / GreatCall $800M | Senior Housing News / SEC | seniorhousingnews.com/2018/08/15/... | 2018 | Acquisition | HIGH |
| Current Health $400M + divestiture | Forbes / Bloomberg / SEC 10-K | forbes.com/sites/saibala/2021/11/30/... ; bloomberg.com/news/articles/2025-06-24/... | 2021 / 2025 | Acquisition + wind-down | HIGH |
| Alexa Together launch + discontinuation | TechCrunch / caregiver sites | techcrunch.com/2021/12/07/... | 2021 / 2025 | Launch + fate | HIGH launch / MEDIUM date |
| SafelyYou $43M Series C | BusinessWire / SHN | businesswire.com/news/home/20250128706931/en/ | 2025-01 | Funding | HIGH |
| Sensi.ai $45M Series C | Sensi.ai / PRNewswire | sensi.ai/blog/sensi-ai-raises-45m-series-c... | 2025-10 | Funding | HIGH |
| Origin AI $170M ADT acquisition | ADT / GlobeNewswire | globenewswire.com/news-release/2026/02/24/... | 2026-02 | Acquisition | HIGH |

### 9.3 vendors.md (additions this phase)

| Vendor | Supplies | MOQ / startup-friendly | Published pricing | Conf. |
|--------|----------|------------------------|-------------------|-------|
| Vayyar | 60GHz mmWave radar modules | Product line, works with integrators | ~$250/device | MEDIUM |
| Texas Instruments | IWR/xWR radar | Distributor, yes | Distributor list | MEDIUM |
| Infineon | 60GHz radar | Distributor, yes | Distributor list | MEDIUM |
| NVIDIA | Jetson compute + Inception program | Startup program yes | Module (Phase 3) | MEDIUM |
| Ambarella / Hailo / ST | Vision SoC / accelerator / STM32N6 | Varies | Phase 3 | MEDIUM |
| PERS monitoring centers | White-label 24/7 escalation | Buy not build | UNKNOWN | LOW |
| University gait labs | Instrumented-walkway validation | Research agreements | UNKNOWN | MEDIUM |

### 9.4 funding.md (category deal evidence)

| Investor / event | Deal | Amount | Date | Thesis signal |
|------------------|------|--------|------|---------------|
| Touring Capital (+ Foundation, Founders Fund, Samsung Next, Qualcomm Ventures) | SafelyYou Series C | $43M | 2025-01 | Operator per-bed fall AI is fundable |
| Qumra Capital | Sensi.ai Series C | $45M | 2025-10 | Home care agency audio AI is fundable |
| Insight Partners | Sensi.ai Series B | $31M | 2024 | same |
| SV Health / Aspire | CarePredict Series A-3 | $29M | 2023-07 | Wearable senior monitoring |
| ADT | Origin AI acquisition | $170M | 2026-02 | Sensing IP monetizes via distribution giant |
| Best Buy | GreatCall / Lively | $800M | 2018 | Consumer PERS + retail channel wins |
| Best Buy | Current Health | $400M (impaired $475M, divested 2025) | 2021 | Enterprise clinical + retailer = failure |

---

## Open Questions

1. **PERS-specific churn / retention rate. UNKNOWN.** Not published; held in private filings. This is the single most material gap for the business case (Phase 8 LTV depends on it). Blocks a defensible LTV:CAC.
2. **Senior-living per-bed-per-month monitoring price. UNKNOWN.** SafelyYou, Securitas Foresite, Xandar Kardian all quote per-community, publish nothing. Requires direct RFQ. Blocks precise sizing of the best channel.
3. **Real DTC CAC for a premium multi-node monitoring product. UNKNOWN.** Generic subscription CAC ~$72 is a floor this considered, trust-heavy purchase exceeds; no category-specific figure found.
4. **Share of living-alone 65+ with a genuinely remote adult child. Estimated, not measured.** Funnel steps 2-4 rest on assumptions (0.80, 0.25, 0.60). A dedicated data pull (Census PUMS cross-tab of household + child proximity) would tighten the SAM.
5. **Per-benefit MA dollar spend on PERS / in-home monitoring. UNKNOWN.** ATI shows the trend (14.5% of plans, contracting) but no spend figure.
6. **Life Alert ownership and total raised. UNKNOWN.**
7. **Exact resale price of Current Health (2025 divestiture). Undisclosed.**

## Assumptions Made

| # | Assumption | Value | Impact if wrong |
|---|-----------|-------|-----------------|
| 1 | Share of living-alone 65+ with a living adult child | 0.80 | Scales SAM linearly. If 0.70, SAM population falls ~12% |
| 2 | Share whose nearest child is "remote" (proxy: 25% of caregivers are 20+ min away) | 0.25 | Largest single lever. If the true remote-child share is 0.15, SAM population drops to ~1.2M and DTC ceiling to ~$500M/yr |
| 3 | Share of remote-child households able/willing to fund $30-50/mo | 0.60 | If 0.40, SAM population ~1.3M |
| 4 | Blended annual subscription for sizing | $420/yr | Anchored to PERS actuals; if the product must price at the $37/mo band ($444) the figure is stable; a premium price above the anchor reduces penetration not price realized |
| 5 | Realistic mature DTC penetration of SAM | 5-10% | PERS is 9% and flat; a pricier product likely lower. Drives SOM |
| 6 | Institutional channels reach the ~1.0M senior-living residents and agency clients, distinct from the DTC funnel | count | Channel sizing, section 1.3 |

All four funnel multipliers (assumptions 1-3) are inherited-or-derived judgments, not measured cross-tabs. They are flagged per framework section 5.8.

## Confidence Summary

Overall confidence: **MEDIUM-HIGH on the strategic conclusions, MEDIUM on the SAM magnitude, HIGH on the competitive and reimbursement findings.**

- **Strongest (HIGH):** the competitive landscape and the failure post-mortems (all from primary announcements, SEC filings, and dated press); the reimbursement tension (airtight from FDA general-wellness guidance + CMS 201(h) requirement); the top-of-funnel living-alone count (ACL/Census); the channel ranking direction.
- **Medium:** the SAM dollar magnitude (rests on three assumed funnel multipliers, section Assumptions); DTC pricing band; MA supplemental-benefit trend.
- **Weakest (LOW / UNKNOWN):** PERS churn (unavailable, blocks LTV), per-bed institutional pricing (unavailable, blocks best-channel sizing), real category DTC CAC. These three gaps are the reason the phase cannot yet produce a defensible LTV:CAC, which is a Phase 8 dependency.

The kill-relevant conclusion is robust to the weak cells: even at the optimistic end of every assumption, DTC alone tops out at a low-hundreds-of-millions revenue ceiling, the two closest product analogs (Alexa Together dashboard, Cherry Home camera) are dead, and the largest revenue pool (reimbursement) is legally foreclosed by the wellness positioning. The channels that work (operator per-bed, agency) require abandoning the DTC/consumer-dashboard thesis that the concept currently centers on.


===================================================================
# (phase8_businesscase.md)
===================================================================

# Concept A, Phase 8: Business Case and Capital

Governed by `00_framework.md` (section 4 cost model, section 5 evidence, section 6 output, section 9 registers) and `01_concept_a_elder_monitoring.md` (Phase 8). Builds on and does not re derive: hardware COGS and NRE in `research/a/phase3_hardware.md`; burn, headcount, timeline, and comparables in `research/a/phase6_devplan.md`; market sizing, channel ranking, competitor post mortems, willingness to pay, and the reimbursement tension in `research/a/phase7_market.md`; the recurring cloud cost in `research/shared/shared_infra_cost.md`; the funding landscape in `research/shared/shared_capital_landscape.md`; and the risk precedents in `research/regulatory_risk_register.md` (risks R1 through R9).

New citation keys are `[F#]` and resolve in Register Entries. Prior keys resolve in their source files. Confidence tags HIGH, MEDIUM, LOW per framework section 5. Every operating assumption that is not a sourced finding is flagged in Assumptions Made and carried as such, not asserted as fact. Where Phase 7 marked a value UNKNOWN (PERS churn, per bed price, real DTC CAC), it is treated as an assumption here, flagged, never as a finding.

The central inherited constraint, established in Phase 7 and not relitigated: the largest revenue pool in aging in place (RPM and RTM reimbursement) is legally foreclosed by the general wellness positioning, and the two closest consumer product analogs (Amazon Alexa Together dashboard, Cherry Home camera) are dead. The business case is built on the channels that survive: senior living operators (per bed), home care agencies, and payers (per member). DTC is modeled for contrast and to size the ceiling, not as the recommended path.

---

## 0. Operative economics, stated before any scenario

Every downstream number rests on the per subscriber monthly economics below. Sourced inputs are labeled. Every unsourced input is an explicit assumption, flagged here and in Assumptions Made. A "home" or "subscriber" is the 13 device, 5 zone system costed in Phase 3.

### 0.1 Recurring monthly unit economics (base case, mid tier scale, per home per month)

| Line | Consumer DTC | Operator per bed | Payer per member (PMPM) | Basis |
|---|---|---|---|---|
| ARPU per month | $35 | $30 | $12 | Consumer anchored to PERS band $25 to $50, midpoint $37 [Phase 7 6.1]; operator and PMPM are assumptions, flagged |
| Cloud and inference COGS | $2.00 | $2.00 | $2.00 | `shared_infra_cost` mid tier $1 to $3 [HIGH] |
| PERS monitoring seat (buy not build) | $5.00 | $4.00 | $4.00 | ASSUMPTION, Phase 4/7 UNKNOWN; buy the 24/7 escalation, do not build it |
| Support and field ops allocation | $4.00 | $3.00 | $2.00 | ASSUMPTION |
| Payment and channel processing | $1.00 | $1.00 | $1.00 | ASSUMPTION (approx 3 percent) |
| Recurring COGS total | $12.00 | $10.00 | $9.00 | |
| Recurring gross profit per month | $23 (66%) | $20 (67%) | $3 (25%) | |

PMPM economics differ in kind: the payer pays per covered member across an attributed population, most of whom carry no device, so the $12 PMPM figure is thin per monitored home but is applied to a large member base. Its attractiveness is contract size and near zero per member CAC once contracted, not per unit margin. Flagged.

### 0.2 Hardware treatment across the pricing models

Hardware COGS per home from Phase 3: $452 at 100 units, $327 at 1k, $254 at 10k, $201 at 100k. The hardware is a one time cost recovered differently under each pricing model (section 2). Category norm, established in Phase 3 and Phase 7, is hardware near cost with margin taken in subscription.

### 0.3 Churn and CAC, the two values Phase 7 could not source

| Input | Planning value | Status | Impact if wrong |
|---|---|---|---|
| Consumer monthly churn | 2.0% (approx 24 to 30 month life) | ASSUMPTION. Phase 7: PERS churn UNKNOWN, held in private filings. The single largest LTV lever | At 3.5% churn consumer LTV falls approx 40 percent and DTC LTV:CAC breaks |
| Operator and payer annual churn | 10 to 15% per year (approx 1% per month, annual contracts) | ASSUMPTION. B2B contracts are stickier than consumer | Lower churn is the structural reason B2B beats DTC here |
| Consumer CAC (blended paid) | $200 marketing plus hardware subsidy | ASSUMPTION anchored to Phase 7 band $150 to $400+ | The Alexa Together failure is the warning; if true CAC is $350 DTC is unviable |
| Operator CAC (per bed, amortized over a multi bed contract) | $50 to $120 per bed | ASSUMPTION; the sale is to the operator, amortized across beds | Long sales cycle (6 to 12 months) is the real cost, not per bed dollars |

Consumer LTV at base case: $23 per month gross profit times 26 month life equals approx $600 gross, less an approx $30 hardware subsidy at 1k volume, yields LTV:CAC of approx 1.4x at a $200 CAC after hardware. That is thin, exactly the DTC caution from Phase 7. Operator LTV at $20 per month times a 4 to 6 year facility relationship is materially higher against a lower per bed CAC, which is why the recommended channel is B2B.

---

## 1. Three scale scenarios (framework section 4)

Scale tiers align with `shared_infra_cost` (300, 5,000, 50,000 subscribers) so the cloud cost per user is carried, not re derived. Headcount builds on the Phase 6 team (3 engineers to G4, a 4th at G3). Burn, capital, and breakeven are modeled; every figure is a planning estimate, MEDIUM confidence, not a quote.

### 1.1 P&L shape and capital at each scale (recommended B2B blend: operator per bed plus some payer, blended ARPU approx $31 per month, recurring gross margin approx 66%)

| Line | Small (300 homes) | Mid (5,000 homes) | Large (50,000 homes) |
|---|---|---|---|
| Gate context | G4 pilot to early G5 | G5 limited commercial | G6 full commercial |
| Annual recurring revenue | approx $112K | approx $1.9M | approx $18.6M |
| Recurring gross profit (66%) | approx $74K | approx $1.25M | approx $12.3M |
| Headcount | 5 to 6 | 16 to 20 | 45 to 60 |
| Annual opex (fully loaded, incl. S&M) | approx $1.6M | approx $6.0M | approx $17.5M |
| One time hardware subsidy on new adds | approx $10K to $40K | approx $0.6M to $1.2M | approx $3M to $6M |
| Annual net burn | approx $1.5M | approx $4.5M to $5.5M | approx breakeven to approx ($4M) |
| Cumulative capital to reach and sustain this scale | approx $3M to $5M | approx $14M to $22M | approx $30M to $45M |
| Months to company cash flow breakeven | not reachable at this scale | not reachable at this scale | approx month 60 to 84 from start, at approx 18K to 28K subscribers |

Reading, and it is blunt:

1. Small (300) is pre commercial. Revenue does not cover a fraction of the engineering burn. This scale exists to prove the product (G4), not to earn. Fund it with non dilutive plus seed, not with revenue.
2. Mid (5,000) is a real but sub scale business. At approx $1.9M ARR against a $6M opex it still burns approx $5M per year. This is the "valley" scale where most category comparables stalled or soft landed (Cherry, Tellus, Phase 7). It is a fundraising waypoint, not a destination.
3. Large (50,000) is where recurring gross profit (approx $12M) finally approaches the opex base and the business can reach cash flow breakeven if growth spend is throttled. Company level breakeven arrives not at 50,000 but earlier, at roughly 18,000 to 28,000 subscribers, when recurring gross profit covers a stabilized opex base. In the recommended B2B path that is roughly 18,000 to 28,000 beds under contract.

### 1.2 The DTC contrast scenario (for the ceiling, not recommended)

At the same scales on the consumer model (ARPU $35, CAC $200 plus hardware, churn 2% per month), the large scenario tops out near the Phase 7 DTC ceiling: 50,000 homes is approx $21M ARR, and the Phase 7 SAM math caps a well executed DTC only business at approx $40M to $80M ARR at maturity (5 to 10 percent of a $840M SAM). The killing feature of DTC is not the ceiling, it is the CAC to churn ratio: at a 1.4x LTV:CAC the model cannot fund its own growth, which is precisely why Amazon, with the lowest CAC on earth, discontinued the identical dashboard subscription (Phase 7 2.2). DTC is a supplement to a B2B core, not the core.

### 1.3 Scenario headline

| Scenario | Recommended interpretation |
|---|---|
| Small | Prove it. Non dilutive plus seed funds a 300 home G4. No revenue thesis. |
| Mid | Bridge it. 5,000 beds proves the operator motion; still burns approx $5M per year; a Series A waypoint. |
| Large | Earn it. Cash flow breakeven at approx 18K to 28K beds, approx $30M to $45M cumulative capital, approx 5 to 7 years from start. |

---

## 2. Pricing model options, each modeled

Five models per the brief. Modeled on the base case unit economics (section 0). The metric that decides is contribution per home over the first 24 months, net of hardware.

| Model | How it works | Yr 1 + Yr 2 contribution per home (approx) | Friction / conversion | Verdict |
|---|---|---|---|---|
| 1. Hardware plus subscription (unsubsidized) | Hardware at approx 2x COGS ($500 to $650 retail) plus $35 per month | Highest gross (hardware margin approx +$150 plus 2x $276 subscription GP) but | Highest upfront friction; a $500+ box in a market anchored to $199 to $449 kits kills conversion (Phase 3, Phase 7) | REJECT for consumer. Only viable if an operator or payer pays the hardware |
| 2. Hardware subsidized plus subscription | Hardware at approx $299 (below COGS at low volume), $35 per month | approx ($30) hardware at 1k volume, +$552 subscription GP over 24 mo, net approx +$522 | Moderate friction; matches CarePredict ($449 kit) and Envoy ($399 kit) [Phase 3] | VIABLE consumer default; the standard category posture |
| 3. Hardware free, long subscription commitment | $0 hardware, 24 to 36 month commitment at $40 per month | Full COGS ($201 to $327) is CAC; recovered by month 9 to 14; net positive only if the commitment holds | Lowest upfront friction, highest churn exposure; a broken commitment is an unrecovered hardware loss | VIABLE only with enforced term and low churn; dangerous at consumer churn of 2%+ per month |
| 4. Per bed per month to an operator | Operator buys/leases hardware or it is bundled; $25 to $35 per bed per month; multi bed contracts | approx $20 per bed per month GP times bed count; hardware absorbed by contract; low per bed CAC | Long sales cycle (6 to 12 mo), pilot gated; but the operator carries fall liability and has a hard financial reason to pay | RECOMMENDED. SafelyYou, Inspiren, Sage all monetize exactly here [F1][Phase 7] |
| 5. Per member per month to a payer | MA plan or LTC insurer pays $8 to $15 PMPM across attributed members; device to a subset | Thin per member, large aggregate; near zero per member CAC once contracted | Longest cycle (12 to 24 mo, annual bid), MA supplemental PERS is contracting in 2025 (Phase 7) | SECONDARY. Large prize, slow and timing risked; pursue after operator traction |

### 2.1 Pricing decision

Primary: model 4, per bed per month to senior living and assisted living operators. It is the only model where the buyer is concentrated (approx 1,000 operators control most of 1.2M beds, Phase 7 3), the buyer is financially motivated (owns fall liability), the margin is high (approx 67 percent recurring), churn is low (annual facility contracts), and the hardware cost is absorbed by the contract rather than fought over at a consumer checkout. Every recent large check in the category landed on a company selling this way (section 3).

Secondary: model 5 (payer PMPM) as the scale prize once operator efficacy data exists. Tertiary: model 2 (subsidized hardware plus subscription) as a DTC supplement for the remote adult child who will not wait for an operator, sold through the operator or agency relationship rather than paid search. Model 1 is rejected. Model 3 is held for a payer or operator subsidized variant only, never at open consumer churn.

---

## 3. Capital plan, non dilutive first

Sequenced against the gates (Phase 6 1.2). Non dilutive leads because every category survivor did exactly this (SafelyYou funded its early science with CITRIS plus NIA SBIR before any venture round, Phase 6 4). The dilutive rounds are sized to the Phase 6 all in cost to G4 (approx $1.8M to $2.0M) and the section 1 capital to scale.

### 3.1 The raise sequence

| Stage | Gate | Instrument | Target amount | Use | Evidence it is real |
|---|---|---|---|---|---|
| Non dilutive 1 | G1 to G2 | NSF SBIR Phase I (26-510) | up to $305K | The sensing, fusion, and on device model engineering, framed as deep tech, no clinical claim (fits the wellness lane) | NSF 26-510 [shared_capital 1.4] |
| Non dilutive 2 | G2 | NIA SBIR Phase I (R43) | up to $300K, or $500K under an AD/ADRD framing | Founder home to friends and family; characterize the field false positive rate | NIA mandate for aging in place; NIA deploys >$140M per year non dilutive [F4]; SafelyYou used exactly this [Phase 6 4] |
| Angel / pre seed | G2 | SAFE or priced | $500K to $1.5M | Bridge the 3 engineer team through G2/G3; the discipline floor is 3 (Phase 6 2.3) | Rosarium Health $6M seed for aging at home, May 2026 [F2] shows seed capital present for the category |
| Seed | G3 | Priced | $3M to $6M | The 4th engineer on the false positive critical path; 5 to 15 home G3; first operator pilots | Category seed and A activity live (below) |
| Non dilutive 3 | G4 | NIA SBIR Phase II (R44) | up to $2.0M, or $2.5M AD/ADRD | The 50 to 200 unit structured cohort; efficacy evidence; FTC gait substantiation study | A 2025 NIA Phase II fall detection aging in place award ran $1,230,163 [F5] |
| Non dilutive 4 | G4 | NSF SBIR Phase II | up to $1.25M | Scale hardening of the sensing and fusion stack | NSF 26-510 [shared_capital 1.4] |
| Series A | G4 to G5 | Priced | $12M to $18M | Certification, manufacturing scale, operator sales motion, scale to mid then toward breakeven | Direct comparables below |
| Series B / growth | G6 | Priced | $25M+ | Scale to the large scenario and breakeven | Inspiren $100M, Sage $65M (below) |

Non dilutive potential across NSF and NIA is approximately $3.3M to $4.6M (both agencies, both phases), which can fund the entire path from G1 to G4 with only a modest angel/pre seed bridge, sharply reducing early dilution. This is the single most important capital move for a hardware plus wellness company that cannot touch reimbursement. Caveat, from `shared_capital`: SBIR/STTR authority lapsed 2025-10-01 and was reportedly reauthorized 2026-04-13 with NOFOs re released 2026-05-29 and the next NIH receipt date 2026-09-05; confirm against SBA.gov before relying on timing. A wellness only framing may also score worse at NIH review (which favors a health outcome hypothesis), which argues for leading the sensing/AI work through NSF, which does not want a clinical claim.

### 3.2 Actual recent deals as thesis evidence (last 24 months, aging in place), beyond the shared file

New evidence pulled this phase, added to the shared file's Inspiren, SafelyYou, and Nobi rows:

| Company | What it does | Round / lead | Amount | Date | Signal for this business |
|---|---|---|---|---|---|
| Sage | AI, privacy conscious fall monitoring (Sage Detect) for senior living; per community model | Series C, Growth Equity at Goldman Sachs Alternatives (lead), IVP, Goldcrest | $65M (total $124M) | 2026-03-05 | The freshest, largest proof that operator sold, privacy conscious fall monitoring is fundable at growth scale; claims 50% fall reduction and $275 NOI per resident per month [F1] |
| Inspiren | AI resident safety and eCall monitoring for senior living | Series B, Insight Partners lead | $100M (total $155M) | 2025-09-25 | Growth capital present specifically for operator monitoring [shared_capital 4.1] |
| SafelyYou | Ceiling camera fall AI, memory care | Series C, Touring Capital lead | $43M | 2025-01-28 | Per bed operator model, funded early by NIA SBIR then venture [shared_capital; Phase 6 4] |
| Nobi | Smart light (ceiling) fall detection, B2B senior care | Series B, Angelini and Nexus NeuroTech co lead | EUR 35M (approx $37M) | 2025-01-28 | The direct ceiling light analog; lives in B2B, not DTC [shared_capital] |
| Rosarium Health | Aging at home assessments, home modification, fall prevention; MA and Medicaid partnerships | Seed | $6M | 2026-05 | Seed capital and payer/Medicaid channel interest are live for aging at home [F2] |
| Palarum | eTextile wearable fall prevention, clinical settings | Series A | $13.6M | 2025-05 | Fall prevention hardware raises A rounds, though in the clinical (not wellness) lane [F3] |

The pattern is uniform and confirms the Phase 7 channel finding: the capital flows to operator and facility sold fall monitoring (Sage, Inspiren, SafelyYou, Nobi), not to consumer dashboards. The recommended pricing model (per bed) is the one the market is funding right now.

---

## 4. Milestone to unlock map (per gate)

| Gate | What it proves | Who cares | Conversation it opens | What it is worth |
|---|---|---|---|---|
| G1 Bench | Core fall, long lie, gait, and ADL detection runs at stated accuracy on real data | NSF reviewers; a technical angel | NSF SBIR Phase I; the first credible technical pitch | approx $305K non dilutive; a pre seed at idea/tech valuation |
| G2 Self test | 30 days uptime and a characterized real world false positive rate (the make or break number, Phase 6 3) | NIA reviewers; pre seed angels; the first design partner | NIA SBIR Phase I; angel/pre seed | approx $300K to $500K non dilutive plus a $0.5M to $1.5M pre seed |
| G3 Friends and family | Install time, retention, and per home false positive rate across varied real geometry | Seed VCs; senior living operators evaluating a pilot | Seed round; first paid operator pilot LOI | $3M to $6M seed; the pilot LOI is the asset that de risks it |
| G4 Pilot | Efficacy evidence (fall reduction, response time), unit economics, certification underway, gait claim FTC substantiated | Series A VCs (Touring, Insight class); operators ready to contract; NIA Phase II | Series A; NIA/NSF Phase II; multi bed operator contract | $12M to $18M Series A plus approx $3M non dilutive; a signed per bed contract is the valuation driver |
| G5 Limited commercial | FCC and triple UL/ETL complete; positive contribution margin per subscriber; support exists | Operators buying at scale; payers evaluating PMPM | Multi operator rollout; first payer PMPM pilot | First real ARR; the operator ARR multiple sets the mark |
| G6 Full commercial | Target CAC and LTV; scaled manufacturing; channel established | Growth investors (Goldman Growth Equity, Insight class); acquirers (ADT model, Phase 7) | Series B/growth; strategic acquisition | $25M+ growth round; Sage ($124M raised) and Inspiren ($155M) are the comparables [F1] |

The load bearing move is at G2 to G4: a characterized false positive rate (G2) plus a signed operator pilot (G3/G4) plus efficacy data (G4) is the exact package that unlocks a Series A in this category, and it is what SafelyYou, Inspiren, Nobi, and Sage each proved before their large rounds.

---

## 5. Risk register

Technical, regulatory, commercial, and existential. Likelihood is the probability of materializing before G6 absent mitigation; impact is the worst credible outcome. Regulatory rows cross reference `regulatory_risk_register.md` (R1 to R9) and are not re derived.

| ID | Category | Risk | Likelihood | Impact | Mitigation | Leading indicator |
|---|---|---|---|---|---|---|
| B1 | Technical (the kill risk) | Field false positive rate cannot be driven low enough; the product gets unplugged in month two. Lab fall accuracy collapsed from approx 94% to approx 57% in the field, with up to 84 alarms of which 83 were false in one deployment (Phase 6 3) | HIGH | SEVERE | The entire Phase 6 ground truth plan: staged falls for sensitivity, one tap adjudication for precision, duration gating, modality fusion (radar plus camera plus mesh). Characterize at G2, refine across G3 homes. The 4th engineer lands here | Escalated false positives per home per month not falling below target across G2/G3; sensitivity dropping as thresholds tighten |
| B2 | Technical | IMX500 model fit fails; camera node moves to a costlier SoC and a weaker privacy claim (Phase 3 OQ1) | MEDIUM | MODERATE | Fallback to Ambarella CV25 or RK3576; the privacy claim degrades from "pixels never leave the sensor" to "no video leaves the home" | Phase 4 pose model does not fit IMX500 in package memory at 30 fps at G1 |
| B3 | Regulatory | FDA device creep: a wellness output drifts into a screening claim, leaving the general wellness lane (cross ref R1) | MEDIUM | SEVERE | Claims linter in CI blocks any named disease inference from passive data; input vs inference line enforced in software, not prompts | A Warning Letter to a comparable wellness monitor; a competitor forced to file a 510(k) for a shipped feature |
| B4 | Regulatory | FTC substantiation: the gait speed measurement claim is unvalidated against an instrumented walkway (cross ref R2) | HIGH | HIGH | Fund the instrumented walkway validation study at G4 ($30K to $80K, Phase 6); ship un validated metrics as own baseline trends without an accuracy claim | Internal validation error bars wider than the smallest claimed change; an FTC action naming a measurement app |
| B5 | Regulatory | State biometric privacy (BIPA/CUBI/MHMDA): gait signature, face geometry, voiceprint from in home capture; per subject statutory damages (cross ref R4) | HIGH | SEVERE | Consent architecture as a first class feature; on device (T1) inference so raw biometrics never leave the home; encrypted templates with a deletion trigger; geofence by state | A BIPA/CUBI class filing against any home monitor; plaintiff firm intake ads in Illinois |
| B6 | Regulatory | All party consent audio from the assistant and acoustic sensing (cross ref R6) | MEDIUM | HIGH | Wake word gated capture, on device STT, immediate raw audio discard, visible recording indicator, opt in mic, geofence by consent regime | A wiretap complaint against a home voice device; a visitor complaint in G3/G4 |
| B7 | Regulatory / commercial (existential) | Reimbursement foreclosure: the wellness positioning cannot bill RPM/RTM, removing the largest revenue pool. The central strategic tension (Phase 7 4.2) | HIGH (certain, structural) | HIGH | Do not chase reimbursement. Live on operator per bed, agency, and payer PMPM (none of which require device status). Optionally partner an FDA device RPM vendor to sell the wellness layer adjacent, never inside | It is not a future event; it is a present constraint that caps the revenue map |
| B8 | Commercial | DTC CAC to churn ratio does not close (LTV:CAC approx 1.4x base case); the Alexa Together and Cherry Home graveyard (Phase 7 2.2) | HIGH (for a DTC led strategy) | SEVERE (for DTC), LOW (for the recommended B2B strategy) | Do not lead with DTC. Lead with operator per bed where CAC is low and churn is annual contract bound. Treat DTC as an operator/agency sourced supplement | Blended DTC CAC above approx $250; consumer monthly churn above approx 3% in any cohort |
| B9 | Commercial | Operator sales cycle is long (6 to 12 mo) and pilot gated; cash burns while contracts close | MEDIUM | HIGH | Fund the gap with non dilutive plus seed; run multiple operator pilots in parallel; use the AgeTech Collaborative (AARP) for warm operator access (shared_capital 3) | Pilot to contract conversion below plan; sales cycle exceeding 12 months |
| B10 | Existential | Category history: every DTC consumer play stalled or soft landed; nobody reached a fundable pilot in under approx 6 years (Phase 6 4) | MEDIUM | SEVERE | Build for the B2B pilot from G4; plan 5 to 7 years and approx $30M+ to breakeven, not a lean fast DTC timeline; sequence non dilutive first | Burn outrunning the milestone map; a Series A thesis that rests on DTC |
| B11 | Existential | Single vendor dependency (Sony IMX500, TI radar, a PERS monitoring partner) revoked or repriced (cross ref R7 pattern) | LOW to MEDIUM | HIGH | Abstract the sensing and monitoring layers so vendors are swappable; qualify a second radar and a second monitoring partner before G5 | A vendor deprecation notice, NDA price hike, or acquisition of a supplier by a competitor |

---

## 6. Kill criteria, stated in advance

A business case without kill criteria is a pitch. These are the findings that would make Concept A not worth building, ordered by how early and how decisively they resolve.

| # | Kill criterion | Gate it resolves at | Why it kills |
|---|---|---|---|
| K1 (primary) | The escalated false positive rate cannot be driven below approx 1 per home per month without sensitivity falling below the level a paying operator will accept, after the full Phase 6 ground truth effort | G2, confirmed G3 | This is the "unplugged in month two" failure. The literature says lab accuracy collapses in the field (Phase 6 3); if it cannot be fixed, there is no product, regardless of everything else. Nothing downstream matters if K1 fails |
| K2 | No senior living operator, home care agency, or payer will sign a per bed or PMPM pilot at a price that yields positive contribution margin, after a characterized false positive rate and efficacy data exist | G3 to G4 | The recommended channel is the only venture scale path (Phase 7). If the motivated, liability bearing buyer will not pay at margin, the remaining option is DTC, which K3 covers |
| K3 | DTC is the only available channel, and blended DTC CAC exceeds approx $250 against consumer churn above approx 3% per month | G3 to G4 | This is the Alexa Together outcome with real CAC. A sub 1.3x LTV:CAC on a bounded ceiling ($40M to $80M ARR, Phase 7) is not a venture business and cannot fund its own growth |
| K4 | The gait speed measurement cannot be substantiated against an instrumented walkway within the error bars the claim requires (FTC, R2/B4), and removing the gait claim collapses the differentiation versus a cheaper PERS or single node radar competitor | G4 | If the only defensible differentiator over a $250 Vayyar node or a $37 per month PERS is unvalidated, the added hardware cost (Phase 3: radar plus camera are approx 68% of BOM) is not justified |
| K5 | A regulatory shift (FDA lane narrowing per R1/B3, or a state biometric ruling per R4/B5) makes the core passive in home biometric capture legally untenable at acceptable cost | any gate | The product is in situ biometric capture in the home; if the legal envelope closes, the cost of compliance (or the tail liability) exceeds the business value |

If K1 fails, stop. If K2 and K3 both fail, the venture case is dead even if the technology works. K4 and K5 reshape rather than always kill, but each can be terminal in combination.

---

## Register Entries

Per framework section 9, staged for the register owner. This phase does not edit `research/registers/`. New funding evidence and sources this phase:

### Funding (stage into registers/funding.md)

| Investor / event | Deal | Amount | Date | Thesis signal | Confidence |
|---|---|---|---|---|---|
| Growth Equity at Goldman Sachs Alternatives (lead), IVP, Goldcrest | Sage Series C | $65M (total $124M) | 2026-03-05 | Operator sold, privacy conscious fall monitoring is fundable at growth scale | HIGH |
| Seed investors (Rosarium Health) | Seed | $6M | 2026-05 | Aging at home plus MA/Medicaid channel; seed capital live | MEDIUM |
| Series A investors (Palarum) | Series A | $13.6M | 2025-05 | Fall prevention hardware raises A rounds (clinical lane) | MEDIUM |
| NIH / NIA SBIR-STTR | Program (non dilutive) | >$140M per year deployed; a 2025 aging in place fall detection Phase II award ran $1,230,163 | 2025 | Non dilutive lead for aging in place; the SafelyYou path | HIGH |
| (carried) Insight Partners; Touring Capital; Angelini/Nexus | Inspiren $100M; SafelyYou $43M; Nobi EUR 35M | as logged | 2025 | Operator monitoring is the funded thesis | HIGH |

### Sources (stage into registers/sources.md)

| Key | Source | URL | Date | Used for | Credibility |
|---|---|---|---|---|---|
| F1 | Sage Raises $65M Series C Led by Goldman Sachs Alternatives | https://www.prnewswire.com/news-releases/sage-raises-65m-series-c-led-by-goldman-sachs-alternatives-to-redefine-care-for-americas-aging-population-302705363.html ; https://seniorhousingnews.com/2026/03/05/ai-platform-sage-raises65m-in-new-equity-round-led-by-goldman-sachs-alternatives/ ; https://am.gs.com/en-hk/advisors/news/press-release/2026/sage-growth-equity | 2026-03-05 / accessed 2026-07-10 | Sage $65M Series C, $124M total, IVP + Goldcrest, Sage Detect, 50% fall reduction, $275 NOI/resident/mo | HIGH (co + investor press) |
| F2 | Startup Enabling Aging at Home Raises $6M (Rosarium Health) | https://medcitynews.com/2026/05/aging-home-funding-rosarium/ | 2026-05 / accessed 2026-07-10 | Rosarium $6M seed, aging at home, MA/Medicaid partnerships, fall prevention/home modification | MEDIUM (trade) |
| F3 | Palarum $13.6M Series A (eTextile fall prevention) | fiercehealthcare fundraising tracker '26; Palarum press | 2025-05 / accessed 2026-07-10 | Palarum $13.6M Series A, smart textile fall prevention, clinical | MEDIUM |
| F4 | About NIA Small Business Funding | https://www.nia.nih.gov/research/sbir/about-nia-small-business-funding ; https://www.nia.nih.gov/news/topics/nia-funded-small-business-spotlights | accessed 2026-07-10 | NIA deploys >$140M/yr non dilutive; SafelyYou NIA SBIR spotlight | HIGH (primary gov) |
| F5 | NIA SBIR fall detection aging in place Phase II award | https://www.sbir.gov/awards/215117 | 2025 / accessed 2026-07-10 | 2025 NIA Phase II aging in place fall detection award $1,230,163 | MEDIUM (gov award record, single) |

No source is older than 18 months. Carried funding rows (Inspiren, SafelyYou, Nobi, NSF/NIA/NICHD program mechanics) resolve in `shared_capital_landscape.md`.

---

## Open Questions

1. PERS/monitoring subscription churn is UNKNOWN (Phase 7 OQ1), held in private filings. Every LTV, breakeven, and DTC viability number here rests on the assumed 2% per month consumer / 10 to 15% per year B2B churn. This is the single most material gap. Blocks a defensible LTV:CAC.
2. Senior living per bed per month monitoring price is UNKNOWN (Phase 7 OQ2). SafelyYou, Inspiren, Sage publish nothing per bed. The recommended pricing model's absolute revenue rests on an assumed $25 to $35 per bed. Requires direct RFQ or an operator conversation.
3. Real category DTC CAC is UNKNOWN (Phase 7 OQ3). The $200 assumption drives the DTC contrast; if true CAC is $350, DTC is dead earlier.
4. PERS monitoring partner per seat cost is UNKNOWN (Phase 4/6). It is a recurring COGS line ($4 to $5 assumed) and moves the recurring gross margin.
5. SBIR/STTR reauthorization timing (lapsed 2025-10-01, reportedly reauthorized 2026-04-13) is single source (shared_capital OQ1). Confirm against SBA.gov before modeling non dilutive runway.
6. Whether a general wellness framing weakens NIH SBIR competitiveness (shared_capital OQ3). May force leading the sensing work through NSF. Untested.
7. FTC gait substantiation study cost ($30K to $80K) is an estimate, not a quote (Phase 6 OQ5). It sits in the G4 capital line.
8. Company cash flow breakeven at approx 18K to 28K subscribers assumes the section 0 unit economics hold at scale and that growth spend is throttled. It is a modeled inflection, not a bottom up operating plan.

## Assumptions Made

| # | Assumption | Value | Impact if wrong |
|---|---|---|---|
| 1 | Consumer monthly churn | 2.0% | Highest sensitivity. At 3.5% consumer LTV falls approx 40% and DTC breaks. B2B less exposed |
| 2 | B2B annual churn | 10 to 15% | The structural reason B2B beats DTC; higher churn narrows the gap |
| 3 | Consumer CAC (blended, ex hardware) | $200 | At $350 DTC LTV:CAC falls below 1.0; K3 triggers |
| 4 | Operator CAC per bed | $50 to $120 | The real cost is the sales cycle length, not per bed dollars |
| 5 | PERS monitoring seat (recurring COGS) | $4 to $5 per month | Moves recurring gross margin by approx 10 points |
| 6 | Support + ops + processing (recurring COGS) | $6 to $7 per month | Modeled, not quoted |
| 7 | Blended ARPU (recommended B2B) | approx $31 per month | Drives all scenario ARR; anchored to PERS band and assumed per bed price |
| 8 | Headcount and opex at each scale (5 to 6 / 16 to 20 / 45 to 60) | modeled | Drives burn and breakeven timing; built on the Phase 6 team |
| 9 | Cash flow breakeven at approx 18K to 28K subscribers | modeled inflection | If unit economics are weaker, breakeven scale and capital rise |
| 10 | Non dilutive is winnable and additive (NSF + NIA, both phases, approx $3.3M to $4.6M) | planning | If SBIR is not won or timing slips, dilutive need rises by that amount at the earliest, most expensive gates |
| 11 | Hardware COGS, NRE, and cloud cost per user carried unchanged from Phase 3 and shared_infra_cost | as logged | If BOM or cloud assumptions move, contribution margin moves |
| 12 | Reimbursement remains foreclosed under the wellness positioning (Phase 7 4.2), treated as fixed | fixed | If a compliant reimbursement bridge opens, the revenue map expands materially (upside, not downside) |

## Confidence Summary

Overall confidence: HIGH on the strategic conclusions and the capital plan, MEDIUM on the absolute scenario numbers, LOW on the three values Phase 7 could not source (churn, per bed price, DTC CAC), which are carried as flagged assumptions.

- Strongest (HIGH): the pricing decision (per bed per month to operators) and the capital sequence (non dilutive first, then seed, then a $12M to $18M Series A at G4), both corroborated by fresh, dated, named deals (Sage $65M Series C March 2026, Inspiren $100M September 2025, SafelyYou $43M January 2025, Nobi EUR 35M January 2025) and by the Phase 7 channel ranking. The kill criteria, led by K1 (field false positive rate), are robust and inherited from the Phase 6 critical path.
- Medium: the three scenario P&L shapes, the approx $30M to $45M cumulative capital to breakeven, and the approx 18K to 28K subscriber breakeven inflection. These are internally consistent planning models built on sourced COGS and cloud costs plus flagged operating assumptions, not an operating plan.
- Weakest (LOW / UNKNOWN): PERS churn (blocks a hard LTV:CAC), per bed price (blocks precise recommended channel ARR), and real DTC CAC. All three are Phase 7 open questions carried forward; none was invented.

The load bearing conclusion, HIGH confidence and robust to the weak cells: fund the path from G1 to G4 primarily with NSF and NIA SBIR (approx $3M to $4M non dilutive) plus a modest seed, build for a senior living operator pilot rather than DTC, price per bed per month, and plan for approx $30M cumulative capital and 5 to 7 years to cash flow breakeven at roughly 18K to 28K beds. The venture dies first at K1 (the field false positive rate); it dies second if no operator or payer will pay at margin (K2); and a DTC led strategy dies at K3 the way Amazon Alexa Together already did. Reimbursement, the largest pool, stays foreclosed by the positioning and is designed around, not chased.


===================================================================
# (CONCEPT_A_BUSINESS_CASE.md)
===================================================================

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

