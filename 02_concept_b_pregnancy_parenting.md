# 02_CONCEPT_B: PREGNANCY AND PARENTING COMPANION
## Phased Research and Business Case Brief

Read `00_framework.md` first. It governs this file.

---

## CONCEPT STATEMENT

A subscription application for first time parents, spanning pregnancy, postpartum, and early child development. An AI layer sits in front of the entire experience, grounded in clinical best practice and child development literature, and personalized by three inputs: continuous physiological data from a wearable worn by the mother, structured lab and biomarker data drawn into the app, and the developmental stage of the pregnancy or child.

The product speaks to both parents, separately. To the mother: contextualized explanation of what her body is doing, normalization of what she is feeling, and specific, actionable, non prescriptive guidance. To the partner: what is happening, what she may be experiencing today, and what would help.

It does not stop at delivery. Postpartum is a first class part of the product, and the developmental guidance continues into toddlerhood and beyond, evolving into a parenting companion that tells a parent what a child at this age needs, what boundaries to hold, and when to step back.

Positioning is general wellness. See framework section 2.

---

## FOUNDER ASSUMPTIONS TO VALIDATE, NOT INHERIT

| # | Assumption | Why it may be wrong |
|---|-----------|---------------------|
| B1 | A Function Health style cash pay lab panel is a viable component | Prenatal labs are ordered by an OB and covered by insurance. A parallel cash pay panel sells the patient something she is already getting for free. Adherence and value proposition both suspect. The interesting version is ingesting labs she already has. |
| B2 | Raw physiological data from a consumer wearable is accessible | See `shared_wearable_data_access.md`. Most vendors expose derived metrics only. |
| B3 | The product can tell the partner about the mother's physiological and emotional state | This is disclosure of one person's health data to another. Without an explicit, revocable, granular consent architecture, it is both a legal exposure and a product women will reject. |
| B4 | Mood and emotional state can be inferred from passive physiology (HRV, sleep, skin temperature) | Search the literature honestly. The evidence for inferring affect from consumer grade physiology is weaker than the market implies. Note that the product does not need this inference: **daily self report is cheap, accurate, defensible, and already what the user expects.** Establish what passive physiology adds on top of self report, if anything, and cost it accordingly. |
| B5 | An at home ultrasound is a feature | It is a Class II medical device with its own clearance pathway, its own manufacturing, and its own liability. It is not a feature. Park it as a separate program and cost it separately if at all. |
| B6 | Subscription DTC is the business model | Pregnancy has a hard, dated churn cliff. Model it. The successful companies in this category sell to employers and payers, not to parents. |
| B7 | The market is first time parents | It is. But the buyer may be their employer or their health plan. |

---

## PHASE 0: SCOPE NORMALIZATION
**Output: `/research/b/phase0_scope.md`**

1. Restate the concept in one page. Settled versus open.
2. Feature inventory, numbered. At minimum: maternal physiological tracking, lab and biomarker ingestion, personalized nutrition guidance, sleep guidance, symptom normalization and education, week by week fetal development content, partner facing guidance, mood and stress support, postpartum recovery tracking, postpartum depression screening or support, infant development milestones, feeding and sleep guidance, and long horizon parenting guidance by child age.
3. Classify each: CORE, DIFFERENTIATOR, LATER, BLOCKED.
4. **Claims matrix** per framework section 2. This concept has a much sharper claims problem than Concept A, because the entire product surface is health guidance to a pregnant woman.

Specific claims landmines to resolve in the matrix:
- Nutrition guidance during pregnancy that references a condition (gestational diabetes, preeclampsia, anemia) is not wellness. Generic healthy eating guidance is.
- A validated screening instrument (EPDS, PHQ-9) is a clinical tool. Administering it, scoring it, and returning a diagnostic result is a claim. **A daily mood question of the product's own design, trended and shown back to her, is a journal and is not a claim.** Research how consumer apps currently handle each, and what enforcement posture exists. Do not assume the instrument is unavailable and do not assume it is free.
- Interpreting a lab value and telling the user what it means is clinical decision support. Displaying the value she already has, with the reference range her lab printed on it, is not.
- Telling a user her HRV pattern indicates a disease is a claim. Showing her HRV, trending it, comparing it to her own baseline and to a published normative pregnancy curve, and explaining what HRV is, is not.
- Restating the warning signs her own provider and ACOG already instructed her to watch for is patient education, not diagnosis. This is the safety layer and the core feature.
- Any output that could cause a user to delay seeking care is the highest severity failure mode in this product. Define the escalation and disclaimer architecture at Phase 0, not at launch.

5. Define the **safety envelope for the language model layer**. This product will be asked, by a frightened person at 3am, whether her symptom is dangerous. Specify the refusal behavior, the escalation behavior, the red flag symptom list that triggers an immediate direct to care response, and how those are enforced rather than prompted. This is a Phase 0 deliverable because the entire architecture depends on it. Search for how existing regulated and unregulated health apps handle this.

**Stop. Report. Wait.**

---

## PHASE 1: MARKER AND TREND CATALOG
**Output: `/research/b/phase1_markers.md` and append to `/research/registers/markers.md`**

Same table structure and same field requirements as Concept A Phase 1. The markers define the data requirement. Do not pick a wearable and then ask what it measures.

**The organizing insight for this concept.** The highest value, most defensible, most differentiated feature in this product is not AI mood inference. It is this: **the urgent maternal warning signs that ACOG and CDC already instruct every pregnant and postpartum person to watch for, surfaced at the right moment, trended against her own self reported history, and delivered to a person who is not currently paying attention because she is exhausted.**

That is patient education. It is the exact instruction her OB gave her at discharge and that she forgot. It requires no inference and makes no claim. And it addresses the leading preventable causes of maternal death, most of which occur postpartum, after the last appointment, when nobody is watching. Research this. It may be the entire company.

### Seed list. Research every one. Add what is missing.

**Antepartum physiological, passive.** Resting heart rate trajectory across gestation. HRV trajectory. Respiratory rate. Skin temperature. Sleep duration and fragmentation by trimester. Activity and step count decline. Establish, from primary literature, the **published normative trajectories** for each, stratified by trimester, maternal age, BMI, and parity. Personalization needs both her baseline and the population curve. If the normative curve does not exist in adequately stratified published form, that is a finding, and it constrains the product.

**Antepartum self report.** Nausea and vomiting severity, including the hyperemesis threshold. Fatigue. Pelvic and back pain. Contractions. Fetal movement and kick counts, which are a long established self report practice. Mood, daily, on a simple scale of the product's own design. Sleep quality. Appetite. Anxiety.

**The urgent maternal warning signs.** Research the current ACOG and CDC Hear Her lists directly. They include, and verify each: severe headache that will not go away, vision changes, difficulty breathing, chest pain, severe abdominal or epigastric pain, sudden or severe swelling of face and hands, fever, thoughts of self harm, heavy bleeding, and fluid leaking. Design the symptom logger around this list. Design the escalation around it. This is the hard coded safety layer required by Phase 0.

**Blood pressure and preeclampsia.** Preeclampsia is the case that decides whether this product matters. A home blood pressure cuff is a cleared device the user can already buy. Displaying her readings, trending them, and reminding her of the threshold her own provider told her to call about is education. Research: current ACOG guidance on home blood pressure monitoring in pregnancy, current evidence on remote BP monitoring programs and their outcomes, which cuffs are validated for use in pregnancy specifically since many consumer cuffs are not, and **postpartum preeclampsia, which can onset days to weeks after discharge and is a leading cause of postpartum readmission.** The postpartum window is the unwatched window. That is the opportunity.

**Weight and nutrition.** Gestational weight gain trajectory against published guideline ranges by pre pregnancy BMI. This is a public, established, non diagnostic reference range. Nutrient intake and the specific micronutrients with established pregnancy requirements. Hydration. The concept's diet from photographs feature: research current food recognition accuracy and whether nutrient estimation from images is accurate enough to say anything, or only accurate enough to log.

**Glucose.** If she wears a CGM, or if she has gestational diabetes and is already monitoring. Display and trend. Do not interpret.

**Antepartum mood and mental health.** Self reported daily mood. Trend. Streak of low days. Anxiety self report. Sleep and mood correlation, shown as two lines on a chart, not as a causal claim. Research the current evidence base on antenatal depression and anxiety prevalence and screening practice, and research how consumer apps currently handle screening instruments. Log the finding rather than assuming the answer.

**Fetal and gestational.** Gestational age driven developmental content, which is the table stakes feature every competitor has. Fetal movement patterns. Fundal height if self measured. Ultrasound and appointment results, ingested not generated.

**Preterm labor.** Self reported contraction frequency and timing. Fluid. Pressure. Research the evidence on home uterine activity monitoring, which has a contested history and a cautionary regulatory story worth knowing.

**Postpartum physiological.** Recovery trajectory of resting heart rate and HRV toward pre pregnancy baseline, which is a genuine and underexploited signal. Sleep debt accumulation. Blood pressure, per the preeclampsia note above. Bleeding, self reported. Fever. Incision or perineal healing, self reported. Return to activity.

**Postpartum mood.** Daily self report. Trend across the first year, not the first six weeks. Research the timing distribution of postpartum mood disorder onset, and research the leading causes of pregnancy related death in the postpartum year, because in multiple state maternal mortality review datasets mental health conditions and overdose are among the leading causes. Verify this from primary sources. If it holds, it is the strategic center of the postpartum product and the reason a payer will pay.

**Bonding, intrusive thoughts, and identity.** Self report. Research how to ask about intrusive thoughts safely, because the question itself carries risk and the response requires an escalation path.

**The partner.** Paternal and non birthing partner perinatal depression is real and has published prevalence. Research it. The partner is not only a support instrument, the partner is also a user with their own risk. This is a differentiator no competitor is serving well.

**Partner facing disclosure.** Everything the partner sees about her is a disclosure. It is granted by her, granularly, revocably, and with a visible indicator of what is shared. Research consent architectures in shared health applications. The concept's "tell him she slept badly, help her today" is excellent product and unacceptable surveillance, and the only thing separating those two is the consent layer. Design it as a feature, not a checkbox.

**Infant, first two years.** Feeding frequency and volume. Sleep consolidation. Growth against published growth charts, which are free and public. Developmental milestones against published milestone checklists, which are also free and public. Research which milestone frameworks are usable without license and which are proprietary. Note that developmental screening instruments are clinical tools and sit in the risk register.

**Early childhood, two years and beyond.** The concept extends into boundaries, discipline, autonomy, and problem solving. Research the evidence base honestly. It is real but far weaker, more contested, and more culturally variable than the obstetric evidence. Determine whether the product takes a position or presents a range. State the reputational and content risk of taking a position. This layer is a content and trust product, not a data product, and it should be costed as one.

### Required outputs of this phase

1. The full marker table.
2. Ranked v1 shortlist by actionability multiplied by evidence strength divided by data acquisition cost.
3. **The data requirement matrix**: for each v1 marker, what data is needed, from where, at what fidelity. This is the input to Phase 2 and it is what determines whether the wearable dependency is fatal.
4. **The two daily surfaces, written as copy.** What she sees each morning. What he sees each morning. Thirty seconds each. If they are not worth opening, nothing else matters.
5. Explicit list of markers requiring data that cannot be obtained under current consumer wearable terms.

**Stop. Report. Wait.**

---

## PHASE 2: DATA INPUTS AND FEASIBILITY
**Output: `/research/b/phase2_data_inputs.md`**

Input: the data requirement matrix from Phase 1.

### 2.1 Wearable

Inherits `shared/shared_wearable_data_access.md`. Concept specific: which device, which metrics, at what sampling rate, obtainable how. Evaluate at least: Oura, Whoop, Apple Watch and HealthKit, Garmin, Withings, Samsung, Fitbit and Google, Polar, Empatica, and the option of a white label or contract manufactured band. For each: raw versus derived access, API terms, commercial redistribution rights, cost, and the specific contractual clause that permits or forbids what we intend.

Establish explicitly: **can we get raw PPG, raw accelerometer, continuous skin temperature, and continuous SpO2, from any consumer device, under terms that permit a commercial product to ingest and act on them.** If the answer is no for all of them, the product design changes and every downstream phase must reflect that.

Physiological changes across pregnancy are large and well characterized: resting heart rate rises substantially, HRV drops, temperature and respiratory rate shift. Find the primary literature that quantifies these trajectories. A personalization engine needs the normative curve, not just the individual's baseline. Establish whether that normative curve exists in published form and whether it is stratified adequately by trimester, age, BMI, and parity.

### 2.2 Labs and biomarkers

Three models, cost and evaluate each:
- **Model 1, ingest.** Pull the labs her OB already ordered, from the patient portal or a health data aggregator. Research the current state of patient mediated health record access, the relevant interoperability rules, and the vendors that broker this. This is almost certainly the correct answer and it is far cheaper than Model 2.
- **Model 2, order.** Cash pay panel through a national reference lab. Research what it actually takes: lab partnership, a telehealth physician network to order the tests, the physician ordering requirement per state, phlebotomy access, CLIA, and per panel cost. This is the Function Health model. Establish its real cost structure and whether the panel adds anything a prenatal panel does not already contain.
- **Model 3, manual.** The user photographs or uploads her lab report. Cheapest, worst data quality, no partnership required.

Recommend one and state the cost delta.

### 2.3 Mood, affect, and stress inference

Search the literature. Establish what is actually supported. Report honestly, including negative findings. If the inference is not defensible, redesign the feature: the product can normalize and educate on a schedule and on self report without claiming to detect. Self reported daily check in is cheap, accurate, and defensible. Say so if the evidence supports it.

### 2.4 Content and knowledge base

The AI layer must be grounded, not generative from parametric memory. Specify the retrieval corpus:
- Obstetric clinical guidance (ACOG and equivalents)
- Pediatric guidance (AAP)
- Infant and child development literature and validated milestone frameworks
- Nutrition guidance
- Evidence based parenting frameworks for the older child stages described in the concept

For each: is it licensable, is it free, what are the terms, and what is the update cadence. **Content licensing is a real line item and is frequently overlooked.** Also determine what medical review the content requires and what that costs, because a clinical reviewer on staff or on retainer is a permanent operating cost in this business.

The long horizon parenting layer (age appropriate boundaries, discipline, autonomy, problem solving) has a much weaker evidence base than the pregnancy layer, and its guidance is culturally contested. Note that. Determine whether the product takes a position or presents a range.

**Stop. Report. Wait.**

---

## PHASE 3: PRODUCT AND TECHNICAL ARCHITECTURE
**Output: `/research/b/phase3_architecture.md`**

1. Application stack. Mobile first, cross platform versus native, backend, data model.
2. Retrieval architecture for the grounded AI layer. Corpus, chunking, retrieval, citation, and how a response is constrained to the corpus. Cost per user per month at each scale.
3. Personalization engine. How wearable data, lab data, gestational age, and self report combine into a daily output. Specify the rules layer versus the model layer. Most of this should be a rules engine with a language model doing presentation, not a language model doing inference. Justify the split.
4. **Dual user architecture and consent.** The mother and the partner are separate accounts with separate views. Every data element the partner can see is a disclosure the mother must grant, granularly, and must be able to revoke instantly and without friction. Design it. This is a differentiator if done well and a lawsuit if done badly.
5. Safety enforcement layer. Red flag symptom detection, hard coded escalation, disclaimer surfacing, and logging. Not a prompt. An enforced layer.
6. Data architecture and privacy. Inherits `shared/shared_privacy_security.md`. Note specifically: reproductive health data carries elevated legal risk in the current US environment. Research the current state of state law on reproductive health data, and the implications for data retention, minimization, subpoena exposure, and where data is stored. This is a first order architecture input, not a compliance afterthought. Address it explicitly.
7. Wearable integration layer.
8. Notification and engagement architecture. Retention in this category is driven by daily habit. Specify the daily loop.

**Stop. Report. Wait.**

---

## PHASE 4: DEVELOPMENT PLAN, COST, AND TIMELINE
**Output: `/research/b/phase4_devplan.md`**

Per framework section 4 and mirroring Concept A Phase 6.

1. WBS to each gate. Mobile, backend, retrieval and AI, wearable integration, content operations, clinical review, design, QA.
2. Timeline and cost at 1, 2, 3, and 4 engineers, plus the non engineering roles this product cannot ship without: a clinical reviewer and a content lead. Name them and cost them. A pure engineering headcount model is wrong for this product.
3. AI assisted velocity multiplier, cited, low mid high.
4. Critical path. Likely content, clinical review, and wearable data access, not code.
5. Comparable ventures. Maven Clinic, Ovia Health, Babyscripts, Bloomlife, Elvie, Peanut, Poppy Seed Health, Cleo, Carrot, Progyny, Pomelo Care, Oath Care. Establish what each raised, at what stage, how long to revenue, and what the exits looked like. Include the ones that failed.
6. Test plan by gate. G2 is founder circle. G3 is friends and family. Note that the tester population for this product is narrow and time bounded, which makes recruiting testers harder than it looks. Solve it.

**Stop. Report. Wait.**

---

## PHASE 5: MARKET, COMPETITION, AND CHANNEL
**Output: `/research/b/phase5_market.md`**

1. **Bottom up sizing.** US annual births. First births as a share. Subset with a partner engaged enough to use a partner app. Subset reachable per channel. Realistic price, realistic penetration. Then check against analyst femtech and digital health TAM figures as a secondary reference.
2. **The churn cliff.** Model it explicitly. A pregnancy subscription has a maximum natural life of roughly ten months. Compute LTV under a pregnancy only product and compute it again with the postpartum and early childhood extension. The delta is the strategic argument for the extension. Quantify it.
3. **Competition.** Profile at minimum: Ovia, Flo, What to Expect, BabyCenter, Peanut, Maven Clinic, Cleo, Carrot, Progyny, Pomelo Care, Babyscripts, Bloomlife, Owlet, Nanit, Huckleberry, Wonder Weeks, Big Little Feelings and the parenting content category. For each: business model, buyer, price, funding, current status. Separate the ad supported content plays from the clinical services plays. They are different businesses and the concept currently sits between them.
4. **Channel comparison** on CAC, sales cycle, contract size, gross margin: direct to consumer subscription, employer benefit, health plan, OB practice and health system, Medicaid managed care, and retail or bundle with a wearable.

Medicaid covers a very large share of US births. Maternal health outcomes are a payer quality measure. Research the current CMS and state quality measures relevant to maternal and postpartum care, because a product that moves a measure a payer is graded on has a buyer with a budget. Verify the current state of this, do not assume.

5. **Reimbursement and coverage.** Remote physiologic monitoring in pregnancy, remote therapeutic monitoring, behavioral health integration, and postpartum coverage extension. Establish what is billable, by whom, and what positioning is required to bill it. Name the tension with the wellness positioning, as in Concept A.
6. **Partners.** Wearable vendors, lab and diagnostics, health data interoperability vendors, telehealth networks, content licensors, employer benefit platforms and brokers, OB practice groups, and doula and lactation networks.
7. **Willingness to pay.** Published data on consumer spend in pregnancy and early parenthood, and published retention data for pregnancy apps.

**Stop. Report. Wait.**

---

## PHASE 6: BUSINESS CASE AND CAPITAL
**Output: `/research/b/phase6_businesscase.md`**

Mirrors Concept A Phase 8.

1. Small, mid, large scenarios. Full model. Burn, headcount, capital, breakeven.
2. Pricing models: consumer monthly, consumer bundle with a wearable, PMPM to a payer, PEPM to an employer, per patient to an OB practice.
3. Capital plan. Non dilutive first. NIH and NICHD have directly relevant funding lines for maternal and infant health. Research them by name. Then angel, pre seed, seed. Identify actual funds and actual recent deals in maternal and family health, with the deals as evidence.
4. Milestone to unlock map per gate.
5. Risk register. Include: wearable API dependency risk (a vendor can revoke access and end the company), content licensing risk, reproductive health data legal risk, clinical liability risk, and the churn cliff.
6. Kill criteria.

**Stop. Report. Wait.**

---

## PHASE 7: SYNTHESIS
**Output: `/research/b/CONCEPT_B_BUSINESS_CASE.md`**

Same standard as Concept A Phase 9.

---

## CROSS CONCEPT PHASE: PORTFOLIO DECISION
**Output: `/research/PORTFOLIO_DECISION.md`**

Run only after both concept business cases exist.

1. What is genuinely shared between the two: sensing and fusion, the grounded AI layer, the consent architecture, the wellness claims discipline, the caregiver or partner dual user model. Quantify the reuse.
2. Compare on: capital to first revenue, time to first revenue, regulatory exposure, defensibility, founder fit, and market size.
3. Recommend: build one, build both, sequence them, or kill one. State the reasoning and the evidence.
4. If sequencing, state which goes first and what the second one inherits.

---

## PRIORITY ORDER IF TIME OR BUDGET IS CONSTRAINED

Phase 1 (markers), Phase 2 (data access), and Phase 5 (market and churn) can kill this concept. Wearable data access and the channel and churn reality are the two findings most likely to invalidate the plan as described. Do them first.
