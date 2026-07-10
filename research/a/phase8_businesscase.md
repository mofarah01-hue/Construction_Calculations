# Concept A, Phase 8: Business Case and Capital

Governed by `00_framework.md` (section 4 cost model, section 5 evidence, section 6 output, section 9 registers) and `01_concept_a_elder_monitoring.md` (Phase 8). Builds on and does not re derive: hardware COGS and NRE in `research/a/phase3_hardware.md`; burn, headcount, timeline, and comparables in `research/a/phase6_devplan.md`; market sizing, channel ranking, competitor post mortems, willingness to pay, and the reimbursement tension in `research/a/phase7_market.md`; the recurring cloud cost in `research/shared/shared_infra_cost.md`; the funding landscape in `research/shared/shared_capital_landscape.md`; and the risk precedents in `research/regulatory_risk_register.md` (risks R1 through R9).

New citation keys are `[F#]` and resolve in Register Entries. Prior keys resolve in their source files. Confidence tags HIGH, MEDIUM, LOW per framework section 5. Every operating assumption that is not a sourced finding is flagged in Assumptions Made and carried as such, not asserted as fact. Where Phase 7 marked a value UNKNOWN (PERS churn, per bed price, real DTC CAC), it is treated as an assumption here, flagged, never as a finding.

The central inherited constraint, established in Phase 7 and not relitigated: the largest revenue pool in aging in place (RPM and RTM reimbursement) is legally foreclosed by the general wellness positioning, and the two closest consumer product analogs (Amazon Alexa Together dashboard, Cherry Home camera) are dead. The business case is built on the channels that survive: senior living operators (per bed), home care agencies, and payers (per member). DTC is modeled for contrast and to size the ceiling, not as the recommended path.

---

## 0. Operative economics, stated before any scenario

Every downstream number rests on the per subscriber monthly economics below. Sourced inputs are labeled. Every unsourced input is an explicit assumption, flagged here and in Assumptions Made. A "home" or "subscriber" is the 13 device, 5 zone system costed in Phase 3.

### 0.1 Recurring monthly unit economics (base case, mid tier scale, per home per month)

| Line | Consumer DTC | Operator per bed | Payer per member (PMPM) | Basis |
|---|---|---|---|---|
| ARPU per month | $35 | $30 | $12 | Consumer anchored to PERS band $25 to $50, midpoint $37 [Phase 7 6.1]; operator and PMPM are assumptions, flagged |
| Cloud and inference COGS | $2.00 | $2.00 | $2.00 | `shared_infra_cost` mid tier $1 to $3 [HIGH] |
| PERS monitoring seat (buy not build) | $5.00 | $4.00 | $4.00 | ASSUMPTION, Phase 4/7 UNKNOWN; buy the 24/7 escalation, do not build it |
| Support and field ops allocation | $4.00 | $3.00 | $2.00 | ASSUMPTION |
| Payment and channel processing | $1.00 | $1.00 | $1.00 | ASSUMPTION (approx 3 percent) |
| Recurring COGS total | $12.00 | $10.00 | $9.00 | |
| Recurring gross profit per month | $23 (66%) | $20 (67%) | $3 (25%) | |

PMPM economics differ in kind: the payer pays per covered member across an attributed population, most of whom carry no device, so the $12 PMPM figure is thin per monitored home but is applied to a large member base. Its attractiveness is contract size and near zero per member CAC once contracted, not per unit margin. Flagged.

### 0.2 Hardware treatment across the pricing models

Hardware COGS per home from Phase 3: $452 at 100 units, $327 at 1k, $254 at 10k, $201 at 100k. The hardware is a one time cost recovered differently under each pricing model (section 2). Category norm, established in Phase 3 and Phase 7, is hardware near cost with margin taken in subscription.

### 0.3 Churn and CAC, the two values Phase 7 could not source

| Input | Planning value | Status | Impact if wrong |
|---|---|---|---|
| Consumer monthly churn | 2.0% (approx 24 to 30 month life) | ASSUMPTION. Phase 7: PERS churn UNKNOWN, held in private filings. The single largest LTV lever | At 3.5% churn consumer LTV falls approx 40 percent and DTC LTV:CAC breaks |
| Operator and payer annual churn | 10 to 15% per year (approx 1% per month, annual contracts) | ASSUMPTION. B2B contracts are stickier than consumer | Lower churn is the structural reason B2B beats DTC here |
| Consumer CAC (blended paid) | $200 marketing plus hardware subsidy | ASSUMPTION anchored to Phase 7 band $150 to $400+ | The Alexa Together failure is the warning; if true CAC is $350 DTC is unviable |
| Operator CAC (per bed, amortized over a multi bed contract) | $50 to $120 per bed | ASSUMPTION; the sale is to the operator, amortized across beds | Long sales cycle (6 to 12 months) is the real cost, not per bed dollars |

Consumer LTV at base case: $23 per month gross profit times 26 month life equals approx $600 gross, less an approx $30 hardware subsidy at 1k volume, yields LTV:CAC of approx 1.4x at a $200 CAC after hardware. That is thin, exactly the DTC caution from Phase 7. Operator LTV at $20 per month times a 4 to 6 year facility relationship is materially higher against a lower per bed CAC, which is why the recommended channel is B2B.

---

## 1. Three scale scenarios (framework section 4)

Scale tiers align with `shared_infra_cost` (300, 5,000, 50,000 subscribers) so the cloud cost per user is carried, not re derived. Headcount builds on the Phase 6 team (3 engineers to G4, a 4th at G3). Burn, capital, and breakeven are modeled; every figure is a planning estimate, MEDIUM confidence, not a quote.

### 1.1 P&L shape and capital at each scale (recommended B2B blend: operator per bed plus some payer, blended ARPU approx $31 per month, recurring gross margin approx 66%)

| Line | Small (300 homes) | Mid (5,000 homes) | Large (50,000 homes) |
|---|---|---|---|
| Gate context | G4 pilot to early G5 | G5 limited commercial | G6 full commercial |
| Annual recurring revenue | approx $112K | approx $1.9M | approx $18.6M |
| Recurring gross profit (66%) | approx $74K | approx $1.25M | approx $12.3M |
| Headcount | 5 to 6 | 16 to 20 | 45 to 60 |
| Annual opex (fully loaded, incl. S&M) | approx $1.6M | approx $6.0M | approx $17.5M |
| One time hardware subsidy on new adds | approx $10K to $40K | approx $0.6M to $1.2M | approx $3M to $6M |
| Annual net burn | approx $1.5M | approx $4.5M to $5.5M | approx breakeven to approx ($4M) |
| Cumulative capital to reach and sustain this scale | approx $3M to $5M | approx $14M to $22M | approx $30M to $45M |
| Months to company cash flow breakeven | not reachable at this scale | not reachable at this scale | approx month 60 to 84 from start, at approx 18K to 28K subscribers |

Reading, and it is blunt:

1. Small (300) is pre commercial. Revenue does not cover a fraction of the engineering burn. This scale exists to prove the product (G4), not to earn. Fund it with non dilutive plus seed, not with revenue.
2. Mid (5,000) is a real but sub scale business. At approx $1.9M ARR against a $6M opex it still burns approx $5M per year. This is the "valley" scale where most category comparables stalled or soft landed (Cherry, Tellus, Phase 7). It is a fundraising waypoint, not a destination.
3. Large (50,000) is where recurring gross profit (approx $12M) finally approaches the opex base and the business can reach cash flow breakeven if growth spend is throttled. Company level breakeven arrives not at 50,000 but earlier, at roughly 18,000 to 28,000 subscribers, when recurring gross profit covers a stabilized opex base. In the recommended B2B path that is roughly 18,000 to 28,000 beds under contract.

### 1.2 The DTC contrast scenario (for the ceiling, not recommended)

At the same scales on the consumer model (ARPU $35, CAC $200 plus hardware, churn 2% per month), the large scenario tops out near the Phase 7 DTC ceiling: 50,000 homes is approx $21M ARR, and the Phase 7 SAM math caps a well executed DTC only business at approx $40M to $80M ARR at maturity (5 to 10 percent of a $840M SAM). The killing feature of DTC is not the ceiling, it is the CAC to churn ratio: at a 1.4x LTV:CAC the model cannot fund its own growth, which is precisely why Amazon, with the lowest CAC on earth, discontinued the identical dashboard subscription (Phase 7 2.2). DTC is a supplement to a B2B core, not the core.

### 1.3 Scenario headline

| Scenario | Recommended interpretation |
|---|---|
| Small | Prove it. Non dilutive plus seed funds a 300 home G4. No revenue thesis. |
| Mid | Bridge it. 5,000 beds proves the operator motion; still burns approx $5M per year; a Series A waypoint. |
| Large | Earn it. Cash flow breakeven at approx 18K to 28K beds, approx $30M to $45M cumulative capital, approx 5 to 7 years from start. |

---

## 2. Pricing model options, each modeled

Five models per the brief. Modeled on the base case unit economics (section 0). The metric that decides is contribution per home over the first 24 months, net of hardware.

| Model | How it works | Yr 1 + Yr 2 contribution per home (approx) | Friction / conversion | Verdict |
|---|---|---|---|---|
| 1. Hardware plus subscription (unsubsidized) | Hardware at approx 2x COGS ($500 to $650 retail) plus $35 per month | Highest gross (hardware margin approx +$150 plus 2x $276 subscription GP) but | Highest upfront friction; a $500+ box in a market anchored to $199 to $449 kits kills conversion (Phase 3, Phase 7) | REJECT for consumer. Only viable if an operator or payer pays the hardware |
| 2. Hardware subsidized plus subscription | Hardware at approx $299 (below COGS at low volume), $35 per month | approx ($30) hardware at 1k volume, +$552 subscription GP over 24 mo, net approx +$522 | Moderate friction; matches CarePredict ($449 kit) and Envoy ($399 kit) [Phase 3] | VIABLE consumer default; the standard category posture |
| 3. Hardware free, long subscription commitment | $0 hardware, 24 to 36 month commitment at $40 per month | Full COGS ($201 to $327) is CAC; recovered by month 9 to 14; net positive only if the commitment holds | Lowest upfront friction, highest churn exposure; a broken commitment is an unrecovered hardware loss | VIABLE only with enforced term and low churn; dangerous at consumer churn of 2%+ per month |
| 4. Per bed per month to an operator | Operator buys/leases hardware or it is bundled; $25 to $35 per bed per month; multi bed contracts | approx $20 per bed per month GP times bed count; hardware absorbed by contract; low per bed CAC | Long sales cycle (6 to 12 mo), pilot gated; but the operator carries fall liability and has a hard financial reason to pay | RECOMMENDED. SafelyYou, Inspiren, Sage all monetize exactly here [F1][Phase 7] |
| 5. Per member per month to a payer | MA plan or LTC insurer pays $8 to $15 PMPM across attributed members; device to a subset | Thin per member, large aggregate; near zero per member CAC once contracted | Longest cycle (12 to 24 mo, annual bid), MA supplemental PERS is contracting in 2025 (Phase 7) | SECONDARY. Large prize, slow and timing risked; pursue after operator traction |

### 2.1 Pricing decision

Primary: model 4, per bed per month to senior living and assisted living operators. It is the only model where the buyer is concentrated (approx 1,000 operators control most of 1.2M beds, Phase 7 3), the buyer is financially motivated (owns fall liability), the margin is high (approx 67 percent recurring), churn is low (annual facility contracts), and the hardware cost is absorbed by the contract rather than fought over at a consumer checkout. Every recent large check in the category landed on a company selling this way (section 3).

Secondary: model 5 (payer PMPM) as the scale prize once operator efficacy data exists. Tertiary: model 2 (subsidized hardware plus subscription) as a DTC supplement for the remote adult child who will not wait for an operator, sold through the operator or agency relationship rather than paid search. Model 1 is rejected. Model 3 is held for a payer or operator subsidized variant only, never at open consumer churn.

---

## 3. Capital plan, non dilutive first

Sequenced against the gates (Phase 6 1.2). Non dilutive leads because every category survivor did exactly this (SafelyYou funded its early science with CITRIS plus NIA SBIR before any venture round, Phase 6 4). The dilutive rounds are sized to the Phase 6 all in cost to G4 (approx $1.8M to $2.0M) and the section 1 capital to scale.

### 3.1 The raise sequence

| Stage | Gate | Instrument | Target amount | Use | Evidence it is real |
|---|---|---|---|---|---|
| Non dilutive 1 | G1 to G2 | NSF SBIR Phase I (26-510) | up to $305K | The sensing, fusion, and on device model engineering, framed as deep tech, no clinical claim (fits the wellness lane) | NSF 26-510 [shared_capital 1.4] |
| Non dilutive 2 | G2 | NIA SBIR Phase I (R43) | up to $300K, or $500K under an AD/ADRD framing | Founder home to friends and family; characterize the field false positive rate | NIA mandate for aging in place; NIA deploys >$140M per year non dilutive [F4]; SafelyYou used exactly this [Phase 6 4] |
| Angel / pre seed | G2 | SAFE or priced | $500K to $1.5M | Bridge the 3 engineer team through G2/G3; the discipline floor is 3 (Phase 6 2.3) | Rosarium Health $6M seed for aging at home, May 2026 [F2] shows seed capital present for the category |
| Seed | G3 | Priced | $3M to $6M | The 4th engineer on the false positive critical path; 5 to 15 home G3; first operator pilots | Category seed and A activity live (below) |
| Non dilutive 3 | G4 | NIA SBIR Phase II (R44) | up to $2.0M, or $2.5M AD/ADRD | The 50 to 200 unit structured cohort; efficacy evidence; FTC gait substantiation study | A 2025 NIA Phase II fall detection aging in place award ran $1,230,163 [F5] |
| Non dilutive 4 | G4 | NSF SBIR Phase II | up to $1.25M | Scale hardening of the sensing and fusion stack | NSF 26-510 [shared_capital 1.4] |
| Series A | G4 to G5 | Priced | $12M to $18M | Certification, manufacturing scale, operator sales motion, scale to mid then toward breakeven | Direct comparables below |
| Series B / growth | G6 | Priced | $25M+ | Scale to the large scenario and breakeven | Inspiren $100M, Sage $65M (below) |

Non dilutive potential across NSF and NIA is approximately $3.3M to $4.6M (both agencies, both phases), which can fund the entire path from G1 to G4 with only a modest angel/pre seed bridge, sharply reducing early dilution. This is the single most important capital move for a hardware plus wellness company that cannot touch reimbursement. Caveat, from `shared_capital`: SBIR/STTR authority lapsed 2025-10-01 and was reportedly reauthorized 2026-04-13 with NOFOs re released 2026-05-29 and the next NIH receipt date 2026-09-05; confirm against SBA.gov before relying on timing. A wellness only framing may also score worse at NIH review (which favors a health outcome hypothesis), which argues for leading the sensing/AI work through NSF, which does not want a clinical claim.

### 3.2 Actual recent deals as thesis evidence (last 24 months, aging in place), beyond the shared file

New evidence pulled this phase, added to the shared file's Inspiren, SafelyYou, and Nobi rows:

| Company | What it does | Round / lead | Amount | Date | Signal for this business |
|---|---|---|---|---|---|
| Sage | AI, privacy conscious fall monitoring (Sage Detect) for senior living; per community model | Series C, Growth Equity at Goldman Sachs Alternatives (lead), IVP, Goldcrest | $65M (total $124M) | 2026-03-05 | The freshest, largest proof that operator sold, privacy conscious fall monitoring is fundable at growth scale; claims 50% fall reduction and $275 NOI per resident per month [F1] |
| Inspiren | AI resident safety and eCall monitoring for senior living | Series B, Insight Partners lead | $100M (total $155M) | 2025-09-25 | Growth capital present specifically for operator monitoring [shared_capital 4.1] |
| SafelyYou | Ceiling camera fall AI, memory care | Series C, Touring Capital lead | $43M | 2025-01-28 | Per bed operator model, funded early by NIA SBIR then venture [shared_capital; Phase 6 4] |
| Nobi | Smart light (ceiling) fall detection, B2B senior care | Series B, Angelini and Nexus NeuroTech co lead | EUR 35M (approx $37M) | 2025-01-28 | The direct ceiling light analog; lives in B2B, not DTC [shared_capital] |
| Rosarium Health | Aging at home assessments, home modification, fall prevention; MA and Medicaid partnerships | Seed | $6M | 2026-05 | Seed capital and payer/Medicaid channel interest are live for aging at home [F2] |
| Palarum | eTextile wearable fall prevention, clinical settings | Series A | $13.6M | 2025-05 | Fall prevention hardware raises A rounds, though in the clinical (not wellness) lane [F3] |

The pattern is uniform and confirms the Phase 7 channel finding: the capital flows to operator and facility sold fall monitoring (Sage, Inspiren, SafelyYou, Nobi), not to consumer dashboards. The recommended pricing model (per bed) is the one the market is funding right now.

---

## 4. Milestone to unlock map (per gate)

| Gate | What it proves | Who cares | Conversation it opens | What it is worth |
|---|---|---|---|---|
| G1 Bench | Core fall, long lie, gait, and ADL detection runs at stated accuracy on real data | NSF reviewers; a technical angel | NSF SBIR Phase I; the first credible technical pitch | approx $305K non dilutive; a pre seed at idea/tech valuation |
| G2 Self test | 30 days uptime and a characterized real world false positive rate (the make or break number, Phase 6 3) | NIA reviewers; pre seed angels; the first design partner | NIA SBIR Phase I; angel/pre seed | approx $300K to $500K non dilutive plus a $0.5M to $1.5M pre seed |
| G3 Friends and family | Install time, retention, and per home false positive rate across varied real geometry | Seed VCs; senior living operators evaluating a pilot | Seed round; first paid operator pilot LOI | $3M to $6M seed; the pilot LOI is the asset that de risks it |
| G4 Pilot | Efficacy evidence (fall reduction, response time), unit economics, certification underway, gait claim FTC substantiated | Series A VCs (Touring, Insight class); operators ready to contract; NIA Phase II | Series A; NIA/NSF Phase II; multi bed operator contract | $12M to $18M Series A plus approx $3M non dilutive; a signed per bed contract is the valuation driver |
| G5 Limited commercial | FCC and triple UL/ETL complete; positive contribution margin per subscriber; support exists | Operators buying at scale; payers evaluating PMPM | Multi operator rollout; first payer PMPM pilot | First real ARR; the operator ARR multiple sets the mark |
| G6 Full commercial | Target CAC and LTV; scaled manufacturing; channel established | Growth investors (Goldman Growth Equity, Insight class); acquirers (ADT model, Phase 7) | Series B/growth; strategic acquisition | $25M+ growth round; Sage ($124M raised) and Inspiren ($155M) are the comparables [F1] |

The load bearing move is at G2 to G4: a characterized false positive rate (G2) plus a signed operator pilot (G3/G4) plus efficacy data (G4) is the exact package that unlocks a Series A in this category, and it is what SafelyYou, Inspiren, Nobi, and Sage each proved before their large rounds.

---

## 5. Risk register

Technical, regulatory, commercial, and existential. Likelihood is the probability of materializing before G6 absent mitigation; impact is the worst credible outcome. Regulatory rows cross reference `regulatory_risk_register.md` (R1 to R9) and are not re derived.

| ID | Category | Risk | Likelihood | Impact | Mitigation | Leading indicator |
|---|---|---|---|---|---|---|
| B1 | Technical (the kill risk) | Field false positive rate cannot be driven low enough; the product gets unplugged in month two. Lab fall accuracy collapsed from approx 94% to approx 57% in the field, with up to 84 alarms of which 83 were false in one deployment (Phase 6 3) | HIGH | SEVERE | The entire Phase 6 ground truth plan: staged falls for sensitivity, one tap adjudication for precision, duration gating, modality fusion (radar plus camera plus mesh). Characterize at G2, refine across G3 homes. The 4th engineer lands here | Escalated false positives per home per month not falling below target across G2/G3; sensitivity dropping as thresholds tighten |
| B2 | Technical | IMX500 model fit fails; camera node moves to a costlier SoC and a weaker privacy claim (Phase 3 OQ1) | MEDIUM | MODERATE | Fallback to Ambarella CV25 or RK3576; the privacy claim degrades from "pixels never leave the sensor" to "no video leaves the home" | Phase 4 pose model does not fit IMX500 in package memory at 30 fps at G1 |
| B3 | Regulatory | FDA device creep: a wellness output drifts into a screening claim, leaving the general wellness lane (cross ref R1) | MEDIUM | SEVERE | Claims linter in CI blocks any named disease inference from passive data; input vs inference line enforced in software, not prompts | A Warning Letter to a comparable wellness monitor; a competitor forced to file a 510(k) for a shipped feature |
| B4 | Regulatory | FTC substantiation: the gait speed measurement claim is unvalidated against an instrumented walkway (cross ref R2) | HIGH | HIGH | Fund the instrumented walkway validation study at G4 ($30K to $80K, Phase 6); ship un validated metrics as own baseline trends without an accuracy claim | Internal validation error bars wider than the smallest claimed change; an FTC action naming a measurement app |
| B5 | Regulatory | State biometric privacy (BIPA/CUBI/MHMDA): gait signature, face geometry, voiceprint from in home capture; per subject statutory damages (cross ref R4) | HIGH | SEVERE | Consent architecture as a first class feature; on device (T1) inference so raw biometrics never leave the home; encrypted templates with a deletion trigger; geofence by state | A BIPA/CUBI class filing against any home monitor; plaintiff firm intake ads in Illinois |
| B6 | Regulatory | All party consent audio from the assistant and acoustic sensing (cross ref R6) | MEDIUM | HIGH | Wake word gated capture, on device STT, immediate raw audio discard, visible recording indicator, opt in mic, geofence by consent regime | A wiretap complaint against a home voice device; a visitor complaint in G3/G4 |
| B7 | Regulatory / commercial (existential) | Reimbursement foreclosure: the wellness positioning cannot bill RPM/RTM, removing the largest revenue pool. The central strategic tension (Phase 7 4.2) | HIGH (certain, structural) | HIGH | Do not chase reimbursement. Live on operator per bed, agency, and payer PMPM (none of which require device status). Optionally partner an FDA device RPM vendor to sell the wellness layer adjacent, never inside | It is not a future event; it is a present constraint that caps the revenue map |
| B8 | Commercial | DTC CAC to churn ratio does not close (LTV:CAC approx 1.4x base case); the Alexa Together and Cherry Home graveyard (Phase 7 2.2) | HIGH (for a DTC led strategy) | SEVERE (for DTC), LOW (for the recommended B2B strategy) | Do not lead with DTC. Lead with operator per bed where CAC is low and churn is annual contract bound. Treat DTC as an operator/agency sourced supplement | Blended DTC CAC above approx $250; consumer monthly churn above approx 3% in any cohort |
| B9 | Commercial | Operator sales cycle is long (6 to 12 mo) and pilot gated; cash burns while contracts close | MEDIUM | HIGH | Fund the gap with non dilutive plus seed; run multiple operator pilots in parallel; use the AgeTech Collaborative (AARP) for warm operator access (shared_capital 3) | Pilot to contract conversion below plan; sales cycle exceeding 12 months |
| B10 | Existential | Category history: every DTC consumer play stalled or soft landed; nobody reached a fundable pilot in under approx 6 years (Phase 6 4) | MEDIUM | SEVERE | Build for the B2B pilot from G4; plan 5 to 7 years and approx $30M+ to breakeven, not a lean fast DTC timeline; sequence non dilutive first | Burn outrunning the milestone map; a Series A thesis that rests on DTC |
| B11 | Existential | Single vendor dependency (Sony IMX500, TI radar, a PERS monitoring partner) revoked or repriced (cross ref R7 pattern) | LOW to MEDIUM | HIGH | Abstract the sensing and monitoring layers so vendors are swappable; qualify a second radar and a second monitoring partner before G5 | A vendor deprecation notice, NDA price hike, or acquisition of a supplier by a competitor |

---

## 6. Kill criteria, stated in advance

A business case without kill criteria is a pitch. These are the findings that would make Concept A not worth building, ordered by how early and how decisively they resolve.

| # | Kill criterion | Gate it resolves at | Why it kills |
|---|---|---|---|
| K1 (primary) | The escalated false positive rate cannot be driven below approx 1 per home per month without sensitivity falling below the level a paying operator will accept, after the full Phase 6 ground truth effort | G2, confirmed G3 | This is the "unplugged in month two" failure. The literature says lab accuracy collapses in the field (Phase 6 3); if it cannot be fixed, there is no product, regardless of everything else. Nothing downstream matters if K1 fails |
| K2 | No senior living operator, home care agency, or payer will sign a per bed or PMPM pilot at a price that yields positive contribution margin, after a characterized false positive rate and efficacy data exist | G3 to G4 | The recommended channel is the only venture scale path (Phase 7). If the motivated, liability bearing buyer will not pay at margin, the remaining option is DTC, which K3 covers |
| K3 | DTC is the only available channel, and blended DTC CAC exceeds approx $250 against consumer churn above approx 3% per month | G3 to G4 | This is the Alexa Together outcome with real CAC. A sub 1.3x LTV:CAC on a bounded ceiling ($40M to $80M ARR, Phase 7) is not a venture business and cannot fund its own growth |
| K4 | The gait speed measurement cannot be substantiated against an instrumented walkway within the error bars the claim requires (FTC, R2/B4), and removing the gait claim collapses the differentiation versus a cheaper PERS or single node radar competitor | G4 | If the only defensible differentiator over a $250 Vayyar node or a $37 per month PERS is unvalidated, the added hardware cost (Phase 3: radar plus camera are approx 68% of BOM) is not justified |
| K5 | A regulatory shift (FDA lane narrowing per R1/B3, or a state biometric ruling per R4/B5) makes the core passive in home biometric capture legally untenable at acceptable cost | any gate | The product is in situ biometric capture in the home; if the legal envelope closes, the cost of compliance (or the tail liability) exceeds the business value |

If K1 fails, stop. If K2 and K3 both fail, the venture case is dead even if the technology works. K4 and K5 reshape rather than always kill, but each can be terminal in combination.

---

## Register Entries

Per framework section 9, staged for the register owner. This phase does not edit `research/registers/`. New funding evidence and sources this phase:

### Funding (stage into registers/funding.md)

| Investor / event | Deal | Amount | Date | Thesis signal | Confidence |
|---|---|---|---|---|---|
| Growth Equity at Goldman Sachs Alternatives (lead), IVP, Goldcrest | Sage Series C | $65M (total $124M) | 2026-03-05 | Operator sold, privacy conscious fall monitoring is fundable at growth scale | HIGH |
| Seed investors (Rosarium Health) | Seed | $6M | 2026-05 | Aging at home plus MA/Medicaid channel; seed capital live | MEDIUM |
| Series A investors (Palarum) | Series A | $13.6M | 2025-05 | Fall prevention hardware raises A rounds (clinical lane) | MEDIUM |
| NIH / NIA SBIR-STTR | Program (non dilutive) | >$140M per year deployed; a 2025 aging in place fall detection Phase II award ran $1,230,163 | 2025 | Non dilutive lead for aging in place; the SafelyYou path | HIGH |
| (carried) Insight Partners; Touring Capital; Angelini/Nexus | Inspiren $100M; SafelyYou $43M; Nobi EUR 35M | as logged | 2025 | Operator monitoring is the funded thesis | HIGH |

### Sources (stage into registers/sources.md)

| Key | Source | URL | Date | Used for | Credibility |
|---|---|---|---|---|---|
| F1 | Sage Raises $65M Series C Led by Goldman Sachs Alternatives | https://www.prnewswire.com/news-releases/sage-raises-65m-series-c-led-by-goldman-sachs-alternatives-to-redefine-care-for-americas-aging-population-302705363.html ; https://seniorhousingnews.com/2026/03/05/ai-platform-sage-raises65m-in-new-equity-round-led-by-goldman-sachs-alternatives/ ; https://am.gs.com/en-hk/advisors/news/press-release/2026/sage-growth-equity | 2026-03-05 / accessed 2026-07-10 | Sage $65M Series C, $124M total, IVP + Goldcrest, Sage Detect, 50% fall reduction, $275 NOI/resident/mo | HIGH (co + investor press) |
| F2 | Startup Enabling Aging at Home Raises $6M (Rosarium Health) | https://medcitynews.com/2026/05/aging-home-funding-rosarium/ | 2026-05 / accessed 2026-07-10 | Rosarium $6M seed, aging at home, MA/Medicaid partnerships, fall prevention/home modification | MEDIUM (trade) |
| F3 | Palarum $13.6M Series A (eTextile fall prevention) | fiercehealthcare fundraising tracker '26; Palarum press | 2025-05 / accessed 2026-07-10 | Palarum $13.6M Series A, smart textile fall prevention, clinical | MEDIUM |
| F4 | About NIA Small Business Funding | https://www.nia.nih.gov/research/sbir/about-nia-small-business-funding ; https://www.nia.nih.gov/news/topics/nia-funded-small-business-spotlights | accessed 2026-07-10 | NIA deploys >$140M/yr non dilutive; SafelyYou NIA SBIR spotlight | HIGH (primary gov) |
| F5 | NIA SBIR fall detection aging in place Phase II award | https://www.sbir.gov/awards/215117 | 2025 / accessed 2026-07-10 | 2025 NIA Phase II aging in place fall detection award $1,230,163 | MEDIUM (gov award record, single) |

No source is older than 18 months. Carried funding rows (Inspiren, SafelyYou, Nobi, NSF/NIA/NICHD program mechanics) resolve in `shared_capital_landscape.md`.

---

## Open Questions

1. PERS/monitoring subscription churn is UNKNOWN (Phase 7 OQ1), held in private filings. Every LTV, breakeven, and DTC viability number here rests on the assumed 2% per month consumer / 10 to 15% per year B2B churn. This is the single most material gap. Blocks a defensible LTV:CAC.
2. Senior living per bed per month monitoring price is UNKNOWN (Phase 7 OQ2). SafelyYou, Inspiren, Sage publish nothing per bed. The recommended pricing model's absolute revenue rests on an assumed $25 to $35 per bed. Requires direct RFQ or an operator conversation.
3. Real category DTC CAC is UNKNOWN (Phase 7 OQ3). The $200 assumption drives the DTC contrast; if true CAC is $350, DTC is dead earlier.
4. PERS monitoring partner per seat cost is UNKNOWN (Phase 4/6). It is a recurring COGS line ($4 to $5 assumed) and moves the recurring gross margin.
5. SBIR/STTR reauthorization timing (lapsed 2025-10-01, reportedly reauthorized 2026-04-13) is single source (shared_capital OQ1). Confirm against SBA.gov before modeling non dilutive runway.
6. Whether a general wellness framing weakens NIH SBIR competitiveness (shared_capital OQ3). May force leading the sensing work through NSF. Untested.
7. FTC gait substantiation study cost ($30K to $80K) is an estimate, not a quote (Phase 6 OQ5). It sits in the G4 capital line.
8. Company cash flow breakeven at approx 18K to 28K subscribers assumes the section 0 unit economics hold at scale and that growth spend is throttled. It is a modeled inflection, not a bottom up operating plan.

## Assumptions Made

| # | Assumption | Value | Impact if wrong |
|---|---|---|---|
| 1 | Consumer monthly churn | 2.0% | Highest sensitivity. At 3.5% consumer LTV falls approx 40% and DTC breaks. B2B less exposed |
| 2 | B2B annual churn | 10 to 15% | The structural reason B2B beats DTC; higher churn narrows the gap |
| 3 | Consumer CAC (blended, ex hardware) | $200 | At $350 DTC LTV:CAC falls below 1.0; K3 triggers |
| 4 | Operator CAC per bed | $50 to $120 | The real cost is the sales cycle length, not per bed dollars |
| 5 | PERS monitoring seat (recurring COGS) | $4 to $5 per month | Moves recurring gross margin by approx 10 points |
| 6 | Support + ops + processing (recurring COGS) | $6 to $7 per month | Modeled, not quoted |
| 7 | Blended ARPU (recommended B2B) | approx $31 per month | Drives all scenario ARR; anchored to PERS band and assumed per bed price |
| 8 | Headcount and opex at each scale (5 to 6 / 16 to 20 / 45 to 60) | modeled | Drives burn and breakeven timing; built on the Phase 6 team |
| 9 | Cash flow breakeven at approx 18K to 28K subscribers | modeled inflection | If unit economics are weaker, breakeven scale and capital rise |
| 10 | Non dilutive is winnable and additive (NSF + NIA, both phases, approx $3.3M to $4.6M) | planning | If SBIR is not won or timing slips, dilutive need rises by that amount at the earliest, most expensive gates |
| 11 | Hardware COGS, NRE, and cloud cost per user carried unchanged from Phase 3 and shared_infra_cost | as logged | If BOM or cloud assumptions move, contribution margin moves |
| 12 | Reimbursement remains foreclosed under the wellness positioning (Phase 7 4.2), treated as fixed | fixed | If a compliant reimbursement bridge opens, the revenue map expands materially (upside, not downside) |

## Confidence Summary

Overall confidence: HIGH on the strategic conclusions and the capital plan, MEDIUM on the absolute scenario numbers, LOW on the three values Phase 7 could not source (churn, per bed price, DTC CAC), which are carried as flagged assumptions.

- Strongest (HIGH): the pricing decision (per bed per month to operators) and the capital sequence (non dilutive first, then seed, then a $12M to $18M Series A at G4), both corroborated by fresh, dated, named deals (Sage $65M Series C March 2026, Inspiren $100M September 2025, SafelyYou $43M January 2025, Nobi EUR 35M January 2025) and by the Phase 7 channel ranking. The kill criteria, led by K1 (field false positive rate), are robust and inherited from the Phase 6 critical path.
- Medium: the three scenario P&L shapes, the approx $30M to $45M cumulative capital to breakeven, and the approx 18K to 28K subscriber breakeven inflection. These are internally consistent planning models built on sourced COGS and cloud costs plus flagged operating assumptions, not an operating plan.
- Weakest (LOW / UNKNOWN): PERS churn (blocks a hard LTV:CAC), per bed price (blocks precise recommended channel ARR), and real DTC CAC. All three are Phase 7 open questions carried forward; none was invented.

The load bearing conclusion, HIGH confidence and robust to the weak cells: fund the path from G1 to G4 primarily with NSF and NIA SBIR (approx $3M to $4M non dilutive) plus a modest seed, build for a senior living operator pilot rather than DTC, price per bed per month, and plan for approx $30M cumulative capital and 5 to 7 years to cash flow breakeven at roughly 18K to 28K beds. The venture dies first at K1 (the field false positive rate); it dies second if no operator or payer will pay at margin (K2); and a DTC led strategy dies at K3 the way Amazon Alexa Together already did. Reimbursement, the largest pool, stays foreclosed by the positioning and is designed around, not chased.
