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
