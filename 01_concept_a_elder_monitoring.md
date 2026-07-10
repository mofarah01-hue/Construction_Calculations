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
