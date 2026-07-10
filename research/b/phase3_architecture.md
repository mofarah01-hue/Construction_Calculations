# CONCEPT B, PHASE 3: PRODUCT AND TECHNICAL ARCHITECTURE

Governed by `00_framework.md`. Builds on and cites Phase 0 (`research/b/phase0_scope.md`, safety envelope and claims matrix), Phase 1 (`research/b/phase1_markers.md`, V1 shortlist and the two daily surfaces), Phase 2 (`research/b/phase2_data_inputs.md`, Model 1 lab ingest, self report confirmed over affect inference, content corpus split), and the shared files `shared_privacy_security.md`, `shared_llm_layer.md`, `shared_infra_cost.md`. Does not re research what those settled. All access dates 2026-07-10.

## Architecture thesis, stated first

Three decisions govern this build and every section serves them.

1. This is a **pure cloud SaaS application with a local first sensitive data tier**. There is no device, no raw sensor stream, and no cloud vision path (Phase 2, 2.1; `shared_infra_cost.md` section 2). The one architectural exception to cloud is that the highest risk reproductive fields are held client side encrypted, because the post Dobbs legal environment makes "what the company can be compelled to produce" a first order design input, not a compliance afterthought (`shared_privacy_security.md` section 6).
2. The product is **a rules engine that a language model narrates, not a language model that infers**. Every clinical, safety, and personalization decision is deterministic code. The model phrases outputs and answers grounded questions. It never decides what is true about the user. This is the direct consequence of the claims boundary (framework section 2; Phase 0) and the finding that affect inference from consumer physiology is not defensible (Phase 2, 2.3; assumption B4).
3. The **consent layer is the product's spine, not a setting**. The mother is the resource owner. Every element the partner sees is a scoped, revocable grant modeled on User Managed Access. Done well this is the differentiator no competitor serves (Phase 0, feature 7 and 10; Phase 1, 1H). Done badly it is a nonconsensual disclosure of one person's reproductive health data to another, which is both a lawsuit and a product women reject (`shared_privacy_security.md` section 5.3).

---

## 1. APPLICATION STACK

### 1.1 Client: cross platform, mobile first

| Decision | Choice | Rationale | Confidence |
|---|---|---|---|
| Platform priority | Mobile first, iOS and Android at parity, thin web companion for onboarding and account only | The daily loop (section 8) is a phone habit; the partner surface is a phone habit; labs and content are consumed on phone | HIGH |
| Framework | React Native (Expo) | Larger talent pool, mature native module ecosystem for HealthKit and Bluetooth, established HealthKit and Health Connect wrappers, faster hiring than Flutter for a healthtech MVP. Flutter is the alternative and wins only if a high fidelity custom UI is the priority, which this product does not need [RN-HEALTH, MEDIUM] | MEDIUM |
| Framework caveat | Neither framework is HIPAA relevant by itself; compliance lives in encryption, storage, transport, logging, and the backend (section 6) [RN-HEALTH, MEDIUM] | The framework choice is an engineering and hiring decision, not a compliance one | HIGH |
| Local secure storage | SQLCipher (AES 256 full database file encryption) with the per user, per device key held in iOS Keychain / Android Keystore | This is the client side encrypted tier for reproductive sensitive fields (section 6). Key generated at runtime with sufficient entropy, never leaves the secure element [SQLCIPHER, MEDIUM] | MEDIUM |

The single most important reason to pick the incumbent cross platform framework the team knows: the load bearing risk in this product is content, clinical review, and consent correctness, not UI. Spend the engineering budget there, not on a framework migration.

### 1.2 Backend

Per `shared_infra_cost.md` section 2, Concept B is a pure cloud SaaS backend with no vision path. The stack is deliberately boring so the novel risk budget goes to the rules engine, the consent layer, and the safety layer.

| Layer | Choice | Basis |
|---|---|---|
| Compute | Serverless containers (AWS Fargate) or edge workers (Cloudflare) for the API tier | Sourced unit prices in `shared_infra_cost.md` section 3; scales to the tiers there |
| API | TypeScript service, REST plus a thin GraphQL read layer for the two daily surfaces | Single language across client and server; hiring efficiency |
| Primary datastore | PostgreSQL (Aurora Serverless v2), one relational store, extended with `pgvector` for the retrieval corpus (section 2) | Avoids a second database system; pgvector is enough at this corpus size (section 2.3) |
| Time series | Same PostgreSQL for derived wearable scalars and self report logs; partition by user and date | Volumes are low (derived scalars, one daily brief), not raw waveforms; a dedicated TSDB is unjustified |
| Object storage | Cloudflare R2 (zero egress) or S3 for content assets and generated media | `shared_infra_cost.md` section 3 |
| Wearable ingest | HealthKit / Health Connect on device plus server side connectors to Oura, Whoop, Garmin (section 7) | Phase 2, 2.1 |
| Lab ingest | Health data aggregator (Model 1) returning FHIR R4 `Observation` / `DiagnosticReport` (section 6, Phase 2 2.2) | Phase 2 recommendation |

### 1.3 Data model

Five domains. The separation is a privacy and consent requirement, not only a schema convenience: the reproductive sensitive tier and the consent grant tier are isolated so that disclosure, retention, and deletion can be enforced per element.

| Domain | Contents | Store | Sensitivity tier |
|---|---|---|---|
| Identity and account | Mother account, partner account, auth, device keys, provider and crisis contacts | PostgreSQL | Standard |
| Gestational timeline | Due date or delivery date, gestational or postpartum day (the personalization clock), milestones ingested | PostgreSQL; **reproductive sensitive fields (pregnancy status, loss) held client side encrypted** | Elevated (section 6) |
| Measurement and self report | Derived wearable scalars, BP readings, daily mood and symptom logs, kick counts, weight, labs | PostgreSQL time series; labs as FHIR resources | Elevated |
| Consent grants | Per element scope grants from mother to partner, grant state, timestamps, revocation log | PostgreSQL, isolated `consent` schema, append only audit | Elevated (governs disclosure) |
| Content and retrieval corpus | Chunked, embedded clinical and educational corpus; citations | PostgreSQL + pgvector; shared, not per user | Non personal |

Modeling notes. Self report and measurement are stored as immutable, timestamped events (event sourced), which matches the framework's "self report is a journal" posture (framework section 2): the log is the asset and is never overwritten. The gestational clock (days since LMP or delivery) is the single most reused field in the system; it drives content selection, the postpartum warning window, and every rule threshold in section 3.

---

## 2. RETRIEVAL ARCHITECTURE FOR THE GROUNDED AI LAYER

The design rule is inherited verbatim from `shared_llm_layer.md` section 4: the interpretation layer must never assert a health fact from parametric memory. Retrieval binds every educational claim to a citable, substantiable source and converts the FTC substantiation question (framework section 2) into a content operations line item. This section specifies the mechanism.

### 2.1 Corpus

Composition is settled by Phase 2 (2.4). V1 grounds entirely on free public domain government content plus the product's own clinically reviewed original copy, carrying zero licensing cost. Licensed ACOG and AAP depth is a deliberate V2 investment.

| Corpus tier | Contents | License | Phase |
|---|---|---|---|
| V1 grounding (free) | CDC Hear Her warning signs, CDC Learn the Signs milestones, WHO/CDC growth charts, USDA MyPlate and Dietary Guidelines, NIH/ODS nutrient requirements, FDA pregnancy dietary advice | Public domain US government (Phase 2, 2.4) | V1 |
| V1 original | Product authored normalization and education copy, clinically reviewed by the retained OB-GYN (Phase 2, 2.4) | Owned | V1 |
| V2 licensed | ACOG clinical guidance, AAP Bright Futures and HealthyChildren depth | Licensed via CCC / AAP org license, quote based, UNKNOWN fee (Phase 2 Open Q4) | V2 |

Every chunk carries provenance metadata: source, publisher, publication or revision date, and a gestational or child age applicability range. Provenance is not optional; it is what makes a retrieved passage citable and what lets the rules layer (section 3) filter the corpus to the user's current stage before the model ever sees it.

### 2.2 Chunking, retrieval, citation, and corpus constraint

Standard 2026 production RAG stack: chunk and embed the corpus, store dense vectors in an ANN index alongside a lexical (BM25) index, retrieve hybrid top k at query time, rerank with a cross encoder, then condition the model on the surviving passages via a template with explicit citation slots [RAG-2026, MEDIUM].

| Stage | Specification | Rationale |
|---|---|---|
| Chunking | Structure aware, roughly 200 to 400 tokens per chunk, split on document headings not fixed windows, one clinical concept per chunk, provenance attached | Warning sign and milestone content is already list structured; concept level chunks keep citations atomic |
| Embedding | Off the shelf embedding model at ingest time; corpus is small and shared, so embedding is a one time batch cost, not per user | Corpus is thousands of chunks, not millions of documents |
| Vector store | `pgvector` in the existing PostgreSQL, HNSW index | At this corpus size (well under 1M vectors) a dedicated vector DB is unjustified; pgvector on the existing Postgres "costs almost nothing to add" and avoids a second system [VECTORDB-2026, MEDIUM] |
| Retrieval | Hybrid: dense ANN plus BM25, top k, pre filtered by the rules layer to the user's stage and topic | Lexical recall recovers exact clinical terms (drug names, analytes) that pure vector search misses |
| Rerank | Cross encoder rerank of the hybrid candidate set | Precision on the passage actually cited |
| Generation | Model receives only the reranked passages plus the user query in a template with numbered citation slots; instructed to answer only from provided passages and to cite each claim | Fluency with citation precision |
| **Corpus constraint (the enforced part)** | If retrieval returns no passage above a relevance threshold, the model is **not** asked to answer from parametric memory. It returns a fixed "I do not have vetted information on that; here is how to reach your provider" response. Ungrounded generation is disabled by the orchestration layer, not requested in the prompt | This is the substantiation guarantee: no citation, no health claim. It mirrors the safety layer's enforced posture (section 5): the deterministic wrapper, not the model's goodwill, holds the line |

The corpus constraint and the safety layer share one principle: the model is a presentation surface bounded by deterministic code on both ends. On the input end, the red flag classifier (section 5) can bypass the model entirely. On the output end, the retrieval gate refuses to let the model speak a health fact it cannot cite.

### 2.3 Cost per user per month, at each scale

Cross referenced from `shared_llm_layer.md` section 7 and `shared_infra_cost.md` sections 5 to 7. The retrieval layer adds three cost elements on top of base inference: a one time corpus embedding cost (amortized, negligible per user), a per query retrieval compute cost (pgvector query plus rerank, fractions of a cent), and the retrieved passage tokens that enlarge the model input. The passage tokens are already inside the `shared_llm_layer.md` 2,500 token input assumption. Model tier is the dominant lever; the rules first design (section 3) keeps the model on a cheap tier for the presentation majority.

| Cost element | Small (300 users) | Mid (5,000 users) | Large (50,000 users) | Source |
|---|---|---|---|---|
| Corpus embedding (one time, amortized) | Negligible per user | Negligible | Negligible | Corpus is shared fixed overhead, thousands of chunks |
| Vector store (`pgvector` on existing Aurora) | Inside DB overhead | Inside DB overhead | Inside DB overhead | No separate vector DB bill [VECTORDB-2026] |
| Retrieval compute + rerank per query | < $0.01 per user per month | < $0.01 | < $0.01 | Fargate + pgvector query, `shared_infra_cost.md` section 3 |
| Model inference (grounded turns), Haiku 4.5 tier | ~$0.50 | ~$0.50 | ~$0.50 to $1.00 | `shared_llm_layer.md` section 7; `shared_infra_cost.md` section 5 |
| Model inference if Sonnet 5 used on grounded turns | ~$1.00 to $1.50 | ~$1.00 to $1.50 | ~$1.00 to $1.50 | Same |
| **Grounded AI layer subtotal per user per month** | **~$0.50 to $1.50** | **~$0.50 to $1.50** | **~$0.50 to $1.50** | Inference dominates; retrieval overhead is immaterial |

Reading. The retrieval machinery itself is nearly free per user; the grounded AI layer cost is essentially the model inference cost, which `shared_llm_layer.md` and `shared_infra_cost.md` already bound at roughly $0.50 to $1.50 per user per month depending on tier, before prompt caching. Caching the stable system prompt and few shot prefix at 0.1x (Claude, HIGH) pulls the low end below $0.50. The full platform cost per user (this layer plus compute, storage, database, and amortized fixed overhead) is the `shared_infra_cost.md` section 7 total: $7 to $19 small, $1.50 to $4.50 mid, $1 to $3 large. The retrieval design does not move those bands; model tier selection does.

Recommendation: Claude Haiku 4.5 for the grounded presentation majority (safety aligned, cache and batch economics), reserving a higher tier only for the small share of genuinely complex multi signal questions, per `shared_llm_layer.md` section 8. Non interactive daily briefs run through the Batch API at 50 percent off.

---

## 3. PERSONALIZATION ENGINE: RULES LAYER VS MODEL LAYER

### 3.1 The split, stated as a principle

The personalization engine combines four inputs into a daily output: gestational or postpartum age (the clock), self report (mood, symptoms, logs), ingested lab values, and derived wearable scalars. **The combination is done by a deterministic rules engine. The language model does presentation, not inference.** The model is handed a fully resolved decision (which content, which trend, which nudge, which threshold) and writes it in plain, warm language. It is never asked what the data means.

This is not a stylistic preference. It is forced by three findings already established:

1. The claims boundary (framework section 2; Phase 0 claims matrix). Inference of a named condition from data is a claim; measurement plus reference and self report reflection are not. A rules engine that selects published reference ranges and reflects self report stays in the lane by construction. A model asked to interpret would wander out of it.
2. Affect inference from consumer physiology is not defensible for a new user (Phase 2, 2.3; B4). The engine therefore must not try; it trends self report and shows physiology as correlation, never as an affective verdict.
3. The safety layer (Phase 0 section 5; section 5 below) requires deterministic, testable, auditable behavior on the highest severity path. A probabilistic component cannot own a life safety decision.

### 3.2 What each layer owns

| Function | Layer | Why |
|---|---|---|
| Gestational / postpartum day computation | RULES | Arithmetic on due or delivery date. The clock every other rule reads |
| Content selection for the stage | RULES | Deterministic lookup: stage plus topic maps to corpus chunks (section 2) |
| Trend computation vs own baseline | RULES | Measurement math (deltas, streaks, moving averages) |
| Comparison vs published normative curve | RULES | Lookup against the stored reference curve (Phase 1 AWHS/IOM tables) |
| Threshold checks (BP threshold, low mood streak, weight band) | RULES | Compare value to the user's provider set or published threshold |
| Red flag symptom detection and escalation | RULES (enforced, section 5) | Life safety; deterministic and bypasses the model |
| Which nudge to surface today, and to whom | RULES | Priority ordering over the resolved facts and the consent grants |
| Lab display: value, the lab's own range, analyte explanation | RULES (value/range) + MODEL (plain language explanation from corpus) | Landmine 3: display, do not interpret (Phase 0) |
| Phrasing the daily brief, warmly and readably | MODEL | Presentation |
| Answering a grounded educational question | MODEL, corpus constrained (section 2) | Presentation with citation |
| Normalizing a feeling on a schedule | MODEL, from corpus | Education, not detection |

### 3.3 Daily output pipeline

The morning brief (Phase 1 section 4 copy) is assembled by this deterministic pipeline; the model is the last, bounded step.

1. Compute the clock (gestational or postpartum day).
2. Pull today's self report state, latest measurements, latest labs, latest derived scalars.
3. **Run the red flag classifier first (section 5).** If any input matches, short circuit to the escalation interstitial; the daily brief is not generated by the model on that path.
4. If clear, run the rules engine: select stage content, compute trends and threshold checks, rank candidate nudges, resolve which warning sign strip and which single "one thing that helps" to show.
5. Apply the consent filter (section 4) to produce the partner variant: render only granted elements.
6. Hand the fully resolved facts, selected corpus passages, and persona to the model, which writes the two surfaces. The model receives decisions, not raw data, and cannot introduce a fact not in the resolved set or the retrieved passages.

### 3.4 Justification of the "mostly rules" claim

The great majority of this product's logic is a rules engine because the great majority of its value is deterministic: a published warning sign list surfaced on the right postpartum day, a self reported mood streak reflected back, a lab value shown with its own range, a weight plotted against a public band, a BP reading compared to the user's own provider threshold. None of that requires or permits a model to infer anything. The model earns its place only where warmth, readability, and grounded question answering matter, which is presentation. This split is also the cheapest and the most auditable: deterministic rules carry unit tests and a fixed audit trail, and they keep the model on the cheap inference tier (section 2.3) because it is never asked to reason over raw signals.

---

## 4. DUAL USER ARCHITECTURE AND CONSENT

Inherits `shared_privacy_security.md` section 5.3 and Phase 1 section 1H. The mother and partner are separate accounts with separate views. Every element the partner sees is a disclosure the mother grants, granularly, and can revoke instantly and without friction. This section designs it.

### 4.1 Model: the mother is the resource owner (UMA style scoped grant)

The correct mental model is not a shared household record. It is **party to party authorization**: the mother is the resource owner and the partner is a requesting party who sees only what she has explicitly authorized. This is exactly the pattern User Managed Access (UMA 2.0), the Kantara federated authorization standard built on OAuth 2.0, was designed for, and its canonical example is a patient selectively sharing slices of health data with family and providers, view only, revocable, without ever sharing credentials [UMA-KANTARA, MEDIUM]. We do not need to run a full UMA authorization server in V1; we implement its grant semantics.

| Property | Specification | Basis |
|---|---|---|
| Separation | Two accounts, two data views. The partner has zero default visibility into the mother's data. Nothing is shared until granted | `shared_privacy_security.md` 5.3 |
| Grant object | A scoped authorization from mother to partner, per data element category (for example `mood`, `sleep`, `bp_trend`, `symptoms`, `appointments`, `weight`), stored in the isolated `consent` schema | UMA scope grant model [UMA-KANTARA] |
| Granularity | Per element category, defaulting to the finest practical grain, not one global "share with partner" toggle | Phase 1 1H; `shared_privacy_security.md` 5.3 |
| Directionality | One way grant, mother to partner. The partner cannot request elevation in a way that pressures her; requests, if allowed at all, are silent and deniable | Avoids relational coercion |
| Default closed | Mood, intrusive thoughts, mental health signals, and any reproductive status field default to **not shared** and carry the highest bar to share | `shared_privacy_security.md` 5.3; Phase 0 landmine 2 |
| Revocation | Instant, frictionless, one tap, effective immediately, with no notification to the partner that could create relational pressure. On revoke, the partner's next read of that element returns nothing | UMA "kill access instantly" property; micro consent [UMA-KANTARA] |
| Visible indicator | The mother always sees exactly what is currently shared; the partner always sees what he has access to and what he does not. No silent sharing in either direction | Phase 1 section 4B copy already renders this ("Shared: mood, BP trend. Not shared: journal") |
| Enforcement point | The consent filter runs server side in the personalization pipeline (section 3.3 step 5), before the partner brief is generated. The partner client never receives ungranted data over the wire, so revocation is not a UI hide, it is a data non delivery | Enforced, not cosmetic |

### 4.2 Why enforced server side, not filtered on the client

If the partner's app fetched the full record and hid ungranted fields in the UI, a revoked grant would still have shipped the data to his device, and a compromised or modified client would expose it. The consent filter therefore executes in the backend: the partner's brief is assembled from only the currently granted elements, and revocation takes effect at the data delivery boundary. This is the same enforcement discipline the framework demands of the "no raw video leaves the device" claim in Concept A (`shared_privacy_security.md` section 2): the promise must be true against every code path, not intended.

### 4.3 The partner is also a user with his own data

Paternal and non birthing partner perinatal depression has published prevalence around 8 to 10 percent, peaking 3 to 6 months postpartum (Phase 1 1H, PAT-DEP). The partner has his own daily mood check in, his own journal, and his own resources. His self report is his data, defaulting private from the mother by the same symmetric consent model. This is a differentiator no competitor serves and it costs nothing extra architecturally because the consent engine is already symmetric.

### 4.4 The line this draws

"Tell him she slept badly, help her today" is excellent product with consent and unacceptable surveillance without it, and the consent layer is the only thing separating them (`shared_privacy_security.md` section 5.3). Building it as a first class scoped grant system, defaulting closed on the sensitive categories, enforcing revocation at the data boundary, and showing both parties the share state, is what converts the concept's most attractive feature from a legal exposure into its strongest moat.

---

## 5. SAFETY ENFORCEMENT LAYER

Inherits and implements Phase 0 section 5. It is an enforced layer, not a prompt. The full design (the red flag list, the pre model classifier, the enforced behaviors, and the rationale for enforced over prompted) is specified in Phase 0 and is not repeated here. This section states how it sits in the Phase 3 architecture.

### 5.1 Placement: first in the pipeline, before the model

Every user input, both structured symptom logger entries and free text messages, passes through the deterministic red flag classifier before any generation occurs (Phase 0 section 5). In the daily pipeline it is step 3, ahead of both the rules engine and the model (section 3.3). On a match the pipeline short circuits: the model is bypassed, a fixed legally reviewed full screen direct to care interstitial is served, and the event is logged. The model is reached only for inputs that clear the classifier.

### 5.2 The enforced components in this build

| Component | Implementation in the Phase 3 stack | Source |
|---|---|---|
| Red flag classifier | Deterministic service, runs on device and server side, matching structured symptom fields and free text against the hard coded CDC Hear Her / AIM list (Phase 0 section 5). Unit tested, fixed response set | Phase 0 section 5 |
| Additional triggers | BP reading at or above the user's provider threshold (default 140/90); any positive self harm response on any mood scale | Phase 0 section 5; Phase 1 1B |
| Escalation interstitial | Fixed full screen response with provider contact, ER/911, and 988 for self harm. Never softened, never model generated | Phase 0 section 5 |
| Refusal guardrails | The orchestration layer refuses diagnosis, lab interpretation, safety adjudication of a symptom, and dose guidance in code, redirecting to the provider or escalation path. Refusal scope is code, not model discretion | Phase 0 section 5; framework section 2 |
| Corpus constraint | No health fact without a cited passage (section 2.2). The output side complement to the input side classifier | `shared_llm_layer.md` section 4 |
| Persistent disclaimer | Rendered on every session and every health relevant output by the client shell, not by the model | Phase 0 section 5 |
| Immutable logging | Every escalation and refusal written to an append only audit log for liability defense and as the leading indicator that the layer is firing as designed | Phase 0 section 5 |

### 5.3 Why this is architecture, not configuration

A prompt instruction is defeated by paraphrase, adversarial input, context window pressure, and ordinary model variance (Phase 0 section 5). The failure to escalate scenario is the highest severity, highest liability event in this product. It runs as deterministic code with unit tests and a fixed response set, on both client and server, and it cannot be jailbroken out of because the model is downstream of it and, on a red flag, is never invoked. The red flag path always wins over the conversational path.

---

## 6. DATA ARCHITECTURE AND PRIVACY

Inherits `shared_privacy_security.md` in full. This section addresses the reproductive health data legal risk as a first order architecture input, per Concept B brief item 6, and does not relitigate the encryption baselines or the HIPAA trigger analysis, which the shared file settled.

### 6.1 The governing facts (inherited)

| Fact | Consequence for this architecture | Source |
|---|---|---|
| HIPAA does not attach in the DTC channel; it attaches through the customer | In the base DTC case the product is governed by FTC HBNR plus state law, not HIPAA. A payer or provider channel converts it to a business associate | `shared_privacy_security.md` section 3 |
| Washington MHMDA is the binding constraint; no revenue threshold, broad "consumer health data" definition, opt in consent, deletion right, geofence ban | Design to MHMDA and clear BIPA and CUBI by a margin | `shared_privacy_security.md` section 4.3 |
| The HIPAA Reproductive Health Rule was vacated nationwide (Purl v. HHS, 2025-06-18) and not appealed | Reproductive data enjoys no federal attestation shield. State law and the architecture are the only protections | `shared_privacy_security.md` section 6.1 |
| Data on a company server is subpoenable | Minimize what exists on the server to minimize what can be compelled | `shared_privacy_security.md` section 6.2 |

### 6.2 Reproductive data architecture posture (first order)

The architecture is built so that the most sensitive reproductive fields are the hardest to compel, breach, or sell. This implements `shared_privacy_security.md` section 6.3 concretely.

| Principle | Implementation in this build | Basis |
|---|---|---|
| Collect the minimum | Do not collect precise location, ever. No geofencing near facilities (MHMDA ban). Persist reproductive status fields (pregnancy, loss) only as long as the daily loop requires | `shared_privacy_security.md` 6.3; 4.3 |
| Store the most sensitive fields on device | Pregnancy status and pregnancy loss fields held in the SQLCipher client side encrypted store (section 1.1), key in the secure element, so the server holds ciphertext or nothing. Client side encryption means the operator "genuinely cannot produce plaintext in response to a subpoena," only ciphertext [SQLCIPHER, MEDIUM] | `shared_privacy_security.md` 6.3 (prefer local first for the most sensitive fields) |
| Minimize retention | Short, defined retention windows on server side sensitive data; automatic deletion; honor user deletion instantly and completely, including backups | MHMDA deletion right; `shared_privacy_security.md` 6.3 |
| Do not sell or broker | No sale, no secondary sharing of reproductive data, full stop | MHMDA sale authorization; `shared_privacy_security.md` 6.3 |
| Encrypt to safe harbor | AES 256 at rest, TLS 1.3 in transit, per user data keys (`shared_privacy_security.md` section 1 baseline), so a compromised store is unusable | Breach safe harbor |
| Storage location | US region, single region for sensitive data, no cross border replication of reproductive fields; HIPAA eligible service configuration if the payer/provider channel is taken | `shared_privacy_security.md` sections 1, 3; `shared_infra_cost.md` Open Q5 (KMS/HIPAA premium) |
| Design for the adverse jurisdiction | Assume a user in a state that criminalizes abortion related conduct. The architecture must not create the evidence | `shared_privacy_security.md` 6.3 |

### 6.3 The consent grant store is part of the privacy architecture

The section 4 consent grants are themselves sensitive: the fact that a mother shared or revoked a mental health element is inferential data. The `consent` schema is held to the same elevated tier, append only for audit but minimized in what it retains, and never shared with the partner beyond the visible share state.

### 6.4 Claim posture

Every privacy claim maps to an enforced control and a code path; if it is not enforced, it is not said (`shared_privacy_security.md` section 7). Approved here: "You control exactly what your partner can see, and you can turn off sharing at any time" (section 4 enforces it); "Reproductive health information is stored on your device and minimized" (section 6.2 enforces it); "We do not sell your health data." Prohibited: any implied promise that data cannot be subpoenaed, and "fully HIPAA compliant" in the DTC channel.

---

## 7. WEARABLE INTEGRATION LAYER

Inherits Phase 2 (2.1) and `shared_wearable_data_access.md`. The load bearing finding: no V1 marker requires wearable data, and the product ships V1 with no wearable integration at all if required (Phase 2, 2.1). Wearables are a V2 physiological enhancement supplying derived scalars only.

### 7.1 Integration posture

| Layer | Choice | Basis |
|---|---|---|
| Primary | HealthKit (iOS) and Health Connect (Android) on device aggregation | They aggregate whatever band the user already owns at zero incremental cost and zero vendor lock in (Phase 2, 2.1). Unified RN packages exist [RN-HEALTH] |
| Secondary | Server side connectors to Oura, Whoop, Garmin, added on user demand | Direct connectors for users whose device is not surfaced through the platform stores (Phase 2, 2.1) |
| Data scope | Derived scalars only: RHR, derived HRV, nightly temperature deviation, spot/sleep SpO2, sleep summaries, steps. No raw PPG, no raw accelerometer, no continuous temperature or SpO2 | No consumer device exposes those under commercial terms (Phase 2, 2.1; `shared_wearable_data_access.md`) |
| Terms constraints | Whoop forbids redistribution/resale even with user consent; Oura requires the user to hold an active paid membership; Fitbit Web API sunsets Sept 2026, build on Google Health; Garmin requires partner approval | Phase 2, 2.1 table |
| Role in the product | Feeds V2 physiological trending and illness flagging only; shown as correlation (for example sleep and mood as two lines), never as an affective or diagnostic verdict | Phase 2, 2.3; framework section 2 |
| BP note | Blood pressure, the one clinical fidelity input in V1, comes from a validated home cuff (Bluetooth or manual entry), not a wristband, and is treated as its own connector, not part of the wearable layer | Phase 1 1B; Phase 2, 2.1 |

### 7.2 Consequence for the build

Because the wearable layer is optional and derived only, it is a set of adapters behind a common internal schema (one normalized "derived scalar" model), not a core dependency. A vendor revoking API access degrades a V2 feature; it does not end the company (contrast the wearable API dependency risk the framework flags for concepts that depend on raw access). The ingestion is a scheduled server side pull (hourly sync, `shared_infra_cost.md` section 4) plus HealthKit/Health Connect background delivery.

---

## 8. NOTIFICATION AND ENGAGEMENT ARCHITECTURE

Retention in this category is driven by a daily habit. The daily loop is the retention engine, and it is the same pipeline as section 3.3 delivered on a schedule.

### 8.1 The daily loop

| Element | Specification | Basis |
|---|---|---|
| Morning brief | One push per day, per user, delivering the two 30 second surfaces (mother, and partner if he has an account and grants). Assembled by the section 3.3 pipeline, generated as a non interactive Batch API job overnight at 50 percent inference cost | Phase 1 section 4 copy; `shared_llm_layer.md` section 7 |
| The single daily ask | One mood tap and, in the relevant window, one BP entry or kick count. One tap, low friction, "this is just for you" | Phase 1 section 4A; self report is the journal (framework section 2) |
| The always present strip | The warning sign strip is on every brief, taps to the full CDC list and a one tap call, and never depends on inference | Phase 1 section 4; section 5 |
| Stage change moments | Gestational week rollover and postpartum day milestones trigger a content unlock (the table stakes engagement spine, Phase 1 rank 8) | Phase 1 |
| Safety interrupts | A red flag or a BP threshold breach fires an immediate high priority notification and the escalation interstitial, outside the daily cadence | Section 5; Phase 0 |
| Partner nudge | The partner's "one thing that helps today," rendered only from granted elements | Section 4; Phase 1 4B |
| Postpartum full year cadence | The daily mood ask and warning sign strip continue across the full first year, not stopping at six weeks, because that is the real onset and mortality window competitors miss (Phase 1 rank 2, PPD-ONSET, MMRC-3619) | Phase 1 |

### 8.2 Delivery stack

Push via FCM (Android) and APNs (iOS); SMS via a provider (Twilio class) reserved for safety escalations where push may be missed; email for account and weekly summary only. Volume dependent, costed in `shared_infra_cost.md` section 6 fixed overhead. Notification scheduling is server side, timezone aware, and quiet hours aware, with the hard exception that safety interrupts ignore quiet hours.

### 8.3 The retention logic, and the churn reality it must respect

The daily loop is what makes the product a habit rather than a reference app. Two design consequences follow from the business reality (framework B6, the pregnancy churn cliff, to be modeled in Phase 5). First, the engagement spine must not be pregnancy only: the postpartum full year and the infant/early childhood layers are what extend the subscriber life past the roughly ten month pregnancy window, so the notification architecture is built from day one to carry a user across the delivery transition without a re onboarding. Second, the strongest retention hook is also the highest value feature: an exhausted postpartum person who has been shown, every morning, the warning signs no one else is watching for, has a daily reason to open that a week by week fetal size comparison does not provide after delivery. The daily loop is therefore anchored on the safety and mood surfaces, not on the content novelty that decays at birth.

---

## Register Entries

Per framework section 9. Register files are not edited by this phase; entries are staged for the register keeper.

### Sources (stage into `research/registers/sources.md`)

| ID | Source | Org | URL | Pub/accessed | Used for | Credibility |
|---|---|---|---|---|---|---|
| RAG-2026 | RAG Architecture Guide 2026; RAG in 2026 practical blueprint | jobsbyculture; dev.to (Khaitan) | https://jobsbyculture.com/blog/rag-architecture-guide-2026 ; https://dev.to/suraj_khaitan_f893c243958/-rag-in-2026-a-practical-blueprint-for-retrieval-augmented-generation-16pp | 2026-07-10 | Chunk/embed, hybrid ANN+BM25, cross encoder rerank, citation slots, corpus constraint | MEDIUM (secondary) |
| VECTORDB-2026 | pgvector vs Pinecone vs Qdrant vs Weaviate 2026; Do you need a dedicated vector DB | selfhost.dev; kalviumlabs; groovyweb | https://selfhost.dev/blog/pgvector-vs-pinecone/ ; https://www.kalviumlabs.ai/blog/vector-databases-compared-pgvector-pinecone-qdrant-weaviate/ | 2026-07-10 | pgvector sufficient under ~1M vectors; adds ~nothing to existing Postgres; dedicated DB cost multiple | MEDIUM (secondary) |
| UMA-KANTARA | User-Managed Access (UMA 2.0) Grant for OAuth 2.0; UMA overview | Kantara Initiative; SSOJet; Wikipedia | https://docs.kantarainitiative.org/uma/wg/rec-oauth-uma-grant-2.0.html ; https://en.wikipedia.org/wiki/User-Managed_Access | 2026-07-10 | Party-to-party scoped grant model; patient health data sharing example; instant revocation, micro consent | MEDIUM (standard + secondary) |
| RN-HEALTH | React Native vs Flutter for healthcare apps 2026; HIPAA compliance guide | Taction; 42works; themomentum | https://www.tactionsoft.com/react-native-vs-flutter-healthcare/ ; https://42works.net/how-developers-can-achieve-hipaa-compliance-in-flutter-and-react-native-apps-in-2026/ | 2026-07-10 | RN mature HealthKit/Bluetooth ecosystem; neither framework HIPAA compliant alone; team expertise governs | MEDIUM (secondary) |
| SQLCIPHER | SQLite/SQLCipher secure storage; client-side encryption and compelled disclosure | sqliteforum; NowSecure; opensecurityarchitecture | https://www.sqliteforum.com/p/sqlite-encryption-and-secure-storage ; https://books.nowsecure.com/secure-mobile-development/en/sensitive-data/implement-secure-data-storage.html | 2026-07-10 | AES-256 SQLite file encryption, per user/device key in Keychain/Keystore; operator cannot produce plaintext under subpoena | MEDIUM (secondary/technical) |

### OSS (stage into `research/registers/oss.md`)

| Name | Source | SPDX license | Commercial | Does | Confidence |
|---|---|---|---|---|---|
| pgvector | github.com/pgvector/pgvector | `PostgreSQL` (permissive; verify from license file before adoption) | Yes | Vector similarity search inside PostgreSQL; HNSW index for the RAG corpus | MEDIUM (license not read from file; Open Question) |
| SQLCipher (community edition) | github.com/sqlcipher/sqlcipher | `BSD-3-Clause` (community edition; verify from license file) | Yes (community edition) | AES-256 full-database-file encryption for the client side sensitive tier | MEDIUM (license not read from file; Open Question) |
| React Native | github.com/facebook/react-native | `MIT` | Yes | Cross platform mobile client | MEDIUM (license not read from file) |

Edge/RAG models (`Qwen3` `Apache-2.0`, `Phi-4-mini` `MIT`, `llama.cpp` `MIT`, `Ollama` `MIT`) and their license caveats are already recorded in `shared_llm_layer.md` and are not re-adopted here; V1 grounded generation runs on the cloud API tier (section 2.3), so an edge model is not a V1 dependency for Concept B.

### Vendors (stage into `research/registers/vendors.md`)

No new vendors beyond those in Phase 2 (health data aggregators for Model 1 lab ingest; wearable APIs; ACOG/AAP content licensors) and the shared infra vendors in `shared_infra_cost.md` (AWS, Cloudflare, Anthropic). Push/SMS providers (FCM, APNs, Twilio class) are inherited from `shared_infra_cost.md` section 6 as estimates, not quotes.

---

## Open Questions

1. **pgvector and SQLCipher license text not read from the license file.** Framework section 9 requires reading the license file. Both are widely used permissive licenses (`PostgreSQL` and `BSD-3-Clause` community edition respectively) per secondary sources, but the files were not directly read. Close before adoption. SQLCipher also has a commercial edition; confirm which edition and license applies.
2. **Exact per user aggregator ingest cost (Model 1).** Inherited UNKNOWN from Phase 2 Open Q1; it lands in the section 1.2 lab ingest line and the Phase 6 business case, not resolved here.
3. **HIPAA eligible service premium and KMS cost** if the payer/provider channel is taken (`shared_infra_cost.md` Open Q5). Not modeled; would raise the section 2.3 and section 6.2 cost bands in the covered channel.
4. **Whether a full UMA authorization server is warranted at scale**, or whether the in application scoped grant implementation (section 4.1) suffices through mid tier. V1 implements UMA grant semantics without running a standalone UMA AS; revisit if a provider or employer channel demands federated sharing.
5. **Cross platform framework final selection (React Native vs Flutter)** is a team expertise decision (section 1.1); the recommendation is RN but the governing factor is which the engineering team ships fastest, resolved at hiring in Phase 4.
6. **Structured lab return rate** (FHIR `Observation` vs C-CDA/PDF), inherited from Phase 2 Open Q2, determines how often the lab display renders cleanly vs degrades to Model 3 quality; a data quality input to section 1.3.
7. **Reproductive field retention window precision.** Section 6.2 mandates short defined windows and client side storage of the most sensitive fields; the exact window (and which fields are client side only vs server minimized) needs legal review against the launch state footprint before implementation.

## Assumptions Made

1. **Pure cloud SaaS with a client side encrypted sensitive tier** is the correct topology. Inherited from `shared_infra_cost.md` section 2 (Concept B has no vision path) and `shared_privacy_security.md` section 6.3 (prefer local first for the most sensitive reproductive fields). Impact if wrong: if regulators or a payer channel force all data server side, the subpoena minimization posture in section 6.2 weakens and the compliance surface expands.
2. **Model tier is Claude Haiku 4.5 for the presentation majority.** A founder-facing selection consistent with `shared_llm_layer.md` section 8 and the rules-first design; a higher tier raises the section 2.3 band toward $1.50 per user per month. Impact: inference cost, not architecture.
3. **The corpus is small enough (well under 1M vectors) that pgvector on the existing Postgres is sufficient** and no dedicated vector database is needed. Consistent with the free public domain V1 corpus (Phase 2, 2.4). Impact if wrong: at a much larger licensed corpus a dedicated vector store adds a modest fixed cost (VECTORDB-2026), not an architectural change.
4. **UMA grant semantics can be implemented in-application in V1** without a standalone UMA authorization server. Impact if wrong (a federated channel needs true UMA): additional identity engineering in a later phase; the grant model and enforcement point do not change.
5. **The rules engine owns all clinical, safety, and personalization inference; the model only presents.** Load bearing, inherited from framework section 2, Phase 0, and Phase 2 2.3 (affect inference not defensible). Impact if wrong: any drift toward model inference reopens the claims boundary and the substantiation exposure the whole design exists to avoid.
6. **The daily loop and full-year postpartum cadence are the retention engine.** A product design assumption consistent with Phase 1's strategic center; the churn economics that justify the postpartum and early childhood extension are quantified in Phase 5, not here.

## Confidence Summary

Overall confidence HIGH on the architectural decisions, which are dictated by prior phases rather than newly researched: the rules-vs-model split (framework section 2, Phase 0, Phase 2 2.3), the pure-cloud-plus-local-sensitive-tier topology (`shared_infra_cost.md`, `shared_privacy_security.md`), the consent-as-resource-owner model (`shared_privacy_security.md` 5.3), the enforced safety layer (Phase 0 section 5), and the optional derived-only wearable layer (Phase 2 2.1). These rest on settled prior findings and are robust.

HIGH on the retrieval mechanism being standard 2026 production practice (RAG-2026) and on pgvector being sufficient at this corpus size (VECTORDB-2026). HIGH that the grounded AI layer cost is dominated by model inference and bounded by the shared cost files at roughly $0.50 to $1.50 per user per month, with retrieval overhead immaterial.

MEDIUM on the specific technology picks that are team- or fee-dependent: the React Native vs Flutter choice is a hiring decision (RN-HEALTH), and the SQLCipher/pgvector licenses were not read from the license file (Open Q1). MEDIUM on whether in-application UMA grant semantics suffice long term versus a full authorization server (Open Q4).

The weakest and most consequential open item is the reproductive-field retention and client-side-storage boundary (Open Q7): the posture is HIGH confidence (minimize, encrypt client side, do not create the evidence) but the exact field-by-field implementation must pass legal review against the launch-state footprint before it ships, because in this data category the architecture is the primary legal protection, HIPAA having been removed by the Purl v. HHS vacatur (`shared_privacy_security.md` section 6.1).
