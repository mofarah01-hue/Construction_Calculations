# shared_capital_landscape.md
## Capital Landscape: Non-Dilutive Funding, Venture and Strategic Investors, Accelerators

Scope per 00_framework.md section 8. Covers both concepts: Concept A (Elder Home Monitoring, aging in place) and Concept B (Pregnancy and Parenting Companion, maternal and family health). Evidence rules per section 5. All amounts carry source, URL, and date. Confidence marked HIGH, MEDIUM, LOW. Sources dated before 2025-01-10 are flagged stale (older than 18 months from the 2026-07-10 research date).

Both products are positioned as general wellness, not medical devices (section 2). This affects funding fit. NSF SBIR and NIH SBIR both fund wellness-adjacent and digital health tools, but NSF explicitly will not fund clinical trials or efficacy studies, and NIH awards skew toward projects with a health outcome hypothesis. This is called out where it bears on eligibility.

---

## 1. NON-DILUTIVE FUNDING (LEAD)

### 1.1 Program status, critical timing gate

| Fact | Detail | Confidence | Source |
|------|--------|-----------|--------|
| SBIR/STTR authority lapsed | Legislative authority expired 2025-10-01; NIH had no active solicitations during the lapse | HIGH | NIA Small Business Funding page |
| Reauthorized | SBIR and STTR reauthorized 2026-04-13 | MEDIUM | NIA page (search-surfaced, verify against SBA before relying) |
| NOFOs re-released | New NIH SBIR/STTR NOFOs released 2026-05-29 | MEDIUM | NIA page |
| Next NIH standard receipt date | 2026-09-05 | MEDIUM | NIA page |
| Next NSF full-proposal deadline | 2026-07-27 (Project Pitch first, invitation required) | MEDIUM | NSF 26-510 solicitation |

The reauthorization dates are single-source and should be confirmed against SBA.gov and the NIH Guide before any filing decision. Flagged in Open Questions.

### 1.2 NIH / NIA SBIR-STTR, aging in place (Concept A primary)

| Attribute | Value | Confidence | Source |
|-----------|-------|-----------|--------|
| Program owner | National Institute on Aging (NIA), NIH | HIGH | nia.nih.gov/research/sbir |
| Thesis fit | Explicit mandate for "innovation to support healthy aging and aging in place" | HIGH | NIA About page |
| Phase I award | Up to $300,000, up to 1 year; up to $500,000 for Alzheimer's and AD-related dementias (AD/ADRD) | HIGH | NIA Small Business Funding |
| Phase II award | Up to $2,000,000, generally 2 years; up to $2,500,000 for AD/ADRD | HIGH | NIA Small Business Funding |
| Mechanisms | SBIR: R43 (Phase I), R44 (Phase II). STTR: R41 (Phase I), R42 (Phase II) | HIGH | NICHD/NIBIB program structure |
| Eligibility | US small business, fewer than 500 employees, for-profit; SBIR requires more than 50% US individual ownership; STTR requires formal partnership with a research institution and 40/30 work split | HIGH | Seed.nih.gov, NIA FAQ |

Read: an AD/ADRD framing (cognitive decline, dementia care, caregiver support) raises the Phase I cap to $500,000 and the Phase II cap to $2.5M. The Elder Home Monitoring concept's cognitive and passive-sensing markers plausibly qualify. This is the single most relevant non-dilutive lever for Concept A.

### 1.3 NIH / NICHD SBIR-STTR, maternal and infant health (Concept B primary)

| Attribute | Value | Confidence | Source |
|-----------|-------|-----------|--------|
| Program owner | Eunice Kennedy Shriver National Institute of Child Health and Human Development (NICHD), NIH | HIGH | nichd.nih.gov |
| Thesis fit | SBIR/STTR activities serving NICHD mission: maternal, infant, pregnancy, and child health | HIGH | NICHD About / Priorities pages |
| Phase I award (guideline) | Up to $256,580 (NIH statutory guideline figure; hard cap waivers exist for topics on the published list) | MEDIUM | NICHD types page |
| Phase II award (guideline) | Up to $1,710,531 (NIH statutory guideline figure) | MEDIUM | NICHD types page |
| Mechanisms | Same R41/R42/R43/R44 structure as NIA | HIGH | NICHD types page |
| Standard due dates | 2026-09-05, 2027-01-05, 2027-04-05 | HIGH | NICHD funding page |
| Eligibility | Same SBIR/STTR eligibility as 1.2 | HIGH | Seed.nih.gov |

Note the two different Phase I figures across NIA ($300K) and NICHD ($256,580). NICHD cites the NIH statutory guideline; NIA cites the higher hard-cap figure that NIH institutes may use. Both are legitimate; the operative cap depends on the specific NOFO. Do not treat either as the number until the target NOFO is read. Flagged.

### 1.4 NSF SBIR-STTR (both concepts, secondary)

| Attribute | Value | Confidence | Source |
|-----------|-------|-----------|--------|
| Program | NSF SBIR/STTR, "America's Seed Fund," solicitation NSF 26-510 | HIGH | nsf.gov NSF 26-510 |
| Phase I award | Up to $305,000 | HIGH | NSF 26-510 |
| Phase II award | Up to $1,250,000 over 2 years | HIGH | NSF 26-510 |
| Eligibility | US small business, fewer than 500 employees, more than 50% US-citizen or permanent-resident ownership; Project Pitch and invitation required before full proposal | HIGH | NSF 26-510 |
| Constraint | Will not fund clinical trials, clinical efficacy, or safety studies; limited human-subject feasibility work only | HIGH | NSF 26-510 |
| Deep-tech framing | 2026 solicitation themed on deep technologies advancing US competitiveness and security | MEDIUM | NSF 26-510 |

Read: NSF fits the sensing, fusion, and on-device model layers (the shared technical spine, section 8) far better than the care-delivery outcome layer. Frame an NSF pitch around the multimodal sensor-fusion and edge-inference engineering, not the health claim. NSF non-dilutive dollars pair cleanly with the general-wellness positioning because NSF does not want a clinical claim.

### 1.5 Non-dilutive summary

| Program | Best-fit concept | Phase I ceiling | Phase II ceiling | Why |
|---------|-----------------|-----------------|------------------|-----|
| NIH / NIA SBIR-STTR | A (aging) | $300K, or $500K AD/ADRD | $2.0M, or $2.5M AD/ADRD | Direct aging-in-place mandate; dementia framing lifts cap |
| NIH / NICHD SBIR-STTR | B (maternal/family) | approx $256K (NOFO-dependent) | approx $1.71M | Direct maternal and infant mandate |
| NSF SBIR-STTR | A and B (tech layer) | $305K | $1.25M | Funds the sensing/AI engineering; no clinical-claim requirement |

---

## 2. VENTURE AND STRATEGIC INVESTORS

### 2.1 Aging tech / aging in place (Concept A)

| Investor | Type | Thesis | Tied recent check (see section 4) | Confidence | Source |
|----------|------|--------|-----------------------------------|-----------|--------|
| Primetime Partners | Early-stage VC (Alan Patricof, Abby Miller Levy) | Products improving quality of living for older adults | Bold Series A participant (Sept 2023) | HIGH | primetimepartners.com; Bold PR |
| Ziegler Link-age Funds | Growth VC, 160+ senior-living-provider LPs | Post-acute and aging care delivery and tech-enabled services; new ~$50M AgeTech fund planned | Portfolio incl. True Link, CareLinx, OnShift (dates UNKNOWN, likely stale) | MEDIUM | ziegler.com; longevity.technology |
| Insight Partners | Growth VC | Scale-stage software; entered senior-living AI via Inspiren | Inspiren $100M Series B lead (Sept 2025) | HIGH | Inspiren PR; insightpartners.com |
| Touring Capital | Growth, AI-SaaS | AI-powered SaaS | SafelyYou $43M Series C lead (Jan 2025) | HIGH | SafelyYou PR |
| Foundation Capital | VC | Participated SafelyYou Series C | SafelyYou (Jan 2025) | HIGH | SafelyYou PR |
| Founders Fund | VC | Participated SafelyYou Series C | SafelyYou (Jan 2025) | HIGH | SafelyYou PR |
| Qualcomm Ventures | Strategic CVC | Edge silicon and connectivity; SafelyYou investor | SafelyYou (Jan 2025) | HIGH | SafelyYou PR |
| Samsung Next | Strategic CVC | Consumer hardware and health; in SafelyYou and Bold | SafelyYou (Jan 2025); Bold (Sept 2023) | HIGH | SafelyYou PR; Bold PR |
| Angelini Ventures | VC (healthcare) | AgeTech; co-led Nobi | Nobi EUR 35M Series B co-lead (Jan 2025) | HIGH | Nobi/GlobeNewswire |
| Nexus NeuroTech Ventures | VC | Neurotech and aging; co-led Nobi | Nobi Series B co-lead (Jan 2025) | HIGH | Nobi/GlobeNewswire |
| EQT (Health Economics; Dementia Fund) | Growth/strategic | Dementia and aging care; Nobi backer | Nobi (Jan 2025) | HIGH | Nobi PR |
| Longevity Venture Partners | Early-stage VC | AgeTech, aging in place, longevity; ~$30M fund | Fund closed 2023, no specific tied check found (UNKNOWN) | LOW | thegerontechnologist.com |
| Best Buy Health | Strategic (corporate) | RPM and care-at-home (Current Health + Lively); channel partner more than check-writer | No 2025 startup check confirmed (UNKNOWN) | MEDIUM | Tracxn; seniorlivinginnovationforum |

Aging strategic-partner note: Best Buy Health, Bosch, Philips, and ADT are more valuable as distribution and integration partners than as equity investors. No confirmed 2025 equity check from Bosch, Philips, or ADT was found. Flagged in Open Questions.

### 2.2 Maternal, family, and femtech (Concept B)

| Investor | Type | Thesis | Tied recent check (see section 4) | Confidence | Source |
|----------|------|--------|-----------------------------------|-----------|--------|
| Andreessen Horowitz (a16z Bio + Health) | VC | Digital health at scale; Pomelo backer across rounds; also in Bold (aging) | Pomelo Series C (Jan 2026) | HIGH | Pomelo PR; Bold PR |
| Stripes | Growth VC | Consumer and healthcare scale-ups | Pomelo $92M Series C lead (Jan 2026) | HIGH | Pomelo PR |
| TMV | Early-stage VC | Health and consumer; co-led Millie | Millie $12M Series A co-lead (Feb 2025) | HIGH | Millie PR; Fierce Healthcare |
| Foreground Capital (fmr GingerBread affiliate context) | VC (women's health) | Women's health; co-led Millie | Millie Series A co-lead (Feb 2025) | HIGH | Millie PR |
| U.S. Venture Partners (USVP) | VC | Healthcare; led Delfina | Delfina $17M Series A lead (Jan 2025) | HIGH | Delfina PR/HIT Consultant |
| ARTIS Ventures | VC | Deep tech and health; Delfina | Delfina (Jan 2025) | HIGH | Delfina PR |
| Mayo Clinic (ventures) | Strategic | Clinical validation and maternal outcomes; Delfina backer | Delfina (Jan 2025) | HIGH | Delfina PR |
| Tokio Marine Future Fund | Strategic (insurer CVC) | Maternal-outcome cost savings; Delfina | Delfina (Jan 2025) | HIGH | Delfina PR |
| Springcoast Partners | Growth VC | Consumer health hardware/software; led Nanit | Nanit $50M growth (Dec 2025) | HIGH | Nanit PR |
| Upfront Ventures | VC | Consumer and health; Nanit | Nanit (Dec 2025) | HIGH | Nanit PR |
| Rhia Ventures | Impact VC | Contraception, maternal health, reproductive health | No 2024-2026 tied check surfaced (UNKNOWN) | MEDIUM | rhiaventures.org |
| Avestria Ventures | Early-stage VC | Women's health, women-led, life science | Portfolio incl. Mae, Raydiant (dates UNKNOWN) | MEDIUM | avestria.vc |
| Portfolia (FemTech Fund II) | Investor collective | Women's health, Seed to Series B, fund open | No single tied check surfaced (UNKNOWN) | MEDIUM | femtechinsider.com |

---

## 3. ACCELERATORS

| Program | Focus | Fit | Terms | Confidence | Source |
|---------|-------|-----|-------|-----------|--------|
| AgeTech Collaborative from AARP | Aging, ~700 member companies | Concept A: distribution, pilots, senior-living access, CES showcase | Membership/cohort; not primarily equity | HIGH | agetechcollaborative.org; AARP CES 2026 release |
| Techstars Healthcare (sponsored by Cedars-Sinai, Point32Health, UCI Health, UnitedHealthcare) | Digital health incl. women's health, mental health, access | Both concepts; payer and provider sponsors are the exact buyers | Techstars standard: ~$120K for ~6-9% equity (verify current terms) | MEDIUM | techstars.com; Aging2.0 blog |
| Cedars-Sinai Accelerator+ | Seed+ / late-seed healthcare, incl. women's and maternal health | Concept B (maternal mortality, chronic conditions) | Venture-building platform; equity terms UNKNOWN | MEDIUM | csaccelerator.com; cedars-sinai.org |
| MedTech Innovator | Largest medtech accelerator | Hardware path (sensor device); note wellness positioning limits medical-device framing | Non-dilutive/equity mix; ~$100K-$500K noted, verify | MEDIUM | digital.health; search-surfaced |
| Aging2.0 | Global aging-innovation network | Concept A ecosystem, pilots, corporate intros | Network, not a check | MEDIUM | aging2.com |

Techstars and MedTech Innovator equity terms are from secondary sources and must be confirmed against the current program agreement before signing. Flagged.

---

## 4. ACTUAL RECENT DEALS (THESIS-FIT EVIDENCE)

Window: last 24 months (2024-07 to 2026-07). Rows outside the window are labeled. These are the concrete checks that anchor the funds above.

### 4.1 Aging in place / senior monitoring (Concept A)

| Company | What it does | Investor(s) | Round | Amount | Date | In window | Confidence | Source URL |
|---------|-------------|-------------|-------|--------|------|-----------|-----------|-----------|
| Inspiren | AI resident-safety and monitoring ecosystem for senior living (eCall video triage) | Insight Partners (lead); Avenir, Primary, Scale, Story, Third Prime, Studio VC | Series B | $100M (total to $155M) | 2025-09-25 | Yes | HIGH | prnewswire.com Inspiren Series B |
| SafelyYou | AI fall detection and prevention, memory care | Touring Capital (lead); Foundation Capital, Founders Fund, Cross Creek, Omega Healthcare, Samsung Next, Qualcomm Ventures | Series C | $43M (total >$100M) | 2025-01-28 | Yes | HIGH | businesswire.com / safely-you.com |
| Nobi | AI smart-light fall detection for senior care | Angelini Ventures and Nexus NeuroTech Ventures (co-leads); 15th Rock, EQT Health Economics, EQT Dementia Fund, PMV | Series B | EUR 35M (approx $37M) | 2025-01-28 | Yes | HIGH | globenewswire.com Nobi Series B |
| Bold | Movement-as-medicine exercise for older adults, Medicare | Rethink Impact (lead); Samsung Next, a16z Bio+Health, Khosla, GingerBread, Primetime Partners | Series A | $17M (total $27M) | 2023-09-12 | No (stale, ~34 mo) | HIGH | prnewswire.com Bold Series A |
| CarePredict | AI wearable and platform for senior activity monitoring | Multiple (round-level detail not confirmed) | Cumulative | approx $48.7M total | Date UNKNOWN | UNKNOWN | MEDIUM | Crunchbase Base via news.crunchbase.com |

### 4.2 Maternal, infant, and family health (Concept B)

| Company | What it does | Investor(s) | Round | Amount | Date | In window | Confidence | Source URL |
|---------|-------------|-------------|-------|--------|------|-----------|-----------|-----------|
| Pomelo Care | Virtual value-based maternity, newborn, women's and children's care | Stripes (lead); a16z, PLUS Capital, Atomico, BoxGroup, SV Angel | Series C | $92M at $1.7B valuation | 2026-01-08 | Yes | HIGH | prnewswire.com Pomelo Series C |
| Nanit | AI baby monitor and parenting-intelligence infant health | Springcoast Partners (lead); Upfront Ventures, JVP | Growth | $50M (total $125M) | 2025-12-16 | Yes | HIGH | prnewswire.com Nanit $50M |
| Millie | Tech-enabled midwife-led maternity clinics and platform | TMV and Foreground Capital (co-leads) | Series A | $12M | 2025-02-20 | Yes | HIGH | businesswire.com Millie Series A |
| Delfina | AI-powered proactive maternal health, risk prediction | USVP (lead); ARTIS Ventures, Mayo Clinic, Tokio Marine Future | Series A | $17M | 2025-01 | Yes | HIGH | hitconsultant.net Delfina $17M |
| Maven Clinic | Virtual women's and family health, fertility to pediatrics | Existing syndicate | Series F | $125M at $1.7B valuation | 2024-10 | Yes (near 18-mo edge) | HIGH | prnewswire.com Maven Series F |
| Pomelo Care | (prior round, for trend context) | Andreessen Horowitz (lead), First Round | Seed + Series A | $33M combined | 2023-06 | No (stale) | HIGH | businesswire.com Pomelo 2023 |

Read: Both categories show live, scaled, recent checks. The maternal/family side is running larger and later-stage ($92M Series C, $1.7B valuation) than the aging side, but the aging side has a fresh $100M Series B (Inspiren) proving growth capital is present for senior-monitoring specifically.

---

## Register Entries

Per framework section 9. These entries are staged here for the maintainer of `research/registers/`. This file does not write to the registers directly (out of scope per task instruction).

### Sources (for registers/sources.md)

| Title | Org | URL | Pub date | Accessed | Used for | Credibility |
|-------|-----|-----|----------|----------|----------|-------------|
| About NIA Small Business Funding | NIA / NIH | nia.nih.gov/research/sbir/about-nia-small-business-funding | ongoing | 2026-07-10 | NIA SBIR award sizes, timing, AD/ADRD caps | HIGH (primary gov) |
| NIA Small Business Programs FAQ | NIA / NIH | nia.nih.gov/research/sbir/nia-small-business-programs-frequently-asked-questions | ongoing | 2026-07-10 | Eligibility | HIGH (primary gov) |
| NICHD Small Business Application Types | NICHD / NIH | nichd.nih.gov/grants-contracts/SBIR_STTR/types | ongoing | 2026-07-10 | NICHD Phase I/II figures, mechanisms | HIGH (primary gov) |
| NICHD SBIR/STTR NOFOs | NICHD / NIH | nichd.nih.gov/grants-contracts/SBIR_STTR/funding | ongoing | 2026-07-10 | Due dates | HIGH (primary gov) |
| NSF 26-510 Solicitation | NSF | nsf.gov/funding/opportunities/.../nsf26-510/solicitation | 2026 | 2026-07-10 | NSF award sizes, eligibility, clinical constraint | HIGH (primary gov) |
| Seed.nih.gov Understanding SBIR/STTR | NIH SEED | seed.nih.gov/small-business-funding | ongoing | 2026-07-10 | Cross-institute eligibility | HIGH (primary gov) |
| Inspiren Raises $100M Series B | PR Newswire / Inspiren | prnewswire.com/news-releases/inspiren-raises-100m-series-b... | 2025-09-25 | 2026-07-10 | Deal, Insight Partners lead | HIGH (co press release) |
| SafelyYou $43M Series C | BusinessWire / SafelyYou | businesswire.com/news/home/20250128706931/en | 2025-01-28 | 2026-07-10 | Deal, syndicate | HIGH (co press release) |
| Nobi EUR 35M Series B | GlobeNewswire / Angelini | globenewswire.com/news-release/2025/01/28/3016061 | 2025-01-28 | 2026-07-10 | Deal, co-leads | HIGH (co press release) |
| Bold $17M Series A | PR Newswire / Bold | prnewswire.com/.../bold-announces-17-million-series-a... | 2023-09-12 | 2026-07-10 | Deal, Primetime/Samsung participation | HIGH but STALE |
| Pomelo Care $92M Series C | PR Newswire / Pomelo | prnewswire.com/.../pomelo-care-raises-92-million-series-c... | 2026-01-08 | 2026-07-10 | Deal, Stripes lead, valuation | HIGH (co press release) |
| Nanit $50M Growth | PR Newswire / Nanit | prnewswire.com/.../nanit-raises-50m... | 2025-12-16 | 2026-07-10 | Deal, Springcoast lead | HIGH (co press release) |
| Millie $12M Series A | BusinessWire / Millie | businesswire.com/news/home/20250220127655/en | 2025-02-20 | 2026-07-10 | Deal, TMV/Foreground co-leads | HIGH (co press release) |
| Delfina $17M Series A | HIT Consultant / PRWeb | hitconsultant.net/2025/01/29/delfina-raises-17m... | 2025-01-29 | 2026-07-10 | Deal, USVP lead, Mayo/Tokio Marine | HIGH (trade + PR) |
| Maven $125M Series F | PR Newswire / Maven | prnewswire.com/.../maven-clinic-announces-125-million-series-f... | 2024-10 | 2026-07-10 | Deal, valuation | HIGH but near-stale |
| Primetime Partners site | Primetime Partners | primetimepartners.com | ongoing | 2026-07-10 | Aging VC thesis | HIGH (primary) |
| Ziegler Link-age Funds | Ziegler | ziegler.com/.../ziegler-link-age-funds | ongoing | 2026-07-10 | Aging growth VC, LP base | HIGH (primary) |
| Rhia Ventures | Rhia Ventures | rhiaventures.org | ongoing | 2026-07-10 | Femtech VC thesis | HIGH (primary) |
| Avestria Ventures | Avestria | avestria.vc | ongoing | 2026-07-10 | Femtech VC thesis | HIGH (primary) |
| AgeTech Collaborative from AARP | AARP | agetechcollaborative.org | ongoing | 2026-07-10 | Accelerator/network | HIGH (primary) |
| Techstars Healthcare / Cedars-Sinai | Techstars | techstars.com/blog/techstars-healthcare-accelerator... | 2025 | 2026-07-10 | Accelerator | MEDIUM (primary, terms secondary) |
| 2025 Guide to AgeTech Funds and Accelerators | TheGerontechnologist | thegerontechnologist.com | 2025 | 2026-07-10 | Aging investor/accelerator map | MEDIUM (curated blog) |
| Femtech Investors list | Femtech Insider | femtechinsider.com/femtech-investors | ongoing | 2026-07-10 | Femtech investor map | MEDIUM (curated trade) |

### Funding (for registers/funding.md)

| Fund / program / accelerator | Type | Concept fit | Stage / check | Thesis-fit deal (evidence) | Deal date | Confidence |
|------------------------------|------|-------------|---------------|----------------------------|-----------|-----------|
| NIH / NIA SBIR-STTR | Non-dilutive grant | A | PhI $300K/$500K; PhII $2.0M/$2.5M | Program-level (award list not pulled) | n/a | HIGH |
| NIH / NICHD SBIR-STTR | Non-dilutive grant | B | PhI approx $256K; PhII approx $1.71M | Program-level | n/a | HIGH |
| NSF SBIR-STTR (26-510) | Non-dilutive grant | A, B (tech layer) | PhI $305K; PhII $1.25M | Program-level | n/a | HIGH |
| Insight Partners | Growth VC | A | Series B+ | Inspiren $100M | 2025-09-25 | HIGH |
| Touring Capital | Growth VC | A | Series C | SafelyYou $43M | 2025-01-28 | HIGH |
| Angelini Ventures | VC | A | Series B | Nobi EUR 35M | 2025-01-28 | HIGH |
| Nexus NeuroTech Ventures | VC | A | Series B | Nobi EUR 35M | 2025-01-28 | HIGH |
| Primetime Partners | Early VC | A | Seed/Series A | Bold $17M (participant) | 2023-09-12 (stale) | HIGH |
| Ziegler Link-age Funds | Growth VC | A | Growth | Portfolio: True Link, CareLinx (dates UNKNOWN) | UNKNOWN | MEDIUM |
| Samsung Next | Strategic CVC | A | Multi | SafelyYou; Bold | 2025-01 / 2023-09 | HIGH |
| Qualcomm Ventures | Strategic CVC | A | Series C | SafelyYou $43M | 2025-01-28 | HIGH |
| Stripes | Growth VC | B | Series C | Pomelo $92M | 2026-01-08 | HIGH |
| Andreessen Horowitz (Bio+Health) | VC | A, B | Seed to C | Pomelo; Bold | 2026-01 / 2023-09 | HIGH |
| USVP | VC | B | Series A | Delfina $17M | 2025-01 | HIGH |
| TMV | Early VC | B | Series A | Millie $12M | 2025-02-20 | HIGH |
| Foreground Capital | VC (women's health) | B | Series A | Millie $12M | 2025-02-20 | HIGH |
| Springcoast Partners | Growth VC | B | Growth | Nanit $50M | 2025-12-16 | HIGH |
| Mayo Clinic (ventures) | Strategic | B | Series A | Delfina $17M | 2025-01 | HIGH |
| Tokio Marine Future | Strategic (insurer) | B | Series A | Delfina $17M | 2025-01 | HIGH |
| Rhia Ventures | Impact VC | B | Early | Tied check UNKNOWN | UNKNOWN | MEDIUM |
| Avestria Ventures | Early VC | B | Early | Mae, Raydiant (dates UNKNOWN) | UNKNOWN | MEDIUM |
| Portfolia FemTech Fund II | Investor collective | B | Seed to B | Tied check UNKNOWN | UNKNOWN | MEDIUM |
| AgeTech Collaborative (AARP) | Accelerator/network | A | Non-equity | Ecosystem | n/a | HIGH |
| Techstars Healthcare / Cedars-Sinai | Accelerator | A, B | ~$120K / ~6-9% (verify) | Cohort | 2025 | MEDIUM |
| Cedars-Sinai Accelerator+ | Accelerator | B | Seed+ (terms UNKNOWN) | Women's/maternal cohort | 2025 | MEDIUM |
| MedTech Innovator | Accelerator | A (hardware) | ~$100K-$500K (verify) | Cohort | ongoing | MEDIUM |

---

## Open Questions

1. SBIR/STTR reauthorization dates (2026-04-13 reauth, 2026-05-29 NOFO release) are single-source from the NIA page as surfaced in search. Confirm against SBA.gov and the NIH Guide before any filing decision.
2. NIA Phase I cap ($300K/$500K) versus NICHD Phase I guideline ($256,580) differ. The operative cap is NOFO-specific. Read the exact target NOFO before modeling non-dilutive runway.
3. Whether the general-wellness positioning (section 2) weakens NIH competitiveness. NIH review favors a health-outcome hypothesis; a pure wellness framing may score worse. Untested. May argue for leading with NSF (which does not want a clinical claim) for the sensing/AI work.
4. CarePredict round-level history (which round, when, at what valuation) not confirmed; only a cumulative approx $48.7M figure found.
5. Ziegler Link-age, Rhia Ventures, Avestria, Portfolia: no specific 2024-2026 tied check surfaced. Their portfolio dates need Crunchbase or PitchBook confirmation to qualify as in-window thesis evidence.
6. No confirmed 2025-2026 equity check from Bosch, Philips, or ADT into aging-tech startups. Best Buy Health reads as a channel/M&A partner, not an early-stage check-writer. Confirm CVC posture.
7. Accelerator equity terms (Techstars ~6-9%, MedTech Innovator $100K-$500K) are secondary-source and must be verified against current program agreements.
8. Delfina exact announcement day within Jan 2025 and Maven exact day within Oct 2024 not pinned; both confirmed to month.

## Assumptions Made

1. Research date treated as 2026-07-10 for the 18-month staleness line (before 2025-01-10 flagged stale) and the 24-month deal window (2024-07 onward).
2. EUR-to-USD for Nobi taken from the company's own press materials ($37M for EUR 35M); not independently FX-checked.
3. "Concept A = aging" and "Concept B = maternal/family" inherited from 00_framework.md line 3. Treated as fixed.
4. NICHD figures labeled MEDIUM because they are the NIH statutory guideline numbers; actual per-NOFO caps can differ and were not read at the NOFO level.
5. Investor thesis-fit is inferred from the specific deal each led or joined, not from a stated fund mandate document, except where a primary fund page was read (Primetime, Ziegler, Rhia, Avestria).

## Confidence Summary

Overall: HIGH on the non-dilutive award mechanics and sizes (all primary NIH/NSF sources) and HIGH on every in-window deal in section 4 (each traced to a company or wire press release with a date and named lead investor). 

Strongest evidence: the deal table. Inspiren ($100M, Sept 2025) and SafelyYou ($43M, Jan 2025) for aging; Pomelo ($92M, Jan 2026) and Nanit ($50M, Dec 2025) for maternal/family. These are unambiguous, recent, named-syndicate rounds.

Weakest: (a) the SBIR reauthorization timeline (single-source, MEDIUM, must verify before filing); (b) the NIA-versus-NICHD Phase I cap discrepancy; (c) the investors with no tied in-window check (Ziegler, Rhia, Avestria, Portfolia, Longevity Venture Partners), which are LOW-to-MEDIUM as thesis evidence until a dated deal is attached; (d) accelerator equity terms, which are secondary-source. Bold (Sept 2023) and Maven (Oct 2024) are retained for trend context but Bold sits outside the 24-month window and is flagged stale.
