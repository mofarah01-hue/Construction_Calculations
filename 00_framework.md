# 00_FRAMEWORK.md
## Shared Research and Business Case Framework
### Applies to: Concept A (Elder Home Monitoring) and Concept B (Pregnancy and Parenting Companion)

This file is authoritative. Both concept briefs inherit every convention below. Do not restate these rules in output files. Reference them.

---

## 1. WHAT THESE BRIEFS ARE FOR

Produce a defensible business development case for each concept. A business development case answers, with evidence:

1. What exactly gets built, at what technical specification.
2. What it costs to build one, one hundred, ten thousand.
3. What it costs to develop, over what timeline, with how many engineers.
4. Who buys it, why, at what price, and how big that market is.
5. Who we partner with, who funds it, and what milestone unlocks what.
6. Where it goes after v1.

Anything that does not serve one of those six questions is out of scope.

---

## 2. POSITIONING AND CLAIMS BOUNDARY

Both products are positioned as **general wellness**, not medical devices. This is a settled strategic decision, taken with input from an FDA regulator and a quality expert. The lane is broad and the research must reflect that rather than argue with it.

**Established precedent, to be verified and documented, not relitigated:**
- Consumer wearables ship gait and mobility metrics (walking speed, step length, double support time, walking asymmetry) as wellness features.
- Consumer wearables ship walking steadiness classification with notifications referencing fall likelihood, as wellness features.
- Consumer wearables ship fall detection with automatic emergency service escalation, as wellness features.
- Consumer rings and bands ship illness onset, temperature deviation, and readiness signals as wellness features.

The job of this section is **not** to argue that these features are unavailable. It is to **document exactly why they are available**, with citations, so the position survives investor diligence and payer legal review. That artifact is an asset. Build it.

### The lane, stated precisely
FDA general wellness policy covers claims about maintaining or encouraging a healthy lifestyle. It extends to claims that a healthy lifestyle may help reduce the risk of, or help living well with, certain chronic conditions, where that relationship is well understood and accepted. Software functions intended for maintaining or encouraging a healthy lifestyle, unrelated to diagnosis or treatment, are further carved out of the device definition by statute.

### Comfortably inside the lane
- An event occurred. "A fall was detected in the kitchen."
- A measured metric and its trend. "Walking speed is 18 percent below the 30 day baseline."
- A steadiness or stability classification with a general notification.
- A pattern change. "Bathroom visits are up from 4 to 9 per night this week."
- Encouragement of general healthy behavior, activity, sleep, nutrition.
- Education and normalization. "Resting heart rate typically rises across pregnancy. Here is why."
- Event notification and escalation to a designated contact or emergency service.

### The distinction that actually matters: input versus inference

This is the single most important line in this document. Get it right and almost everything both concepts want to do is available.

**Self report is not a claim.** If the app asks the user how she feels and she answers, storing that answer, trending it, charting it, and showing it back to her is a journal. The app has asserted nothing. Mood journals, symptom logs, sleep diaries, pain scales, and daily check ins are ubiquitous consumer features. The user supplied the data. The app reflected it.

**Measurement is not a claim about disease.** Walking speed, stride length, sway amplitude, sit to stand duration, turn count, resting heart rate, HRV, temperature. These are quantities. Trending them, comparing them to the user's own baseline, and comparing them to a published normative range are all measurement and reference, not diagnosis.

**Inference of a named disease from passive data is a claim.** The output string is what matters. "Your mood scores have been low for 14 straight days, and you flagged this yourself" is reflection. "This pattern is consistent with depression" is a screening result. Same underlying data, different assertion.

### Design rule that follows
Prefer self report for anything affective or cognitive. Prefer measurement and trend for anything physical. Let the user, the caregiver, or the clinician draw the conclusion. The product surfaces the pattern and hands it to a human. That posture is both the safest and, in this category, the better product, because a caregiver who is shown a chart trusts it more than a caregiver who is told a verdict.

### The narrow set that stays outside the lane
Not a list of things to abandon. A list of things that must be engineered a specific way, and that go in the risk register with a mitigation, not a strikethrough.

| Item | Why | Available reframing |
|------|-----|---------------------|
| Outputting a disease name inferred from passive data ("signs of depression," "signs of dementia") | Screening claim on a diagnosable condition | Trend the self reported input. Surface it. Prompt a conversation with a clinician. |
| Administering, scoring, and returning a validated clinical instrument as a result (PHQ-9, EPDS, MoCA, M-CHAT) | The instrument is the clinical tool | Two options to research: (a) present the instrument as an educational self check with the score shown to the user only and routed to her provider, which many consumer apps do, or (b) use a non instrument self report scale of the product's own design. Establish current practice and current enforcement posture. Do not assume either is settled. |
| Interpreting a lab value clinically | Clinical decision support | Display the value with the reference range printed by the lab. Explain what the analyte is. Do not tell her what her result means for her. |
| Instructing a change to treatment or medication | Treatment claim | Reminders and adherence logging are fine. Dose guidance is not. |
| Any output that could cause a user to delay seeking care | Severity, not classification | Hard coded red flag escalation layer. See concept briefs. |

### The second regulator, which is the one people forget
FDA governs whether it is a device. **FTC governs whether the claim is true.** FTC Health Products Compliance Guidance requires competent and reliable scientific evidence behind health related claims, and applies to wellness products with full force. A product that states "walking speed is down 18 percent" is making a measurement claim, and the substantiation question is whether the measurement is accurate against a recognized reference standard.

This converts a regulatory question into a **validation cost**, which lands in the business case at G3 and G4 either way. Research the FTC guidance, research what substantiation looks like for a gait metric derived from a camera, and cost it. This is a real line item, not a footnote, and it is where the money actually goes.

### The second regulator, which is the one people forget
FDA governs whether it is a device. **FTC governs whether the claim is true.** FTC Health Products Compliance Guidance requires competent and reliable scientific evidence behind health related claims, and applies to wellness products with full force. A product that states "walking speed is down 18 percent" is making a measurement claim, and the substantiation question is whether the measurement is accurate against a recognized reference standard.

This converts a regulatory question into a **validation cost**, which lands in the business case at G3 and G4 either way. Research the FTC guidance, research what substantiation looks like for a gait metric, and cost it. Do not treat it as a footnote.

### Required deliverables

**1. Claims matrix**, produced in Phase 0 of each brief. For every intended feature: the shipping phrasing, whether the data is self report or measurement or inference, the specific guidance or precedent that permits it, the phrasing that would cross the line, and the validation evidence required to substantiate it under FTC standards.

**2. `regulatory_precedent_dossier.md`**, produced once. The defensible written record: current FDA general wellness guidance, the statutory software function exclusions, current SaMD and Clinical Decision Support guidance, FTC Health Products Compliance Guidance, and the specific consumer product precedents above, with citations and dates. This is the document handed to a diligence lawyer and to a payer's legal team. It is an asset. Build it properly.

**3. `regulatory_risk_register.md`**, produced once, covering both concepts. Not a list of prohibitions. For each identified risk: description, likelihood, impact, the engineering or product mitigation, the leading indicator that tells us it is materializing, and the cost of the mitigation. Include FDA reclassification risk, FTC substantiation risk, product liability, state biometric and reproductive health privacy law, and the failure to escalate scenario.

Verify all guidance from primary sources. Do not rely on memory. Cite document title, issuing body, and date.

---

## 3. MATURITY GATES

All cost, timeline, and business case output is organized against these gates. Never present a single blended "cost to build the product." Always present cost to reach each gate.

| Gate | Name | Definition | Exit criteria |
|------|------|------------|---------------|
| G0 | Concept | Architecture chosen, BOM estimated, no hardware | Signed off architecture, costed BOM |
| G1 | Bench | Breadboard or dev kit, algorithms running on desk hardware, no enclosure | Core detection works on recorded and live data at stated accuracy |
| G2 | Self test | Founder installs in own home, runs continuously | 30 days continuous uptime, false positive rate characterized |
| G3 | Friends and family | 5 to 15 units, real homes, real users, instrumented | Install time measured, retention measured, failure modes cataloged |
| G4 | Pilot | 50 to 200 units, structured cohort, partner site or paying design partner | Efficacy evidence sufficient for a partner conversation, unit economics measured |
| G5 | Limited commercial | Sellable, manufactured at low volume, support exists, certifications complete | Positive contribution margin per unit or per subscriber |
| G6 | Full commercial | Scaled manufacturing, full feature set, channel established | Target CAC and LTV achieved |

For each gate, output: engineering cost, hardware and tooling cost, certification cost, headcount, elapsed months, cumulative burn, and what the gate unlocks (which conversation, which customer, which funding round).

---

## 4. COST MODEL CONVENTIONS

### Hardware
- Quote **BOM at 5 volume tiers: 1, 100, 1,000, 10,000, 100,000 units.**
- Every line item: part number, function, unit cost at each tier, source, date of quote, whether the price is public list, distributor (Digi-Key, Mouser, LCSC), or an estimated contract manufacturer or Alibaba style quote. Label estimates as estimates.
- Separate BOM from **landed cost**: add assembly, test, packaging, freight, duty, yield loss.
- Separate landed cost from **COGS**: add warranty reserve, returns, support allocation.
- **NRE is separate**: injection mold tooling, PCB spins, certification, firmware bring up.
- **Certification is a hard line item, not a footnote.** For any mains powered device sold in the US, at minimum: FCC Part 15 (and Part 15C intentional radiator if it has a radio), UL or ETL listing, and if it screws into a lamp holder, the safety standard applicable to that lamp form factor. Research the actual applicable standards, do not guess. Certification is frequently the single most underestimated cost in a hardware startup and it lands at G5.

### Software and development
- Model timeline and cost at **1, 2, 3, and 4 engineers.**
- State the loaded engineer cost assumption explicitly (San Diego market, fully loaded including benefits, equipment, overhead). Do not use salary alone.
- Apply an **AI assisted development velocity multiplier.** This multiplier must be justified with cited empirical evidence, not asserted. Search for published data on AI assisted developer productivity. If credible published data shows a range, use the range and run low, mid, and high cases. If the evidence is weak or contested, say so and default to a conservative multiplier. **Do not invent a productivity number.**
- Model **Brooks's law**: adding engineers does not scale linearly. State the coordination overhead assumption and its source.
- Distinguish work that is buy from work that is build. For every "we will develop X," first answer: does an off the shelf or open source X already exist, what does it cost, what does it not do?

### Business
- Unit economics: price, COGS, gross margin, CAC, payback period, churn, LTV, LTV to CAC ratio.
- For subscription concepts, model churn explicitly and separately from acquisition. A product with a naturally bounded lifespan (a pregnancy is finite) must model the churn cliff, not average it away.
- Three scale scenarios per concept: small (hundreds of units or subscribers), mid (thousands), large (tens of thousands or more). For each: revenue, burn, headcount, capital required, months to breakeven.

---

## 5. EVIDENCE RULES

These are non negotiable. A business case built on invented numbers is worse than no business case.

1. **Every number gets a source, a URL, and a date.** No exceptions.
2. **Never invent a price, a lead time, a market size, or a timeline.** If it cannot be found, write `UNKNOWN` and add it to the open questions list.
3. **Mark confidence on every material claim: HIGH, MEDIUM, LOW.** HIGH means primary source, current, directly on point. LOW means inference or analogy.
4. **Flag anything older than 18 months as stale.** Semiconductor pricing, module availability, and reimbursement policy all move fast.
5. **Distinguish list price from quoted price from estimated price at volume.** These differ by multiples.
6. **Market sizing must be bottom up first.** Count the addressable units or subscribers and multiply by realistic price and penetration. Only after a bottom up estimate exists may a top down analyst TAM figure be cited, and it must be labeled as a secondary check, not the primary number.
7. **When two sources disagree, present both and say which is more credible and why.** Do not average them silently.
8. **Distinguish a founder assumption from a research finding.** Anything inherited from the concept description is an assumption until validated. Label it.
9. Prefer primary sources: manufacturer datasheets, distributor pricing pages, FDA guidance documents, CMS fee schedules, SEC filings, published papers. Avoid content marketing, listicles, and SEO blog aggregators.

---

## 6. OUTPUT CONTRACT

Every phase writes exactly one markdown file to `/research/`, named as specified in the concept brief. Every phase output file ends with three mandatory sections:

```
## Open Questions
Things that could not be resolved and that block or weaken the next phase.

## Assumptions Made
Every assumption, explicitly listed. If an assumption was necessary to proceed, it goes here, flagged, with the impact if wrong.

## Confidence Summary
Overall confidence in this phase's output, and which specific findings are weakest.
```

Update `/research/decision_log.md` after every phase: what was decided, what evidence supported it, what was rejected and why.

---

## 7. EXECUTION RULES FOR CLAUDE

- **Execute one phase at a time.** Stop at the end of each phase. Do not begin the next phase without instruction.
- **Ask before assuming.** For any technical specific (component selection, register settings, parameter values, process configuration, price point, market segment), ask rather than assume. If a question blocks progress on one thread but not others, ask it and continue on the unblocked threads.
- **Never guess or fill gaps silently.** Any assumption must be explicitly stated and flagged.
- **Do not spawn broad, open ended research.** Every search has a stated target and a stop condition. If a phase specifies "identify 5 candidate compute modules meeting criteria X," find 5 and stop.
- **Read the framework and prior phase outputs before starting a phase.** Do not re research what a prior phase already established and logged.
- **When something in the concept description is technically contradictory or commercially implausible, say so in the output. Do not build around it quietly.**

### Writing style
- No em dashes, en dashes, or hyphens as punctuation. Hyphens permitted only inside part numbers and proper names.
- C suite engineering leadership tone. Authoritative, precise. No hedging, no filler, no throat clearing.
- Tables over prose for anything comparative.
- Short, blunt, comparative summaries. Not narrative.

---

## 8. SHARED TECHNICAL SPINE

Both concepts are the same underlying system: **passive multimodal sensing, plus a fusion layer, plus a language model interpretation layer, delivered into a care context.** Research that serves both should be done once and shared.

Shared research, do once, write to `/research/shared/`:

| Topic | File |
|-------|------|
| LLM interpretation layer: on device vs API, cost per user per month, latency, privacy posture, model selection | `shared_llm_layer.md` |
| Consumer wearable raw data access: which devices expose raw HR, HRV, SpO2, accelerometer, skin temperature, via what API, under what terms, at what cost, with what rate limits | `shared_wearable_data_access.md` |
| Privacy, security, and data architecture: encryption at rest and in transit, edge versus cloud inference, what triggers HIPAA, what triggers state biometric privacy law (Illinois BIPA, Texas CUBI, Washington My Health My Data), consent architecture | `shared_privacy_security.md` |
| Cloud and inference infrastructure cost per user per month at each scale tier | `shared_infra_cost.md` |
| Capital landscape: relevant VCs, strategic investors, non dilutive funding (NIH SBIR, NSF SBIR, NIA specifically for aging tech), accelerators | `shared_capital_landscape.md` |

On wearable data access, be specific and skeptical. The concept description assumes raw sensor data from a consumer band. Most consumer wearable vendors expose derived metrics only, gate raw data behind research agreements, or prohibit it entirely in their developer terms. Establish what is actually obtainable before any downstream design depends on it. If raw data is not obtainable from a given vendor, identify the alternatives: research grade wearables, white label modules, contract manufactured band, or non wearable substitutes.

On privacy law, note that continuous video of a person's home, and any biometric identifier derived from it, is among the most heavily regulated data categories that exists, and that "we only send metadata, not video" is a claim the architecture must actually enforce, not just intend.

---

## 9. RESEARCH ARTIFACT REGISTERS

Everything found gets saved. The registers are the durable asset of this project. They persist across phases and across both concepts. Append to them continuously. Never let a source be cited in a phase output without also landing in the register.

Write to `/research/registers/`.

| File | Contents |
|------|----------|
| `sources.md` | Running bibliography. Every source consulted, including ones rejected. Title, author or org, URL, date accessed, publication date, one line on what it was used for, and a credibility rating. |
| `papers.md` | Academic and clinical literature. Full citation, DOI, what it establishes, sample size and study design, effect size where relevant, whether it is validated against a gold standard, and which marker or claim it supports. Note replication status. Note when a result is a single lab demo and not a productized capability. |
| `components.md` | Every hardware part evaluated, including rejected ones. Part number, manufacturer, function, key specs, price at each volume tier, distributor and link, lead time, lifecycle status, datasheet URL, and why selected or rejected. |
| `oss.md` | Every open source project, model, dataset, and library evaluated. Name, repo URL, license (exact SPDX identifier), maintenance status, last commit, whether commercial use is permitted, whether it requires specific hardware or runtime, what it does, what it does not do, and the estimated engineering effort to integrate. **License is not optional and is not a guess. Read the license file.** Several widely used vision and pose models carry non commercial or restrictive licenses. Flag every one. |
| `datasets.md` | Datasets usable for training, validation, or benchmarking. Name, size, license, access terms, whether it contains the population of interest (older adults in home settings, pregnant people), and known biases. |
| `markers.md` | The unified trend and marker catalog across both concepts. See the marker phase in each concept brief. |
| `vendors.md` | Every vendor, ODM, CM, lab, content licensor, and potential partner. Contact path, what they supply, minimum order quantity, whether they work with startups, and any published pricing. |
| `competitors.md` | Every company profiled. Product, buyer, price, funding history, current status, and if dead, why. |
| `funding.md` | Every fund, grant program, and accelerator identified, with actual recent deals in the category as evidence of thesis fit. |

Register discipline:
1. A register entry is created the moment a thing is evaluated, not at the end of a phase.
2. Rejected items stay in the register with the rejection reason. The rejected list is as valuable as the selected list, and it prevents re researching the same dead end.
3. Every register entry carries a date and a confidence rating.
4. No register entry is ever deleted. It is superseded, with the superseding entry linked.
