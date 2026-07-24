# FACT SHEET 1: WiFi CSI / PIR / Acoustic Sensing for Elder Monitoring

Raw working fact sheet from the Phase 2 architecture research. Product path vs research path. Access date for all URLs: 2026-07-10.

## SECTION 1: WiFi CSI / RF Sensing

### 1a. Emerald Innovations (MIT CSAIL / Dina Katabi spinout)
- Co-founded 2016 by MIT Prof. Dina Katabi; commercializes contactless RF health monitoring. [MedTech Boston, 2016, HIGH]
- CRITICAL DISTINCTION: Emerald does NOT use commodity WiFi CSI. It transmits and receives its OWN low-power radio that reflects off the body, at power ~1000x lower than a typical WiFi device. [PRNewswire BlueRock release, 2023, HIGH]
- Measured metrics: gait speed, mobility, sleep quality/stages, respiration, body elevation/location, behavioral patterns; originally built for fall detection; through-wall sensing documented in the MIT/Katabi line. [BioCentury; Emerald science page; MIT News, HIGH on metrics, MEDIUM on current fall emphasis]
- CUSTOMER = PHARMA / CLINICAL TRIALS, not consumer retail. Partners BlueRock Therapeutics (Bayer, Parkinson's, with Rune Labs), Aspen Neuroscience, Verge Genomics; study NCT05287620. [HIGH]
- STATUS VERDICT: shipping/deployed but ONLY into pharma clinical-trial and research channels (devices placed in participants' homes). NOT consumer-purchasable, no consumer FDA clearance for fall alerting. [HIGH]

### 1b. Do commodity WiFi routers expose CSI to developers?
- Historical research CSI tools all require modified firmware/drivers, NOT normal APIs: Intel 5300 (Halperin), Atheros CSI Tool, Nexmon / nexmon_csi (Broadcom/Cypress, incl. Raspberry Pi, via firmware patching), ESP32 CSI (Espressif, exposes CSI to researchers directly). [survey arXiv:2111.07038; github.com/seemoo-lab/nexmon_csi; github.com/Gi-z/CSIKit, HIGH]
- KEY FINDING: Standard consumer router firmware does NOT expose CSI to developers. Nexmon exists specifically because consumer routers ship locked firmware that deliberately does not expose Channel State Information. CSI access on commodity hardware is jailbreak/firmware-patch/research territory, not a supported developer API. [seemoo-lab/nexmon; arXiv:1601.07077, HIGH]

### 1c. IEEE 802.11bf (WLAN Sensing standard)
- PUBLISHED as IEEE Std 802.11bf-2025 on 2025-09-26. [IEEE SA standards.ieee.org/ieee/802.11bf/11574, HIGH]
- Scope: MAC/PHY modifications to standardize sensing in 1-7.125 GHz and above 45 GHz. [IEEE Xplore, HIGH]
- PRODUCT-PATH IMPACT: standard exists on paper (2025) but does not yet mean shipping consumer silicon/firmware; chipset/AP support, certification, and rollout lag ratification by years. Near-term an enabler, not a shipping capability. [MEDIUM]

### 1d. Commercial WiFi motion sensing
- Xfinity WiFi Motion (Comcast): SHIPPING. Detects MOTION/MOVEMENT only. No fall or gait claim. [xfinity.com, HIGH]
- Plume + Cognitive Systems WiFi Motion: SHIPPING software add-on, no new hardware. Motion/presence only. [Forbes 2020; Wi-Fi NOW, HIGH]
- Origin Wireless / Hex Home: SHIPPING consumer product, Hex Home from 179.99 USD (June 2021). Origin MARKETS fall detection, ADL, sleep, breathing, wander detection; partnered with Noonlight. [PRNewswire; MIT Tech Review 2024, HIGH on shipping+price; LOW on independent fall-accuracy validation]
- Arlo + Origin AI partnership to add ambient WiFi sensing to future products. [CEPRO, MEDIUM]

### 1e. Can commodity WiFi detect FALLS or GAIT SPEED reliably outside a lab?
- Lab fall-detection papers report high numbers: WiFall 90-94% precision (13-15% false alarm); CNN-LSTM ~94.85%; some 99% on test sets. [arXiv:1507.01057; ScienceDirect S2949715924000283, HIGH that claimed]
- BUT generalization is the documented failure mode: performance drops cross-user, cross-environment, cross-device. In-the-wild datasets (CSI-Bench) exist precisely because lab numbers do not transfer. [survey arXiv:2503.08008; arXiv:2005.11932, HIGH]

### BLUNT VERDICT (Section 1)
- Motion/presence: PRODUCT PATH. Shipping today (Xfinity, Plume, Origin/Verizon). Coarse room-level motion works. [HIGH]
- Fall detection: RESEARCH PATH on commodity WiFi CSI (poor cross-domain generalization; only marketed, not independently validated, in consumer products). PRODUCT PATH only via dedicated RF hardware (Emerald), confined to pharma channels. [HIGH]
- Gait speed: RESEARCH PATH on commodity WiFi. A real product only on Emerald's dedicated radio in clinical trials, not commodity WiFi, not consumer. [HIGH]

## SECTION 2: PIR Motion + Door/Window Contact Sensors (cheap baseline)

### 2a. Pricing (current, US)
- Aqara Motion Sensor P1 (Zigbee, MS-S02): ~12.99 promo / low-20s USD. Requires Aqara hub. [Home Depot 322277797, MEDIUM]
- Aqara Door/Window Sensor: DW-S03D ~17.99 USD; DW-S02D ~26.14 USD. [Home Depot, MEDIUM]
- Third Reality Zigbee Contact Sensor: ~13-15 USD; 2x AAA, ~2 year battery; needs Zigbee hub. [Amazon B08R9PH4JT, MEDIUM]
- General range: PIR motion ~13-25 USD; door/window contact ~13-20 USD single unit, cheaper in multipacks. [MEDIUM]

### 2b. Detection capability
- CAN detect: room occupancy/presence, room-to-room transitions (mesh), entry/exit (door contacts), bed/bathroom trips and nocturia counts (motion + door events at night), coarse activity, day/night routine deviations. [HIGH]
- CANNOT detect: falls, gait speed, posture, breathing, or a motionless fallen person (PIR needs movement; a motionless person on the floor becomes invisible). [HIGH]

### 2c. Battery / install
- Battery life: Aqara P1 advertised 5-year (CR2450); typical contacts 1-2 years. [HIGH]
- Install: peel-and-stick, no wiring; contact sensors are a two-piece magnet; requires a Zigbee/Z-Wave hub or SmartThings/Home Assistant. [HIGH]

## SECTION 3: Acoustic Fall / Distress Detection (brief)
- Research systems report strong LAB numbers: circular-array ~91% accuracy / 96% precision; acoustic-FADE 100% sensitivity at 97% specificity; AP-Fall >93%. Height/3D localization cut false alarms from 32/hr to 5/hr at 100% detection. [PubMed 21096795; ACM 10.1145/3478094; Springer AP-Fall, HIGH that claimed, LOW real-home]
- REALITY: constrained datasets; false-alarm rates (even the improved 5/hr) are far too high for unattended home deployment. Acoustic fall detection is a RESEARCH PATH, not a shipping consumer product. [MEDIUM]
- No prominent commercial acoustic-signature fall detector found; SafelyYou is CAMERA-based. [MEDIUM absence of evidence]
- Two-party consent constraint (continuous home audio) applies and is a known adoption blocker. [HIGH]

## Bottom line
- Commodity WiFi = PRODUCT PATH for coarse motion/presence only; RESEARCH PATH for falls and gait. CSI not exposed by consumer routers without firmware hacks. 802.11bf published Sept 2025 but silicon/products lag.
- Emerald = real deployed product for gait/sleep/breathing/falls, but on its OWN low-power radio and ONLY in pharma/clinical channels, not consumer, not commodity WiFi.
- PIR + door contacts = mature, cheap (~13-25 USD/unit), 1-5yr battery, peel-and-stick; great for occupancy/transitions/nocturia, useless for falls/gait/posture.
- Acoustic fall detection = research-grade only; no notable acoustic consumer product; SafelyYou is camera-based.
