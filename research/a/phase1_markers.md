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
