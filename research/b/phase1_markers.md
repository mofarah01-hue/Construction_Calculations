# CONCEPT B, PHASE 1: MARKER AND TREND CATALOG

Governed by `00_framework.md`. Markers define the data requirement. No wearable is selected here.

## Strategic finding, stated first

The urgent maternal warning signs feature is the strategic center of this product, not a safety appendix to it. The evidence supports treating it as potentially the entire company:

1. It is patient education. The CDC Hear Her and ACOG or AWHONN warning sign lists already instruct every pregnant and postpartum person to watch for these symptoms. Restating them is not a claim, not inference, and not a device function. It sits comfortably inside the general wellness lane (framework section 2).
2. It addresses the leading preventable causes of maternal death. Mental health conditions are the single leading underlying cause of US pregnancy related death (22.7 percent, MMRC 36 states 2017 to 2019), and 53 percent of pregnancy related deaths occur 7 to 365 days postpartum, the window after the last appointment when nobody is watching. More than 80 percent are deemed preventable. [MMRC-3619, HIGH]
3. It requires no wearable. The load bearing inputs are the published warning sign list, gestational or postpartum day, and her self report. This is the finding that de risks the whole concept: the differentiated feature does not depend on raw sensor access.

Everything below is scored against that spine.

---

## 1. FULL MARKER TABLE

Column key: Data type is Self report (SR), Measurement (M), or Inference (I). Fidelity is Consumer, Clinical, or Reference. Confidence on evidence is HIGH, MEDIUM, or LOW. Verdict is V1, V2, LATER, or KILL.

### 1A. The urgent maternal warning signs (the safety layer)

| Marker | Indicates | Evidence [cite] | Data type | Modality or source and fidelity | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Severe headache that will not go away or worsens | Preeclampsia, cerebral event | CDC Hear Her list [CDC-HH, HIGH]; ACOG headaches in pregnancy CO [ACOG-HA22, HIGH] | SR | User taps symptom; app holds the list. Reference | Her own report of new or worsening | Immediate | Direct to care escalation | Restating provider and ACOG instruction. Education, not diagnosis | Zero clinical inference. Validate copy against CDC list verbatim | V1 |
| Vision changes | Preeclampsia | CDC-HH [HIGH]; ACOG-HA22 [HIGH] | SR | Symptom tap. Reference | New onset | Immediate | Direct to care | Education | Copy match | V1 |
| Trouble breathing | Cardiac, embolism, preeclampsia | CDC-HH [HIGH] | SR | Symptom tap. Reference | New onset | Immediate | Direct to care or 911 | Education | Copy match | V1 |
| Chest pain or fast beating heart | Cardiac, embolism | CDC-HH [HIGH] | SR | Symptom tap. Reference | New onset | Immediate | Direct to care or 911 | Education | Copy match | V1 |
| Severe belly or epigastric pain that will not go away | HELLP, preeclampsia, abruption | CDC-HH [HIGH] | SR | Symptom tap. Reference | New onset | Immediate | Direct to care | Education | Copy match | V1 |
| Severe nausea and vomiting (not morning sickness) | Hyperemesis, HELLP | CDC-HH [HIGH] | SR | Symptom tap plus severity scale. Reference | Her own report | Immediate | Direct to care | Education | Copy match | V1 |
| Sudden or severe swelling of face or hands | Preeclampsia | CDC-HH [HIGH] | SR | Symptom tap. Reference | New onset | Immediate | Direct to care | Education | Copy match | V1 |
| Fever of 100.4 F or higher | Infection, sepsis, chorioamnionitis, endometritis | CDC-HH [HIGH] | SR or M | Manual entry or thermometer. Clinical if thermometer | 100.4 F threshold, hard coded | Immediate | Direct to care | Threshold is CDC published, not app derived | Copy and threshold match | V1 |
| Thoughts of harming yourself or your baby | Suicide, the leading postpartum death cause | CDC-HH [HIGH]; MMRC-3619 [HIGH] | SR | Guarded prompt with escalation path. Reference | Any positive | Immediate | Crisis line plus direct to care | Education plus crisis routing. Not a screening instrument | Escalation must be enforced, not prompted. Highest liability | V1 |
| Heavy vaginal bleeding or fluid leaking after birth | Postpartum hemorrhage, retained products | CDC-HH [HIGH] | SR | Symptom tap plus pad count. Reference | Her own report | Immediate | Direct to care or 911 | Education | Copy match | V1 |
| Vaginal bleeding or fluid leaking during pregnancy | Abruption, preterm rupture | CDC-HH [HIGH] | SR | Symptom tap. Reference | Any | Immediate | Direct to care | Education | Copy match | V1 |
| Baby movement stopping or slowing | Fetal compromise, stillbirth risk | CDC-HH [HIGH]; ACOG fetal movement | SR | Symptom tap plus kick count history | Her own pattern | Immediate (third trimester) | Direct to care | Education | Copy match | V1 |
| Dizziness or fainting | Hemorrhage, cardiac, hypertensive | CDC-HH [HIGH] | SR | Symptom tap. Reference | New onset | Immediate | Direct to care | Education | Copy match | V1 |
| Swelling, redness, or pain in the leg | Deep vein thrombosis | CDC-HH [HIGH] | SR | Symptom tap. Reference | New onset | Immediate | Direct to care | Education | Copy match | V1 |
| Overwhelming tiredness | Cardiomyopathy, anemia, thyroid, depression | CDC-HH [HIGH] | SR | Symptom tap. Reference | Her own baseline | Days | Direct to care if with other signs | Education. Low specificity noted | Copy match | V1 |

CDC Hear Her also carries the instruction that some problems can occur up to a year after delivery. That statement is the product thesis in one line and is quoted verbatim in the copy. [CDC-HH, HIGH]

### 1B. Blood pressure and preeclampsia

| Marker | Indicates | Evidence [cite] | Data type | Modality or source and fidelity | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Home blood pressure, antepartum | Gestational hypertension, preeclampsia | ACOG hypertension guidance; STRIDE BP [STRIDE-PG, HIGH] | M | Validated cuff, manual or Bluetooth. Clinical if validated cuff | Her own trend plus provider threshold | Hours to days | Trend plus threshold reminder, call provider | Displaying her readings and her provider threshold. Not interpretation | Cuff must be validated for pregnancy; only 7 percent of pharmacy devices are [STRIDE-PG] | V1 |
| Home blood pressure, POSTPARTUM | Postpartum preeclampsia, the unwatched window | Readmission median 6 days, range 2 to 15; hypertension foremost cause of postpartum readmission; ACOG BP check day 3 to 10; most acute readmissions day 10 to 20, before the 6 week visit [PP-HTN, HIGH] | M | Validated cuff. Clinical | Her own trend plus threshold | Hours to days | Trend plus reminder to call | Education on a self measured value | Same cuff validation issue | V1, highest value |
| Rapid weight jump plus swelling | Preeclampsia adjunct | Adjunctive only; low specificity | SR or M | Scale plus symptom. Consumer | Her own | Days | Prompt to check BP and symptoms | Reflection of self measured inputs | Do not present as a preeclampsia test | V2 |

### 1C. Antepartum physiological, passive

| Marker | Indicates | Evidence [cite] | Data type | Modality or source and fidelity | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Resting heart rate trajectory | Normal cardiovascular adaptation; illness onset | Apple Womens Health Study, 757 pregnancies: prepregnancy median 65.0 bpm rising to 75.5 bpm third trimester, reversing about 7 weeks before birth [AWHS-24, HIGH] | M | Wrist wearable, derived. Consumer | Her own plus population curve | Weeks | Normalize and educate. Illness deviation flag | Trend versus her baseline and a published curve. Explicitly permitted (framework 2) | Requires wearable data access (Phase 2). Curve exists but not stratified by BMI, parity, age | V2 |
| HRV trajectory | Autonomic adaptation | AWHS-24: prepregnancy 39.9 ms to third trimester nadir 29.9 ms, rebound near term [HIGH] | M | Wrist wearable, derived. Consumer | Her own plus curve | Weeks | Educate and normalize | Trend and reference only | Same wearable dependency; affect inference NOT supported (B4) | V2 |
| Respiratory rate trajectory | Cardiorespiratory adaptation, illness | Rises modestly across gestation; Oura ring large observational analysis [OURA-25, MEDIUM] | M | Ring or wrist, derived. Consumer | Her own plus curve | Weeks | Educate; illness flag | Trend and reference | Wearable dependency; magnitude of change small | V2 |
| Skin or wrist temperature | Ovulation history, illness, circadian shift | Nocturnal temperature elevated in pregnancy, falls near term [OURA-25, MEDIUM] | M | Ring or wrist, derived. Consumer | Her own | Days | Illness onset education | Trend only | Wearable dependency; absolute skin temp is not core temperature | V2 |
| Sleep duration and fragmentation | Recovery, mood correlate | AWHS-24: prepregnancy 7.2 h, first trimester 7.4 h, postpartum nadir 6.2 h [HIGH] | M plus SR | Wearable derived or self report. Consumer | Her own plus curve | Days to weeks | Sleep guidance; shown against mood as two lines | Trend and reference; correlation shown, not causal claim | Wearable improves fidelity but self report suffices | V2, self report path V1 |
| Activity and step decline | Deconditioning; wellbeing | AWHS-24: steps, exercise, stand minutes decreased each trimester, nadir postpartum [HIGH] | M | Phone or wearable pedometer. Consumer | Her own plus curve | Weeks | General activity encouragement | Trend and encouragement | Phone pedometer removes wearable dependency | V2 |

### 1D. Antepartum self report

| Marker | Indicates | Evidence [cite] | Data type | Modality or source and fidelity | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Nausea and vomiting severity plus hyperemesis threshold | Hyperemesis gravidarum | ACOG NVP guidance; PUQE score is an instrument, use own scale | SR | Daily scale of own design | Her own | Days | Hydration and care prompts; escalate at severe | Journal plus education | Do not return PUQE as a clinical result | V1 |
| Fetal movement and kick counts | Fetal wellbeing | Count the Kicks observational 30 to 32 percent stillbirth reduction; AFFIRM RCT negative for awareness package alone; ACOG endorses movement awareness [KICKS, MEDIUM] | SR | Third trimester kick timer | Her own pattern | Same day | Care prompt on reduced movement | Long established self report practice | Present as awareness, not a screen. Evidence is mixed, disclose it | V1 |
| Daily mood, own scale | Mood trend | Journal, not instrument (framework 2, B4) | SR | Single daily question | Her own | Days to weeks | Trend, streak of low days, conversation prompt | Journal. Explicitly not EPDS or PHQ-9 | Zero, provided no instrument is scored | V1 |
| Anxiety self report | Anxiety trend | Antenatal anxiety pooled 18 to 25 percent, up to 37 percent any symptoms [ANX-DEP, HIGH] | SR | Single daily question | Her own | Days | Trend and education | Journal | Same | V1 |
| Pelvic and back pain, contractions | Discomfort; preterm labor signal | ACOG | SR | Symptom log plus contraction timer | Her own | Same day | Education; escalate on pattern | Journal plus education | Contraction timer is a clock, not a monitor | V1 |
| Sleep quality, appetite | Wellbeing correlates | Supportive | SR | Daily questions | Her own | Days | Guidance | Journal | Zero | V1 |

### 1E. Weight, nutrition, glucose

| Marker | Indicates | Evidence [cite] | Data type | Modality or source and fidelity | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Gestational weight gain vs guideline range | On or off recommended trajectory | IOM or NASEM 2009: underweight 28 to 40 lb, normal 25 to 35 lb, overweight 15 to 25 lb, obese 11 to 20 lb by prepregnancy BMI [IOM-09, HIGH] | M plus SR | Home scale or manual entry. Consumer | Her prepregnancy BMI plus published range | Weeks | Show her band; general guidance | Public non diagnostic reference range | Zero clinical inference; range is published | V1 |
| Micronutrient intake (folate, iron, iodine, DHA, calcium) | Meeting pregnancy requirements | ACOG and NIH nutrition guidance | SR | Self logged or supplement tracker | Established requirements | Days | General healthy eating guidance | Generic nutrition education only; not condition specific | Nutrition tied to a condition (GDM, anemia) leaves the lane | V2 |
| Diet from photographs | Logging aid | Photo nutrient estimation median absolute error about 22 percent, range 8 to 55 percent; portion is the error source [FOOD-AI, MEDIUM] | M or I | Phone camera plus model. Consumer | n/a | Immediate | Accurate enough to LOG, not to quantify nutrients | Present as a food diary, not a nutrient claim | Do not display derived calorie or nutrient totals as fact | V2, logging only |
| Hydration | Wellbeing | Supportive | SR | Daily log | Her own | Days | Encouragement | Journal | Zero | V2 |
| Glucose, if she wears a CGM or has GDM | Glycemic pattern | CONCEPTT and GDM RCTs show CGM benefit in managed diabetes [CGM-PG, HIGH] | M | CGM or meter, ingested. Clinical | Her provider targets | Hours | DISPLAY and trend only | Show the value and her provider target; do not interpret | Interpreting glucose is clinical decision support. Display only | V2 |

### 1F. Fetal, gestational, preterm

| Marker | Indicates | Evidence [cite] | Data type | Modality or source and fidelity | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Gestational age developmental content | Table stakes | Every competitor ships this | Reference | Gestational day drives content | LMP or due date | Weekly | Education and engagement | Content, not measurement | Content licensing and clinical review cost (Phase 2) | V1 (engagement spine) |
| Fundal height, self measured | Growth proxy | Low reliability self measured | SR or M | Tape measure entry. Consumer | Her own | Weeks | Log only | Journal | Unreliable when self measured; do not flag | LATER |
| Ultrasound and appointment results | Clinical status | Ingested not generated | M | Manual entry or portal ingest. Clinical | Her records | n/a | Store and display | Displaying her own records | No interpretation | V2 |
| Contraction frequency and timing | Preterm labor signal | ACOG; self timing is standard | SR | Contraction timer | Her own | Same day | Educate; escalate on pattern | A clock. Not uterine monitoring | Do not market as detecting preterm labor | V1 |
| Home uterine activity monitoring | Preterm labor | ACOG and USPSTF do NOT recommend; no benefit; FDA reclassified Class III to II in 2001 [HUAM, HIGH] | M | Tocodynamometer. Clinical | n/a | n/a | None supported | Cautionary regulatory history | Evidence says no benefit. Do not build | KILL |

### 1G. Postpartum physiological and mood

| Marker | Indicates | Evidence [cite] | Data type | Modality or source and fidelity | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Postpartum BP (see 1B) | Postpartum preeclampsia | [PP-HTN, HIGH] | M | Validated cuff. Clinical | Her trend plus threshold | Hours to days | Reminder to call | Education | Cuff validation | V1 |
| Postpartum bleeding, self reported | Hemorrhage, retained products | CDC-HH [HIGH] | SR | Pad count log | Her own | Same day | Escalate on heavy | Education | Zero | V1 |
| Fever postpartum | Endometritis, mastitis, sepsis | CDC-HH threshold 100.4 F [HIGH] | SR or M | Thermometer or entry | 100.4 F | Immediate | Direct to care | Threshold is published | Copy match | V1 |
| Incision or perineal healing, self reported | Wound infection | CDC-HH (redness, pain) [HIGH] | SR | Symptom log | Her own | Days | Care prompt | Education | Zero | V1 |
| RHR and HRV recovery toward prepregnancy | Recovery trajectory | AWHS-24 shows postpartum nadir and recovery [MEDIUM] | M | Wearable derived. Consumer | Her prepregnancy baseline | Weeks | Educate; underexploited signal | Trend and reference | Wearable dependency; requires prepregnancy baseline capture | V2 |
| Sleep debt accumulation | Wellbeing, mood risk | AWHS-24 postpartum nadir 6.2 h [MEDIUM] | M or SR | Wearable or self report | Her own | Days | Guidance and partner nudge | Trend | Self report suffices | V2 |
| Daily postpartum mood across the FIRST YEAR | Postpartum mood disorder | PPD two onset peaks, average onset about 14 weeks, late onset 2 to 12 months, symptoms elevated to 9 to 17 months [PPD-ONSET, HIGH]; mental health leading death cause, 63 percent of MH deaths at day 43 to 365 [MMRC-3619, HIGH] | SR | Single daily question, full year | Her own | Weeks | Trend, streak, conversation and care prompt | Journal, not EPDS. Tracks the real onset window competitors miss at 6 weeks | Must not stop at 6 weeks; must not score an instrument | V1, strategic |
| Intrusive thoughts and bonding | OCD, psychosis, bonding difficulty | Question itself carries risk; needs escalation path | SR | Carefully worded, guarded prompt | Her own | Weeks | Normalize plus escalation for harm content | Education plus routing | Wording and escalation are the entire risk. Design with clinician | V1, handled carefully |

### 1H. The partner and consent

| Marker | Indicates | Evidence [cite] | Data type | Modality or source and fidelity | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Paternal or non birthing partner perinatal depression | Partner is a patient too | Pooled prevalence about 8 to 10 percent, peak 3 to 6 months postpartum [PAT-DEP, HIGH] | SR | Partner own daily or weekly mood question | His own | Weeks | Trend and resources for him | Journal for the partner. Differentiator no competitor serves | Same as maternal mood: journal not instrument | V1, differentiator |
| Partner facing disclosure of her state | Consent surface | Disclosure of one person health data to another (B3) | Consent metadata | Granular, revocable grants with visible indicator | Her explicit grants | Real time | She controls every element he sees | Excellent product only with consent; surveillance without it | Consent architecture is a Phase 3 build; must be a feature | V1 (as consent layer) |

### 1I. Infant and early childhood

| Marker | Indicates | Evidence [cite] | Data type | Modality or source and fidelity | Baseline | Time to signal | Actionability | Defensible framing | Validation burden | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|
| Infant growth vs charts | Growth tracking | WHO standards 0 to 24 months, CDC charts 2 years and up, both free public [GROWTH, HIGH] | M plus SR | Manual entry of weight, length, head circ. Reference | Published percentiles | Weeks | Plot percentile, general guidance | Plotting on a public chart; not a diagnosis | Free reference; do not flag failure to thrive | V2 |
| Developmental milestones | Development tracking | CDC milestone checklists FREE; ASQ (Brookes) and Denver II are PROPRIETARY, licensed [MILESTONE, HIGH] | SR | Checklist against CDC milestones | CDC age bands | Monthly | Education and encouragement | CDC checklist is free educational content | Screening instruments (ASQ, M-CHAT) are clinical tools, risk register | V2, CDC list only |
| Feeding and sleep consolidation | Routine tracking | Supportive | SR | Logs | Infant own | Days | Guidance | Journal | Zero | V2 |
| Early childhood 2 yr plus: boundaries, discipline, autonomy | Parenting guidance | Evidence real but weaker, contested, culturally variable | Content | Curated content | n/a | n/a | Present a range, disclose contested areas | Content and trust product, not a data product | Reputational and content risk of taking a position | LATER |

---

## 2. RANKED V1 SHORTLIST

Ranking metric: actionability multiplied by evidence strength, divided by data acquisition cost. Data acquisition cost is lowest for self report and published reference, highest for raw wearable sensor access.

| Rank | Marker or bundle | Actionability | Evidence | Data cost | Why it ranks here |
|---|---|---|---|---|---|
| 1 | Urgent maternal warning signs logger and escalation (1A) | Highest, prevents death | HIGH, CDC and ACOG verbatim | Lowest, list plus self report | The company. No wearable, no inference, no instrument. Addresses the leading preventable death causes |
| 2 | Postpartum daily mood across the full year (1G) | Highest, leading death cause | HIGH prevalence and mortality data | Lowest, one daily question | Tracks the real 2 to 12 month onset window that six week screening misses. The payer reason |
| 3 | Postpartum blood pressure, home cuff (1B, 1G) | Highest, top readmission cause | HIGH | Low, validated cuff she buys | The unwatched window, day 3 to 20. Cuff is a cleared device; app only displays and reminds |
| 4 | Antepartum blood pressure, home cuff (1B) | High | HIGH | Low, validated cuff | Preeclampsia is the case that decides if the product matters |
| 5 | Antepartum daily mood and anxiety, own scale (1D) | High | HIGH prevalence | Lowest | Journal, defensible, expected, feeds the conversation prompt |
| 6 | Gestational weight gain vs IOM range (1E) | Medium | HIGH, public range | Low | Public reference, zero inference, easy engagement |
| 7 | Fetal movement and kick counts (1D, 1F) | High third trimester | MEDIUM, mixed | Lowest | Established self report practice; frame as awareness |
| 8 | Gestational age developmental content (1F) | Medium, engagement | HIGH as table stakes | Medium, licensing | Retention spine; every competitor has it; cost is content and clinical review |
| 9 | Paternal or partner perinatal depression check in (1H) | Medium | HIGH prevalence | Lowest | Differentiator; the partner is an unserved patient |
| 10 | Partner facing disclosure and consent layer (1H) | Enabling | n/a | Build cost | Converts surveillance into product; required for anything partner facing |

The top 5 all clear on self report and published reference alone. None of the top 5 requires raw wearable data. Passive physiological markers (RHR, HRV, respiratory rate, temperature) rank as V2 enhancements, not V1 dependencies.

---

## 3. DATA REQUIREMENT MATRIX (input to Phase 2)

For each V1 marker: what data, from where, at what fidelity. This determines whether the wearable dependency is fatal. It is not: no V1 marker requires raw consumer wearable sensor data.

| V1 marker | Data element | Source | Fidelity required | Wearable required |
|---|---|---|---|---|
| Warning signs logger | The canonical warning sign list; symptom taps; gestational or postpartum day | CDC Hear Her plus ACOG (list); user (taps); user due date or delivery date (day) | Reference (list must match source verbatim); self report | No |
| Warning signs escalation | Local emergency number, crisis line, her provider contact | Static config plus user entry | Reference | No |
| Postpartum mood, full year | One daily mood value; days since delivery | User self report; delivery date | Self report, longitudinal to 365 days | No |
| Self harm and intrusive thought prompt | Guarded question response; crisis routing | User; static crisis config | Self report plus enforced escalation | No |
| Postpartum BP | Systolic and diastolic; her provider threshold; postpartum day | Validated home cuff (manual or Bluetooth); user enters threshold | Clinical (cuff validated for pregnancy per STRIDE BP) | No (cuff is a separate cleared device, not a wristband) |
| Antepartum BP | Same as above; gestational week | Validated home cuff; user | Clinical | No |
| Antepartum mood and anxiety | One to two daily values | User self report | Self report | No |
| Gestational weight gain | Prepregnancy BMI (height, prepregnancy weight); serial weights | User entry or home scale; IOM range table (static) | Consumer scale; reference table | No |
| Fetal movement and kick counts | Kick timer sessions; third trimester flag | User; gestational week | Self report | No |
| Gestational content | Gestational day; licensed obstetric content corpus | Due date; licensed and clinically reviewed content (Phase 2) | Reference content | No |
| Partner mood check in | One mood value from the partner | Partner self report | Self report | No |
| Consent and disclosure | Per element grant and revoke state; visible share indicator | Mother explicit action | Consent metadata, revocable in real time | No |

Fidelity note carried to Phase 2: the only clinical fidelity input in V1 is blood pressure, and it comes from a cuff the user already buys, not from a wristband. The wearable question therefore does not gate V1. It gates V2 physiological enhancement only.

---

## 4. THE TWO DAILY SURFACES (copy, 30 seconds each)

Written as shipping copy. Warning sign wording tracks the CDC Hear Her list. Bracketed tokens are personalization variables.

### 4A. What SHE sees each morning (postpartum example, day 11)

> Good morning, [Name]. You are 11 days postpartum.
>
> How are you today? [ tap: Rough | OK | Good ]  (one tap, this is just for you)
>
> This week your body: your blood pressure readings are trending flat and in range. Nice. [ Add today reading ]
>
> Worth 20 seconds: the postpartum weeks are when serious problems are most often missed, because your next appointment is still weeks away. Call your care team now, day or night, if you have any of these:
>
> - a bad headache that will not go away or a change in your vision
> - trouble breathing, chest pain, or a racing heart
> - heavy bleeding, or soaking a pad in an hour
> - swelling, redness, or pain in one leg
> - a fever of 100.4 F or higher
> - severe belly pain
> - thoughts of harming yourself or your baby
>
> These can happen up to a year after birth. If something does not feel right, you are not overreacting. [ Call my care team ]  [ See all signs ]
>
> [ Anything on your mind today? ]  (private journal)

### 4B. What HE sees each morning (partner view, day 11, only what she has shared)

> Good morning. [Name] is 11 days postpartum. Here is what she chose to share.
>
> Today she is likely: still bleeding and healing, running on broken sleep, and her hormones are shifting fast. This is the hardest stretch.
>
> One thing that helps today: take the 2 am feed or the morning so she gets one four hour block of sleep. Ask nothing of her before coffee.
>
> Watch with her, not over her. If you notice any of these, help her call her care team today: a headache that will not quit, trouble breathing or chest pain, heavy bleeding, a swollen painful leg, a fever, or her saying she feels hopeless or unsafe. Serious problems can appear up to a year after birth.
>
> And you: how are you doing this week? [ tap: Struggling | OK | Good ]  (about 1 in 10 new dads hit depression too; this is for you)
>
> [ She controls what you see here. Shared: mood, BP trend. Not shared: journal. ]

Design rule enforced in both: the warning sign strip is always present, always taps to the full CDC list and a one tap call, and never depends on any inference. His view renders only elements she has granted, with the grant state visible to both.

---

## 5. MARKERS REQUIRING DATA UNOBTAINABLE UNDER CURRENT CONSUMER WEARABLE TERMS

These markers depend on raw or continuous sensor streams that most consumer vendors expose as derived metrics only, gate behind research agreements, or forbid in developer terms. Confirmation is Phase 2 (`shared_wearable_data_access.md`), but flagged here as the constraint.

| Marker | Data needed | Why it may be unobtainable | Fallback |
|---|---|---|---|
| RHR trajectory | Continuous or nightly resting HR | Most vendors expose derived RHR via API with commercial restrictions; some forbid resale or acting on it | Use vendor derived RHR where terms permit; else self reported symptoms |
| HRV trajectory | Beat to beat or derived HRV | Raw PPG almost never exposed commercially; derived HRV varies by vendor algorithm, not comparable to published curves | Derived HRV where permitted; do not benchmark against literature curves computed differently |
| Respiratory rate | Continuous RR | Derived only, vendor specific, small change magnitude | Vendor derived where permitted |
| Skin or wrist temperature | Continuous skin temperature | Derived nightly deviation only on most rings and bands; absolute skin temp restricted or absent | Vendor derived deviation where permitted |
| Objective sleep staging | Accelerometer plus PPG derived stages | Raw accelerometer rarely exposed; staging is proprietary | Self reported sleep quality and duration |
| Postpartum RHR and HRV recovery | Prepregnancy baseline plus continuous postpartum | Requires enrollment before conception AND raw or derived access | Rarely available; treat as research feature only |
| Continuous SpO2 and raw PPG | Raw photoplethysmography | Effectively never available under consumer commercial terms | None; not a V1 or V2 dependency |

Markers that DIE outright regardless of wearable terms:
- Home uterine activity monitoring: KILL on evidence, not on data access. ACOG and USPSTF do not recommend it; RCTs show no benefit. [HUAM, HIGH]
- Passive affect or mood inference from physiology: not supported by evidence (B4). Redesign as self report, which is cheaper, accurate, and defensible.
- Nutrient quantification from food photos: accurate enough to log, not to state nutrient totals (median error about 22 percent). Ships as a diary, not a nutrient claim.

---

## Register Entries

### papers (append to `/research/registers/papers.md`)

| ID | Citation | Establishes | Design or N | Confidence | Supports marker |
|---|---|---|---|---|---|
| MMRC-3619 | CDC, Pregnancy Related Deaths: Data From Maternal Mortality Review Committees in 36 US States, 2017 to 2019. archive.cdc.gov/www_cdc_gov/maternal-mortality/php/data-research/mmrc-2017-2019.html | Mental health leading underlying cause (22.7 pct); 53 pct of deaths 7 to 365 days postpartum; MH deaths 63 pct at day 43 to 365; >80 pct preventable | 36 state MMRC review | HIGH | Warning signs; postpartum mood |
| AWHS-24 | Trends in sensor based health metrics during and after pregnancy: descriptive data from the Apple Womens Health Study. PMC11408385 (2024). sciencedirect.com/science/article/pii/S2666577824000820 | RHR 65.0 to 75.5 bpm; HRV 39.9 to 29.9 ms nadir; sleep 7.2 to 6.2 h; activity declines each trimester; near term reversal | 757 pregnancies, 733 participants, Apple Watch, descriptive, not stratified by BMI/parity/age | HIGH (trajectory), LOW (stratification) | Passive physiological |
| OURA-25 | Temporal Trajectories in Sleep, Temperature, Cardiorespiratory and Activity Metrics via Oura Ring During Pregnancy. PubMed 40996267; mhealth.jmir.org/2025/1/e80213 | Respiratory rate rise; nocturnal temperature elevation falling near term | Large observational, Oura ring | MEDIUM | Respiratory rate; skin temperature |
| PP-HTN | Factors associated with early readmission for postpartum hypertension. PMC11197109; Postpartum preeclampsia defining its place, AJOG S0002-9378(20)31201-1 | Readmission median 6 days (2 to 15); hypertension foremost postpartum readmission cause; ACOG BP check day 3 to 10; readmit day 10 to 20 before 6 week visit | Cohort and review | HIGH | Postpartum BP and preeclampsia |
| IOM-09 | Institute of Medicine (NASEM) 2009 Weight Gain During Pregnancy; ACOG committee opinion, acog.org/clinical/clinical-guidance/committee-opinion/articles/2013/01/weight-gain-during-pregnancy | GWG ranges by prepregnancy BMI: 28 to 40, 25 to 35, 15 to 25, 11 to 20 lb | Guideline | HIGH | Gestational weight gain |
| ANX-DEP | Prevalence of antenatal depression meta-analyses (S0272735820301203); antenatal and postnatal anxiety, Br J Psychiatry | Antenatal depression pooled 20.7 pct any, 15.0 pct major; antenatal anxiety 18 to 25 pct, 37 pct any symptoms | Systematic reviews, 173 and 72 studies | HIGH | Antepartum mood and anxiety |
| PPD-ONSET | Timing of Postpartum Depressive Symptoms, cdc.gov/pcd/issues/2023/23_0107.htm; IGEDEPP early vs late onset PMC11059250 | Two onset peaks; average onset about 14 weeks; late onset 2 to 12 months; elevated symptoms 9 to 17 months | Cohort and GWAS cohort | HIGH | Postpartum mood full year |
| PAT-DEP | Cameron et al., Prevalence of paternal depression in pregnancy and postpartum, updated meta-analysis. pubmed.ncbi.nlm.nih.gov/27475890; Perinatal depression and anxiety in both parents, PMC9233234 | Paternal perinatal depression about 8 to 10 pct; peak 3 to 6 months | Meta-analysis, 74 studies, 41,480 | HIGH | Partner depression |
| KICKS | AFFIRM cluster RCT (Lancet 2018); Count the Kicks evidence, countthekicks.org/why-we-count/evidence | AFFIRM negative for awareness package; observational 30 to 32 pct stillbirth reduction; ACOG endorses movement awareness | Cluster RCT plus observational | MEDIUM | Fetal movement |
| HUAM | ACOG and USPSTF policy; AHRQ evidence report; FDA Home Uterine Activity Monitors Class II guidance | Not recommended; no maternal or neonatal benefit; FDA reclassified III to II in 2001 | Policy and RCT synthesis | HIGH | Home uterine monitoring (KILL) |
| FOOD-AI | Evaluation of AI nutrient estimation from meal photographs, PMC11858203; commercial system testing | Median absolute error about 22 pct (8 to 55); portion is main error; ID 85 to 95 pct top 1 | Benchmark studies | MEDIUM | Diet from photographs |
| CGM-PG | CONCEPTT, Lancet 2017 PMC5713979; RT-CGM in GDM RCT, Diabetes Care 2025 | CGM improves glycemic control and time in range in managed diabetes and GDM | Multicenter RCTs | HIGH | Glucose display |
| STRIDE-PG | STRIDE BP validated devices for pregnancy, stridebp.org/pregnancy-pdf; Lack of validated BP devices in pharmacies, Hypertens Res 2025 | Only about 7 pct of pharmacy BP devices validated for pregnancy | Device survey | HIGH | Blood pressure cuff selection |
| GROWTH | CDC and AAP: WHO standards 0 to 24 months, CDC charts 2 yr plus; MMWR RR5909 | Which chart when; both free public | Guideline | HIGH | Infant growth |
| MILESTONE | CDC developmental milestones (free); Brookes ASQ and Denver II (proprietary) | CDC checklist free; ASQ and Denver II licensed | Reference | HIGH | Infant milestones |

### markers (append to `/research/registers/markers.md`)
All rows in section 1 above are marker entries for Concept B. Verdicts: 25 markers scored; V1 = warning signs bundle (14 signs) plus postpartum mood, antepartum and postpartum BP, antepartum mood and anxiety, GWG, kick counts, gestational content, partner mood, consent layer; V2 = passive physiological, nutrition, glucose, growth, milestones; KILL = home uterine activity monitoring; LATER = early childhood content, self measured fundal height.

### sources (append to `/research/registers/sources.md`)
| Source | URL | Pub or accessed | Used for | Credibility |
|---|---|---|---|---|
| CDC Hear Her, Urgent Maternal Warning Signs [CDC-HH] | cdc.gov/hearher/maternal-warning-signs/index.html | Accessed 2026-07-10 | Verbatim warning sign list, fever threshold, up to a year statement | HIGH, primary |
| ACOG, Headaches in Pregnancy and Postpartum CO [ACOG-HA22] | journals.lww.com/greenjournal/abstract/2022/05000/headaches_in_pregnancy_and_postpartum__acog.37.aspx | 2022, accessed 2026-07-10 | Headache and vision warning framing | HIGH, primary |
| AIM, Urgent Maternal Warning Signs | saferbirth.org/aim-resources/aim-cornerstones/urgent-maternal-warning-signs | Accessed 2026-07-10 | Standardized list cross check | HIGH |
| Plus every paper URL in the papers table above | | Accessed 2026-07-10 | As noted per row | see per row |

---

## Open Questions

1. Normative passive physiological curves stratified by maternal age, BMI, and parity: the Apple and Oura studies publish trajectories by gestational week but NOT adequately stratified by these covariates. Stratified published curves appear to be UNKNOWN. This constrains V2 personalization to individual baseline plus an unstratified population mean. Impact: passive markers cannot claim covariate adjusted normalcy.
2. Exact current CDC Hear Her list version and whether the 14 to 15 item wording has changed in 2025 to 2026: direct page fetch returned 403; list content confirmed via CDC search index and state health department mirrors. Item by item wording should be re verified against the live CDC page before shipping copy.
3. Whether presenting the CDC self harm warning sign with a crisis route, without scoring EPDS or PHQ-9, is sufficient for postpartum mental health capture, or whether payers will require a validated instrument for reimbursement. Enforcement posture on consumer app instrument use is a Phase 0 and Phase 2 item.
4. Which specific pregnancy validated home BP cuffs (STRIDE BP list) expose a Bluetooth API for ingestion, and at what cost. Device level detail is Phase 2.
5. Respiratory rate and skin temperature change magnitudes across gestation: directionally confirmed, precise trimester values not yet extracted from primary Oura paper (403 on direct fetch).
6. Postpartum mortality figure precision: 22.7 pct (2017 to 2019 MMRC) versus 27.7 pct (2022 summary via MMHLA). Both cite mental health as leading; use the primary MMRC figure and re verify the 2022 update from CDC primary.

## Assumptions Made

1. The row structure follows the task specification (Marker, Indicates, Evidence, Data type, Modality and fidelity, Baseline, Time to signal, Actionability, Defensible framing, Validation burden, Verdict) because Concept A Phase 1 does not yet exist to mirror. If Concept A later defines a different structure, reconcile.
2. Data acquisition cost ordering (self report < published reference < cleared companion device < derived wearable < raw wearable) is a founder facing engineering judgment used to rank, not a researched cost. Validate against Phase 2 wearable and device findings.
3. The two daily surfaces are illustrative shipping copy, not clinically reviewed. All warning sign copy must pass clinical review and verbatim source match before launch.
4. Treating home uterine activity monitoring as KILL assumes the product will not pursue a cleared medical device path. Consistent with the general wellness positioning (framework 2).

## Confidence Summary

Overall confidence: HIGH on the strategic conclusion and the V1 shortlist. The warning signs feature, postpartum mood across the full year, and postpartum blood pressure are supported by primary CDC, ACOG, MMRC, and peer reviewed sources, and none requires raw wearable data. That is the load bearing finding and it is robust.

Weakest elements: (1) stratified normative physiological curves by age, BMI, and parity appear not to exist in published form, which caps V2 personalization; (2) precise trimester magnitudes for respiratory rate and skin temperature were not extracted from primary text due to publisher fetch blocks; (3) the exact live wording and version of the CDC Hear Her list must be re verified against the primary page before copy ships, since the primary URL returned 403 and content was confirmed via the CDC search index and official mirrors. None of these weaknesses touches the V1 core, all of which stands on self report and published reference.
