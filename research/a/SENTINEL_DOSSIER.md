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
