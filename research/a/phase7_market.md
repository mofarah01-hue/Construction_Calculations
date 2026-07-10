# PHASE 7: MARKET, COMPETITION, AND CHANNEL
## Concept A: Elder Home Monitoring
Output file. Governed by `00_framework.md` (sections 5 evidence rules, 9 registers) and `01_concept_a_elder_monitoring.md` Phase 7.

Positioning under evaluation: general wellness, consumer subscription, remote adult child as buyer (founder assumption A7, flagged for challenge).

Date of analysis: 2026-07-10. Currency USD.

---

## 1. BOTTOM-UP MARKET SIZING

Method per framework section 6: count addressable units, apply realistic price and penetration, then check against an analyst TAM. The funnel below sizes the **direct-to-consumer (DTC) segment** first, because that is the buyer the concept assumes. Channel-specific reachable populations are treated separately in section 1.3, because the reachable count is a function of channel, not of the total.

### 1.1 The funnel

| Step | Population | Multiplier | Result | Confidence | Source / basis |
|------|-----------|-----------|--------|-----------|----------------|
| 1 | US adults 65+ living alone, community-dwelling | baseline | **16.2M** | HIGH | ACL 2023 Profile of Older Americans / Census CPS 2023: ~28% of community-dwelling 65+ live alone; 5.7M men + 10.5M women = 16.2M |
| 2 | Have at least one living adult child | x 0.80 | 13.0M | MEDIUM | Assumption. Childlessness among current 65+ cohort ~20%. The buyer in the concept is an adult child; elders with no child fall out of the DTC thesis |
| 3 | Nearest child is "remote" (not within ~20 minutes) | x 0.25 | 3.25M | MEDIUM | AARP/NAC Caregiving in the US 2020: 75% of caregivers live with or within 20 min of the recipient; ~25% are farther; 11% are 1hr+. Used as proxy for the share whose child cannot simply drop by |
| 4 | Household able and willing to fund ~$30-50/mo discretionary | x 0.60 | **1.95M** | LOW-MEDIUM | Assumption. Elders living alone are lower income (median individual income $29,740, 2022; 17.7% in poverty). Ability to pay sits with the adult child. 60% is a judgment call, flagged |

**Addressable DTC households (SAM population): ~1.95M, round to ~2.0M.**

### 1.2 Price and penetration to revenue

Product economics assumed for sizing (validated downstream in Phase 3 / Phase 8, here used only to convert units to dollars):
- Hardware: $200-400 one-time (comparable to CarePredict @Home kit $449.99, Vayyar ~$250/device x3).
- Subscription: $30-40/mo, i.e. ~$360-480/yr. Anchored to PERS market actual pricing (section 6), midpoint $420/yr used.

| Layer | Households | x annual subscription | Result | Note |
|-------|-----------|----------------------|--------|------|
| TAM (all living-alone 65+, theoretical ceiling) | 16.2M | $420 | **~$6.8B/yr** | Ignores buyer, ability to pay, competition. Not a real target |
| SAM (remote-child, able to pay) | 2.0M | $420 | **~$840M/yr** | The defensible DTC ceiling for this product |
| SOM at 5% penetration of SAM | 100,000 | $420 | **~$42M/yr ARR** | Realistic mature DTC outcome. PERS 65+ penetration is 9% and flat (section 6); a pricier, more complex product should assume less |
| SOM at 10% penetration of SAM | 195,000 | $420 | **~$82M/yr ARR** | Optimistic DTC case |

Add-in hardware revenue at SOM 5%: 100,000 units x $300 blended = ~$30M one-time, recurring only on replacement/new adds.

**Headline: the realistic DTC SAM is ~$840M/yr of subscription revenue; a well-executed DTC-only business captures $40-80M ARR at maturity. That is a real business but not a venture-scale outcome on DTC alone. This is the single most important number in the phase and it corroborates founder assumption A7's warning that DTC in this category is CAC- and churn-bound.**

### 1.3 Reachable population by channel (the count changes with the channel)

The framework requires "subset reachable per channel." Reachable universe differs by go-to-market:

| Channel | Reachable universe | Basis | Confidence |
|---------|-------------------|-------|-----------|
| DTC | ~2.0M households (funnel above) | derived | LOW-MEDIUM |
| Senior living / assisted living operators | ~1.0M residents across ~30,600-33,000 communities, ~1.2M licensed beds | NCHS / NIC / A Place for Mom 2024 | HIGH |
| Home health / home care agencies | Clients of ~11,500 Medicare-certified home health agencies plus a larger fragmented non-medical home care base | CDC NCHS 2023 (11,506 HHAs); Definitive tracks 17,300+ active | MEDIUM |
| Medicare Advantage supplemental benefit | ~34M+ MA enrollees, but only ~14.5% of plans ever offered PERS and that is contracting in 2025 | KFF; ATI Advisory | MEDIUM |

Note: institutional channels reach fewer total elders than the DTC funnel but reach them in aggregated, higher-contract-value units. See section 3.

### 1.4 Analyst TAM check (secondary only)

| Source | Figure | Scope | Read |
|--------|--------|-------|------|
| Laurie Orlov, Aging & Health Technology Watch, Market Overview 2024 | **$9.1B (2024)**, aging-in-place technology | All aging-in-place tech, not just monitoring | Our DTC SAM ($840M/yr) is ~9% of this broad category. Plausible |
| AARP + Consumer Technology Association (Jan 2025) | **$120B by 2030**, "aging technology" | Very broad (all agetech incl. mobility, hearing, telehealth) | Too broad to anchor on. Marketing-grade |
| Mordor Intelligence / Grand View | **$10.2-10.8B (2025-26)** medical alert / PERS market | Global PERS, the closest comparable | Our product is one entrant in a ~$10B global PERS market. $40-80M ARR SOM is a ~0.5-0.8% share. Credible |

The bottom-up and the PERS-specific analyst figure agree in order of magnitude. The broad "agetech" TAMs are not usable as a target and are cited only to show the concept does not contradict them.

---

## 2. COMPETITIVE LANDSCAPE

Full profiles. Register rows in section 9. Failures emphasized per brief.

### 2.1 Master table

| Company | What they sell | Buyer / channel | Price (list vs actual) | Raised / ownership | Status 2025-26 | Conf. |
|---------|---------------|-----------------|------------------------|--------------------|----------------|-------|
| **SafelyYou** | Ceiling camera + "Safety AI" fall detection/prevention, memory-care focus | B2B senior living / memory care operators | Per-bed monthly subscription (undisclosed); 15-bed minimum; install ~$200/bed | ~$100M+ total; $43M Series C Jan 2025 (Touring Capital) | Operating, scaling | HIGH status / LOW price |
| **Vayyar Care** | 60GHz mmWave radar, camera-free/wearable-free fall detection | DTC (Amazon), senior living, UK councils, care-software partners | List ~$250/device (~3/home) + $20/mo emergency calling; bulk undisclosed | Parent Vayyar Imaging ~$308M total ($108M Series E 2021, Koch) | Operating (product line) | HIGH price / MEDIUM attribution |
| **CarePredict** | "Tempo" AI wrist wearable + room beacons; activity, behavior, fall, location | Senior living + aging-in-place @Home | @Home kit ~$449.99 hardware + monthly subscription; facility undisclosed | ~$42-46M; $29M Series A-3 Jul 2023 | Operating; KamiCare partnership Nov 2025 | HIGH status / MEDIUM raise |
| **Sensi.ai** | Acoustic/audio AI "virtual care agent", no cameras/wearables, 100+ insights | B2B home care agencies | Custom B2B subscription by agency size (undisclosed) | ~$98M+; $45M Series C Oct 2025 (Qumra); $31M Series B 2024 (Insight) | Operating, high growth (~400% YoY claimed) | HIGH status / LOW price |
| **Cherry Home / Cherry Labs** | Wall camera + computer vision (skeletonized, local); falls, gait, inactivity | Home care agencies + families (DTC) | Historical list ~$1,600 (2-room) to $2,000 (6-room) + monitoring; current unknown | ~$6M total ($5.2M Dec 2018, GSR) | Dormant / low-traction; no funding or news since 2018-19 | MEDIUM status / LOW price |
| **Origin Wireless / Origin AI** | WiFi/RF "AI Sensing"; motion, presence, fall, breathing; 200+ patents | Licensing/OEM to carriers, ISPs, security (Verizon, Alarm.com) | Licensing/embedded (undisclosed) | ~$52M raised | **ACQUIRED by ADT for $170M cash, announced Feb 24 2026** | HIGH |
| **Emerald Innovations** | MIT (Katabi) spinout; contactless RF through-wall movement, breathing, HR, sleep, falls | Pharma (drug trials) + research | B2B/research contracts (undisclosed) | Bootstrapped / employee-owned; $1.1M grant 2023 | Operating, profitable, pharma-focused | HIGH status / MEDIUM raise |
| **Tellus (fka Tellus You Care)** | Bedroom radar, contactless HR/respiration/sleep/gait/falls | B2B eldercare; heavy Japan pilots | Undisclosed | Seed-stage only | ACQUIRED by AIP Healthcare ~Oct 2024 (terms undisclosed) | MEDIUM |
| **Lively / GreatCall** | Jitterbug phones, Lively Mobile PERS, Urgent Response | DTC + Best Buy retail; seniors + caregivers | Device from ~$79.99; plans from $14.99/mo; health/safety tiers layered | **Best Buy acquired for $800M, closed Oct 1 2018** (~900k subs) | Active as Lively from Best Buy Health; retained after Current Health divestiture | HIGH |
| **Medical Guardian** | PERS in-home + mobile + MGMove smartwatch | DTC online/phone | Monitoring from $27.95/mo; range to ~$46.95; fall detection +$10/mo; device $149.95-$199.95 | $100M growth (Water Street, 2020); acquired MobileHelp May 2024 | Active, growing via M&A | HIGH |
| **Bay Alarm Medical** | PERS (SOS Home, Micro, All-in-One, Smartwatch) | DTC online/phone | From $27.95/mo (landline) to ~$64.95; cellular $34.95/mo | Family-owned (Westphal); no outside funding | Active | HIGH |
| **Life Alert** | PERS ("I've fallen and I can't get up"), no fall detection | DTC, heavy TV/telemarketing | $49.95-$89.95/mo (well above ~$29 avg) + ~$197 setup; mandatory 36-month contract | Private; ownership/raise UNKNOWN | Active but reputationally strained (2,300+ FTC complaints 2020-25) | HIGH price / LOW ownership |
| **Apple Watch fall detection** | Consumer smartwatch wellness/safety feature (not monitored PERS) | Retail; mainstream consumers, auto-enabled 55+ | Hardware $249 (SE) to ~$799 (Ultra); **no monthly fee** | Apple Inc. (feature) | Active, expanding (satellite SOS) | HIGH |
| **Amazon Alexa Together** | Elder-monitoring subscription: caregiver activity feed, remote Alexa mgmt, 24/7 Urgent Response, 3rd-party fall detection | Amazon; adult-child caregivers | $19.99/mo or $199/yr, 6-mo free trial | Amazon (in-house) | **DISCONTINUED May 21 2025** (launched Dec 7 2021); emergency piece folded into Alexa Emergency Assist | HIGH |
| **Best Buy Health / Current Health** | Care-at-home / RPM platform + hospital-at-home | B2B enterprise sales to health systems | Enterprise/contract (undisclosed) | **Best Buy acquired Current Health for ~$400M, closed Nov 2 2021** | **DIVESTED late June 2025**, sold back to co-founder McGhee; preceded by $475M goodwill impairment + 161 layoffs | HIGH |

### 2.2 The failures, which are the instructive part

**Amazon Alexa Together (dead, May 2025). The most instructive failure in the set.**
A $19.99/mo subscription from the company with the lowest customer acquisition cost on earth (installed Alexa base, Prime relationship, zero-cost distribution) still could not sustain a bundled elder-monitoring product. Amazon unbundled it and kept only the one feature with genuine willingness to pay, professional emergency response, migrating it into the cheaper Alexa Emergency Assist and discarding the caregiver activity-monitoring layer entirely. Lesson: the caregiver "activity feed / dashboard" layer that this concept centers on is precisely the layer Amazon found people would not pay for. If the entity with the best distribution in the world could not make the monitoring-dashboard subscription work, a startup paying real CAC should not assume it can. This directly stress-tests the concept's core value proposition.

**Best Buy Health / Current Health (bought $400M 2021, written down $475M and divested 2025, under 4 years).**
Enterprise B2B care-at-home / RPM sold to health systems. Best Buy took a $475M goodwill impairment (business worth far less than paid), 161 layoffs, and sold it back to its founder. The enterprise-clinical market "did not scale as originally forecasted." Meanwhile Best Buy **kept** Lively, the consumer PERS subscription that fit its retail channel. Lesson: channel-fit dominates. The provider-side clinical sale is slow, complex, and did not scale even for a $40B retailer; the consumer subscription with retail distribution survived.

**Tellus You Care (soft landing ~2024) and Cherry Home (dormant since 2019).**
Two sensing startups that never cleared senior-living CAC and reimbursement hurdles on seed capital. Tellus pivoted to Japan (better demographics), then was quietly absorbed by AIP Healthcare. Cherry Home (camera-based in-home vision for seniors, the closest architectural analog to this concept's default) raised $6M in 2018-19 and has shown no funding, pricing, or product news since: effectively dead. Lesson: in-home camera vision for elders faces privacy resistance and family CAC that a lightly funded company cannot outrun. This is a direct warning to the concept's camera-in-a-bulb default (assumption A1/A3).

**Origin AI (exit, not failure, but instructive).** WiFi-sensing never became a standalone senior product; the durable value was the RF-sensing IP, monetized by embedding it in ADT's installed base ($170M, Feb 2026). Lesson: component-layer sensing tech monetizes better inside a distribution giant than sold direct. Relevant if this concept's real asset turns out to be an algorithm rather than a product.

**Synthesis:** The winners in this category are (a) simple monitored PERS with retail/DTC distribution (Lively, Medical Guardian, Bay Alarm), (b) B2B sensing sold per-bed into operators who already carry liability for falls (SafelyYou, Sensi.ai), and (c) IP licensors (Origin). The losers are consumer monitoring **dashboards** (Alexa Together) and enterprise clinical platforms bought by non-clinical parents (Current Health). The concept as framed (consumer dashboard + in-home camera) sits closest to the two failure archetypes.

---

## 3. CHANNEL ANALYSIS

Compared on CAC, sales cycle, contract size, and gross margin. Hard CAC and margin figures for this specific category are largely private; cells are marked with confidence and basis. Directional ranking is HIGH confidence even where individual cells are LOW.

| Channel | CAC | Sales cycle | Contract size | Gross margin | Verdict |
|---------|-----|-------------|---------------|--------------|---------|
| **DTC (consumer subscription)** | HIGH: $150-400+ blended (paid search/TV/affiliate). Generic subscription CAC avg ~$72 is a floor this category exceeds due to trust-heavy, considered purchase | Short (days-weeks) | Small: ~$420/yr sub + $200-400 hardware | MEDIUM: hardware-subsidized; PERS margins under commoditization pressure, ~40-60% blended vs 78% pure SaaS | Fast but CAC/churn-bound; the Alexa Together graveyard. LOW confidence this scales to venture size alone |
| **Medicare Advantage supplemental benefit (PMPM)** | LOW per-member once contracted; the sale is to the plan | Long (12-24 mo; annual bid cycle) | Large (PMPM x thousands of members) | HIGH if software-led | Attractive economics but **contracting in 2025** (UnitedHealthcare dropped Lifeline PERS as core benefit; only ~14.5% of plans ever offered PERS). Timing risk |
| **Home health / home care agencies** | MEDIUM (sell to ~11,500 agencies, fragmented) | Medium (3-9 mo) | Medium (per-client or per-agency SaaS) | HIGH (software/analytics margins) | Sensi.ai's proven lane. Agency carries the care relationship and some liability. Fragmentation is the tax |
| **Senior living / assisted living operators (per-bed)** | MEDIUM-LOW (concentrated: ~1,000 operators control most of 1.2M beds) | Medium-long (6-12 mo, pilot-gated) | Large (per-bed/mo x 100s of beds per deal) | HIGH (per-bed software) | SafelyYou's proven lane. Operator buys because it **owns fall liability**. Best margin+contract combination |
| **Health systems / ACOs** | HIGH (enterprise clinical sale) | Very long (12-24+ mo) | Large but slow | MEDIUM | Current Health's graveyard. Requires medical-device positioning + clinical evidence. Contradicts the wellness lane |
| **LTC insurers** | MEDIUM | Long (12-18 mo) | Medium-large | HIGH | Insurer funds monitoring to defer claims (delayed institutionalization). Small number of carriers; underdeveloped but rational buyer |
| **Hardware retail (Best Buy, Amazon)** | Shifts CAC to channel (slotting/margin share) | Medium to get on shelf | Small unit, high volume | LOW (retail margin share erodes it) | Distribution, not a buyer. Works for simple SKUs (Lively). Poor fit for install-heavy multi-node systems |

**Best channel by CAC-to-margin: senior living / assisted living operators, per-bed.** Concentrated buyer base (low CAC per bed), high gross margin on per-bed software, large multi-bed contracts, and the buyer has a hard financial reason to pay (it carries fall liability and insurance exposure). This is exactly where SafelyYou raised $100M+ and where the concept's fall-detection and long-lie-detection features have a buyer who is legally and financially motivated. Home care agencies (Sensi.ai's lane) are a close second. DTC and health-system/ACO are the two channels the failure record most strongly warns against.

This finding directly challenges founder assumption A7's implied DTC default and confirms its explicit warning: the money is in operators and payers, not the consumer.

---

## 4. REIMBURSEMENT

### 4.1 Code families and current payment

| Code | Covers | ~2025 national avg Medicare | Device requirement | Conf. |
|------|--------|----------------------------|--------------------|-------|
| **RPM 99453** | Device setup + patient education (once/device) | ~$19.73 | Must be FDA 201(h) device | HIGH code / MEDIUM $ |
| **RPM 99454** | Device supply + transmission; **≥16 days data / 30** | ~$43.03 | Must be FDA 201(h) device | HIGH / MEDIUM |
| **RPM 99457** | First 20 min/mo clinical management + 1 interactive contact | ~$47.87-51.77 | — | HIGH / MEDIUM |
| **RPM 99458** | Each additional 20 min/mo (add-on) | ~$38.49 | — | HIGH / MEDIUM |
| **RTM 98975/76/77** | Setup; respiratory device; musculoskeletal device (≥16 days/30) | ~$19 / ~$50 / ~$43 | Must be FDA 201(h) device | HIGH / MEDIUM |
| **RTM 98980/81** | First 20 min / additional 20 min management | ~$48 / ~$38 | — | HIGH / MEDIUM |
| **CCM 99490 / 99439** | Non-complex, first / additional 20 min; **≥2 chronic conditions** | ~$60.49 / ~$45.93 | No device required | HIGH / MEDIUM |
| **CCM 99487 / 99489** | Complex CCM, first 60 min / additional 30 min | ~$130 (LOW) / ~$70.52 | No device | MEDIUM/LOW |
| **PCM 99424 / 99426** | Physician / clinical-staff time, first 30 min; **exactly 1 complex chronic condition** | ~$88 / ~$68 | No device | MEDIUM |
| **PCM 99425 / 99427** | Each additional 30 min (add-on) | UNKNOWN / ~$48.45 | No device | LOW/MEDIUM |

2026 note: CMS finalized shorter-duration RPM/RTM codes effective 1/1/2026 (e.g. 99445 device supply for 2-15 days, priced ~$52; 99470 first 10 min management ~$26), lowering the data-day threshold. Source: CMS CY2026 PFS Final Rule (CMS-1832-F).

### 4.2 What a wellness-positioned product can and cannot bill. The central tension.

**Cannot bill RPM or RTM.** The logic chain is airtight from primary sources:
1. CMS requires the RPM/RTM monitoring device to meet the FDA definition of a "medical device" under **Section 201(h) of the FD&C Act** (established CY2019/2020 PFS policy).
2. The 21st Century Cures Act (Dec 2016, section 3060) amended the FD&C Act to **remove** general-wellness software "intended for maintaining or encouraging a healthy lifestyle **unrelated to the diagnosis, cure, mitigation, prevention, or treatment of a disease**" from the 201(h) device definition. FDA's own general-wellness guidance states such products are not regulated as devices.
3. Therefore a product that is, by design and by claim, a general-wellness product is **excluded from 201(h)** and cannot serve as the qualifying device for RPM (99453/99454) or RTM (98975-98977). Note: 201(h) status does not require FDA clearance, but it does require a disease-related intended use, which is exactly what the wellness positioning forbids.

**Cannot directly bill CCM or PCM either, though for a different reason.** CCM and PCM are time/service codes that pay a **clinician** for care-coordination time and require **no device**. A wellness product could be a workflow tool *supporting* a clinician's CCM/PCM delivery, but the payment goes to the clinician for documented time, not to the product vendor. There is no code that pays a non-device wellness product.

**The tension, stated plainly:** Reimbursement is the largest and most durable revenue pool in aging-in-place, and every device-paying code (RPM, RTM) is gated behind FDA medical-device status. The concept's settled strategic decision (framework section 2) is to be a general-wellness product, which is *defined by exclusion from* that device status. **The concept cannot simultaneously be a general-wellness product and bill RPM/RTM. This is the central strategic tension of the business.** The routes out are all costly: (a) build a separate cleared medical-device SKU for the reimbursed channel (adds regulatory cost, contradicts the lane), (b) partner with a clinician/RPM vendor who supplies the qualifying device and sell the wellness layer as adjacent software, or (c) forgo reimbursement entirely and live on DTC + operator per-bed + payer PMPM, none of which require device status. Option (c) is the only one consistent with the current positioning, and it removes the single largest revenue pool from the model.

---

## 5. PARTNERS

Grouped by function per Phase 7 item 5. Detailed vendor rows in section 9.

| Function | Candidate partners | Rationale | Conf. |
|----------|-------------------|-----------|-------|
| Camera / module ODMs | Chinese IP-camera module houses (Allwinner/Rockchip/SigmaStar-based), Western distribution for validated modules | Cost floor for vision node; detailed BOM in Phase 3 | MEDIUM |
| Contract manufacturers | Regional CMs for low-volume G3-G5; Asian CM at G6 | Standard hardware scaling path | LOW |
| Silicon vendors w/ startup programs | NVIDIA (Jetson / Inception), Ambarella, Hailo, ST (STM32N6) | Compute for pose/fall; validate against wellness lane in Phase 3-4 | MEDIUM |
| PERS monitoring call centers (buy, do not build) | Existing 24/7 monitoring centers (the infrastructure Lively/Medical Guardian/Bay Alarm rely on) | Framework/brief: do not build a call center. White-label the escalation layer | MEDIUM |
| Radar / contactless sensing | Vayyar (60GHz modules), TI IWR/xWR, Infineon | Bathroom-viable, no-image modality; addresses camera privacy objection (assumption A3) | MEDIUM |
| Wearable vendors | Only if raw-data access is real (assumption A4, see shared register) | Most vendors expose derived metrics only | LOW |
| Senior living operators (pilot hosts) | Large operators controlling concentrated bed counts | Best channel (section 3); pilot host + design partner | MEDIUM |
| Home care agencies (channel + pilot) | Large multi-site agencies (Sensi.ai's customer profile) | Second-best channel | MEDIUM |
| Academic gait labs (validation) | University gait/biomechanics labs with instrumented walkways | Required to substantiate gait metrics under FTC standards (framework section 2) | MEDIUM |
| RPM vendor (reimbursement bridge) | An FDA-device RPM platform vendor | The only compliant route to touch reimbursement without abandoning the wellness lane (section 4.2 option b) | LOW |

---

## 6. WILLINGNESS TO PAY AND CHURN

### 6.1 What families actually pay (DTC, published)

| Item | Value | Conf. | Source |
|------|-------|-------|--------|
| PERS / medical alert monthly, overall avg 2025 | ~$37/mo (band $25-50) | MEDIUM-HIGH | NCOA; SeniorLiving.org 2026 |
| In-home base unit | $20-40/mo | MEDIUM | NCOA / AgingInPlace |
| Mobile / GPS | $30-50/mo | MEDIUM | same |
| Fall detection add-on | +~$10/mo | MEDIUM | same |
| Equipment / activation one-time | $50-350 device; activation up to ~$200 | MEDIUM | SeniorLiving.org |
| Family caregiver total out-of-pocket (context) | ~$7,200/yr avg | HIGH | AARP/NAC Caregiving in the US 2025 |

The willingness-to-pay ceiling for the monitoring subscription is anchored hard at ~$25-50/mo by an entrenched PERS market. A new product priced above that band fights both the anchor and the incumbents' distribution.

### 6.2 Demand signal and churn

| Metric | Value | Conf. | Source |
|--------|-------|-------|--------|
| 65+ currently using PERS/medical alert | **9%, flat vs 2023** | MEDIUM | The Senior List 2026 Usage Report |
| Adult children who discussed PERS with parent | 26% | MEDIUM | same |
| Purchase intent among adult children | **fell 39% (2023) to 22% (2026)** | MEDIUM | same |
| 65+ reporting a fall since turning 65 | 44% | MEDIUM | same |
| **PERS-specific churn / retention** | **UNKNOWN** — no public figure; held in private filings | — | Open Question |
| Annual plans reduce churn vs monthly | ~51% reduction | LOW (general) | subscription benchmark, not PERS-specific |
| MA plans offering PERS as supplemental benefit | rose 1.2% (2017) to 14.5% (2019), **contracting 2025** | MEDIUM | ATI Advisory |

**Read:** Penetration is stuck at 9% and adult-child purchase intent is falling (39% to 22% in three years) despite 44% of elders having fallen. This is a market with real need but softening discretionary demand and a hard price anchor. It is a demand-softness signal, not a demand vacuum, and it argues against a DTC-led, premium-priced entry. Churn is the single most important number the model needs and it is not publicly available; this is a material open question, not a value to assume.

---

## Register Entries

Per framework section 9. To be appended by the register-maintaining process; reproduced here for the phase record. (This phase does not edit `research/registers/` directly per instruction.)

### 9.1 competitors.md (Product | Buyer | Price | Funding | Status | If dead, why)

| Company | Product | Buyer | Price | Funding/ownership | Status | If dead, why |
|---------|---------|-------|-------|-------------------|--------|--------------|
| SafelyYou | Ceiling camera fall-detection AI | Senior living operators | Per-bed sub (undisclosed) + ~$200/bed install | ~$100M+; $43M Series C 2025 | Operating | - |
| Vayyar Care | 60GHz radar fall detection | DTC + operators | ~$250 device + $20/mo | Parent ~$308M | Operating | - |
| CarePredict | AI wearable + beacons | Senior living + @Home | ~$449.99 kit + sub | ~$42-46M | Operating | - |
| Sensi.ai | Acoustic AI monitoring | Home care agencies | Custom B2B | ~$98M+ | Operating | - |
| Cherry Home | Camera CV monitoring | Agencies + families | ~$1,600-2,000 + sub (historical) | ~$6M | Dormant | No traction; camera privacy resistance + family CAC on seed capital |
| Origin AI | WiFi/RF sensing IP | OEM/licensing | Licensing (undisclosed) | ~$52M | Acquired by ADT $170M Feb 2026 | - (exit) |
| Emerald Innovations | Contactless RF health sensing | Pharma / research | B2B contract | Bootstrapped; $1.1M grant | Operating | - |
| Tellus You Care | Bedroom radar | Eldercare (Japan) | Undisclosed | Seed only | Acquired by AIP Healthcare ~2024 | Sub-scale; soft landing after failing to clear CAC/reimbursement on seed |
| Lively/GreatCall | Jitterbug + PERS | DTC + retail | Device $79.99+; $14.99/mo+ | Best Buy $800M 2018 | Active | - |
| Medical Guardian | PERS + smartwatch | DTC | $27.95-46.95/mo + device | $100M growth 2020 | Active | - |
| Bay Alarm Medical | PERS | DTC | $27.95-64.95/mo | Family-owned | Active | - |
| Life Alert | PERS | DTC/TV | $49.95-89.95/mo + $197 setup; 36-mo contract | Private, UNKNOWN | Active | - |
| Apple Watch | Fall detection wellness feature | Retail consumers | $249-799 hardware, no fee | Apple | Active | - |
| Amazon Alexa Together | Caregiver monitoring subscription | Adult-child caregivers | $19.99/mo or $199/yr | Amazon | **Dead May 21 2025** | Dashboard layer had no willingness-to-pay; only emergency response valued, folded into Emergency Assist |
| Best Buy Health / Current Health | RPM / care-at-home platform | Health systems | Enterprise (undisclosed) | Best Buy $400M 2021 | **Divested June 2025** | Enterprise-clinical did not scale; $475M impairment; channel mismatch with retailer parent |

### 9.2 sources.md (additions this phase)

| Source | Org | URL | Pub date | Used for | Credibility |
|--------|-----|-----|----------|----------|-------------|
| 2023 Profile of Older Americans | ACL | acl.gov/sites/default/files/Profile%20of%20OA/ACL_ProfileOlderAmericans2023_508.pdf | 2024 | 65+ living-alone count | HIGH (gov) |
| Living Arrangements Varied Across Age Groups | US Census | census.gov/library/stories/2024/05/living-arrangements.html | 2024-05 | Living-alone shares | HIGH |
| Caregiving in the US 2020 | AARP/NAC | aarp.org/pri/topics/ltss/family-caregiving/caregiving-in-the-united-states/ | 2020 | Long-distance caregiver share | HIGH |
| Caregiving in the US 2025 | AARP/NAC | aarp.org/press/releases/2025-07-24... | 2025-07 | Family OOP spend | HIGH |
| Market Overview: Technology for Aging 2024 | L. Orlov / Aging & Health Tech Watch | ageinplacetech.com/files/aip/Market%20Overview%202024%20Final%20January-2024.pdf | 2024-01 | Analyst TAM check | MEDIUM |
| Aging tech $120B by 2030 | AARP + CTA | aarp.org/press/releases/2025-1-8... | 2025-01 | Broad TAM (context only) | LOW-MEDIUM |
| PERS market report | Mordor Intelligence | mordorintelligence.com/industry-reports/medical-alert-system-personal-emergency-response-system-market | 2025-26 | PERS market size | MEDIUM |
| Medical Alert Systems Market | Grand View Research | grandviewresearch.com/industry-analysis/medical-alert-personal-emergency-response-system-pers-market | 2024-25 | PERS market size | MEDIUM |
| 2026 Medical Alert Device Usage Report | The Senior List | theseniorlist.com/research/medical-alert-device-consumer-usage-study/ | 2026 | Penetration, intent, churn context | MEDIUM |
| Medical alert cost | NCOA | ncoa.org/product-resources/medical-alert-systems/medical-alert-systems-cost/ | 2025 | DTC pricing | MEDIUM-HIGH |
| RPM CPT quick guide | Prevounce / OpenLoop | blog.prevounce.com/quick-guide-remote-patient-monitoring-rpm-cpt-codes-to-know | 2025 | RPM codes + 16-day rule | MEDIUM |
| Billing for RPM | HHS Telehealth | telehealth.hhs.gov/providers/best-practice-guides/telehealth-and-remote-patient-monitoring/billing-remote-patient | 2025 | RPM billing rules | HIGH (gov) |
| General Wellness: Policy for Low Risk Devices | FDA | fda.gov/regulatory-information/search-fda-guidance-documents/general-wellness-policy-low-risk-devices | rev. 2026-01 | 201(h) exclusion | HIGH (gov) |
| CY2026 PFS Final Rule (CMS-1832-F) | CMS | cms.gov/newsroom/fact-sheets/calendar-year-cy-2026-medicare-physician-fee-schedule-final-rule-cms-1832-f | 2025 | 2026 RPM/RTM codes | HIGH (gov) |
| CCM 2025 rates | SignalLamp / ChartSpan | signallamphealth.com/2025-medicare-cpt-code-reimbursements-for-chronic-care-management-ccm/ | 2025 | CCM payment | MEDIUM |
| PCM 2025 codes | ThoroughCare / RHIhub | thoroughcare.net/blog/2025-principal-care-management-pcm-cpt-codes-billing-and-reimbursements | 2025 | PCM payment | MEDIUM |
| CY2025 MA market trends | ATI Advisory | atiadvisory.com/resources/cy-2025-medicare-advantage-market-trends-first-look/ | 2024 | MA supplemental PERS trend | MEDIUM |
| Medicare Advantage 2024 Spotlight | KFF | kff.org/medicare/medicare-advantage-2024-spotlight-first-look/ | 2024 | MA plan counts | HIGH |
| Assisted living statistics | A Place for Mom / NCHS / NIC | aplaceformom.com/senior-living-data/articles/assisted-living-statistics | 2024 | Bed/community counts | MEDIUM-HIGH |
| Home Health Care FastStats | CDC NCHS | cdc.gov/nchs/fastats/home-health-care.htm | 2023 | HHA counts | HIGH (gov) |
| Best Buy / GreatCall $800M | Senior Housing News / SEC | seniorhousingnews.com/2018/08/15/... | 2018 | Acquisition | HIGH |
| Current Health $400M + divestiture | Forbes / Bloomberg / SEC 10-K | forbes.com/sites/saibala/2021/11/30/... ; bloomberg.com/news/articles/2025-06-24/... | 2021 / 2025 | Acquisition + wind-down | HIGH |
| Alexa Together launch + discontinuation | TechCrunch / caregiver sites | techcrunch.com/2021/12/07/... | 2021 / 2025 | Launch + fate | HIGH launch / MEDIUM date |
| SafelyYou $43M Series C | BusinessWire / SHN | businesswire.com/news/home/20250128706931/en/ | 2025-01 | Funding | HIGH |
| Sensi.ai $45M Series C | Sensi.ai / PRNewswire | sensi.ai/blog/sensi-ai-raises-45m-series-c... | 2025-10 | Funding | HIGH |
| Origin AI $170M ADT acquisition | ADT / GlobeNewswire | globenewswire.com/news-release/2026/02/24/... | 2026-02 | Acquisition | HIGH |

### 9.3 vendors.md (additions this phase)

| Vendor | Supplies | MOQ / startup-friendly | Published pricing | Conf. |
|--------|----------|------------------------|-------------------|-------|
| Vayyar | 60GHz mmWave radar modules | Product line, works with integrators | ~$250/device | MEDIUM |
| Texas Instruments | IWR/xWR radar | Distributor, yes | Distributor list | MEDIUM |
| Infineon | 60GHz radar | Distributor, yes | Distributor list | MEDIUM |
| NVIDIA | Jetson compute + Inception program | Startup program yes | Module (Phase 3) | MEDIUM |
| Ambarella / Hailo / ST | Vision SoC / accelerator / STM32N6 | Varies | Phase 3 | MEDIUM |
| PERS monitoring centers | White-label 24/7 escalation | Buy not build | UNKNOWN | LOW |
| University gait labs | Instrumented-walkway validation | Research agreements | UNKNOWN | MEDIUM |

### 9.4 funding.md (category deal evidence)

| Investor / event | Deal | Amount | Date | Thesis signal |
|------------------|------|--------|------|---------------|
| Touring Capital (+ Foundation, Founders Fund, Samsung Next, Qualcomm Ventures) | SafelyYou Series C | $43M | 2025-01 | Operator per-bed fall AI is fundable |
| Qumra Capital | Sensi.ai Series C | $45M | 2025-10 | Home care agency audio AI is fundable |
| Insight Partners | Sensi.ai Series B | $31M | 2024 | same |
| SV Health / Aspire | CarePredict Series A-3 | $29M | 2023-07 | Wearable senior monitoring |
| ADT | Origin AI acquisition | $170M | 2026-02 | Sensing IP monetizes via distribution giant |
| Best Buy | GreatCall / Lively | $800M | 2018 | Consumer PERS + retail channel wins |
| Best Buy | Current Health | $400M (impaired $475M, divested 2025) | 2021 | Enterprise clinical + retailer = failure |

---

## Open Questions

1. **PERS-specific churn / retention rate. UNKNOWN.** Not published; held in private filings. This is the single most material gap for the business case (Phase 8 LTV depends on it). Blocks a defensible LTV:CAC.
2. **Senior-living per-bed-per-month monitoring price. UNKNOWN.** SafelyYou, Securitas Foresite, Xandar Kardian all quote per-community, publish nothing. Requires direct RFQ. Blocks precise sizing of the best channel.
3. **Real DTC CAC for a premium multi-node monitoring product. UNKNOWN.** Generic subscription CAC ~$72 is a floor this considered, trust-heavy purchase exceeds; no category-specific figure found.
4. **Share of living-alone 65+ with a genuinely remote adult child. Estimated, not measured.** Funnel steps 2-4 rest on assumptions (0.80, 0.25, 0.60). A dedicated data pull (Census PUMS cross-tab of household + child proximity) would tighten the SAM.
5. **Per-benefit MA dollar spend on PERS / in-home monitoring. UNKNOWN.** ATI shows the trend (14.5% of plans, contracting) but no spend figure.
6. **Life Alert ownership and total raised. UNKNOWN.**
7. **Exact resale price of Current Health (2025 divestiture). Undisclosed.**

## Assumptions Made

| # | Assumption | Value | Impact if wrong |
|---|-----------|-------|-----------------|
| 1 | Share of living-alone 65+ with a living adult child | 0.80 | Scales SAM linearly. If 0.70, SAM population falls ~12% |
| 2 | Share whose nearest child is "remote" (proxy: 25% of caregivers are 20+ min away) | 0.25 | Largest single lever. If the true remote-child share is 0.15, SAM population drops to ~1.2M and DTC ceiling to ~$500M/yr |
| 3 | Share of remote-child households able/willing to fund $30-50/mo | 0.60 | If 0.40, SAM population ~1.3M |
| 4 | Blended annual subscription for sizing | $420/yr | Anchored to PERS actuals; if the product must price at the $37/mo band ($444) the figure is stable; a premium price above the anchor reduces penetration not price realized |
| 5 | Realistic mature DTC penetration of SAM | 5-10% | PERS is 9% and flat; a pricier product likely lower. Drives SOM |
| 6 | Institutional channels reach the ~1.0M senior-living residents and agency clients, distinct from the DTC funnel | count | Channel sizing, section 1.3 |

All four funnel multipliers (assumptions 1-3) are inherited-or-derived judgments, not measured cross-tabs. They are flagged per framework section 5.8.

## Confidence Summary

Overall confidence: **MEDIUM-HIGH on the strategic conclusions, MEDIUM on the SAM magnitude, HIGH on the competitive and reimbursement findings.**

- **Strongest (HIGH):** the competitive landscape and the failure post-mortems (all from primary announcements, SEC filings, and dated press); the reimbursement tension (airtight from FDA general-wellness guidance + CMS 201(h) requirement); the top-of-funnel living-alone count (ACL/Census); the channel ranking direction.
- **Medium:** the SAM dollar magnitude (rests on three assumed funnel multipliers, section Assumptions); DTC pricing band; MA supplemental-benefit trend.
- **Weakest (LOW / UNKNOWN):** PERS churn (unavailable, blocks LTV), per-bed institutional pricing (unavailable, blocks best-channel sizing), real category DTC CAC. These three gaps are the reason the phase cannot yet produce a defensible LTV:CAC, which is a Phase 8 dependency.

The kill-relevant conclusion is robust to the weak cells: even at the optimistic end of every assumption, DTC alone tops out at a low-hundreds-of-millions revenue ceiling, the two closest product analogs (Alexa Together dashboard, Cherry Home camera) are dead, and the largest revenue pool (reimbursement) is legally foreclosed by the wellness positioning. The channels that work (operator per-bed, agency) require abandoning the DTC/consumer-dashboard thesis that the concept currently centers on.
