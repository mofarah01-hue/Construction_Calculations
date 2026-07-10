# shared_privacy_security.md
## Shared Research: Privacy, Security, and Data Architecture

Governed by `00_framework.md` (sections 5, 6, 8). Serves Concept A (Elder Home Monitoring) and Concept B (Pregnancy and Parenting Companion). Both products are positioned as general wellness, not medical devices (framework section 2). This file establishes the privacy and security baselines both concepts inherit. Concept specific work lives in `research/a/phase5_privacy.md` and the Concept B data architecture phase.

Legal landscape note: US health data privacy law moved materially in 2024 and 2025. Two 2024 era anchors (the HIPAA Security Rule NPRM and the HIPAA Reproductive Health Rule) have since changed status. Both are flagged inline. Verify status again before any G4 partner or payer legal review.

---

## 1. ENCRYPTION BASELINES

### 1.1 Regulatory floor vs engineering baseline

Two different questions. The regulatory floor is what law requires. The engineering baseline is what a breach forensics report, a payer security questionnaire, and a SOC 2 auditor will expect regardless of whether HIPAA formally attaches. Build to the engineering baseline. It is higher, it is cheap, and it removes the "was encryption reasonable and appropriate" argument entirely.

### 1.2 What HIPAA actually says (when it applies)

| Control | Citation | Status under current rule | Confidence |
|---|---|---|---|
| Encryption/decryption of ePHI at rest | 45 CFR 164.312(a)(2)(iv), under Access Control | Addressable, not Required | HIGH |
| Encryption of ePHI in transit | 45 CFR 164.312(e)(2)(ii), under Transmission Security | Addressable, not Required | HIGH |

"Addressable" is not "optional." It requires the entity to assess whether the safeguard is reasonable and appropriate, implement it if so, or document why not and deploy an equivalent alternative. Source: eCFR, 45 CFR 164.312 (current); HIPAA Journal, "HIPAA Encryption Requirements," updated 2026. For any product handling a person's home video, gait, or reproductive signals, "not reasonable to encrypt" is not a defensible position. Treat both as mandatory.

Proposed change, not yet law: the HHS OCR Notice of Proposed Rulemaking published in the Federal Register on 2025-01-06 would eliminate the addressable/required distinction and make encryption of ePHI at rest and in transit mandatory using "prevailing cryptographic standards," plus mandatory MFA, network segmentation, and anti malware. Comment period closed 2025-03-07. As of mid 2026 no final rule has issued; OCR is still processing roughly 4,700 comments and the targeted spring 2026 window passed with nothing published. Source: HHS.gov Security Rule NPRM fact sheet (2025-01); HIPAA Journal, "HIPAA Security Rule Update Postponed" (2026). Confidence HIGH that it is still proposed. Plan as if mandatory encryption is the near term direction of travel.

### 1.3 Engineering baseline (build to this regardless of HIPAA status)

| Layer | Baseline | Rationale | Confidence |
|---|---|---|---|
| Data at rest | AES 256 (FIPS 197 / NIST validated), full disk plus application level envelope encryption for the sensitive fields | NIST validated AES is the recognized standard cited across HIPAA guidance and payer questionnaires | HIGH |
| Data in transit | TLS 1.3 preferred, TLS 1.2 floor, no downgrade, HSTS, certificate pinning on device to cloud links | TLS 1.2/1.3 is the recognized in transit standard | HIGH |
| Key management | HSM or cloud KMS, envelope encryption, per tenant or per user data keys, documented rotation, keys never on the edge device in plaintext | Limits blast radius of a single device compromise | MEDIUM |
| On device storage (camera or phone) | Encrypted storage tied to secure element, secure boot, signed firmware, signed OTA | A bedroom camera and a pregnancy phone are high value targets. See section 2 | MEDIUM |
| Breach safe harbor | Encrypt to NIST standards so lost or stolen data is "unsecured" no longer, removing breach notification exposure | HHS and FTC breach rules both key notification obligations to whether data was rendered unusable/unreadable via encryption | HIGH |

Cost posture: encryption at these levels is a design decision, not a material recurring cost line. It does not move the per user per month economics in `shared_infra_cost.md`. The cost is in key management operations and secure boot provisioning on hardware, which lands as NRE at G1 to G2 and a small per unit provisioning cost at G5. Quantify in the concept phases.

---

## 2. EDGE VS CLOUD INFERENCE: PRIVACY TRADEOFF

The framework (section 8) states the position bluntly: "we only send metadata, not video" is a claim the architecture must enforce, not intend. Edge inference is the primary mechanism that makes that claim true.

| Dimension | Edge / on device inference | Cloud inference | Verdict for these products |
|---|---|---|---|
| Data minimization | Raw video, raw audio, raw PPG never leave the device; only derived metrics, scores, or events transit | Raw sensitive data leaves the home and is retained on third party infrastructure | Edge. Data that is never transmitted cannot be subpoenaed, breached in the cloud, or sold |
| Compliance surface | Keeping raw capture on device shrinks the surface for HIPAA, BIPA, MHMDA, CCPA | Every hop and store is in scope, expands BAA and vendor diligence obligations | Edge materially reduces scope |
| Breach exposure | A breach reaches one home's device, not a central corpus | A cloud breach can expose the entire user base at once | Edge |
| Latency for safety events | Fall detection and red flag escalation run locally, no round trip | Network dependent, fails when connectivity drops | Edge for the safety path |
| Attack surface at the edge | Requires secure boot, signed firmware, secure enclave, continual OTA patching, or the device itself becomes the weak point | Centralized patching, mature cloud security tooling | Cloud is easier to secure operationally; edge is easier to justify legally |
| Model capability | Constrained by thermal and cost envelope of the device (framework assumption A2 flags this) | Frontier model capability, unconstrained | Cloud for heavy language and reasoning |

Recommended posture for both concepts: tiered/hybrid architecture. Sensitive raw modality processing (video for gait and fall, audio, raw wearable streams) runs on device; only derived, non reconstructable features and events transit to cloud. Heavy language interpretation runs in the cloud on features already stripped of raw identifiers. This is consistent with the tiered pattern that production AI teams have converged on and with the LLM layer split in `shared_llm_layer.md`. Confidence MEDIUM (architecture recommendation; final split depends on Concept A sensor decision and Concept B LLM cost work).

Enforcement, not intent: the "no raw video leaves the device" claim must be provable against every code path. Concept A phase 5 item 2 already scopes this (debug, OTA, crash dumps, remote support). A crash dump that ships a video frame breaks the claim and the marketing built on it. Source basis: Edge AI privacy and data minimization literature (Fora Soft, 2026; Medium/Goldshtein, 2026; ResearchGate preprint "Privacy Preserving AI Inference in Edge Systems," 2026). These are secondary/technical sources, not primary law; used only for the architecture tradeoff framing, not for any legal claim.

---

## 3. WHAT TRIGGERS HIPAA, AND WHEN A BAA IS REQUIRED

### 3.1 The load bearing fact

HIPAA does not attach because a product touches health data. It attaches because of who the customer is. HIPAA regulates covered entities and their business associates. A direct to consumer wellness product sold to the resident, the caregiver, or the mother is neither, and HIPAA does not apply to it, no matter how sensitive the data. The same product sold through or on behalf of a covered entity pulls the product in as a business associate, and a BAA becomes mandatory. The trigger is the channel, not the data.

### 3.2 The definitions

| Term | Definition | Citation | Confidence |
|---|---|---|---|
| Covered entity | A health plan, a health care clearinghouse, or a health care provider who transmits health information electronically in connection with a HIPAA covered transaction | 45 CFR 160.103; HHS.gov "Covered Entities and Business Associates" | HIGH |
| Business associate | A person or entity that creates, receives, maintains, or transmits PHI on behalf of a covered entity for a regulated function (for example data analysis, processing, quality assurance) | 45 CFR 160.103; HHS.gov "Business Associates" | HIGH |
| Neither | An entity meeting neither definition is not subject to the HIPAA Rules | HHS.gov guidance | HIGH |

### 3.3 Trigger matrix for these products

| Sales channel | HIPAA status | BAA required? | Confidence |
|---|---|---|---|
| Direct to consumer (caregiver buys Concept A; mother buys Concept B) | Not a covered entity, not a business associate. HIPAA does not attach | No | HIGH |
| Sold through / integrated by a home health agency, hospital, or health plan, handling PHI on their behalf | Business associate | Yes, before any PHI is exchanged | HIGH |
| Reimbursed by a payer where the product performs a regulated function for the payer | Likely business associate | Yes | MEDIUM |
| Data sold or licensed to a covered entity that is not acting through us | Fact specific; may not create BA status | Analyze per deal | LOW |

Framework alignment: Concept A brief section on applicable law states HIPAA "attaches through the customer, not the product, so a home health agency channel changes everything." This research confirms that reading from primary sources. A home health agency or payer channel is a strategic decision that converts the product into a business associate and imposes the full Security Rule, the BAA obligation, and breach notification under 45 CFR 164.400 to 414.

### 3.4 The gap filler people forget: FTC

When HIPAA does not attach (the direct to consumer default), the product is not unregulated. The FTC Health Breach Notification Rule covers vendors of personal health records and connected health apps not covered by HIPAA. The 2024 amendments (effective 2024-07-29) explicitly bring health apps and connected devices into scope and broaden "breach" to include unauthorized disclosures, not only cyber intrusions. Source: FTC, "Health Breach Notification Rule" final rule, Federal Register 2024-05-30; FTC business guidance blog, 2024-04. Confidence HIGH. Note: this is over 18 months old as of 2026-07 but remains current law; no superseding rule found.

Net: there is no "HIPAA does not apply so we are free" state. Direct to consumer means FTC HBNR plus state law (section 4). Covered entity channel means HIPAA plus state law.

---

## 4. STATE BIOMETRIC AND CONSUMER HEALTH PRIVACY LAW

Three regimes matter most for these products. Illinois BIPA and Texas CUBI govern biometric identifiers (a face or voice derived template, gait signatures arguably included depending on construction). Washington MHMDA governs "consumer health data" far more broadly, and is the binding constraint.

### 4.1 Comparison

| Feature | Illinois BIPA (740 ILCS 14) | Texas CUBI (Tex. Bus. & Com. Code 503.001) | Washington My Health My Data Act (RCW 19.373) |
|---|---|---|---|
| Scope of data | Biometric identifiers (retina/iris scan, fingerprint, voiceprint, hand/face geometry) and biometric information derived from them | Biometric identifiers (retina/iris scan, fingerprint, voiceprint, record of hand or face geometry) | "Consumer health data": any personal data linked to a consumer that identifies past/present/future physical or mental health status. Very broad, includes precise location near health facilities and inferences |
| Consent standard | Written notice of purpose and retention term, plus a written release before collection (15(b)); separate consent before disclosure (15(d)) | Notice and consent before capture for a commercial purpose | Opt in, prior, express consent for collection/sharing beyond what is necessary; separate consent to share; signed authorization to sell |
| Retention limit | Written retention schedule; destroy when purpose met or within 3 years of last interaction (15(a)) | Destroy within a reasonable time, no later than 1 year after purpose expires | Honor deletion requests; data minimization to stated purpose |
| Private right of action | Yes. The only one of the three. Individuals may sue directly | No. Texas AG has exclusive enforcement | Yes, via Washington Consumer Protection Act (RCW 19.86); AG also enforces |
| Penalties | Greater of liquidated or actual damages: $1,000 per negligent violation, $5,000 per intentional/reckless, plus fees, costs, injunctive relief (Section 20) | Civil penalty up to $25,000 per violation (AG only) | CPA remedies: actual damages, up to $25,000 civil penalty per violation via AG, plus private suits |
| Notable enforcement | Cothron v. White Castle (per scan accrual); mitigated by 2024 amendment | Meta settlement, $1.4B, announced 2024-07-30 (AG Paxton) | New (in force 2024). Litigation wave anticipated; no landmark judgment yet |
| Confidence | HIGH | HIGH | HIGH |

Sources: 740 ILCS 14 (Illinois Compiled Statutes; Justia 2025 mirror); Public Act 103-0769, effective 2024-08-02; Davis Wright Tremaine, "Seventh Circuit Holds BIPA Amendment Applies Retroactively," 2024-08. Tex. Bus. & Com. Code 503.001 (FindLaw); Texas AG Biometric Identifier Act page; Holland & Knight, 2022-11. RCW Chapter 19.373; Washington AG page; Goodwin, 2024-03; IAPP MHMDA overview; EFF, 2025-06.

### 4.2 The two facts that reshape the risk

BIPA per violation damages were reformed. Public Act 103-0769 (effective 2024-08-02) provides that repeated collection or disclosure of the same identifier from the same person by the same method counts as a single violation with a single recovery, reversing the multiplier from Cothron. The Seventh Circuit held the amendment applies retroactively (2024). This lowers, but does not remove, BIPA exposure. The private right of action remains the defining risk. Confidence HIGH.

BIPA has a health care exclusion. Section 10 excludes information captured from a patient in a health care setting, and information collected/used/stored for treatment, payment, or operations under HIPAA. The Illinois Supreme Court (Mosby v. Ingalls Memorial Hospital, 2023) read this disjunctively and relatively broadly. Practical effect: if the product operates in a HIPAA covered channel (section 3.3), the same data can fall outside BIPA. Direct to consumer, it does not. Confidence MEDIUM (the exclusion is real but its boundary for a consumer wellness product with no HIPAA nexus is untested; do not rely on it in the DTC channel).

### 4.3 Washington MHMDA is the binding constraint

MHMDA is broader than the biometric statutes on three axes that hit these products directly:

1. "Consumer health data" sweeps in far more than a biometric template. Home activity patterns inferring health status, sleep, gait decline, pregnancy status, and mood signals are all in scope. Both products generate exactly this.
2. Consumer is defined as a Washington resident or any natural person whose consumer health data is collected in Washington. It reaches nonresidents whose data is collected in state. Source: RCW 19.373 definitions; California Lawyers Association analysis, 2024.
3. There is no revenue or size threshold to be a "regulated entity" the way CCPA has. A small startup is in scope from the first Washington user. Small business gets a short compliance extension only.

MHMDA also carries a geofencing prohibition: unlawful to erect a geofence of 2,000 feet or less around an entity providing in person health care services to identify or track consumers, collect their health data, or send them targeted messages (RCW 19.373.100). Neither product should implement location features near health facilities. Confidence HIGH.

Design to MHMDA and you clear BIPA and CUBI by a wide margin, because MHMDA's opt in consent, separate sharing consent, and signed sale authorization are stricter than what either biometric statute requires.

### 4.4 Audio triggers a separate regime: two party consent wiretap law

If either product records audio in the home (Concept A conversational assistant; any ambient audio capture), state eavesdropping law applies independently of biometric law. Illinois and Washington are both all party consent states. Recording a private conversation without the consent of all parties is a crime, a felony in Illinois (up to 1 to 3 years, up to $25,000) and a gross misdemeanor in Washington. Source: 720 ILCS 5/14-2 (Illinois eavesdropping); RCW 9.73.030; Recording Law state guides, 2026. Confidence HIGH.

Product consequence for Concept A: a device that captures audio in a household where a visitor, aide, or family member speaks cannot lawfully record without all party consent. Prefer on device wake word processing that does not retain audio, and explicit consent signage/onboarding. This is a design constraint, not a footnote.

---

## 5. CONSENT ARCHITECTURE WHEN THE DATA SUBJECT IS NOT THE BUYER

Both products separate the person the data is about from the person who buys and operates. This is the central privacy design problem, and it is a product differentiator, not a compliance checkbox (Concept A phase 5 item 3; Concept B item 4).

### 5.1 The two cases

| | Concept A: elder resident | Concept B: pregnant mother vs partner |
|---|---|---|
| Data subject | The resident being monitored | The mother |
| Buyer / co user | Remote caregiver (adult child) | Partner |
| Core tension | Resident may not want to be watched; may have cognitive impairment affecting capacity to consent | Everything the partner sees is a disclosure of the mother's health data to a third party |
| Failure mode | Covert surveillance of a competent adult (legal and ethical exposure); or invalid consent from an incapacitated adult | "Tell him she slept badly" becomes nonconsensual disclosure; a lawsuit and a product women reject |

### 5.2 Pattern for the elder resident (capacity and surrogate consent)

| Layer | Requirement | Basis |
|---|---|---|
| Default: resident is the consenting party | The competent resident must be informed and must consent. Covert monitoring of a competent adult is not a design option (framework Concept A brief flags covert monitoring as a distinct legal/ethical problem) | BIPA/CUBI/MHMDA consent runs to the data subject; wiretap law (section 4.4) |
| Capacity assessment | Product must not assume the buyer can consent for the resident. Capacity is condition specific and can fluctuate | Surrogate consent doctrine: capacity is presumed until shown otherwise |
| Legally authorized representative path | Where the resident lacks capacity, consent flows through a legally authorized representative in a defined priority order (durable power of attorney for health care, court appointed guardian, spouse, adult child) | Surrogate/LAR consent frameworks (e.g. UC/UCSF IRB guidance; Cal. Health & Safety Code 24178 as a model of the priority ordering). Confidence MEDIUM: these are research consent models; the exact enforceable order for a consumer product varies by state and should be confirmed per launch state |
| Assent even without capacity | Where the resident cannot legally consent, still solicit assent and provide a visible, dignified indicator that monitoring is active | Ethical best practice; supports the trust and adoption argument |
| Revocability and transparency | Resident (or LAR) can see what is captured and shared, and can revoke. A visible active state, not a hidden one | MHMDA deletion/withdrawal; product trust |

The product must implement a role and capacity model, not a single owner account. This is engineering work at G0/G1, not legal boilerplate.

### 5.3 Pattern for the pregnancy dual user (granular, revocable, per element disclosure)

The mother and partner are separate accounts with separate views. Every data element the partner can see is a disclosure the mother grants, granularly, and can revoke instantly and without friction (Concept B brief item 4). Recommended architecture:

| Control | Specification |
|---|---|
| Separation | Two accounts, two views. Partner has no default visibility into the mother's data |
| Granularity | Consent is per data category and ideally per element (sleep, mood, symptoms, appointments, biometric trends), not one global toggle |
| Directionality | Consent is a grant from the mother to the partner, modeled like a scoped authorization (an OAuth style scope grant is the right mental model), not a shared household record |
| Revocation | Instant, frictionless, no negotiation, no notification requirement to the partner that could create relational pressure. Revocation takes effect immediately |
| Visible indicator | The mother always sees what is currently shared. No silent sharing |
| Sensitive categories default closed | Mood, intrusive thoughts, mental health signals default to not shared. These require the highest bar |
| Sale/secondary use | Never without separate signed authorization (MHMDA) |

This is the line the framework draws: "tell him she slept badly, help her today" is excellent product with consent and unacceptable surveillance without it. The consent layer is the only thing separating them. Build it as a feature. Confidence HIGH on the design principle; MEDIUM on the exact enforceable minimum, which depends on state law of the launch footprint.

---

## 6. REPRODUCTIVE HEALTH DATA LEGAL RISK (CURRENT US ENVIRONMENT)

Concept B generates reproductive health data (pregnancy status, gestational progression, potentially pregnancy loss). In the post Dobbs environment this is the single highest legal risk data category the program touches, and it is a first order architecture input (Concept B brief item 6).

### 6.1 The environment shifted twice, both adverse to a "rely on federal protection" posture

1. HIPAA does not cover most consumer reproductive apps. HIPAA reaches covered entities and business associates only (section 3). A direct to consumer pregnancy app is neither, so HIPAA provides no protection to its data by default. Source: ProPublica, "Federal Patient Privacy Law Does Not Cover Most Period Tracking Apps," 2022; confirmed by section 3 analysis. Confidence HIGH.
2. The federal patch that would have helped was vacated. HHS issued the HIPAA Privacy Rule to Support Reproductive Health Care Privacy (2024, effective 2024-06-25), requiring an attestation before disclosing PHI related to lawful reproductive care. On 2025-06-18 the US District Court for the Northern District of Texas (Purl v. HHS, No. 2:24-CV-228-Z) vacated that rule nationwide. HHS did not appeal by the 2025-08-18 deadline. As of 2026-07 the rule is vacated and not in force; intervenor motions are keeping the case procedurally alive but the protection is gone. Source: Holland & Knight, 2025-06; Husch Blackwell, 2025; Dorsey Health Law, 2025. Confidence HIGH.

Consequence: reproductive data in this product enjoys no HIPAA attestation shield even in the covered channel, and no HIPAA coverage at all in the DTC channel. State law (MHMDA and its analogues) and the architecture itself are the only protections.

### 6.2 The specific exposures

| Exposure | Mechanism | Confidence |
|---|---|---|
| Subpoena / court order | Data on a company server can be compelled by subpoena or court order. Many apps' own terms commit them to comply. Data could be used to infer pregnancy status or loss and prosecute in states that criminalize abortion related conduct | HIGH |
| Location / geofence warrants | Location data timestamping a visit to a reproductive health provider can be compelled. MHMDA bars the product from geofencing near facilities (section 4.3); the architecture must also avoid retaining precise location | HIGH |
| Data sale / sharing | Secondary sharing or sale to data brokers who then receive law enforcement or civil demands | MEDIUM |
| Breach | Central store of reproductive data is a high value target | HIGH |
| Sources | Take Back Trust (2024); Stateline, 2024-07; NBC News, 2022; ProPublica, 2022 | |

### 6.3 Required architecture posture (data minimization, retention, storage location)

| Principle | Implementation | Basis |
|---|---|---|
| Collect the minimum | Do not collect precise location. Do not persist reproductive status fields beyond what the daily loop requires | MHMDA data minimization; subpoena exposure reduction |
| Store on device where possible | Data held only on the user's device, encrypted, is far harder to compel than data a company can be subpoenaed for. Prefer local first for the most sensitive fields | Local storage is materially safer against compelled disclosure |
| Minimize retention | Short, defined retention windows; automatic deletion; honor user deletion instantly and completely, including backups | MHMDA deletion right; less retained data means less to compel or breach |
| Do not sell or broker | No sale, no secondary sharing of reproductive data, full stop. Separate signed authorization would be required and is not worth the risk | MHMDA sale authorization; reputational catastrophe risk |
| Encrypt to safe harbor | Section 1 baseline, so a compromised store is unusable | Breach safe harbor |
| Design for the adverse jurisdiction | Assume a user in a state that criminalizes abortion related conduct. The architecture must not create the evidence | Post Dobbs subpoena reality |

Confidence HIGH on the posture direction; the exact state by state criminal exposure map is out of scope here and belongs in `regulatory_risk_register.md`.

---

## 7. APPROVED CLAIM LANGUAGE POSTURE

Privacy and security claims are marketing claims and are subject to FTC substantiation the same way health claims are (framework section 2, the second regulator). A privacy promise the architecture does not enforce is a deceptive practice. Say only what the build makes true.

| Approved (if and only if the architecture enforces it) | Prohibited or high risk | Why |
|---|---|---|
| "Video is processed on the device. Raw video is not sent to our servers." (only after every code path is proven, per Concept A phase 5 item 2) | "Your video never leaves your home." (absolute, unqualified) | The claim must survive debug, OTA, crash dump, and remote support paths. Absolutes invite a single counterexample |
| "Encrypted in transit and at rest using AES 256 and TLS 1.2 or higher." | "Military grade encryption." | Specific, verifiable vs vague puffery FTC disfavors |
| "You control exactly what your partner can see, and you can turn off sharing at any time." | "Fully HIPAA compliant" in the direct to consumer channel | HIPAA does not attach DTC; claiming compliance where the law does not apply is misleading |
| "We do not sell your health data." | "We will never share your data with anyone." | Legal process (subpoena) can compel disclosure; an absolute never is false |
| "Reproductive health information is stored on your device and minimized." | Any implied promise that data cannot be subpoenaed | No company can promise immunity from lawful process |

Rule: every privacy claim maps to an enforced control and a code path. If it is not enforced, it is not said. Confidence HIGH.

---

## Register Entries

Per framework section 9, all sources land in `research/registers/sources.md`. This phase does not edit the registers directly (instructed scope limit). The following is the staged source list for append into `sources.md`, including rejected sources.

### Sources consulted (stage into registers/sources.md)

| Source | Org | URL | Pub date | Used for | Credibility |
|---|---|---|---|---|---|
| 45 CFR 164.312 Technical Safeguards | eCFR (US gov) | ecfr.gov/current/title-45/.../section-164.312 | Current | Encryption at rest/in transit addressable status | HIGH (primary) |
| HIPAA Encryption Requirements 2026 | HIPAA Journal | hipaajournal.com/hipaa-encryption-requirements | 2026 | AES/TLS baselines, addressable meaning | MEDIUM (secondary, current) |
| HIPAA Security Rule NPRM fact sheet | HHS.gov OCR | hhs.gov/hipaa/for-professionals/security/hipaa-security-rule-nprm/factsheet | 2025-01 | Proposed mandatory encryption | HIGH (primary) |
| HIPAA Security Rule Update Postponed | HIPAA Journal | hipaajournal.com/hipaa-security-rule-update-postponed | 2026 | NPRM still not final as of 2026 | MEDIUM |
| 45 CFR 160.103 Definitions | eCFR / HHS | hhs.gov covered entities page | Current | Covered entity, business associate definitions | HIGH (primary) |
| Covered Entities and Business Associates | HHS.gov | hhs.gov/hipaa/for-professionals/covered-entities | Current | HIPAA trigger, BAA requirement | HIGH (primary) |
| FTC Health Breach Notification Rule (final) | FTC / Federal Register | federalregister.gov/documents/2024/05/30/2024-10855 | 2024-05-30 | HBNR covers non HIPAA health apps | HIGH (primary). Over 18 mo, still current |
| FTC HBNR blog (health apps) | FTC | ftc.gov/business-guidance/blog/2024/04 | 2024-04 | Scope of HBNR amendments | HIGH (primary). Over 18 mo |
| 740 ILCS 14 (BIPA) | Illinois Compiled Statutes / Justia | law.justia.com/codes/illinois/.../act-740-ilcs-14 | 2025 mirror | BIPA consent, retention, PRA, damages, Sec 10 exclusion | HIGH (primary) |
| Public Act 103-0769 / SB 2979 retroactivity | Davis Wright Tremaine | dwt.com/blogs/.../2024/08 | 2024-08 | Single violation amendment, retroactive | MEDIUM. Over 18 mo, law still current |
| Mosby v. Ingalls (BIPA health care exclusion) | Sidley / Faegre Drinker | sidley.com / faegredrinker.com | 2023-12 | BIPA Sec 10 health care exclusion scope | MEDIUM. Stale date, ruling still governing |
| Tex. Bus. & Com. Code 503.001 (CUBI) | FindLaw | codes.findlaw.com/tx/.../503-001 | Current | CUBI scope, consent, retention | HIGH (primary text) |
| Texas Biometric Identifier Act | Texas AG | texasattorneygeneral.gov/.../biometric-identifier-act | Current | CUBI enforcement, penalty, no PRA, Meta $1.4B | HIGH (primary agency) |
| RCW Chapter 19.373 (MHMDA) | WA Legislature | app.leg.wa.gov/RCW/?cite=19.373 | Current | MHMDA definitions, consent, geofence, PRA | HIGH (primary) |
| WA MHMDA overview | IAPP | iapp.org/resources/article/washington-my-health-my-data-act | 2024 | MHMDA structure | MEDIUM |
| MHMDA comes into force | Goodwin | goodwinlaw.com/.../my-health-my-data-act-mhmda | 2024-03 | Effective dates, consent standard | MEDIUM. Over 18 mo |
| MHMDA not just WA or health | California Lawyers Assn | calawyers.org/privacy-law/... | 2024 | Nonresident scope, breadth | MEDIUM |
| Purl v. HHS reproductive rule vacated | Holland & Knight | hklaw.com/.../2025/06 | 2025-06 | Nationwide vacatur of repro rule | HIGH (primary case reporting) |
| Repro rule vacated, no appeal | Husch Blackwell / Dorsey | huschblackwell.com / dorseyhealthlaw.com | 2025 | HHS did not appeal, status 2025 to 2026 | MEDIUM |
| Period app data subpoena risk | ProPublica | propublica.org/article/period-app-privacy-hipaa | 2022 | HIPAA does not cover most repro apps | MEDIUM. Stale, still directionally correct |
| Data privacy after Dobbs | Stateline | stateline.org/2024/07/26 | 2024-07 | Subpoena, local storage safety | MEDIUM. Over 18 mo |
| Illinois eavesdropping (720 ILCS 5/14-2) | Recording Law / ISBA | recordinglaw.com; isba.org | 2026 | All party consent, penalties | MEDIUM (secondary, current) |
| RCW 9.73.030 | WA Legislature | app.leg.wa.gov/rcw/?cite=9.73.030 | Current | WA all party consent | HIGH (primary) |
| Edge vs cloud AI privacy | Fora Soft; Medium/Goldshtein; ResearchGate | (multiple) | 2026 | Architecture tradeoff framing only | LOW (secondary, technical, not for legal claims) |

### Sources rejected

| Source | Reason rejected |
|---|---|
| Various HIPAA "encryption requirements" SEO vendor pages (accountablehq, netsec.news, censinet, thoropass, hipaareadycheck, oneguyconsulting) | Content marketing/SEO aggregators. Framework section 5.9 disfavors. Citations traced to primary CFR instead |
| LegalClarity, TermsFeed, CaseGuard CUBI/BIPA explainers | Secondary explainer sites; superseded by statute text and AG pages |
| clinicaltrials.gov protocol PDFs (surrogate consent search) | Off topic; returned by keyword noise, not relevant to consumer product consent |
| Usercentrics, OneTrust, PrivacyOn MHMDA guides | Vendor lead gen content; superseded by RCW and IAPP |

Note: eCFR, HHS.gov, WA Legislature, Texas AG, Cornell LII, and Justia pages returned HTTP 403 to the automated fetcher (site side bot blocking, not an organization policy denial per proxy status check). Substantive content was obtained via search engine extraction of those same primary pages. Primary URLs are cited above for the human reader; direct machine fetch of full statute text is an open item.

---

## Open Questions

1. Full verbatim statute text of 740 ILCS 14/15, RCW 19.373 sections, and Tex. Bus. & Com. Code 503.001 could not be machine fetched (403 site blocks). Section numbers and substance are confirmed via multiple sources; verify exact subsection wording against the primary text before legal review. Does not block the architecture.
2. Whether a gait signature or a whole body movement pattern qualifies as a "biometric identifier" under BIPA/CUBI (both enumerate face/hand geometry, voice, fingerprint, iris; gait is not enumerated). Likely outside the enumerated list but MHMDA's "consumer health data" captures it regardless. Confirm before relying on non applicability of BIPA to gait.
3. Exact enforceable surrogate/LAR consent priority order for a consumer (non research, non clinical) monitoring product, per launch state. The research consent models cited are analogous, not controlling.
4. Final status of the HIPAA Security Rule NPRM (mandatory encryption). No final rule as of 2026-07; recheck at G4.
5. Whether the vacated HIPAA Reproductive Health Rule will be revived by HHS or replaced. Currently vacated, unappealed; intervenors keep the case alive. Recheck before Concept B launch.
6. State by state criminal exposure map for reproductive data. Belongs in `regulatory_risk_register.md`, not resolved here.
7. Applicability of MHMDA analogues now enacted in other states (for example Nevada SB 370, Connecticut, Maryland MODPA) not researched in this phase; scope is the three statutes the framework named.

## Assumptions Made

1. Assumed both products default to a direct to consumer sales channel for the base case, with covered entity channels treated as a variant. If the primary channel is a home health agency or payer, HIPAA attaches from day one and the BAA and full Security Rule become baseline, not optional. Impact if wrong: understates baseline compliance cost.
2. Assumed the products will process the most sensitive raw modalities (video, audio, raw wearable) on device. If cost, thermal, or capability constraints (framework A2) force cloud processing of raw data, the compliance surface and the reproductive/biometric exposure expand materially. Impact if wrong: section 2 and 6 postures weaken.
3. Assumed "consumer health data" under MHMDA covers the derived home activity and pregnancy signals these products generate. The definition is broad and this is a conservative reading. Impact if wrong: overstates MHMDA burden, which is the safe direction to err.
4. Assumed legal claims of law remain as found through 2026-07-10. Two anchors changed status inside 24 months (NPRM, repro rule); treat all as time sensitive.
5. Treated the three named statutes (BIPA, CUBI, MHMDA) as the governing set per the framework, not a complete survey of US state biometric/health privacy law.

## Confidence Summary

Overall confidence: HIGH on the load bearing findings, MEDIUM on the design specifics that depend on downstream product decisions.

- HIGH: HIPAA attaches through the customer not the product (section 3); the BAA trigger; the encryption citations and baselines (section 1); the BIPA/CUBI/MHMDA comparison including PRA and penalties (section 4); MHMDA as the binding constraint; the vacatur of the HIPAA Reproductive Health Rule and its consequence (section 6); the approved claim posture (section 7).
- MEDIUM: the exact enforceable surrogate consent order for elders (section 5.2); the minimum enforceable granularity for the pregnancy dual user consent (section 5.3); the edge/cloud split recommendation (section 2, pending Concept A sensor and Concept B LLM decisions); whether BIPA's health care exclusion helps a DTC product.
- LOW / weakest: whether gait qualifies as a biometric identifier under BIPA/CUBI (open question 2); the edge vs cloud technical sources are secondary and used only for framing, not for any legal claim.
- Staleness flags: FTC HBNR (2024-07), BIPA 2024 amendment (2024-08), Meta/CUBI settlement (2024-07), MHMDA effective date commentary (2024-03), and Mosby (2023-12) are all older than 18 months as of 2026-07 but remain current law; no superseding authority found. The HIPAA Security Rule NPRM and the reproductive rule status are the two items most likely to move and must be rechecked before any G4 legal review.
