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
