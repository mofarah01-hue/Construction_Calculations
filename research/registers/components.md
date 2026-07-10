# components.md

Every hardware part evaluated across the program, including rejected ones, per framework section 9. Concept A is the only hardware concept; Concept B is software plus optional third party devices. Deduplicated across A Phase 2 and A Phase 3. Prices are labeled list, distributor, retail, or estimate. Lead time and lifecycle are UNKNOWN unless a source gave them.

Columns: Part number | Manufacturer | Function | Key specs | Price at volume tiers | Distributor / link | Lead time | Lifecycle | Datasheet / source | Selected or rejected + reason | Source phase

## Radar (fall, presence, vitals)

| Part | Manufacturer | Function | Key specs | Price by tier | Distributor / link | Lead time | Lifecycle | Datasheet / source | Selected/rejected + reason | Source phase |
|---|---|---|---|---|---|---|---|---|---|---|
| IWR6843 | Texas Instruments | 60-64 GHz FMCW radar SoC (DSP+MCU), on-chip fall detection | Fall demo >90% to 6.5 m; HR within ~5 bpm; long lie via point cloud; no image | ~$43 single; est $28 at 1k, $24 at 100k; 1ku quote-gated UNKNOWN | ti.com/product/IWR6843 [S2] | UNKNOWN | Active | ti.com datasheet | SELECTED (radar node core, single largest BOM line, runs fall on-chip DSP) | A P2, A P3 |
| IWR6843ISK-ODS | Texas Instruments | Radar EVM, overhead/ceiling optimized | Evaluation module | ~$188 to $230 | Digi-Key [S2] | UNKNOWN | Active | digikey.com | EVAL only (bench/G1, not production) | A P2 |
| IWRL6432AOP | Texas Instruments | Low power 57-64 GHz radar, antenna in package | Presence, motion, gesture, low power modes | ~$11.19 at 1ku | ti.com/product/IWRL6432AOP [S17] | UNKNOWN | Active | ti.com | CANDIDATE (lower cost presence/vitals, not whole-room fall) | A P2, A P3 |
| BGT60TR13C | Infineon | 58-63.5 GHz radar, antenna in package, 1Tx/3Rx | Range 0.2-15 m; presence + vitals; ~5 mW low power | ~$19.72 | infineon.com/part/BGT60TR13C [S3] | UNKNOWN | Active | infineon.com | CANDIDATE (lower cost, best for presence/vitals not whole-room fall) | A P2, A P3 |
| Vayyar Care | Vayyar | 60 GHz 4D imaging radar node (shipping) | FOV 140x70, range ~13 ft; camera free; bathroom viable; auto fall + long lie | ~$250/device retail, +$20/mo | amazon.com; vayyar.com [S1][S4] | UNKNOWN | Shipping | vayyar.com | BUY reference / competitor (accuracy not published, per-device cost high) | A P2 |

## Camera and vision compute

| Part | Manufacturer | Function | Key specs | Price by tier | Distributor / link | Lead time | Lifecycle | Datasheet / source | Selected/rejected + reason | Source phase |
|---|---|---|---|---|---|---|---|---|---|---|
| IMX500 (RPi AI Camera) | Sony | In-sensor inference image sensor; pixels stay in package | Inference in sensor; only metadata leaves; supports "no image leaves" claim | $70 retail module; bare sensor est $20-35 volume; 1ku UNKNOWN | raspberrypi.com; aitrios.sony-semicon.com [S16] | UNKNOWN | Active | sony-semicon.com | SELECTED (camera node, load-bearing for privacy claim) | A P2, A P3 |
| RK3576 | Rockchip | 6 TOPS NPU SoC, camera node alternative | Pixels enter SoC (weaker privacy claim) | Chip est $15-25 volume; board $103 | bliiot.com [H1] | UNKNOWN | Active | rockchips.net | FALLBACK (if IMX500 model does not fit; weakens privacy claim) | A P3 |
| RK3588 | Rockchip | 6 TOPS NPU SoC, hub upgrade | ~6 TOPS | Chip est $30-50; SBC $150-180 | rockchips.net [H1][S20] | UNKNOWN | Active | rockchips.net | REJECTED for sealed node (too hot, too expensive); hub upgrade only | A P2, A P3 |
| RK3566 | Rockchip | Quad A55 SoC, selected hub | Hub host | From $10.31 chip at LCSC | lcsc.com [H7] | UNKNOWN | Active | lcsc.com | SELECTED (hub SoC where a hub is used) | A P3 |
| Hailo-8L | Hailo | 13 TOPS M.2 accelerator | Edge inference accelerator | Module ~$70 retail; chip est $20-30 volume | mouser.com; digikey.com [H2] | UNKNOWN | Active | hailo.ai | CANDIDATE accelerator | A P3 |
| STM32N657 | STMicroelectronics | 600 GOPS NPU MCU; radar/mesh host or stripped camera | Neural ART accelerator | $10.85 T&R at MOQ 3000 to $20.62 by variant | digikey.com STM32N657X0H3Q [H3] | UNKNOWN | Active | st.com | CANDIDATE (mesh host / low-end camera) | A P3 |
| CV25 / CV22 | Ambarella | CVflow camera SoC, pose and activity | Purpose built pose/activity; closed SDK, NDA | NDA; est $10-18 (CV25), $20-35 (CV22) volume | (design house / NDA) | UNKNOWN | Active | ambarella.com | FALLBACK (closed toolchain, NDA price, design-house route) | A P3 |
| V851 / V853 | Allwinner | Low cost camera SoC, selected IMX500 host | ~0.5 TOPS NPU | Chip est $4-8 | alibaba.com; cnx-software.com [S9][H4] | UNKNOWN | Active | (CM listing) | CANDIDATE host for IMX500 / camera module cost floor | A P2, A P3 |
| SSC338Q / T31 | SigmaStar / Ingenic | Low cost camera SoCs, host alternatives | Camera host | Chip est $4-8 | alibaba.com [S9][H4] | UNKNOWN | Active | (CM listing) | CANDIDATE host alternatives | A P3 |
| Jetson Orin Nano 8GB | NVIDIA | 67 TOPS module, hub upgrade only | VLM/memory tier | ~$299 module; 1ku est $200-260 UNKNOWN | arrow.com; seeedstudio.com [H5] | UNKNOWN | Active | nvidia.com | REJECTED for v1 node (hub upgrade only; too hot/expensive sealed) | A P3 |
| Jetson Orin NX 16GB | NVIDIA | 100-157 TOPS module, hub upgrade only | ~157 TOPS | $399 to $599 at 1ku | arrow.com [H6][S20] | UNKNOWN | Active | nvidia.com | REJECTED for sealed node; optional hub if scene memory enters v1 | A P2, A P3 |
| SC2336 / IMX307 | SmartSens / Sony | 2 MP low light IR-sensitive gait sensor | StarLight low light | Bare MIPI est $8-15; USB integrated est $17-30 | [H4] | UNKNOWN | Active | (CM listing) | CANDIDATE gait sensor (low light) | A P3 |
| IMX335 (5 MP) | Sony | Over-specified low light module | 5 MP | ~$30-40 | [H4] | UNKNOWN | Active | sony-semicon.com | REJECTED (over-specified for need) | A P3 |
| OV2640 | OmniVision | Low cost 2 MP camera | 2 MP | ~$3-5 | [H4] | UNKNOWN | Active | omnivision.com | REJECTED (fails low light and IR requirement) | A P3 |
| Low cost IP camera module | Various (Allwinner/SigmaStar SoC) | RGB camera module for gait node | 1080p, H.265, on-board NPU | module ~$5-25 | alibaba.com [S9] | UNKNOWN | Active | (CM listing) | REFERENCE cost floor | A P2 |
| Intel RealSense D435 | Intel | RGB + stereo depth camera | Depth to 10 m; 30 Hz cap | ~$300+ retail | store.intelrealsense.com [S11] | UNKNOWN | EOL risk | intel.com | REJECTED (too expensive; depth not required for v1) | A P2 |

## Thermal, PIR, contact, radio, power, enclosure

| Part | Manufacturer | Function | Key specs | Price by tier | Distributor / link | Lead time | Lifecycle | Datasheet / source | Selected/rejected + reason | Source phase |
|---|---|---|---|---|---|---|---|---|---|---|
| AMG8833 Grid-EYE | Panasonic | 8x8 thermal IR array | 60 deg FOV, ~7 m, +/-2.5 C | ~$18-40 | digikey.com; mouser.com [S6] | UNKNOWN | Active | panasonic datasheet | CANDIDATE (privacy-friendly presence; steam caution; not bathroom fall) | A P2 |
| MLX90640 | Melexis | 32x24 thermal IR array | 55x35 or 110x75 deg FOV | ~$37-70 | melexis.com; mouser.com [S6] | UNKNOWN | Active | melexis.com/en/product/mlx90640 | CANDIDATE (presence only; degrades in steam) | A P2 |
| Motion Sensor P1 | Aqara | Zigbee PIR occupancy | ~5 yr CR2450 battery | ~$13-25 | (distributor) [S8] | UNKNOWN | Active | aqara.com | SELECTED (cheap mature mesh backbone; needs hub) | A P2 |
| Contact sensor | Aqara / Third Reality | Zigbee door/window contact | ~1-2 yr battery | ~$13-20 | (distributor) [S8] | UNKNOWN | Active | aqara.com | SELECTED (cheap mesh backbone) | A P2 |
| ESP32-C6-MINI / WROOM | Espressif | WiFi 6, BLE 5, Thread, Zigbee radio | Multi-protocol in one part | Module from $2.96; SoC from $2.18 at LCSC | lcsc.com [H8] | UNKNOWN | Active | espressif.com | SELECTED (radio for custom nodes) | A P3 |
| Emfit QS | Emfit Ltd | Under-mattress BCG mat (shipping) | HR LoA +/-4.4 bpm vs ECG; HRV, respiration, bed exit; no subscription; weak sleep staging | ~$299 (CA$420) retail | emfit.com [S10][P15] | UNKNOWN | Shipping | emfit.com | BUY option (bedroom node; validated HR/bed-exit; weak sleep staging) | A P2, A P3 |
| Sleep Analyzer | Withings | Under-mattress BCG mat (shipping) | Validated adults 65-83; HR within 2 bpm; apnea ~88% | $199.95 retail | withings.com [S21] | UNKNOWN | Shipping | withings.com | BUY option (bedroom node; validated) | A P2, A P3 |
| EarlySense bed sensor | Baxter / Hillrom | Clinical under-mattress piezo | FDA 510(k) K180079; HR 96.1%, RR 93.3% | Clinical (not consumer priced) | PMC5337599 [S21] | UNKNOWN | Clinical | (510k) | REJECTED for consumer (clinical price; not consumer channel) | A P2 |
| Piezo / PVDF bed mat (own build) | Various | Bedroom BCG node | Own build BCG | BOM est $45 (1) to $13 (100k) | [S21][H8] | UNKNOWN | n/a | (DIY) | CANDIDATE (build vs buy unresolved) | A P3 |
| Supercap + PMIC (dying gasp) | CAP-XX / TI | Holdup + last gasp radio on mains node | Seconds of holdup, sends power loss packet | est ~$1-3 BOM | cap-xx.com; ti.com SLVAG21 [S15] | UNKNOWN | Active | ti.com app note | SELECTED (mains node power-loss detection) | A P2 |
| AC to DC wall adapter, 5 V 2 A, pre-listed | Various | Mains power, offloads safety cert | Pre-certified adapter | Retail $6-10; OEM CM est $2-4 | jameco.com; digikey.com [H9] | UNKNOWN | Active | (distributor) | SELECTED (external pre-listed adapter offloads UL scope) | A P3 |
| Injection molded enclosure | CM | Node housing | Per-part + tooling | Per part est $0.30-1.50; tooling $2k-30k/mold | formlabs.com; rapiddirect.com [H10] | UNKNOWN | n/a | (CM) | NRE line item | A P3 |

## Rejected paths / not components (recorded to prevent re-research)

| Item | Reason rejected | Source phase |
|---|---|---|
| E26 bulb-camera form factor | Fails on switched mains power and nadir viewing angle; all shipping E26 bulb cameras are security devices, none health/gait; sealed lamp thermal envelope traps heat [S18][S19][S23] | A P2 |
| WiFi CSI on commodity routers | Commodity routers do not expose CSI; requires patched hardware; research path only for fall/gait, product path for coarse motion only [S5] | A P2 |
| Acoustic fall detection | Lab 91-100% but ~5 false alarms/hr; research path, not a product-grade primary [S14] | A P2 |
| Seat pad BCG (seated HR) | Research prototype, 9 subjects, motion-artifact limited; not budgeted for v1 [P21] | A P2 |
| Emerald Innovations contactless RF | Not a consumer component vendor; pharma/research trials only; roadmap reference [S7] | A P2 |
| Smart display / Alexa piggyback | Closed SDK; Alexa Together discontinued May 2025, replaced by Emergency Assist $7.99/mo [S22] | A P2 |
</content>
