# shared_wearable_data_access.md
## Consumer Wearable Raw Sensor Data Access Under Commercial Terms

Governed by `00_framework.md`. Serves Concept A assumption A4 and Concept B assumption B2, and Concept B Phase 2.1. Scope is narrow and deliberate: establish, skeptically, what **raw** sensor data a **commercial** product can lawfully ingest and act on, versus what is only vendor derived output. All access dates 2026-07-10.

---

## 0. Definitions used in this file

The concept briefs ask for four raw signals plus HRV. Precision matters, because vendors market a "temperature" or "SpO2" field that is a once nightly derived scalar, not a stream.

| Signal | What "raw" means here | What vendors usually ship instead |
|--------|-----------------------|-----------------------------------|
| Raw PPG | Optical waveform, per channel (green, red, IR), sampled at 25 Hz or higher | A derived heart rate integer, updated every few seconds to minutes |
| Raw accelerometer | 3 axis waveform at 25 Hz or higher | Step counts, activity minutes |
| Continuous skin temperature | A temperature stream through the day | A single overnight deviation from personal baseline |
| Continuous SpO2 | A blood oxygen stream | A spot reading, or one sleep averaged value per night |
| HRV | Beat to beat interval series (raw) or a computed daily scalar (derived) | A single daily rmssd or SDNN value |

Two structurally different access paths exist, and the distinction decides everything downstream:

- **Cloud data broker API.** You pull vendor computed metrics from the vendor cloud after the fact. Oura, Whoop, Fitbit and Google, Garmin Health API, Withings Public API. These almost never expose raw waveforms.
- **On device SDK.** Your code runs on the watch or streams over BLE and reads the sensor directly. Apple SensorKit and CoreMotion, Samsung Privileged Health SDK, Polar BLE SDK, Withings Advanced Research API, Garmin Health SDK. This is where raw data lives, and it is uniformly gated by approval, contract, or research only restriction.

---

## 1. Raw signal availability matrix

Y means obtainable by a commercial product under stated terms. N means not obtainable commercially. R means the signal exists but is locked to ethics board approved research only. Contract means obtainable only under a negotiated partner or research contract.

| Device / platform | Access path | Raw PPG | Raw accel | Cont. skin temp | Cont. SpO2 | HRV | Confidence |
|-------------------|-------------|:-------:|:---------:|:---------------:|:----------:|:---:|:----------:|
| Apple Watch (HealthKit) | On device, cloud free | N | N (see CoreMotion) | N (nightly only) | N (spot, HW disabled on many US units) | Derived (SDNN) | HIGH |
| Apple Watch (CoreMotion) | On device | N | **Y** | N | N | N | HIGH |
| Apple Watch (SensorKit) | On device, research entitlement | R | R | R | N | R | HIGH |
| Oura Ring | Cloud API v2 | N | N | N (nightly deviation) | N (sleep average) | Derived | HIGH |
| Whoop | Cloud API v2 | N | N | N (one value per cycle) | N (one value per cycle) | Derived (rmssd) | HIGH |
| Garmin | Health API (cloud) | N | N | N | N (pulse ox spot) | Derived | HIGH |
| Garmin | Health SDK (on device, licensed) | N | **Y (licensed)** | N | N | Derived | MEDIUM |
| Fitbit / Google | Web API and Google Health API | N | N | N (nightly) | N (nightly) | Derived | HIGH |
| Samsung Galaxy Watch4+ | Privileged Health SDK (on device, partner) | **Y (partner)** | **Y (partner)** | UNKNOWN | N (derivable from raw red/IR) | Derivable | MEDIUM |
| Withings | Public Health Data API | N | N | N | N (spot) | Derived | HIGH |
| Withings | Advanced Research API (contract) | **Y (contract)** | **Y (contract)** | UNKNOWN | UNKNOWN | Derived | MEDIUM |
| Polar (Verity Sense, H10, OH1) | Polar BLE SDK (on device, BLE) | **Y** (Verity Sense) | **Y** | N (no temp sensor) | N (no SpO2 sensor) | Raw RR/PPI | HIGH |
| Empatica EmbracePlus (research grade) | Empatica platform / API (contract) | **Y** | **Y** | **Y** | N (no SpO2) | Raw PPG derivable | MEDIUM |
| Movesense (white label sensor) | Open SDK, own firmware | HR+ variant only | **Y** | N | N | Raw ECG/RR | MEDIUM |
| Contract manufactured band (MAX86141 / AFE4900) | Own firmware, full control | **Y** | **Y** | **Y** | **Y** (AFE4900) | Raw | HIGH |

The single most important read of this table: **no mainstream consumer cloud API exposes any raw waveform.** Raw PPG and raw accelerometer from a consumer device exist only through on device SDKs that are partner gated (Samsung), open but limited to prosumer chest and arm straps (Polar), or contracted research grade (Withings Advanced Research, Empatica). Continuous skin temperature and continuous SpO2 are not obtainable from any mainstream consumer platform under commercial terms at all.

---

## 2. Terms, cost, rate limits, and the governing clause

| Vendor | Commercial use permitted | Redistribution / resale | Cost to developer | Rate limit | Governing clause or doc | Conf. |
|--------|--------------------------|-------------------------|-------------------|------------|--------------------------|-------|
| Apple HealthKit | Yes for App Store apps; may not use health data for advertising, data mining, or sale | Prohibited by App Store Review Guidelines and HealthKit terms | Free (Apple Developer Program 99 USD/yr) | None (on device); data latency: HR seconds, other types batched up to ~30 min | Apple Developer docs, App Store Review Guideline 5.1.3 / HealthKit usage terms | HIGH |
| Apple SensorKit | **No.** Research only | Prohibited | Free, entitlement per study | n/a | "intended only for ethics board approved health and wellness research ... will not be available for general purpose and commercial apps"; entitlement `com.apple.developer.sensorkit.reader.allow` reviewed per study | HIGH |
| Oura | Yes above 10 users only after app approval; Gen3+ user must hold active Oura Membership | API docs restrict raw data; standard partner terms | Free API; end user needs paid Membership | 5000 requests per 5 minute window; per token and per application layers | Oura API v2 docs, cloud.ouraring.com/v2/docs; "10 user limit" approval gate | HIGH |
| Whoop | Yes above 10 members only after app approval | **Explicitly prohibited even with user consent** | Free API | 100/min and 10000/day default; header `X-RateLimit-Limit 100;window=60, 10000;window=86400`; increases by request to apisupport@whoop.com | WHOOP API Terms of Use: may not "sell, rent, lease, redistribute, or syndicate" API access; may not "market, sell, license or lease data ... to any third party, even if an End User consents"; no sublicensing | HIGH |
| Garmin Health API | Yes, partner approval required | Governed by Garmin Connect Developer Program Agreement | Reported one time 5,000 USD administrative fee for production Health API (secondary source, unverified); Health SDK commercial use requires license fee or device MOQ | Not published; negotiated | Garmin Connect Developer Program Agreement; Health SDK Q&A "commercial use requires either a license fee or device minimum order quantity" | MEDIUM (fee LOW) |
| Fitbit / Google | Case by case for third party intraday; commercial rarely granted; Web API sunsets Sept 2026 | Standard platform terms | Free API | Fitbit 150 req/hr/user historically; Google Health API 5 sec HR default, intraday no longer tier gated | Fitbit Application Design guide: intraday for third parties "granted on a case by case basis"; Google Health API docs | HIGH |
| Samsung Privileged Health SDK | Yes, but only after Samsung Partner Program approval (restricted) | Governed by partner agreement | Cost UNKNOWN; access is application and approval based | Not applicable (on device streaming) | Samsung Privileged Health SDK docs: raw PPG (green, IR, red) and ACCELEROMETER_CONTINUOUS at 25 Hz; "restricted partner program"; Galaxy Watch4 and later | MEDIUM |
| Withings Public API | Yes | Standard | Free tier plus paid API plans | Not published in detail | Withings Developer docs, API plans | MEDIUM |
| Withings Advanced Research API | Contract only | Contract | UNKNOWN; contracted partners | Not published | Withings docs: "access to raw data is a special feature available only for contracted partners"; 3 axis accel 25 Hz default up to 100 Hz, PPG 3 LED or 1 LED | MEDIUM |
| Polar BLE SDK | **Yes, private and commercial** | Permitted under SDK license with copyright/notice retention | Free SDK; device purchase only | None (BLE streaming) | polar-ble-sdk README: "allowed to use the SDK for ... private as well as for commercial use ... in compliance with the license terms" (Polar_SDK_License.txt) | HIGH |
| Empatica EmbracePlus | Enterprise/research contract | Contract | Device plus platform subscription; pricing UNKNOWN (sales quote); E4 predecessor historically ~1,700 USD plus subscription | n/a | Empatica Health Monitoring Platform terms; EmbracePlus records continuous raw PPG, EDA, skin temperature, accelerometry | MEDIUM |
| Movesense | Yes; open SDK, white label available | You own the firmware and data | Dev kits purchasable; unit and white label pricing on request (sales@movesense.com); exact price UNKNOWN | n/a | Movesense product pages: "open APIs ... full access to the sensor raw data"; white label on production line | MEDIUM |
| CM band on MAX86141 / AFE4900 | Unrestricted, you own everything | You own everything | Silicon: MAX86141 8.88 USD at single unit Digi-Key, lower at volume; AFE4900 listed at Digi-Key (unit price UNKNOWN). Real cost is firmware, algorithm, and certification NRE | n/a | Component datasheets (Analog Devices MAX86141, TI AFE4900); Digi-Key listings | HIGH (silicon), LOW (system NRE) |

Notes on staleness. All developer documentation pages were accessed 2026-07-10 and are living documents; treated as current. The Empatica E4 datasheet (2014) is stale and the E4 is retired, superseded by EmbracePlus. The HIT Consultant piece on Samsung partner program expansion (Jan 2024) is older than 18 months and is flagged stale, but the substantive claims are corroborated by live Samsung developer documentation.

---

## 3. Per vendor findings, the parts that decide design

**Apple.** Two truths that are constantly conflated. HealthKit is commercial and gives you no raw waveform: heart rate as an integer, HRV as SDNN, wrist temperature as a single overnight sleeping baseline deviation, blood oxygen as a spot sample. CoreMotion, separately, does give a commercial app the raw 3 axis accelerometer on device. SensorKit does expose raw PPG and raw accelerometer, but Apple states plainly it "cannot be used to develop a commercial product" and gates it behind a per study IRB entitlement. Net: from Apple, a commercial product gets raw accelerometer and nothing else raw. SpO2 is further compromised because Apple disabled the blood oxygen feature on Apple Watch units sold in the US after the Masimo import ban.

**Oura, Whoop, Fitbit and Google, Garmin Health API.** These are the four the concept briefs implicitly assume, and all four are cloud data brokers that expose derived scalars only. Whoop is the most restrictive on paper: the API Terms of Use forbid selling, redistributing, or syndicating the data, and forbid marketing or licensing the data to any third party "even if an End User consents." That clause alone means a Whoop backed product cannot resell or pool the data, and depends entirely on a revocable API grant. Garmin is the most open of the four for movement data, but only through the separately licensed Health SDK and only for accelerometer, at a cost that is negotiated, not published.

**Samsung.** The one genuine outlier among mainstream consumer smartwatches. The Privileged Health SDK runs a Wear OS app on Galaxy Watch4 and later and reads raw PPG (green, IR, red channels) and continuous raw accelerometer at 25 Hz on device. It requires acceptance into the Samsung Partner Program, which is a restricted, application based gate, and the cost is not published. This is the only consumer smartwatch path to raw PPG under commercial terms, subject to that approval.

**Withings.** Bifurcated. The Public API is derived only. The Advanced Research API does expose raw PPG and raw accelerometer (25 Hz default, up to 100 Hz), but Withings states this is "available only for contracted partners." Commercially reachable, but only through a negotiated contract with pricing we could not obtain.

**Polar.** The cleanest commercially permissive raw path from an off the shelf device. The open Polar BLE SDK streams raw PPG (Verity Sense), raw accelerometer (25 to 200 Hz), raw ECG (H10, 130 Hz, microvolts), and beat to beat PPI over BLE, and the license text explicitly permits commercial use. The catch for these concepts: Polar's raw capable devices are chest straps and an optical arm band, not an all day wrist wearable, and they carry no skin temperature or SpO2 sensor. Excellent for a validation rig or a bench prototype, wrong form factor for a consumer daily wear product.

**Empatica.** Research and clinical grade. EmbracePlus streams continuous raw PPG, EDA, skin temperature, and accelerometry through Empatica's platform under an enterprise or research contract. It is the only wrist device evaluated that delivers continuous skin temperature as a genuine stream. It carries no SpO2. It is a research instrument, priced and supported as one, not a consumer product.

**Research grade category.** Empatica EmbracePlus, Movesense, Shimmer3, ActiGraph, Mbient MetaMotion. All give full raw access because you buy the hardware and the SDK. Commercial use is permitted. Cost signals: per unit in the low hundreds to roughly 2,000 USD, plus platform fees, exact figures on quote. These solve the data question and fail the product question: they are not consumer wearables and cannot be shipped as one.

**White label and contract manufacture.** Movesense offers an open SDK with full raw access and production line white labeling with your firmware, but its raw PPG is limited to the HR+ variant; its strength is raw IMU and ECG. The unconstrained path is a contract manufactured band built on a PPG analog front end you control: the Analog Devices MAX86141 (raw multi channel PPG, 8.88 USD single unit at Digi-Key, materially lower at volume) or the TI AFE4900 (combined ECG and PPG with SpO2 capability). Owning the firmware means owning all four raw signals with zero contractual restriction. The cost migrates entirely from license terms to NRE: firmware, signal processing, biometric algorithm development and validation, and certification. That NRE is large and lands at G3 through G5 in the framework cost model.

---

## 4. Explicit conclusion, per the four signals the briefs demand

Question, restated from Concept B Phase 2.1: can we obtain raw PPG, raw accelerometer, continuous skin temperature, and continuous SpO2, from any consumer device, under terms that permit a commercial product to ingest and act on them.

| Signal | Obtainable from a consumer device commercially? | Where, and the catch |
|--------|--------------------------------------------------|----------------------|
| Raw PPG | Yes, narrowly | Samsung Privileged Health SDK (partner approval, on device, cost unknown); Polar BLE SDK (free, but chest/arm strap form factor); Withings Advanced Research API (contract). **Not** from Oura, Whoop, Fitbit/Google, Garmin Health API, or Apple commercial apps |
| Raw accelerometer | Yes | Apple CoreMotion (on device, free), Samsung Privileged SDK, Polar BLE SDK, Withings Research API, Garmin Health SDK (licensed) |
| Continuous skin temperature | **No** from any mainstream consumer device | Every consumer wrist vendor ships a nightly derived deviation, not a stream. A true continuous stream requires research grade (Empatica EmbracePlus) or a band you build. Samsung and Withings continuous capability is UNKNOWN and must be verified |
| Continuous SpO2 | **No** from any consumer device | Every consumer vendor ships spot or sleep averaged SpO2. Apple's is hardware disabled on many US units. A continuous stream requires a CM band on a suitable AFE (TI AFE4900) or a research device |

**The verdict.** No single consumer device delivers all four raw signals under commercial terms. Raw PPG and raw accelerometer are obtainable from a narrow, approval or contract gated set. Continuous skin temperature and continuous SpO2 are not obtainable from any mainstream consumer wearable commercially, period. The closest consumer path is the Samsung Galaxy Watch via the Privileged Health SDK, which yields raw PPG and raw accelerometer on device, but its continuous skin temperature exposure is unverified and it does not provide continuous SpO2. Any design that hard requires all four raw streams cannot rest on a consumer wearable and must move to a fallback.

### Fallbacks, ranked by product realism, with cost signals

| Rank | Fallback | Delivers | Cost signal | Confidence |
|------|----------|----------|-------------|------------|
| 1 | Samsung Galaxy Watch + Privileged Health SDK | Raw PPG, raw accel (consumer form factor, mass market) | Free device to consumer; partner program cost UNKNOWN | MEDIUM |
| 2 | Contract manufactured band on MAX86141 / AFE4900 | All four raw signals, unrestricted commercially | Silicon ~9 USD/unit at low volume, lower at scale; large firmware/algorithm/cert NRE at G3 to G5 | HIGH (silicon), LOW (NRE) |
| 3 | Empatica EmbracePlus (research grade) | Raw PPG, raw accel, continuous skin temp (no SpO2) | Device plus platform subscription; pricing on quote, UNKNOWN | MEDIUM |
| 4 | Withings Advanced Research API (contract) | Raw PPG, raw accel via existing consumer hardware | Contract pricing UNKNOWN | MEDIUM |
| 5 | Polar BLE SDK (Verity Sense / H10) | Raw PPG, raw accel, raw ECG for a validation rig | Free SDK; device retail UNKNOWN, low tens to ~100 USD range unverified | HIGH (terms), LOW (price) |
| 6 | Contactless substitute (Concept A only) | HR, respiration, HRV via seat pad or bed mat ballistocardiography; no wearable needed | Covered in Concept A Phase 2 and Phase 3; not a wearable path | n/a here |

For Concept B specifically, the practical read is that the product should be architected on **derived metrics plus daily self report**, because that is what every commercially licensable consumer wearable actually provides, and self report is cheap, accurate, and defensible (framework section 2, and assumption B4). Raw physiology should be treated as a research and validation input, not a shipping dependency, unless the company commits to a Samsung partner track or its own contract manufactured band.

---

## Register Entries

Per framework section 9. These are proposed entries for the registers. The register files themselves are not edited by this phase.

### Sources (for `sources.md`)

| Title | Org | URL | Accessed | Published | Used for | Credibility |
|-------|-----|-----|----------|-----------|----------|-------------|
| Samsung Privileged Health SDK | Samsung | https://developer.samsung.com/health/privileged | 2026-07-10 | living | Raw PPG/accel partner access, 25 Hz | HIGH primary |
| Samsung Privileged Health SDK FAQ | Samsung | https://developer.samsung.com/health/privileged/faq.html | 2026-07-10 | living | Partner program gate | HIGH primary |
| Polar BLE SDK README | Polar | https://github.com/polarofficial/polar-ble-sdk/blob/master/README.md | 2026-07-10 | living | Commercial license, raw streams | HIGH primary |
| Polar H10 device guide | Polar | https://github.com/polarofficial/polar-ble-sdk/blob/master/documentation/products/PolarH10.md | 2026-07-10 | living | ECG 130 Hz, accel rates | HIGH primary |
| WHOOP API Terms of Use | Whoop | https://developer.whoop.com/api-terms-of-use/ | 2026-07-10 | living | Redistribution prohibition clause | HIGH primary |
| WHOOP API rate limiting | Whoop | https://developer.whoop.com/docs/developing/rate-limiting/ | 2026-07-10 | living | 100/min, 10000/day | HIGH primary |
| Oura API v2 docs | Oura | https://cloud.ouraring.com/v2/docs | 2026-07-10 | living | Derived only, rate limit, approval gate | HIGH primary |
| Apple SensorKit entitlement | Apple | https://developer.apple.com/documentation/bundleresources/entitlements/com.apple.developer.sensorkit.reader.allow | 2026-07-10 | living | Research only entitlement | HIGH primary |
| Apple SensorKit photoplethysmogram | Apple | https://developer.apple.com/documentation/sensorkit/srsensor/photoplethysmogram | 2026-07-10 | living | Raw PPG exists in SensorKit | HIGH primary |
| SensorKit research proposal guidance | ResearchAndCare | https://www.researchandcare.org/media/SensorKit-research-proposal.pdf | 2026-07-10 | undated | "not available for commercial apps" | MEDIUM secondary |
| Garmin Health API overview | Garmin | https://developer.garmin.com/gc-developer-program/health-api/ | 2026-07-10 | living | Cloud derived data | HIGH primary |
| Garmin Health SDK Q&A | Garmin | https://developer.garmin.com/health-sdk/questions-answers/ | 2026-07-10 | living | License fee or MOQ, accel stream | HIGH primary |
| Garmin Connect Developer Program Agreement | Garmin | https://developerportal.garmin.com/sites/default/files/Garmin%20Connect%20Developer%20Program%20Agreement.pdf | 2026-07-10 | living | Commercial terms | HIGH primary |
| Fitbit application design guide | Fitbit/Google | https://dev.fitbit.com/build/reference/web-api/developer-guide/application-design/ | 2026-07-10 | living | Intraday case by case gate | HIGH primary |
| Google Health API about | Google | https://developers.google.com/health/about | 2026-07-10 | living | Web API sunset, 5 sec HR | HIGH primary |
| Withings raw data doc | Withings | https://developer.withings.com/developer-guide/v3/integration-guide/public-health-data-api/data-api/raw-data/ | 2026-07-10 | living | Raw only for contracted partners | HIGH primary |
| Withings Advanced Research API | Withings | https://developer.withings.com/developer-guide/v3/withings-solutions/research-apis/ | 2026-07-10 | living | Raw PPG/accel specs | HIGH primary |
| Empatica EmbracePlus / raw data | Empatica | https://www.empatica.com/rawdata/ | 2026-07-10 | living | Continuous raw PPG/EDA/temp/accel | MEDIUM primary |
| Movesense Flash product page | Movesense | https://www.movesense.com/product/movesense-flash/ | 2026-07-10 | living | Open raw access, white label | MEDIUM primary |
| MAX86141 datasheet | Analog Devices | https://www.analog.com/media/en/technical-documentation/data-sheets/max86140-max86141.pdf | 2026-07-10 | living | Raw multichannel PPG AFE | HIGH primary |
| MAX86141 Digi-Key listing | Digi-Key | https://www.digikey.com/en/products/detail/analog-devices-inc-maxim-integrated/MAX86141ENP-T/7804058 | 2026-07-10 | living | 8.88 USD single unit price | HIGH primary |
| AFE4900 product page | Texas Instruments | https://www.ti.com/product/AFE4900 | 2026-07-10 | living | Combined ECG/PPG/SpO2 AFE | HIGH primary |
| Samsung Privileged SDK partner expansion | HIT Consultant | https://hitconsultant.net/2024/01/08/samsung-expands-its-privileged-health-sdk-partner-program/ | 2026-07-10 | 2024-01-08 | Partner program context | MEDIUM secondary, STALE |
| Garmin API developer guide (fee figure) | TechDepot blog | https://techdepot.blog/garmin-api-access-guide | 2026-07-10 | undated | Reported 5,000 USD fee | LOW secondary, UNVERIFIED |

### Vendors (for `vendors.md`)

| Vendor | Supplies | MOQ | Works with startups | Published pricing | Contact path | Conf. |
|--------|----------|-----|---------------------|-------------------|--------------|-------|
| Apple | HealthKit/CoreMotion/SensorKit APIs | None | Yes (App Store) | 99 USD/yr program | developer.apple.com | HIGH |
| Oura | Derived metrics cloud API | None | Yes, approval to scale | Free API, user pays Membership | cloud.ouraring.com | HIGH |
| Whoop | Derived metrics cloud API | None | Yes, approval to scale | Free API | apisupport@whoop.com | HIGH |
| Garmin | Health API + Health SDK | Possible device MOQ | Yes, via Health team | Fee/MOQ negotiated; 5,000 USD reported (unverified) | developer.garmin.com | MEDIUM |
| Fitbit / Google | Cloud API (migrating to Google Health API) | None | Limited for commercial intraday | Free API | dev.fitbit.com | HIGH |
| Samsung | Privileged Health SDK (raw PPG/accel) | Partner approval | Selective partner program | UNKNOWN | developer.samsung.com/health/privileged | MEDIUM |
| Withings | Public + Advanced Research API (raw contract) | Contract | Yes, B2B/RPM | UNKNOWN for research API | developer.withings.com | MEDIUM |
| Polar | BLE SDK, raw PPG/accel/ECG straps | Device only | Yes, open SDK | Free SDK; device retail UNKNOWN | polar.com/en/developers | HIGH |
| Empatica | EmbracePlus research grade raw platform | Contract | Research/enterprise | UNKNOWN (quote) | empatica.com | MEDIUM |
| Movesense | White label raw sensor + open SDK | Volume for white label | Yes | Dev kits purchasable; volume UNKNOWN | sales@movesense.com | MEDIUM |
| Analog Devices (Maxim) | MAX86141 PPG AFE for CM band | Distributor stock | Yes | 8.88 USD single unit Digi-Key | digikey.com / analog.com | HIGH |
| Texas Instruments | AFE4900 ECG+PPG+SpO2 AFE for CM band | Distributor stock | Yes | Digi-Key listed, unit price UNKNOWN | ti.com | HIGH |

### Rejected / deprioritized (with reason)

| Item | Reason rejected or deprioritized |
|------|----------------------------------|
| Apple SensorKit as a data source | Research only; Apple prohibits use to develop a commercial product |
| Oura, Whoop, Fitbit/Google, Garmin Health API for raw signals | Cloud brokers, derived scalars only, no raw waveform of any kind |
| Whoop as a resellable data backbone | Terms forbid selling/redistributing data even with user consent; revocable dependency |
| Polar as the shipping consumer wearable | Correct terms, wrong form factor (chest/arm strap), no skin temp or SpO2 sensor |
| Empatica EmbracePlus as a consumer product | Research/clinical instrument, not shippable as a consumer daily wear; no SpO2 |
| Fitbit Web API (new builds) | Sunsets September 2026; build against Google Health API instead |

---

## Open Questions

1. Samsung Privileged Health SDK commercial cost and approval bar. UNKNOWN. The partner program gate and any fee are not published. This blocks costing the single most attractive consumer raw data path. Requires direct contact with Samsung.
2. Samsung and Withings continuous skin temperature. UNKNOWN whether either exposes skin temperature as a continuous stream versus a nightly value. Blocks any marker that needs a daytime temperature trajectory.
3. Withings Advanced Research API pricing and whether "research" contract terms permit a commercial consumer product. UNKNOWN.
4. Empatica EmbracePlus current unit and platform pricing. UNKNOWN. The ~1,700 USD figure is for the retired E4 and is inference, not a current quote.
5. Movesense per unit and white label volume pricing. UNKNOWN; sales quote only.
6. Polar Verity Sense and H10 current retail price. UNKNOWN; not verified from a primary distributor page. Flagged rather than guessed.
7. Garmin production Health API 5,000 USD fee. LOW confidence, single secondary source. Not verified against the Garmin agreement PDF text. Treat as unverified.
8. Apple blood oxygen availability. The feature is disabled on many US Apple Watch units after the Masimo import dispute; the exact current status of any software reenablement is UNKNOWN and time sensitive.
9. Google Health API commercial redistribution terms for intraday data. Not fully read against the developer terms; MEDIUM confidence that raw waveforms remain unavailable.

## Assumptions Made

1. "Raw" is defined as a sampled waveform (PPG or accelerometer) or a beat to beat interval series, not a vendor computed scalar. If a downstream reader means something looser by "raw," several N cells become Y. Impact if wrong: overstates scarcity.
2. Continuous skin temperature and continuous SpO2 mean an intraday stream, not a nightly or spot value. This is the strict reading the concept briefs imply. Impact if wrong: understates availability.
3. On device SDK access (CoreMotion, Polar BLE, Samsung Privileged, Garmin Health SDK) is treated as commercially usable data even though no cloud endpoint is involved. This is correct for a product that runs its own companion app. Impact if wrong: none, this is standard.
4. The CM band silicon cost is a component price, not a system cost. The dominant cost is firmware, algorithm, validation, and certification NRE, which this file flags but does not quantify (that belongs in the concept hardware and dev plan phases).
5. Developer documentation accessed today reflects current terms. Living pages can change without notice; the Fitbit sunset and Apple SpO2 situations both show these terms move.

## Confidence Summary

Overall confidence HIGH on the central finding: no consumer cloud API exposes raw waveforms, and no consumer device delivers all four raw signals commercially. This is corroborated across multiple primary developer docs and is unlikely to be wrong.

Strongest sub findings (HIGH): Whoop redistribution prohibition; Oura and Whoop rate limits; Apple SensorKit research only restriction; Polar BLE SDK commercial permission and raw streams; Samsung Privileged SDK raw PPG and accelerometer capability; MAX86141 pricing.

Weakest sub findings (LOW to MEDIUM): all pricing that is contract or quote based (Samsung partner cost, Withings Research API, Empatica, Movesense, Garmin fee); whether Samsung or Withings expose continuous skin temperature; Polar and research device retail prices. Every one of these is listed under Open Questions and none is invented. The pricing gaps do not change the structural conclusion; they only constrain the cost modeling of the fallbacks.
