# vendors.md

Every vendor, ODM, CM, lab, content licensor, and potential partner evaluated, per framework section 9. Deduplicated across shared_wearable, A Phase 2/3/7, B Phase 2/5. Columns: Vendor | What they supply | MOQ | Works with startups? | Published pricing | Contact path | Confidence | Source phase

## Wearable and sensor-data vendors (shared)

| Vendor | Supplies | MOQ | Works with startups? | Published pricing | Contact path | Confidence | Source phase |
|---|---|---|---|---|---|---|---|
| Apple | HealthKit/CoreMotion/SensorKit APIs | None | Yes (App Store) | $99/yr program | developer.apple.com | HIGH | Shared Wearable |
| Oura | Derived-metrics cloud API | None | Yes, approval to scale | Free API, user pays Membership | cloud.ouraring.com | HIGH | Shared Wearable |
| Whoop | Derived-metrics cloud API | None | Yes, approval to scale | Free API | apisupport@whoop.com | HIGH | Shared Wearable |
| Garmin | Health API + Health SDK | Possible device MOQ | Yes, via Health team | Fee/MOQ negotiated; $5,000 reported (unverified) | developer.garmin.com | MEDIUM | Shared Wearable |
| Fitbit / Google | Cloud API (migrating to Google Health API) | None | Limited for commercial intraday | Free API | dev.fitbit.com | HIGH | Shared Wearable |
| Samsung | Privileged Health SDK (raw PPG/accel) | Partner approval | Selective partner program | UNKNOWN | developer.samsung.com/health/privileged | MEDIUM | Shared Wearable |
| Withings | Public + Advanced Research API (raw contract) | Contract | Yes, B2B/RPM | UNKNOWN for research API | developer.withings.com | MEDIUM | Shared Wearable |
| Polar | BLE SDK, raw PPG/accel/ECG straps | Device only | Yes, open SDK | Free SDK; device retail UNKNOWN | polar.com/en/developers | HIGH | Shared Wearable |
| Empatica | EmbracePlus research-grade raw platform | Contract | Research/enterprise | UNKNOWN (quote) | empatica.com | MEDIUM | Shared Wearable |
| Movesense | White-label raw sensor + open SDK | Volume for white label | Yes | Dev kits purchasable; volume UNKNOWN | sales@movesense.com | MEDIUM | Shared Wearable |
| Omron, Withings (BP) | Pregnancy-validated BP cuffs | Retail | Yes | Retail | omron; withings | MEDIUM | B P5 |

## Silicon and hardware component vendors (Concept A)

| Vendor | Supplies | MOQ | Works with startups? | Published pricing | Contact path | Confidence | Source phase |
|---|---|---|---|---|---|---|---|
| Analog Devices (Maxim) | MAX86141 PPG AFE | Distributor stock | Yes | $8.88 single unit Digi-Key | digikey.com / analog.com | HIGH | Shared Wearable |
| Texas Instruments | AFE4900; IWR6843, IWRL6432 radar + reference designs | Distributor stock | Yes | Distributor list; radar 1ku quote-gated | ti.com | HIGH | Shared Wearable, A P2, A P3 |
| Infineon | BGT60TR13C 60 GHz radar | Distributor stock | Yes | ~$19.72 | infineon.com | HIGH | A P2, A P3 |
| Vayyar | 60 GHz radar fall-detection nodes (B2C + operators) | Product line, integrators | Yes | ~$250/device | vayyar.com | MEDIUM-HIGH | A P2, A P3, A P7 |
| Sony (AITRIOS) | IMX500 in-sensor inference | Volume gated | Yes | $70 module retail; volume gated | aitrios.sony-semicon.com | HIGH | A P2, A P3 |
| Rockchip | RK3566 hub, RK3576/RK3588 alternatives | Distributor | Yes (RKNN toolkit) | LCSC listed | rockchips.net / lcsc.com | MEDIUM | A P3 |
| Ambarella | CV25/CV22 camera SoC | Design-house route | Selective | NDA | ambarella.com | MEDIUM | A P3 |
| Allwinner, SigmaStar, Ingenic | Low-cost camera host SoCs | CM/Alibaba | Yes | Alibaba/CM listings | (CM) | MEDIUM | A P3 |
| Espressif | ESP32-C6 radio (WiFi 6/Thread/Zigbee/BLE) | LCSC stock | Yes | From $2.18 SoC / $2.96 module | lcsc.com | HIGH | A P3 |
| Panasonic / Melexis | Thermal IR arrays (AMG8833, MLX90640) | Distributor | Yes | $18-70 | digikey; melexis.com | MEDIUM | A P2 |
| NVIDIA | Jetson Orin Nano/NX modules + Inception program | Distributor + startup program | Yes | $299-599 module | nvidia.com | HIGH | A P3, A P7 |
| Hailo | Hailo-8L 13 TOPS accelerator | Distributor | Yes | ~$70 module | mouser; digikey | HIGH | A P3 |
| STMicroelectronics | STM32N657 NPU MCU | MOQ 3000 | Yes | $10.85-$20.62 | digikey; st.com | HIGH | A P3 |
| Emfit Ltd | Under-mattress BCG sleep/vitals mat + OEM | Product + OEM | Research/enterprise | ~$299 retail | emfit.com | MEDIUM | A P2, A P3 |
| Withings (Sleep Analyzer) | Under-mattress BCG mat + OEM path | Product + OEM | Yes | $199.95 retail | withings.com | MEDIUM-HIGH | A P2, A P3 |
| Aqara / Third Reality | Zigbee PIR and contact sensors | Retail/distributor | Yes | $13-25 | (distributor) | HIGH | A P2 |
| Emerald Innovations | Contactless RF gait/fall (MIT/Katabi) | Contract | Pharma/research only | B2B contract | emeraldinno.com | HIGH | A P2, A P7 |
| Injection-molding / CM (unnamed) | Enclosure, PCBA, assembly | CM MOQ | Yes | Tooling $2k-30k/mold | (CM) | MEDIUM | A P3 |
| UL/ETL recognized test lab (ACB, TUV, Intertek class) | FCC + UL/ETL certification | n/a | Yes | Certification NRE, select at G4-G5 | (labs) | MEDIUM | A P3 |
| PERS monitoring centers | White-label 24/7 escalation/dispatch | Buy not build | Yes | UNKNOWN | (RFQ) | LOW | A P4, A P7 |
| University gait labs | Instrumented-walkway validation | Research agreements | Yes | UNKNOWN | (research) | MEDIUM | A P7 |

## Health-data, lab, telehealth, and content vendors (Concept B)

| Vendor | Supplies | MOQ | Works with startups? | Published pricing | Contact path | Confidence | Source phase |
|---|---|---|---|---|---|---|---|
| Particle Health | Health-record network query, C-CDA to FHIR (160k systems, 320M records) | n/a | Yes | Custom, UNKNOWN | particlehealth.com | MEDIUM | B P2, B P5 |
| Health Gorilla | Health data network + Quest lab subscription | n/a | Yes | Per transaction, UNKNOWN | healthgorilla.com | MEDIUM | B P2, B P5 |
| Metriport | Open-source FHIR API, lab notifications | n/a | Yes | Usage-based, UNKNOWN | metriport.com | MEDIUM | B P2 |
| Flexpa | Consumer patient-access API, consent/IAL2 | n/a | Yes (DTC fit) | Page 403, UNKNOWN | flexpa.com | MEDIUM | B P2 |
| 1upHealth | Patient-access FHIR API | n/a | Yes (enterprise) | Custom, UNKNOWN | 1up.health | MEDIUM | B P2, B P5 |
| PWNHealth (Everly/Labcorp affiliate) | Telehealth ordering physician network, 80+ CLIA labs, 50 states | n/a | Yes (B2B) | Per order, UNKNOWN | ondemand.labcorp.com/pwnhealth-agreements | HIGH capability, LOW price | B P2 |
| Quest Diagnostics | Reference lab (Function's partner) | n/a | Yes | Function retail $365/yr bundle | questhealth.com | HIGH retail, LOW wholesale | B P2, B P5 |
| Wheel, SteadyMD | Telehealth clinician networks | n/a | Yes | UNKNOWN | wheel.com; steadymd.com | MEDIUM | B P5 |
| ACOG | Obstetric clinical + patient-education content license | Via CCC | Via CCC | Quote-based, UNKNOWN | acog.org permissions | HIGH terms, UNKNOWN fee | B P2, B P5 |
| AAP | Bright Futures / pediatric content license | Org license | Yes | Some free, some purchase, UNKNOWN | aap.org | HIGH terms, UNKNOWN fee | B P2, B P5 |
| Triple P International (UniQuest) | Licensed parenting-program content | Purveyor license | Yes | Quote-based, UNKNOWN | triplep.net | MEDIUM | B P2 |
| Incredible Years | Licensed parenting-program content | License | Yes | Quote-based, UNKNOWN | incredibleyears.com | MEDIUM | B P2 |
| Employer benefits brokers/platforms; Medicaid MCOs (TMaH 15-state) | Distribution channel | n/a | Yes | n/a | (channel) | MEDIUM | B P5 |
</content>
