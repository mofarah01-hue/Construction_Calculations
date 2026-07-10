# CONCEPT B, PHASE 0: SCOPE NORMALIZATION

Governed by `00_framework.md` (positioning and claims boundary, section 2). Positioning is general wellness, settled. This file does not relitigate that decision. It normalizes scope, inventories features, classifies them, builds the claims matrix, and defines the language model safety envelope.

Research cutoff for this file: 2026-07-10. The FDA revised its General Wellness and Clinical Decision Support guidances on 2026-01-06. That revision is current and materially changes the sensor analysis below. Treat any pre 2026 regulatory summary as superseded.

---

## 1. ONE PAGE RESTATEMENT

A subscription companion for first time parents spanning pregnancy, postpartum, and early childhood. A grounded language model layer fronts the whole surface, personalized by three inputs: maternal wearable physiology, ingested lab and biomarker data, and gestational or child developmental stage. It speaks to the mother and, separately and only by her granular revocable consent, to the partner. Postpartum is first class. The developmental layer continues into toddlerhood.

The strategic center is not artificial intelligence mood inference. It is the set of urgent maternal warning signs that CDC and the Alliance for Innovation on Maternal Health (AIM) already instruct every pregnant and postpartum person to watch for, surfaced at the right moment to an exhausted person who is not paying attention, in the postpartum window when no clinician is watching. That is patient education. It makes no diagnostic claim. It addresses the leading preventable causes of maternal death. It may be the entire company.

### SETTLED vs OPEN

| Dimension | SETTLED | OPEN |
|-----------|---------|------|
| Regulatory lane | General wellness, not a medical device | Whether the BP threshold reminder and any physiological alarm survive the 2026-01-06 FDA sensor boundary (section 4, landmine 6) |
| Claims posture | Self report is a journal, not a claim. Measurement plus reference is not a claim. Inference of a named disease is a claim. | Whether administering and scoring EPDS or PHQ-9 as an in app result stays in the lane, and at what licensing and escalation cost (section 4, landmine 2) |
| Safety layer | Hard coded, deterministic, enforced, not prompted. Runs before the model. | Exact copy and legal review of every escalation string |
| Business model | Not settled by this phase. Framework B6 flags the pregnancy churn cliff and that winners sell to payers and employers, not parents | Channel. Deferred to Phase 5 |
| Wearable dependency | Not settled. Framework B2 flags most vendors expose derived metrics only | Deferred to Phase 2 and `shared_wearable_data_access.md` |
| Lab model | Ingest what her OB already ordered is the presumptive answer (framework B1) | Deferred to Phase 2 |
| Partner disclosure | Consent must be granular, revocable, visible. A feature, not a checkbox | Architecture deferred to Phase 3 |
| Parenting layer (age 2+) | Content and trust product, weak and culturally contested evidence base | Whether the product takes a position or presents a range. Deferred to Phase 2/4 |

Two founder assumptions are contradicted by evidence and flagged now, not built around quietly (framework rule 7.8): B1 (cash pay lab panel duplicates covered prenatal labs) and B5 (at home ultrasound is a Class II device, not a feature). Both are parked. See Assumptions Made.

---

## 2. FEATURE INVENTORY (NUMBERED)

| # | Feature | Primary data type | One line |
|---|---------|-------------------|----------|
| 1 | Maternal physiological tracking | Measurement | RHR, HRV, respiratory rate, skin temperature, sleep, activity. Display, trend vs own baseline, trend vs published normative pregnancy curve |
| 2 | Lab and biomarker ingestion | Ingested measurement | Display the value she already has with the reference range her lab printed. Explain what the analyte is |
| 3 | Personalized nutrition guidance | Education plus self report | Generic healthy eating personalized to trimester, gestational weight gain vs guideline range by pre pregnancy BMI |
| 4 | Sleep guidance | Education plus measurement | Sleep hygiene, trimester normalization, sleep duration and fragmentation trend |
| 5 | Symptom normalization and education | Education | Explain and normalize common pregnancy symptoms. Restate what her provider and ACOG told her to watch for |
| 6 | Week by week fetal development content | Education | Gestational age driven content. Table stakes. Every competitor has it |
| 7 | Partner facing guidance | Education plus consented disclosure | What is happening, what she may be experiencing, what would help. Every element about her is a disclosure she grants |
| 8 | Mood and stress support | Self report | Daily mood question of the product's own design, trended and shown back to her. A journal |
| 9 | Postpartum recovery tracking | Self report plus measurement | RHR and HRV return to baseline, bleeding, fever, healing, sleep debt, return to activity, self reported |
| 10 | Postpartum depression screening or support | Self report / instrument | The landmine. Own design scale is a journal. A validated instrument scored and returned as a result is a clinical tool. See section 4 |
| 11 | Infant development milestones | Education | CDC and public milestone checklists. Free. Proprietary developmental screening instruments are clinical tools |
| 12 | Infant feeding and sleep guidance | Education plus self report | Feeding frequency and volume log, sleep consolidation, growth vs public growth charts |
| 13 | Long horizon parenting guidance by child age | Content | Boundaries, discipline, autonomy. Weak, contested, culturally variable evidence base |
| 14 | Urgent maternal warning sign surfacing and escalation | Education plus hard coded rules | The safety layer and the strategic differentiator. Surfaces the CDC and AIM list, triggers direct to care. Section 5 |

---

## 3. CLASSIFICATION

CORE means v1 cannot ship without it. DIFFERENTIATOR means it is where the product wins and no competitor serves it well. LATER means real but deferred. BLOCKED means the crossing the line variant is out; the available wellness variant is engineered a specific way and logged in the risk register (framework section 2, "narrow set that stays outside the lane").

| # | Feature | Class | Rationale | BLOCKED variant (available reframing) |
|---|---------|-------|-----------|----------------------------------------|
| 1 | Maternal physiological tracking | CORE | Measurement plus reference. Squarely in lane | Inferring a named disease from the physiology (see landmines 4, 6) |
| 2 | Lab and biomarker ingestion | CORE | Display of her own data with the lab's own range | Interpreting the value clinically (landmine 3). Reframe: display, do not interpret |
| 3 | Personalized nutrition guidance | CORE | Generic healthy eating and public weight gain ranges are in lane | Condition referencing diet (gestational diabetes, preeclampsia, anemia) (landmine 1). Reframe: generic guidance, route condition specific to her provider |
| 4 | Sleep guidance | CORE | Healthy lifestyle encouragement, explicitly in lane | None material |
| 5 | Symptom normalization and education | CORE | Education and normalization, explicitly in lane | Any output that could cause delay of care (landmine 6). Reframe: bounded by the section 5 safety layer |
| 6 | Week by week fetal development content | CORE | Table stakes. Pure education | None material |
| 7 | Partner facing guidance | DIFFERENTIATOR | No competitor serves the partner well. Gated entirely on the consent architecture (framework B3) | Disclosure without consent is a legal exposure and a product women reject. Reframe: consent as a feature |
| 8 | Mood and stress support | CORE | Own design daily self report is a journal, not a claim | Labeling the journal output as a screening result. Reframe: reflect, do not diagnose |
| 9 | Postpartum recovery tracking | CORE | Self report plus measurement. The unwatched window is the opportunity | None material at the tracking layer; escalation is section 5 |
| 10 | Postpartum depression screening or support | DIFFERENTIATOR | Maternal mental health is the strategic center of the postpartum product and the reason a payer pays | Administering, scoring, and returning EPDS or PHQ-9 as a diagnostic result. Reframe: own design scale, or instrument presented as an educational self check with the score shown to her only and routed to her provider (section 4) |
| 11 | Infant development milestones | CORE | CDC milestone checklists are free and public | Returning a result from a proprietary developmental screening instrument (ASQ, M-CHAT). Reframe: public milestone education, route concerns to pediatrician |
| 12 | Infant feeding and sleep guidance | CORE | Log plus education plus public growth charts | None material |
| 13 | Long horizon parenting guidance by child age | LATER | Real but far weaker, contested, culturally variable evidence. Content and trust product, cost it as one | Presenting contested guidance as settled fact. Reputational, not regulatory, risk |
| 14 | Urgent maternal warning sign surfacing and escalation | DIFFERENTIATOR | The single highest value defensible feature. Patient education, no inference, no claim. Addresses leading preventable maternal death | Any wording that reads as diagnosis or that could delay care. Reframe: restate the provider and CDC instruction verbatim, escalate hard (section 5) |

Headline count: CORE = 10 (items 1, 2, 3, 4, 5, 6, 8, 9, 11, 12). DIFFERENTIATOR = 3 (items 7, 10, 14). LATER = 1 (item 13). No feature is BLOCKED in whole. Every feature has a wellness variant that ships; 8 features carry a BLOCKED sub variant that is engineered out and logged in the risk register.

---

## 4. CLAIMS MATRIX (framework section 2)

Columns per framework: shipping phrasing, data type (self report / measurement / inference), permitting guidance or precedent, the phrasing that crosses the line, and the FTC substantiation evidence required. Confidence marked per claim.

### Regulatory baseline, verified

| Fact | Source | Date | Confidence |
|------|--------|------|------------|
| FDA revised final General Wellness: Policy for Low Risk Devices and CDS guidance issued, superseding 2019 versions | FDA (fda.gov/media/90652/download); Covington, King & Spalding, Faegre Drinker, Gardner Law summaries | 2026-01-06 | HIGH |
| Guidance retains two intended use categories: pure wellness claims, and disease referenced claims tied to healthy lifestyle where it is well understood that lifestyle may reduce risk of or help living well with a chronic condition | Covington & Burling; King & Spalding summaries | 2026-01 | HIGH |
| New section: boundaries of enforcement discretion for non invasive sensors that estimate, infer, or output physiological parameters (BP, SpO2, glucose, HRV). Falls outside wellness if labeling, advertising, or functionality references specific diseases or diagnostic thresholds, or includes alarms that direct medical management, or outputs values that mimic clinical values unless validated | Faegre Drinker; Gardner Law summaries of 2026-01-06 guidance | 2026-01 | HIGH |
| WHOOP Blood Pressure Insights: FDA closed its warning letter after WHOOP modified the feature and labeling consistent with the 2026 guidance; closure applied to the modified feature only | Gardner Law summary | closed 2026-06-23 | MEDIUM |
| FTC Health Products Compliance Guidance requires competent and reliable scientific evidence behind health claims; applies to wellness products | FTC (framework section 2) | 2022-12 | HIGH |
| FTC active enforcement against consumer health and mental health apps is directed at data sharing and deceptive privacy promises, not at the administration of screening instruments. BetterHelp $7.8M consent order; Cerebral and Monument proposed settlements; Flo consent order | FTC press releases; Holland & Knight; WSGR Data Advisor | BetterHelp 2023-03-02; Cerebral/Monument 2024-05 | HIGH |

### The matrix

| # | Shipping phrasing (in lane) | Data type | Permitting basis | Line crossing phrasing (out of lane) | FTC substantiation required |
|---|-----------------------------|-----------|------------------|--------------------------------------|------------------------------|
| 1 | "Your resting heart rate is 12 percent above your first trimester baseline. RHR typically rises across pregnancy. Here is why." | Measurement | 2026 General Wellness sensor section; measurement plus reference is not diagnosis | "Your HRV pattern is consistent with preeclampsia." | Accuracy of the derived metric against a recognized reference standard; provenance of the normative pregnancy curve |
| 2 | "Your hemoglobin result was 10.8 g/dL. Your lab's printed reference range is 11.0 to 14.0. Hemoglobin is the protein that carries oxygen in blood." | Ingested measurement | Landmine 3 reframing; display the value and the lab's own range, explain the analyte | "Your hemoglobin is low, which means you are anemic and should take iron." | That the displayed value and range are faithfully reproduced from the source report |
| 3 | "In the second trimester, aim for iron rich foods and adequate protein. Here are examples." | Education | Generic healthy eating is in lane | "To manage your gestational diabetes, keep carbohydrates under X grams per meal." | Substantiation that the generic guidance reflects accepted nutrition consensus (ACOG, dietary guidelines) |
| 5 | "Many people feel round ligament pain in the second trimester. It is usually normal. Call your provider if it is severe, constant, or with bleeding or fever." | Education | Education and normalization is in lane; escalation clause defers severity to the safety layer | "Your pain is round ligament pain and is nothing to worry about." (a diagnosis and a reassurance that could delay care) | Substantiation that the normalization reflects accepted obstetric education |
| 8 | "You have logged low mood 9 of the last 14 days, which you flagged yourself. That is worth a conversation with your provider." | Self report | Framework section 2: self report is a journal. Own design scale. Reflect the input she supplied | "Your scores indicate depression." | None for the reflection itself; the trend is her own data |
| 10a | Own design daily mood scale, trended, shown back to her | Self report | Journal. No instrument, no claim | Labeling it a validated screen or returning a clinical cutoff verdict | None |
| 10b | EPDS or PHQ-9 presented as an educational self check, score shown to her only, routed to her provider, with immediate escalation on the self harm item | Instrument, self administered | Framework section 2 option (a). Consumer precedent: Ovia Health, distributed via employers and health plans, provides mental health screenings plus education plus coaching plus referral, positioned as wellness. FTC enforcement in this category targets data handling, not instrument administration | Returning a diagnosis ("you have postpartum depression"); withholding the score from her provider; failing to escalate item 10 of EPDS (self harm) | Substantiation that the instrument is reproduced faithfully and scored per the validated algorithm; EPDS licensing (below) |
| 1/HRV | "Here is your HRV, your own baseline, and the published normative pregnancy curve. HRV is a measure of beat to beat variation in heart rate." | Measurement | Landmine 4 reframing; measurement plus reference | "Your HRV indicates a disease." | Metric accuracy; provenance of the normative curve |
| 14/BP | "Your reading is 148 over 96. Your provider told you to call at 140 over 90. Reminder: contact your provider." | Measurement plus education | Restating the threshold her own provider gave her is patient education. Cuff is a cleared device she already owns | An app generated alarm that references preeclampsia or directs medical management, which the 2026 sensor section places outside the lane. See landmine 6 | Substantiation that the cuff is validated for pregnancy; faithful display of her reading |

### The named landmines, resolved

| Landmine | Resolution | Confidence |
|----------|-----------|------------|
| 1. Condition referencing nutrition | Generic healthy eating and public gestational weight gain ranges ship as CORE. Any diet keyed to gestational diabetes, preeclampsia, or anemia is a treatment claim, blocked, and routed to her provider. The product does not prescribe a therapeutic diet | HIGH |
| 2. Validated instrument (EPDS, PHQ-9) vs own design daily mood question | Two shipping options, both researched, neither assumed. Option A, own design daily scale: unambiguously a journal, zero licensing, ships in v1. Option B, validated instrument: consumer precedent exists in the wellness lane (Ovia distributes mental health screenings via employers and payers) and current FTC enforcement targets data practices, not instrument use, so administration is not per se blocked. It is engineered as an educational self check, score to her and routed to her provider, with hard escalation on the self harm item. Licensing is not free and not uniform: PHQ-9 is public domain, released by Pfizer at no charge, no permission required. EPDS is copyright of the Royal College of Psychiatrists; individual clinician use is permitted but commercial distribution in an app requires written permission and likely a fee. Recommendation for v1: ship the own design scale (Option A) plus PHQ-9 (public domain) if a validated instrument is wanted; defer EPDS pending a written license. Do not assume EPDS is free | HIGH on licensing; MEDIUM on the enforcement posture inference |
| 3. Lab value interpretation | Blocked as clinical decision support. Ship the display: her value, her lab's printed reference range, and a plain language explanation of what the analyte is. Do not tell her what her result means for her | HIGH |
| 4. HRV disease inference | Inference of a named disease from HRV is blocked. Ship HRV as measurement: her value, her baseline, the published normative pregnancy curve, and an explanation of what HRV is. Note the 2026 sensor section reinforces this line | HIGH |
| 5. Restating ACOG and provider warning signs | This is patient education, in lane, and is the CORE differentiator. Restate the CDC, AIM, and provider instruction. Make no independent severity judgment. It is her provider's instruction, surfaced | HIGH |
| 6. Any output that could delay care | Highest severity failure mode. Governed entirely by the hard coded safety envelope in section 5. Note the tension: the 2026 FDA sensor section says a physiological output that includes an alarm directing medical management can fall outside wellness. The mitigation is that the escalation is framed as restating the user's own provider's instruction and as "contact your provider or 911," never as an app generated clinical alarm tied to a named disease or a diagnostic threshold of the product's own creation. This tension is a live open question and is logged for the risk register and Phase 3 | MEDIUM |

---

## 5. SAFETY ENVELOPE FOR THE LANGUAGE MODEL LAYER

This product will be asked by a frightened person at 3am whether her symptom is dangerous. The safety layer is defined at Phase 0 because the entire architecture depends on it. It is enforced, not prompted. A prompt is a request to a probabilistic system. An enforced layer is deterministic code that the model cannot override, cannot be jailbroken out of, and that runs whether or not the model behaves.

### Architecture: the red flag layer runs before the model, not inside it

Every user input, both structured symptom logger entries and free text messages, passes through a deterministic pre model classifier before any generation occurs. The classifier matches structured fields and text against the hard coded red flag list below. On a match, the pipeline short circuits: the model never generates the response. A fixed, legally reviewed, full screen direct to care interstitial is served, the model is bypassed, and the event is logged. The model is only reached for inputs that clear the red flag layer. This inverts the usual failure mode: the dangerous case is the one case the probabilistic system is never trusted to handle.

### The hard coded red flag list (CDC Hear Her / AIM Urgent Maternal Warning Signs, verified 2026-07-10)

Source: CDC Hear Her Campaign, Urgent Maternal Warning Signs (cdc.gov/hearher); list developed by the Alliance for Innovation on Maternal Health (saferbirth.org). These apply during pregnancy and up to one year after delivery.

| # | Red flag symptom (verbatim intent) |
|---|-------------------------------------|
| 1 | Headache that will not go away or gets worse over time |
| 2 | Dizziness or fainting |
| 3 | Changes in vision |
| 4 | Fever of 100.4 F or higher |
| 5 | Trouble breathing |
| 6 | Chest pain or fast beating heart |
| 7 | Severe belly pain that does not go away |
| 8 | Severe nausea and vomiting (not the same as morning sickness) |
| 9 | Severe swelling of hands or face |
| 10 | Thoughts about harming yourself or your baby |
| 11 | Baby moving less or stopping movement during pregnancy |
| 12 | Vaginal bleeding or fluid leaking during pregnancy |
| 13 | Heavy vaginal bleeding or discharge after pregnancy |
| 14 | Extreme tiredness (added to the list; verify final wording at implementation) |
| 15 | Overwhelming feelings of sadness or hopelessness, or a swelling, red, or painful leg (grouped severity items to verify against the current CDC page at implementation) |

Two additions layered on top of the CDC list for this product: a blood pressure reading at or above the threshold the user's own provider recorded for her (defaults to 140/90 if none set), and any positive response to a self harm item on any mood scale or instrument in the product. Both route to the escalation path.

### Enforced behaviors

| Behavior | Trigger | Enforced action |
|----------|---------|-----------------|
| Escalation | Any red flag list match, self harm response, or BP at or above threshold | Bypass the model. Serve the fixed interstitial: "This can be a sign of a serious condition. Contact your provider now. If you cannot reach them, go to an emergency room or call 911." For self harm: add 988 Suicide and Crisis Lifeline. Log with timestamp. Never soften, never explain away, never delay |
| Refusal | User asks the model to diagnose, to interpret a lab value, to tell her whether a symptom is safe, to adjust a medication or dose, or to override an escalation | Model refuses within its bounds and redirects to her provider or the escalation path. Refusal scope is defined in code guardrails, not left to model discretion |
| No reassurance on a red flag | Any input containing a red flag, even if the user's stated question is minor | The red flag path always wins over the conversational path. The model is never permitted to reassure a user out of a red flag symptom. This is the specific mechanism that prevents the delay of care failure mode |
| Disclaimer surfacing | Every session and every health relevant output | Persistent, not a one time consent. States: general wellness, not medical advice, not a substitute for her provider |
| Logging | Every escalation and every refusal | Immutable event log for liability defense and for the leading indicator that the layer is firing as designed |

### Why enforced not prompted

A prompt instruction ("if the user reports a severe headache, tell her to seek care") is defeated by paraphrase, by adversarial input, by context window pressure, and by ordinary model variance. The failure to escalate scenario is the highest severity, highest liability event in this product and it goes in the regulatory risk register. It cannot depend on the model choosing correctly on the worst night. The red flag classifier is deterministic code with unit tests and a fixed response set; the model is a downstream presentation layer for the cleared, non urgent majority of inputs. This mirrors the framework's design rule: the product surfaces the pattern and hands it to a human, and in the red flag case it hands off before the model speaks.

---

## Register Entries

Sources (to be appended to `/research/registers/sources.md` by the register keeper; not written here per instruction):

| Source | Org | URL | Pub date | Used for | Credibility |
|--------|-----|-----|----------|----------|-------------|
| Urgent Maternal Warning Signs | CDC Hear Her Campaign | cdc.gov/hearher/maternal-warning-signs/index.html | accessed 2026-07-10 | Red flag list, postpartum one year window | HIGH (primary, gov) |
| Urgent Maternal Warning Signs poster | AIM / saferbirth.org | saferbirth.org/wp-content/uploads/urgent-maternal-signs_V4_Final_2022.pdf | 2022 | Verbatim warning sign wording | HIGH (primary) |
| General Wellness: Policy for Low Risk Devices (revised final) | FDA | fda.gov/media/90652/download | 2026-01-06 | Wellness lane, sensor boundary | HIGH (primary) |
| FDA Issues Revised Guidance on General Wellness Products | Covington & Burling | cov.com | 2026-01 | Two intended use categories retained | HIGH (secondary, legal) |
| Key Updates in FDA 2026 General Wellness and CDS Guidance | Faegre Drinker | faegredrinker.com | 2026-01 | Sensor section boundary criteria | HIGH (secondary, legal) |
| FDA 2026 CDS and General Wellness Guidance Updates | Gardner Law | gardner.law | 2026-01 | WHOOP BP Insights closure 2026-06-23 | MEDIUM (secondary) |
| FTC bans BetterHelp from revealing consumer data | FTC | ftc.gov | 2023-03-02 | FTC enforcement posture, data not instruments | HIGH (primary) |
| FTC settlements with Cerebral and Monument | WSGR Data Advisor / FTC | wsgrdataadvisor.com | 2024-05 | FTC enforcement posture | HIGH |
| FTC Health Products Compliance Guidance | FTC | ftc.gov | 2022-12 | Substantiation standard | HIGH (primary) |
| Ovia Health mental health screening overview | Ovia Health | oviahealth.com; utsystem.edu | 2022 to 2026 | Consumer precedent: screening plus referral, wellness, payer distributed | MEDIUM (vendor) |
| PHQ-9 public domain release | Pfizer | pfizer.com press release | historical | PHQ-9 licensing (free, public domain) | HIGH (primary) |
| EPDS copyright and permissions | Royal College of Psychiatrists | rcpsych.ac.uk/about-us/contact-us/permissions | accessed 2026-07-10 | EPDS licensing (permission required for app distribution) | HIGH (primary) |

Competitors noted for `/research/registers/competitors.md`: Ovia Health (payer and employer distributed pregnancy, postpartum, mental health screening plus coaching); Flo (consumer, prior FTC action); Mahmee, Partum Health, Canopie (postpartum and first year extension); WHOOP (wearable, subject of the 2026 BP Insights FDA precedent).

---

## Open Questions

1. Does the blood pressure threshold reminder (feature 14, BP) survive the 2026-01-06 FDA sensor section, which places outside the lane any physiological output that includes an alarm directing medical management? The education framing (restating the user's own provider's threshold) is the mitigation, but the line is live and needs legal review before Phase 3. MEDIUM risk.
2. Exact current CDC wording and full count of the Urgent Maternal Warning Signs list. The core list is verified; three lower frequency items (extreme tiredness, leg swelling or redness, and the exact grouping of self harm and sadness) must be reconciled against the live CDC page at implementation.
3. EPDS commercial license fee and terms from the Royal College of Psychiatrists. UNKNOWN. Needed if Option B uses EPDS rather than PHQ-9.
4. Whether the WHOOP warning letter closure (2026-06-23) is documented in a primary FDA source rather than a law firm summary. MEDIUM confidence pending primary confirmation.
5. Whether any consumer app has faced FDA (not FTC) action specifically for administering a validated screening instrument. No such action surfaced; absence is suggestive, not dispositive.

## Assumptions Made

1. Founder assumption B1 (cash pay lab panel) is treated as contradicted: prenatal labs are OB ordered and insurance covered; a parallel cash pay panel sells what she already gets. Ingest is presumptive. Impact if wrong: the lab feature's business model changes; does not affect the Phase 0 claims analysis.
2. Founder assumption B5 (at home ultrasound) is treated as out of scope: it is a Class II device with its own clearance path. Parked. Impact if wrong: none on this phase.
3. Assumed the 2026-01-06 FDA guidance summaries from four independent law firms accurately represent the primary FDA document, which returned 403 to the fetcher. Corroboration across four independent legal sources is strong but the primary text was not directly read. Impact if wrong: the sensor boundary analysis in landmine 6 could shift.
4. Assumed the FTC enforcement posture (data practices, not instrument administration) generalizes to the screening instrument question. This is an inference from the pattern of actions, not a statement by the FTC. Impact if wrong: Option B (validated instrument) carries more risk than assessed; Option A (own design scale) is unaffected and remains the safe default.
5. Classification of feature 14 as the CORE differentiator inherits the brief's own strategic thesis (framework Phase 1 note). Treated as a founder thesis to be validated in Phase 1 and Phase 5, not yet a research finding.

## Confidence Summary

Overall confidence: HIGH on the claims boundary logic, the red flag list content, the licensing split between PHQ-9 and EPDS, and the safety envelope architecture. HIGH on the existence and date of the 2026-01-06 FDA revision and its retention of the two intended use categories. MEDIUM on the precise application of the new FDA sensor boundary to the BP threshold reminder (landmine 6), which is the weakest and most consequential finding in this phase and should be legal reviewed before any BP alarm ships. MEDIUM on the inference that FDA and FTC posture permits Option B (validated instrument administration); the own design scale (Option A) is HIGH confidence and is the recommended v1 default. The primary FDA guidance text was not directly readable by the tooling and was corroborated through four independent legal summaries.
