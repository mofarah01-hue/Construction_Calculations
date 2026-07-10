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
