# FACT SHEET 3: E26 Bulb Cameras, Gait Viewing Angle, and Edge Inference Cost Floor

Raw working fact sheet produced during the Phase 2 architecture research. This is the pass that killed the light bulb. Compiled 2026-07-10. Every fact tagged [source, URL, date-accessed, CONFIDENCE]. UNKNOWN = not found in primary sources.

## SECTION 1: EXISTING E26 SCREW-IN BULB CAMERAS

### 1a. Real shipping products, price, orientation
- Sengled Snap (PAR38, E26): 1080p, 140-degree wide-angle FOV, IR night vision, two-way audio, 2.4/5GHz WiFi, cloud storage. 129.99 USD at Home Depot (Model AS01-PAR38NAE26W). A PAR38 flood-lamp with an integrated forward-facing HD camera, designed for a porch/outdoor socket aimed outward/downward. [Amazon/Home Depot/Sengled, amazon.com/dp/B01MSRZCWC, 2026-07-10, HIGH]
- Amaryllo Zeus (E26/E27): 1080p, 360-degree auto-tracking ball camera that screws into a light socket and hangs down; biometric/face recognition, motion detection. 249.99 USD; subscription 2.99 to 29.99 USD/month. Indoor security. [Amazon + Zoro, amazon.com/dp/B083183ZBF, 2026-07-10, HIGH]
- Amaryllo Triton: outdoor socket-screw camera, IP66, -40F to 140F. [Lowes 5001602521, 2026-07-10, MEDIUM]
- LaView L2 Bulb Camera: 4MP (2K), 360-degree pan/tilt ball camera, starlight color night vision, 350-lumen spotlight, AI human detection, E27 base 110-240V. MSRP 49.99 USD, often 19.99 USD. [LaView + Micro Center 686742, 2026-07-10, HIGH]
- Generic light bulb security cameras (Galayou/Kagi/no-name): 4MP/2K, 360-degree, WiFi, motion detection, ~19 to 30 USD. [Walmart 3891818807, 2026-07-10, MEDIUM]

Orientation finding (HIGH): Every shipping product is a security/surveillance device. Two form factors: a PAR38 forward-aimed flood, or a 360-degree ball camera that hangs DOWN from a pendant/porch socket and pans/tilts. None is a fixed ceiling-nadir (straight-down) health monitor. All optimized for wide-area intrusion capture, not a controlled overhead walking-path view.

### 1b. Health / gait claims
Finding (HIGH): NONE of these products claim gait analysis, gait speed, stride, sit-to-stand, fall detection health metrics, or any clinical/health monitoring. Marketing is uniformly security ("motion detection," "AI human detection," "biometric auto-tracking," "night vision," "two-way talk"). The assumed form factor exists commercially only as security cameras, not health monitors.

### 1c. Thermal problem (LED + camera SoC in sealed E26 envelope)
- Enclosed/sealed fixtures trap LED driver heat; sustained thermal stress damages driver components, shortens life, causes flicker, buzzing, diffuser yellowing, thermal shutdown, or worst case fire hazard. Only enclosed-rated bulbs tolerate the higher internal temperature. [Bulb Basics / 1000Bulbs, bulbbasics.com led enclosed-fixture guide, 2026-07-10, MEDIUM]
- Dedicated thermal-protection-circuit patents for LED bulbs exist (US 8,283,877; US 8,754,594). [USPTO, 2026-07-10, MEDIUM]
- Quantified thermal derating for a combined camera-SoC-plus-LED in a sealed E26 envelope: UNKNOWN (no manufacturer publishes a thermal budget). Adding a several-watt camera SoC plus WiFi into the same sealed envelope compounds the existing LED heat problem; a real, unquantified design constraint. [LOW]

### 1d. Applicable US safety standards
- UL 8750 (LED Equipment for Use in Lighting Products): governs the LED-light portion of a bulb-camera. [GlobalSpec/ULSE, 2026-07-10, HIGH]
- UL 1993 (Self-Ballasted Lamps and Lamp Adapters): the end-product standard for a bulb that screws into an E26 socket. [ULSE, 2026-07-10, MEDIUM]
- UL 2089 is vehicle battery adapters, NOT applicable (mis-attribution to watch for). [GlobalSpec/ANSI, 2026-07-10, HIGH]
- FCC Part 15: the WiFi radio is an intentional radiator under Subpart C; the camera/SoC circuitry an unintentional radiator under Subpart B. [F2 Labs, 2026-07-10, MEDIUM]
- Which applies: LED portion to UL 8750 (component) under UL 1993 (self-ballasted lamp end product); radio/electronics to FCC Part 15 Subpart B + Subpart C. No camera-specific UL safety standard identified; the lamp standard is the anchor. [MEDIUM]

## SECTION 2: THE VIEWING ANGLE PROBLEM

### 2a. Validated placement = SIDE / SAGITTAL / oblique along a walking path
- Joint angles and gait parameters are more accurate in the sagittal plane (camera to the SIDE of the walking subject); camera viewing angle and distance significantly affect accuracy. [PLOS One PMC6375625, 2026-07-10, HIGH]
- Validated single-camera markerless systems capture the subject walking along a straight path (side/oblique) with good agreement to marker-based reference for stride/step length, gait speed, stance/swing time. [J Biomech S0021929024001040; MDPI Medicina 62/2/418, 2026-07-10, HIGH]
- Depth cameras viewing the walking path correlate r>0.9 with a pressure-sensitive walkway; gait-speed RMSE 0.04 m/s. [PMC11286855, 2026-07-10, HIGH]

Finding (HIGH): Validated spatiotemporal gait extraction uses a side/oblique view of a subject walking a straight path. No validation study extracts gait speed/stride from a fixed ceiling-nadir view.

### 2b. Overhead / nadir view limitations
- No study validating gait speed or stride from a single fixed overhead/nadir RGB camera. Systems described as ceiling-mounted use MULTIPLE infrared cameras arranged around and along the walk (a motion-capture volume), not a single top-down sensor. [PMC3831173, 2026-07-10, MEDIUM]
- Steep/high vertical viewing angles cause up to 60% accuracy degradation from deformation and self-occlusion; mesh reconstruction recovers up to 26% but does not solve it; the swing and stance foot occlude. [FootGait3D arXiv 2507.11037, 2026-07-10, MEDIUM]
- An mmWave sensor near the ceiling was OUTPERFORMED by one near the ground (0.02 m/s error in abnormal-gait evaluation), independent evidence that a near-ceiling vantage is inferior for gait-speed sensing. [LOW]

Finding (MEDIUM-HIGH): Overhead/nadir viewing is geometrically hostile to gait metrics. Horizontal displacement along the walking direction foreshortens toward zero directly under a ceiling camera, and feet self-occlude. No published nadir-view gait-speed validation. Sit-to-stand (a vertical motion) is even less observable from directly overhead.

### 2c. Frame rate, resolution, path length
- Frame rate: 30 fps standard in validated markerless gait studies. [PMC9586966; arXiv 2507.03016, HIGH]
- Resolution: 720p to 1080p sufficient. [HIGH]
- Path length: 4-meter straight flat walk used in markerless validation (aligns with the clinical 4-Meter Walk Test); 2.5 to 4 m working range. [PMC12431465, HIGH]

## SECTION 3: CAMERA SoC / MODULE COST FLOOR FOR ON-NODE INFERENCE

### 3a. Low-cost IP camera SoCs
- Ingenic T31: low-power AI-capable IP-camera SoC. Complete 4MP PCB camera module (T31N + GC4053) from ~5.25 USD at low MOQ. Bare SoC single-unit price UNKNOWN (B2B). [Unifore, 2026-07-10, MEDIUM]
- SigmaStar SSC338Q: highly integrated IP-camera SoC with a Deep Learning Accelerator; pin-compatible with HiSilicon Hi3516/Hi3518. Module ~108 RMB (~17.60 USD), 2021. [CNX Software / OpenIPC, MEDIUM]
- Allwinner / Amlogic single-unit pricing: UNKNOWN (quote-only).

Cost-floor finding (MEDIUM): A complete low-end camera module (SoC + sensor + board) bottoms out around 5 to 20 USD at volume. These SoCs have only small NPU blocks, adequate for person detection, marginal for full 3D pose/gait.

### 3b. NPU-capable edge
- Rockchip RK3588 (6 TOPS NPU): SBC/module from ~99 USD; bare SoM roughly 50 to 150 USD. [Seeed/Forlinx, MEDIUM]
- Rockchip RK3576 (6 TOPS NPU): ~70% of RK3588 performance at ~30% of the cost, the current price/performance leader for AIoT edge inference. [BLIIoT, MEDIUM]
- Sony IMX500 (inference-in-sensor): NN runs inside the sensor. Cheapest real entry is the Raspberry Pi AI Camera at 70 USD. Industrial module (LUCID SENSAiZ) ~335 USD. [Raspberry Pi, HIGH]
- Hailo-8L (13 TOPS NPU): cheapest real path is the Raspberry Pi AI Kit at 70 USD (M.2 HAT+ with Hailo-8L preinstalled). Hailo-8 (26 TOPS) modules ~70 to 110 USD. [Raspberry Pi/CNX, HIGH]

Cost-floor finding (MEDIUM): Real edge inference sufficient for pose/gait sits around 70 USD (RPi AI Camera IMX500, or RPi AI Kit Hailo-8L), or ~99 USD+ for an RK3588 board. This is 5 to 15x the cost of a bare security-camera SoC module, and physically much larger than fits in a sealed E26 envelope with an LED.

### 3c. Depth / stereo camera cost delta and value for gait
- Intel RealSense D435: ~322 to 334 USD. [DigiKey/Intel, HIGH]
- Luxonis OAK-D (W): ~639 EUR ex-VAT (~700+ USD). [Generation Robots, MEDIUM]
- Depth delta vs cheap RGB: roughly +300 to +700 USD. [MEDIUM]
- Does depth improve gait metrics? RGB-D matches marker-based accuracy and gives direct depth (gait-speed RMSE 0.04 m/s), BUT well-optimized MONOCULAR RGB systems also reach excellent agreement (2D-model ICC > 0.969). [PMC11858938; PMC10295566; PMC11286855, HIGH]

Finding (MEDIUM): Depth adds direct 3D and robustness but the literature does NOT show it as strictly necessary for spatiotemporal metrics (speed, stride, cadence, sit-to-stand). Validated monocular RGB achieves clinically acceptable agreement when the camera is correctly placed (side/oblique, straight path, 30 fps). The depth premium buys robustness, not a fundamental capability unlock for the core metrics.

## KEY TAKEAWAYS
1. E26 bulb cameras exist and ship (19 to 250 USD) but ONLY as security cameras with downward/side ball-camera or forward-flood orientation. None does health/gait; the form factor is real, the health application is not commercialized. [HIGH]
2. The nadir/ceiling viewing angle assumed by the concept is the wrong geometry for gait: validated metrics require a side/oblique view of a 2.5 to 4 m straight path at 30 fps; overhead suffers foreshortening and foot self-occlusion, with no published nadir gait-speed validation. [MEDIUM-HIGH]
3. Cost/thermal reality: security-camera SoC modules cost ~5-20 USD but lack the NPU for real pose/gait; adequate edge inference starts ~70 USD and adds heat/volume a sealed E26 LED envelope already struggles to dissipate. Depth adds ~300-700 USD for robustness the core metrics do not strictly require. [MEDIUM]

Genuinely UNKNOWN from primary sources: bare single-unit SoC pricing for Ingenic/Allwinner/Amlogic; quantified thermal derating for a camera+LED E26 combo; standalone bare-module pricing for Hailo-8L and IMX500 (only bundled products publicly priced).
