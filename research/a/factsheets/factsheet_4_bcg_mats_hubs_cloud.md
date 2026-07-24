# FACT SHEET 4: Contactless Sensors (BCG bed/seat mats), Hub Compute, Cloud Cost, Smart Displays

Raw working fact sheet from the Phase 2 architecture research. Prepared 2026-07-10. Estimates labeled.

## 1. Under-mattress / bed BCG sensors and seat-pad BCG

### Consumer / clinical products
Emfit QS (under-mattress piezo/ferroelectret BCG, Finland)
- Measures HR, HRV, respiration, sleep stages, movement, time-in-bed, bed-exit. [emfit.com, 2026, HIGH]
- HR/RR validation vs ECG: 33-patient study, 95% limits of agreement for HR -4.4 to +4.4 bpm; respiration -2.5 to +2.2 breaths/min; comparable to consumer chest straps. [ResearchGate 330118781, 2018/2019, HIGH]
- Independent BCG-vs-PSG validation of the sensor class in J Clin Sleep Med. [jcsm.aasm.org 10.5664/jcsm.9754, 2022, HIGH]. Sleep-stage accuracy mediocre. [MEDIUM]
- Price: CA$420, no subscription. [Mattress Miracle, 2025, MEDIUM]. USD list UNKNOWN (approx US$310-340, LOW).

Withings Sleep Analyzer (under-mattress pneumatic + BCG)
- Measures HR via BCG, respiration, movement, snoring, sleep stages, breathing-disturbance/apnea index. [MedGrade, 2025, HIGH]
- Validation in OLDER ADULTS: 35 community-dwelling adults aged 65-83, 1-night PSG, reliable HR and breathing-rate agreement. [PMC11387924, 2023/2024, HIGH]
- Apnea detection: 88% sensitivity / 88.6% specificity for AHI >=15; HR within ~2 bpm of ECG. [PMC8314651, 2021, HIGH]
- Price: US$199.95 (Withings) / ~US$165 Amazon. [Withings US; Tom's Guide, 2025, HIGH]

EarlySense (acquired by Hillrom/Baxter 2021, piezoelectric under-mattress)
- Measures continuous HR and RR, contactless, plus bed-exit/motion; clinical (hospital beds). [PRNewswire, 2021, HIGH]
- Validation vs PSG: 96.1% (HR), 93.3% (RR). [PMC5337599, HIGH]. FDA 510(k) cleared (K180079, K171836). [HIGH]
- Price: clinical/OEM, UNKNOWN.

Beddit (Apple, under-mattress strip): DISCONTINUED. Apple stopped selling 2022; removed apps Sept 2024. [9to5Mac, 2024, HIGH]

Sleep Number SleepIQ: in-mattress sensors track HR, breathing, movement. Validation numbers UNKNOWN. [MEDIUM]

### Seat-pad / chair BCG, is it real and accurate?
- Status: research prototype / preliminary study, NOT a shipping validated consumer product. [MEDIUM-HIGH]
- Smart seat cushion with load cells: 20-participant pilot across 5 real-world tasks; continuous-wavelet J-peak algorithm gave 91.4% HR accuracy vs ECG overall, 94.6% excluding 3 noisy outliers. [JMIR / PMC8204244, 2021, HIGH]
- Also IEEE prototype (HR via BCG seat cushion). [ieeexplore 8919514, HIGH]
- Verdict: buildable and accurate at rest for HR; degrades with motion/talking; no bed-exit/respiration validation at consumer grade. Demo-to-early-product, not commodity. [MEDIUM]

### BOM estimate, DIY load-cell / piezo bed-mat node (ESTIMATE, LOW-MEDIUM)
- HX711 24-bit load-cell ADC: ~1-2 USD bulk. Load cells ~1-3 USD each, 4 per mat ~4-12 USD. Piezo film strip ~1-5 USD. ESP32 ~3-5 USD (WiFi/BLE). PCB + connectors + enclosure + PSU ~5-10 USD.
- ESTIMATED node BOM total: ~15-30 USD hobby/low volume; plausibly <10 USD at scale. [LOW]

## 2. In-home hub compute
- NVIDIA Jetson Orin Nano 8GB: module ~299 USD; dev kit 249 USD; 7-25W; up to 67 TOPS. [ThinkRobotics; JetsonHacks, 2024-2025, MEDIUM/HIGH]
- NVIDIA Jetson Orin NX 16GB: module ~599 USD (1000-unit tier); 10-40W; up to 157 TOPS. [Geeky Gadgets; Arrow 900-13767-0000-000, 2023, HIGH]
- Rockchip RK3588 SBCs: Orange Pi 5 4GB ~60, 8GB ~80, 16GB ~109+ USD; NPU 6 TOPS. Radxa Rock 5B ~189-229 USD. [Amazon; Radxa, 2026, HIGH]
- Hub adds to per-home BOM (ESTIMATE): RK3588 tier ~80-230 USD hardware; Jetson tier ~300-700 USD + ~30-60 case/PSU. [LOW-MEDIUM]

## 3. Cloud inference cost per user per month
### T3 (raw video to cloud)
- 1080p H.264 ~3-6 Mbps (typ 5 Mbps). Continuous 24/7 at 5 Mbps ~= ~180 GB/month/stream; H.265 ~half (~90 GB). [Dacast/VdoCipher, 2025, HIGH]
- AWS S3 Standard ~0.023 USD/GB-month; egress 0.09 USD/GB (first 10TB, tiering to 0.05). [AWS/egresscost, 2025-2026, HIGH]
- Rough T3 per home: 180 GB egress ~= ~16 USD/mo egress alone plus storage. Video-to-cloud is the dominant cost driver and privacy-heavy. [MEDIUM]
### T1/T2 (only derived events leave)
- Bandwidth tiny (JSON events, KB-MB/day); egress/storage effectively negligible (<0.10 USD/mo). [MEDIUM]
### LLM assistant API cost per user per month (order of magnitude)
- Mid-tier rates (Jul 2026): Claude Sonnet class ~3 USD/1M input, 15 USD/1M output; budget models ~0.10-0.40 USD/1M. NOTE: verify current Anthropic pricing before quoting. [benchlm, 2026, MEDIUM]
- At conversational home-assistant volume: cents to low single-digit USD/user/mo on mid-tier; prompt caching cuts input cost to ~10% for repeated system prompts. [MEDIUM]
### Fall-alert latency: edge vs cloud
- Edge/on-device: ~1-10 ms compute; YOLOv5 fall detection on Raspberry Pi = 98 ms; sub-second edge detection, no round trip. [Springer 978-3-032-02831-0_40, 2026, HIGH]
- Cloud round trip: 50-200+ ms network alone; cloud-centric pipelines can exceed 10 s end-to-end (unacceptable for falls). Edge showed 8x speedup (15.4 ms vs 123.2 ms). Edge+cloud hybrid keeps alert <3 s. [arXiv 2604.14154, MEDIUM-HIGH]

## 4. Smart-display piggyback
- Google Nest Hub (2nd gen): contactless sleep tracking via Soli mmWave radar (motion, breathing, cough/snore), no camera/wearable, opt-in; Soli can also extract HR. NO general third-party sensor SDK; data stays within Google/Fitbit. [Google Research; PMC10590449, HIGH; MEDIUM on closed SDK]
- Amazon Echo Show: reported to be adding radar sleep sensing; no open third-party passive-health platform; Alexa Skills are voice/cloud, not raw sensor. [Pocket-lint, MEDIUM]
- Alexa Together: DISCONTINUED. Was US$19.99/mo or $199/yr; activity feed, Urgent Response, fall-detection integration. Fully shut down ~2025-05-21. [SafeWise; Amazon forum, HIGH]
- Alexa Emergency Assist (replacement): US$7.99/mo or $79/yr (Prime $5.99/$59). Response routing, saved-contact alerts, sound detection; no caregiver activity feed. [Tom's Guide, 2024-2025, HIGH]
- Amazon trajectory: consolidated standalone caregiving (Alexa Together, Guard) into paid Emergency Assist; caregiver activity-feed monitoring was removed, leaving a gap. [Amazon forum; CEPRO, 2024-2025, HIGH]

## Key gaps / lowest-confidence items
- Emfit QS exact USD list price UNKNOWN (CA$420 confirmed).
- Sleep Number SleepIQ and Tempur contactless HR/RR validation UNKNOWN.
- Jetson Orin NX 16GB $599/1ku verified; Orin Nano 8GB ~$299 MEDIUM (NVIDIA buy page 403).
- Claude/LLM per-token rates: verify against official Anthropic API pricing before publishing (third-party comparison sites, MEDIUM).
- Component bulk BOM figures are estimates (LOW), not distributor quotes.
