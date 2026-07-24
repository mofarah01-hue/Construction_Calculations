# FACT SHEET 2: mmWave Radar + Thermal IR Arrays for Elder Fall Detection and Vitals

Raw working fact sheet from the Phase 2 architecture research. Confidence key: HIGH = primary/current/on-point; MEDIUM = secondary or dated; LOW = marketing or inference. All numbers carry source + date. Note: TI.com, DigiKey, Mouser, Vayyar.com, Octopart returned 403 to direct fetch; distributor values are from search-indexed snippets of those primary pages plus fetchable papers, marked MEDIUM.

## 1. VAYYAR CARE / VAYYAR HOME (60 GHz 4D imaging radar)
- Frequency band: 60 GHz mmWave MIMO. [Vayyar tech-specs, 2024, HIGH]
- Radar type: mmWave MIMO, up to 46 antennas, single RFIC with DSP+MCU, 4D point cloud. [Vayyar tech-specs, 2024, HIGH]
- Field of view: 140 degrees azimuth x 70 degrees elevation. [Vayyar tech-specs, 2024, HIGH]
- Range: ~13 ft front, 6 ft 6 in either side (large rooms need more than one unit). [tls.global, 2024, HIGH]
- Camera-free / no wearable: yes, touchless. [Vayyar, 2024, HIGH]
- Bathroom use: yes; works in all lighting and through dense steam; markets that ~80% of falls occur in the bathroom. [Vayyar, 2024, HIGH claim]
- Fall detection: automatic fall detection plus long-lie / immobility, plus activity data. [Vayyar blog, 2024, HIGH]
- Published sensitivity/specificity: UNKNOWN from primary source. Only marketing claim "4X more accurate than other automatic fall alert systems." NOTE: the NCT04224753 "INVSENSOR00027" 93.9% sensitivity study is a CHEST-WORN device, NOT Vayyar; do not attribute. [Vayyar marketing; clinicaltrials.gov, LOW / do-not-attribute]
- Shipping product, to whom: yes. B2C via Amazon (Vayyar Care, Touchless Fall Detection); B2B to senior living and PERS dealers; partners K4Connect, Austco, Anthropos, Skyresponse, Alexa Together. [Amazon; K4Connect and Austco press, 2022-2024, HIGH]
- Device price: ~250 USD per device (2022); avg 3 per home (bath/bed/living). [Ctech, 2022, MEDIUM dated]
- Monitoring subscription: +20 USD/month for emergency-services contact via Alexa. [Ctech, 2022, MEDIUM dated]
- Mounting/install: wall-mount, 9 cm diameter, 1.5 cm deep, 110 g, 2.4 GHz WiFi, OTA. [Vayyar tech-specs, 2024, HIGH]
- Per-room installed cost: ESTIMATE ~250 USD/room hardware + ~20 USD/mo monitoring (2022 B2C; B2B volume UNKNOWN). [LOW estimate]

## 2. TI xWR6843 (60-64 GHz) + IWRL6432
- Chip/band: IWR6843 single-chip FMCW mmWave, 60-64 GHz, 45nm RFCMOS, integrated DSP+MCU. [TI IWR6843 datasheet, HIGH]
- Chip price single unit: ~43.09 USD (DigiKey/Arrow). [2026, MEDIUM]
- Chip price 1ku/volume: UNKNOWN (TI quote-gated). [HIGH that it is gated]
- EVM boards: IWR6843ISK ~195.56 USD; IWR6843ISK-ODS ~187.74 USD; IWR6843AOPEVM listed. [DigiKey, 2026, MEDIUM]
- Range/FOV people counting: TIDEP-01000 detect up to 250 objects, track up to 20 people, +/-60 degrees azimuth. [TI, HIGH]
- Range/FOV area scanner: TIDEP-01010 FOV up to 120 degrees, range 0-10 m, 3D localization. [TI, HIGH]
- Fall detection reference: posture recognition enables fall detection up to 6.5 m at >90% accuracy on IWR6843AOPEVM/ISK and IWRL6432. [TI app page; arXiv 2311.08755, HIGH]
- Vital-signs reference: TI mmWave Vital Signs Lab detects chest displacement on IWR6843AOP/ISK and IWRL6432. [TI, HIGH]
- Vitals accuracy (TI-reported): HR within 5 bpm; resp error 0.14 RPM at 1m to 0.26 RPM at 7m; HR error 1.08 BPM at 3m to 3.6 BPM at range. [TI, HIGH vendor]
- Long-lie / person-on-floor: yes, point-cloud tracking plus posture classification. [TI; arXiv 2403.05634, HIGH]
- Privacy/occlusion: no image, point cloud only, works in darkness, senses through some materials. [TI, HIGH]
- Mount: wall or ceiling (ISK-ODS overhead variant). [DigiKey, HIGH]
- Per-room installed cost: ESTIMATE ~60-120 USD/room custom BOM (chip ~43 + antenna PCB + host MCU + enclosure), or ~188-196 USD using an off-the-shelf EVM. [LOW estimate]

## 3. INFINEON BGT60TR13C (XENSIV, 60 GHz)
- Band/config: 58-63.5 GHz FMCW, antenna-in-package L-array, 1 Tx / 3 Rx, built-in FSM + FIFO. [Infineon datasheet, HIGH]
- Range: 0.2 m min to 15 m max. [Infineon, HIGH]
- Detects: presence, tracking, segmentation, micro/macro motion incl. sub-mm, vital signs (heartbeat, breathing, chest movement). [Infineon, HIGH]
- Power: 1.8 V, ~200 mA active, <5 mW duty-cycled. [Infineon, HIGH]
- Chip price single unit: ~19.72 USD (DigiKey). [2026, MEDIUM]
- Fall-detection fit: primarily presence + vitals, short-range; room-scale fall/long-lie not its primary published use. [MEDIUM]
- Per-room installed cost: ESTIMATE ~30-60 USD/room custom BOM; best for presence/vitals, not whole-room fall. [LOW estimate]

## 4. mmWave 60 GHz CAPABILITY EVIDENCE (cross-vendor, peer-reviewed)
- Contactless heart rate vs reference: 77 GHz FMCW HR relative error ~1.96%, resp ~1.33%. [Nature s41598-024-77683-1, 2024, HIGH]
- Respiration accuracy: breathing-rate error 0.42 bpm (98.8%) at 8 m; 1.07 bpm (97%) beyond 8 m. [2024, MEDIUM]
- Vital signs FMCW: high-precision HR/resp demonstrated. [PMC9572116, 2022, HIGH]
- Gait speed/stride: radar step-length error 4.5 cm / 8.3% vs Zeno Walkway gold standard; ICC 0.91 in home; ground-mounted mmWave gait-speed error ~0.02 m/s. [PMC10891707, 2024; PMC9784666 / MDPI Sensors 22-9901, 2022, HIGH]
- Immobile person on floor (long-lie): detectable via point-cloud plus posture classification. [arXiv 2403.05634; 2311.08755, HIGH]
- Privacy/lighting/occlusion: no image, works in darkness, through steam and some materials, RF power ~1000x weaker than a phone (Vayyar). [HIGH claim]
- Install: wall or ceiling; ceiling/overhead improves floor coverage. [TI ISK-ODS; Vayyar, HIGH]

## 5. THERMAL / LOW-RES IR ARRAYS
### Panasonic Grid-EYE AMG8833 (8x8)
- Resolution 8x8 = 64 thermopiles; FOV 60 degrees; range ~7 m; 10 fps or 1 fps; accuracy +/-2.5 C; 0-80 C. [Panasonic/SparkFun, HIGH]
- Price: bare sensor ~40 USD. [DigiKey/SparkFun, 2026, MEDIUM]
- Fall detection: demonstrated "Real-Time Fall Detection using ESP32 + AMG8833" but 8x8 is very coarse, often interpolated. [IEEE 10250598, 2023, MEDIUM]
### Melexis MLX90640 (32x24)
- Resolution 32x24 = 768 pixels; FOV 55x35 (standard) or 110x75 (wide); price ~36.75-38.41 USD. [Melexis/DigiKey, MEDIUM]
### Thermal array general
- Privacy advantage: no identifiable image, thermal blob only. [HIGH]
- Resolution floor for fall: 8x8 works with ML/interpolation but is the practical low end; 32x24 gives margin. [arXiv 2403.02632; IEEE 10250598, MEDIUM]
- Bathroom viability: CAUTION, thermopiles measure 8-14 um LWIR; hot steam/humidity and warm surfaces reduce person-vs-background contrast, degraded vs mmWave which is explicitly steam-tolerant. No primary bathroom-validation study found. [LOW / UNKNOWN for hard data]
- Per-room installed cost: ESTIMATE ~50-80 USD/room. [LOW estimate]

## KEY CAVEATS
- Vayyar's own fall sensitivity/specificity is NOT publicly sourced (only "4X" marketing). The 93.9% figure is a chest-worn device (NCT04224753), not Vayyar; do not merge.
- TI 1ku silicon pricing is quote-gated; only single-unit distributor (~43 USD IWR6843, ~20 USD BGT60TR13C) and EVM (~188-196 USD) prices are public.
- Thermal IR in bathrooms is the weakest-evidenced claim; mmWave has explicit steam tolerance, thermal does not.
- All DigiKey/Mouser/TI/Vayyar prices came from search-index snippets (direct fetch 403), mark MEDIUM until confirmed on the live distributor page.
