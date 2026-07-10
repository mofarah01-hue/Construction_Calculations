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
