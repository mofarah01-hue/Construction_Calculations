# Idea Backlog

Rolling register of venture ideas under consideration. This is the master index. Formal analysis lives under `research/`. Append only; nothing is deleted, only re-statused.

Last updated: 2026-07-17

## Status legend
- `ANALYZED` full phased business case exists in `research/`
- `RESEARCHING` a phase is in progress
- `PARKED` captured, not yet worked
- `MERGE` overlaps an existing item; track under that item

## How to add an idea
Add a row to the backlog table with the next `I#` id, a one line description, a rough category, a complexity/regulatory flag, and status `PARKED`. Keep the one liner blunt. Detail goes in a notes block below the table, not in the row.

## How this file stays in sync (for later)
This file is committed to the repo. To keep your local copy current: clone the repo into your OneDrive Projects folder, then either use GitHub Desktop (Fetch origin) or a Windows Task Scheduler job that runs `git pull` on a schedule. OneDrive then syncs the local copy across your devices. We can wire up the scheduled pull when you want it.

---

## Analyzed concepts

| ID | Concept | Status | Where |
|----|---------|--------|-------|
| A | Elder home monitoring (passive, in-home, caregiver-facing) | ANALYZED | `research/a/CONCEPT_A_BUSINESS_CASE.md` |
| B | Pregnancy and parenting companion (AI, wearable, self-report) | ANALYZED | `research/b/CONCEPT_B_BUSINESS_CASE.md` |
| Portfolio | Sequence decision across A and B | ANALYZED | `research/PORTFOLIO_DECISION.md` |

## Backlog

| ID | Idea | Category | Complexity / regulatory flag | Overlap | Status |
|----|------|----------|------------------------------|---------|--------|
| I1 | Gut health tracking | Consumer diagnostics + wellness app | Microbiome-to-outcome claims are contested; FTC substantiation risk | Shared spine with B (lab ingest, AI interpretation, wellness claims) | PARKED |
| I2 | Smoker / vaper screening and cessation (the in-ear list) | Behavioral health + wearable device | "Screening" leans clinical; cessation efficacy claims need evidence; in-ear hardware build | AI layer, self-report vs measurement discipline | PARKED |
| I3 | First-time parents full service (bloodwork, fetal doppler, OBGYN telehealth, vitamins, AI layer) | Maternal health service | Fetal doppler is a regulated device with liability (see B assumption B5); cash-pay bloodwork needs telehealth ordering + CLIA (see B assumption B1); supplements | Superset of Concept B | PARKED |
| I4 | At-home blood test + wearable + custom 3D-printed supplement gummies | Personalized diagnostics + DTC supplements | Personalized supplement claims (FTC); gummy manufacturing under FDA dietary-supplement cGMP; lab ordering | Shared spine with B; supplement personalization is the novel part | PARKED |
| I5 | Hormone tracking | Consumer diagnostics + wellness | Interpreting hormone labs crosses into clinical decision support (same input-vs-inference line as A and B) | Shared spine with I1/I4; women's-health adjacency to B | PARKED |
| I6 | Mobile imaging as a service (MRI, X-ray) for hospitals that cannot afford their own, and for overflow | Medical imaging services, B2B | Capital-intensive; FDA-cleared equipment; radiation licensing (X-ray); siting, shielding, radiographer staffing; reimbursement | None with A/B; different business entirely | PARKED |
| I7 | Stateside peptide manufacturing (domestic CDMO) | Pharma manufacturing, B2B | cGMP, FDA facility registration, capital-intensive, specialist skillset | None with A/B; different business entirely | PARKED |

---

## Notes

### I1 Gut health tracking
Consumer microbiome sampling plus an app that trends results and gives diet/behavior guidance. The defensible version is measurement and self-report with education, not disease inference, exactly the claims posture in `00_framework.md`. Watch the evidence base: microbiome-to-health-outcome mapping is scientifically softer than the obstetric evidence in B. User note: category has a graveyard (uBiome bankruptcy, fraud). Research the failures first.

### I2 Smoker / vaper screening and cessation
"The in-ear list" implies an in-ear sensor concept. Two separable products: (a) a cessation program (content + behavioral + AI coach, software only, fast) and (b) an in-ear physiological sensor (hardware, slow, regulatory). The software cessation program is the rough-and-dirty start; the sensor is a later differentiator. Screening for nicotine dependence via a validated instrument is a clinical tool (same issue as EPDS/PHQ-9 in B) and belongs in a risk register.

### I3 First-time parents full service
This is Concept B plus three heavy additions: cash-pay bloodwork, a fetal doppler device, and a vitamins line. Concept B already found (a) the interesting lab model is ingesting labs she already has, not selling a parallel panel (assumption B1), and (b) an at-home fetal device is a regulated Class II product with its own clearance and liability, to be parked as a separate program (assumption B5). Recommendation: do not treat this as a new idea; treat it as the "maximal" version of B and pull features from it into the B roadmap only after the B safety-layer core is proven.

### I4 At-home blood test + wearable + 3D-printed supplement gummies
The diagnostics-plus-wearable-plus-AI half is the same shared spine as B and I1/I5. The novel, defensible-if-done-right piece is on-demand personalized supplement manufacturing (3D-printed gummies). That is a physical-goods manufacturing and FDA dietary-supplement cGMP problem, plus a claims problem (you cannot say a supplement treats a deficiency you diagnosed). Separate the platform (labs + wearable + AI) from the manufacturing (gummies) and cost them independently.

### I5 Hormone tracking
Closely related to I1 and I4: draw or ingest hormone panels, trend against the person's baseline and a published normative range, educate. Defensible as measurement plus reference range; not defensible as "your levels mean you have X." Strong adjacency to Concept B (perimenopause, PCOS, fertility, postpartum). Could be a wedge feature inside the shared diagnostics platform rather than a standalone company.

### I6 Mobile imaging as a service
User note flagged 7/16. Two use cases named: under-resourced hospitals that cannot buy their own MRI/CT/X-ray, and overflow capacity for hospitals that can. This is a capital-heavy, regulated, operations-heavy B2B business with nothing shared with A or B (no consumer AI layer, no wellness claims lane). It competes with established mobile-imaging operators. Needs its own analysis track: capital per truck/trailer, equipment financing, radiographer staffing, state radiation licensing, payer contracting, utilization economics. Very different founder skillset from the software concepts.

### I7 Stateside peptide manufacturing
Domestic contract manufacturing of peptides (reshoring, GLP-1 and research-peptide adjacency). Capital-intensive cGMP facility play. Regulatory and capital barriers are high; moat is real if cleared. Shares nothing with A/B. Needs its own track: FDA facility registration, cGMP buildout cost, offtake/customer commitments before capex, and the specific peptide classes and their demand.

---

## Cross-cutting observation

Ideas I1, I3, I4, and I5 are not five companies. They are variants of ONE platform: **personalized diagnostics (labs plus wearable) with an AI interpretation layer under a disciplined wellness-claims posture.** That is the same shared technical spine `00_framework.md` section 8 already defined for A and B (passive/self-report sensing, fusion, LLM interpretation, wellness claims discipline). If that platform gets built for Concept B, I1/I3/I4/I5 become feature modules or adjacent verticals on top of it, not new builds. I2 rides the same AI layer. Only I6 (mobile imaging) and I7 (peptide manufacturing) are genuinely separate businesses with separate skillsets and capital profiles.

Strategic read, low confidence pending analysis: the software/diagnostics cluster (B, I1, I3, I4, I5, and the software half of I2) is one roadmap. I6 and I7 are opportunistic B2B bets that should be judged on their own, mostly on capital access and operational execution, not on any synergy with the rest.
