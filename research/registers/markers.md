# markers.md

Unified trend and marker catalog across both concepts, per framework section 9. Verdict codes: V1 (in the first version), V2 (later version), RESEARCH-ONLY (evidence exists but not productizable or crosses claims line, surfaced only as self-report/education), LATER (deferred), REJECT/KILL (dropped). Evidence strength is the strength of the underlying literature (see papers.md), not the in-home realizability, which is flagged separately where weak. Columns: Marker | Indication | Data type | Modality / data source | Evidence strength | Verdict | Concept | Note | Source phase

## Concept A: Elder Home Monitoring (40+ markers across 13 clusters)

| Marker | Indication | Data type | Modality / source | Evidence | Verdict | Concept | Note | Source phase |
|---|---|---|---|---|---|---|---|---|
| Gait speed | Mortality, decline, fall risk | Measurement | Oblique camera pose or radar | HIGH [P1][P2][P3][P19] | V1 (DIFFERENTIATOR) | A | Nadir camera view UNVALIDATED; radar fallback error ~0.02 m/s | A P1, A P2 |
| Gait / stride variability | Fall risk | Measurement | Camera/radar | HIGH [P4] | V1 | A | | A P1 |
| Sit-to-stand time (FTSS) | Recurrent falls | Measurement | Camera or seat occupancy | HIGH [P5] | V1 | A | | A P1 |
| Fall event detection | Acute event | Measurement/event | Radar (T1 local), camera confirm | HIGH need, HIGH FP risk [P17][A-WFP][A-FSFP] | V1 (CORE) | A | Real-world false positive rate is the make-or-break, UNKNOWN | A P1, A P4 |
| Long lie (time on floor) | Serious outcome | Event | Radar + duration gating | HIGH [P7] | V1 (CORE) | A | Highest value, lowest claim risk | A P1 |
| Fall location / self-recovery | Severity | Event | Radar/mesh | HIGH | V1 | A | | A P1 |
| Life space (in-home) | Mortality | Measurement | PIR/door mesh | HIGH outcome, analog-only in-home [P9] | V1 | A | No validated in-home instrument; LSA is neighborhood-scale | A P1 |
| Room dwell / transitions | Activity pattern | Measurement | PIR/door mesh | MEDIUM | V1 | A | | A P1 |
| Sedentary bouts | Activity | Measurement | PIR/mesh | MEDIUM | V1 | A | | A P1 |
| Sleep location / time in bed / bed exits | Sleep, safety | Measurement | Bed BCG mat | HIGH [P15] | V1 | A | | A P1 |
| Circadian IS/IV/RA | Cognitive decline, mortality | Measurement | Actigraphy in literature; PIR/activity in-home | HIGH literature, transfer UNVALIDATED [P8] | V1 | A | Transfer from actigraphy to occupancy stream unvalidated | A P1 |
| Nighttime bathroom frequency (nocturia) | Mortality, fall/fracture | Measurement | PIR/mesh | HIGH [P10] | V1 | A | | A P1 |
| Daytime bathroom frequency | Health pattern | Measurement | PIR/mesh | MEDIUM [P10] | V1 | A | | A P1 |
| Bathroom dwell | Health pattern | Measurement | Radar (no camera) | MEDIUM | V1 | A | Bathroom is no-camera room | A P1 |
| Kitchen meal-prep events | Nutrition, MCI | Measurement | Mesh/camera | LOW, small-n [P13] | V1 | A | Maps to meals/nutrition UNKNOWN | A P1 |
| Out-of-home trips | Social isolation | Measurement | Door mesh | HIGH [P11] | V1 | A | | A P1 |
| Visitor counts | Social contact | Measurement | Mesh | MEDIUM [P11] | V1 | A | | A P1 |
| Self-reported mood | Affective | Self-report | App check-in | HIGH (as journal) | V1 | A | Self-report, not a claim | A P1 |
| Contactless HR/RR | Vitals | Measurement | Bed BCG mat | HIGH lab, real-bedroom UNKNOWN [P15][P20] | V1 | A | Multi-occupant accuracy unknown | A P1 |
| Medication reminder response | Adherence | Self-report/event | App | HIGH (reminders only) | V1 | A | Reminders/adherence only, no dose guidance | A P1 |
| Stove / door safety events | Safety | Event | Contact/mesh | HIGH | V1 | A | | A P1 |
| Home hazard inventory | Fall prevention | Measurement | Camera (shared room) | HIGH [P12] | V1 | A | | A P1 |
| Speech markers (acoustic/linguistic) | Cognition | Inference | Microphone | HIGH literature [P14] | RESEARCH-ONLY | A | Disease inference crosses claims line | A P1 |
| Object misplacement | Cognition | Inference | Camera + scene memory | LOW/research | RESEARCH-ONLY | A | Forces a hub; v2 at earliest | A P1 |
| Repeated questions | Cognition | Inference | Assistant | Research | RESEARCH-ONLY | A | Disease inference | A P1 |
| Dual-task gait cost | Cognition | Measurement/inference | Camera | MEDIUM [P6] | RESEARCH-ONLY | A | Cognition inference | A P1 |
| Gait initiation / freezing | Neuro | Measurement | Camera | Research | RESEARCH-ONLY | A | | A P1 |
| Fluid intake | Hydration | Measurement | Mesh | Research | RESEARCH-ONLY | A | | A P1 |
| Sliding in bed | Sleep/safety | Measurement | Bed mat | Research | RESEARCH-ONLY | A | | A P1 |
| Cognition inference (any proxy) | Cognition | Inference | Any | n/a | RESEARCH-ONLY | A | Any named-disease inference from passive data is a claim | A P1 |
| Furniture surfing | Balance/fall risk | Measurement | Camera | LOW [P18] | LATER | A | No primary in-home effect size | A P1 |
| Plant / pet care | ADL | Measurement | Camera | n/a | REJECT (v1) | A | Low value/high cost | A P1 |
| Dressing detection | ADL | Measurement | Camera | n/a | REJECT (v1) | A | Privacy and value | A P1 |

## Concept B: Pregnancy and Parenting Companion (25 markers scored)

| Marker | Indication | Data type | Modality / source | Evidence | Verdict | Concept | Note | Source phase |
|---|---|---|---|---|---|---|---|---|
| Urgent maternal warning signs bundle (14 signs) | Maternal morbidity/mortality | Self-report + education | App + CDC list | HIGH [MMRC-3619][CDC-HH] | V1 (CORE) | B | Verbatim CDC copy; up to one year postpartum | B P1 |
| Postpartum mood (full year) | Postpartum depression | Self-report | App scale | HIGH [PPD-ONSET][MMRC-3619] | V1 | B | Two onset peaks, 9-17 mo; self-report not instrument | B P1 |
| Antepartum mood and anxiety | Perinatal mental health | Self-report | App scale | HIGH [ANX-DEP] | V1 | B | | B P1 |
| Postpartum blood pressure | Postpartum preeclampsia | Measurement (own cuff) | Pregnancy-validated BP cuff | HIGH [PP-HTN][STRIDE-PG] | V1 | B | Readmission median day 6; education framing of own provider threshold | B P1 |
| Antepartum blood pressure | Hypertensive disorders | Measurement | BP cuff | HIGH [PP-HTN] | V1 | B | BP threshold reminder (feature 14) needs legal review vs 2026 sensor boundary | B P0, B P1 |
| Gestational weight gain | Pregnancy health | Self-report/measurement | Scale/app | HIGH [IOM-09] | V1 | B | Reference ranges by BMI | B P1 |
| Kick counts / fetal movement | Stillbirth risk | Self-report | App | MEDIUM [KICKS] | V1 | B | AFFIRM negative; ACOG endorses awareness | B P1 |
| Gestational-age content | Education | Education | Content corpus | HIGH | V1 | B | | B P1 |
| Partner (paternal) mood | Paternal depression | Self-report | App scale | HIGH [PAT-DEP] | V1 | B | ~8-10%, peak 3-6 mo | B P1 |
| Consent layer | Privacy | System | App | n/a | V1 | B | Resource-owner consent model | B P1 |
| Passive physiological (RHR, HRV, sleep, temp, resp) | Pregnancy trajectory | Derived wearable | Derived scalars (commercial terms) | HIGH trajectory, LOW stratification [AWHS-24][OURA-25] | V2 | B | No raw wearable needed; unstratified normal only | B P1, B P2 |
| Nutrition from meal photos | Diet | Measurement/inference | Photo AI | MEDIUM, ~22% error [FOOD-AI] | V2 | B | Display only | B P1 |
| Glucose display | GDM management | Measurement (display) | CGM/meter | HIGH [CGM-PG] | V2 | B | Display value + lab reference range, no interpretation | B P1 |
| Infant growth | Growth tracking | Measurement | WHO/CDC charts | HIGH [GROWTH] | V2 | B | | B P1 |
| Infant milestones | Development | Self-report/checklist | CDC free checklist | HIGH [MILESTONE] | V2 | B | CDC free; ASQ/Denver II proprietary | B P1 |
| Home uterine activity monitoring | Preterm labor | Measurement | HUAM device | HIGH negative [HUAM] | KILL | B | No maternal/neonatal benefit; FDA-reclassified device path | B P1 |
| Early-childhood content | Parenting | Education | Content | n/a | LATER | B | | B P1 |
| Self-measured fundal height | Pregnancy | Measurement | Self-measure | LOW | LATER | B | | B P1 |
| Affect/emotion from wearable | Mental health | Inference | Wearable physiology | LOW, near-chance cross-person [B P2 sources] | RESEARCH-ONLY / REJECT | B | Generalized cross-device affect near chance; use self-report | B P2 |
</content>
