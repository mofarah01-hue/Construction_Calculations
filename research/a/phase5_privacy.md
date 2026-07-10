# Concept A, Phase 5: Data, Privacy, and Security Architecture

Governed by `00_framework.md` (sections 2, 5, 6, 8, 9) and `01_concept_a_elder_monitoring.md` (Phase 5). Inherits `research/shared/shared_privacy_security.md` in full and does not repeat it. This phase does concept specific work only, against the architecture selected in `research/a/phase2_architecture.md`: primary A1, a distributed mesh (PIR and door contact mesh in every zone, an under mattress BCG mat in the bedroom, a 60 GHz radar node in the bathroom and optionally the bedroom, and one oblique mains powered camera node in a shared living area running on node inference), compute topology T4 hybrid with a T1 local fall path. Object memory and natural language query are LATER (Phase 0), so v1 carries a mesh gateway, not an inference hub.

Inherited baselines applied without restatement: encryption floor AES 256 at rest and TLS 1.3 in transit (`shared` section 1.3); edge versus cloud data minimization posture (`shared` section 2); HIPAA attaches through the channel, not the product (`shared` section 3); BIPA, CUBI, and MHMDA comparison with MHMDA as the binding constraint (`shared` section 4); all party consent wiretap regime for audio (`shared` section 4.4); the surrogate consent pattern skeleton (`shared` section 5.2); approved claim posture (`shared` section 7).

Confidence tags HIGH, MEDIUM, LOW per framework section 5. Citation keys `[S#]` resolve in Register Entries. Legal claims carry source, URL, date, and the named authority.

---

## 1. DATA FLOW: EVERY HOP, EVERY STORE, EVERY RETENTION PERIOD

The architecture has six node types plus a mesh gateway plus a cloud tier plus two application clients (resident and caregiver). The governing rule from `shared` section 2 holds throughout: raw sensitive modality (video, audio, radar point cloud, load cell waveform) is processed at the edge; only derived, non reconstructable features and events transit off the home.

### 1.1 Per node data lineage

| Node type | Raw signal captured | Processing location | What leaves the node | Where it goes next | On node store and retention | Off node store and retention |
|---|---|---|---|---|---|---|
| Camera node (oblique, living area), T1 on sensor (IMX500 class) | RGB frames | Inference inside the sensor package; pixels do not reach the application SoC | Pose keypoints, gait metrics, sit to stand timing, fall and long lie events, periodic hazard inventory labels. No frame, no image | Mesh gateway, then cloud | Rolling frame buffer inside the sensor die only, overwritten continuously, never persisted to disk. Derived metrics buffered on the node SoC less than 24 h until gateway ack | Derived metrics and events in cloud, see 1.2 |
| Radar node (bathroom, optional bedroom) | 60 GHz point cloud and range Doppler | On node classifier | Presence, fall, long lie, dwell, nocturia count, coarse gait speed, respiration and resting HR values. No point cloud raw stream | Mesh gateway, then cloud | Point cloud held in RAM only for the classification window, not persisted. Derived events buffered less than 24 h until ack | Events and vitals values in cloud |
| BCG bed mat (bedroom) | Ballistocardiography load waveform | On node or gateway feature extraction | Time in bed, bed exit, sleep fragmentation, resting HR, respiratory rate. No waveform | Mesh gateway, then cloud | Waveform in RAM only during extraction, not persisted. Nightly summary buffered until ack | Nightly summaries in cloud |
| PIR and door and window contacts | Binary motion and open close | Native, no inference | Timestamped occupancy and transition and open close events | Mesh gateway (Zigbee or Thread), then cloud | Battery node, event pushed immediately, minimal local buffer | Event stream in cloud, aggregated to life space, circadian, ADL |
| Microphone (assistant, camera node or a dedicated voice node) | Audio | On device wake word only; no audio retained until wake | After wake word: utterance transcribed. Design target is on device speech to text; if cloud STT is used, the utterance audio transits under explicit consent | Cloud assistant | No audio persisted pre wake; post wake utterance held only for the turn, not stored, unless the resident opts into transcript retention | Transcript text only, not audio, retention per 1.2 |
| Mesh gateway (home) | None of its own; aggregation and transport | Buffering, encryption, backhaul | Encrypted batch of derived events and metrics over TLS 1.3 | Cloud ingest | Encrypted local store of derived events, rolling 7 to 30 days as offline resilience buffer, then purged after cloud ack | n/a |
| Cloud assistant and trend tier | None captured; receives derived features only | LLM interpretation on stripped features; trend analytics | Caregiver report, assistant replies, notifications | Resident app, caregiver app, escalation path | n/a | See 1.2 retention schedule |

### 1.2 Cloud stores and retention schedule (product policy, design decision)

Retention is a product policy input, not a legal constant. The schedule below is set to MHMDA data minimization and the BIPA destroy on purpose completion or three year floor (`shared` section 4.1), and is a recommendation to be confirmed per launch state. Confidence MEDIUM on the exact windows, HIGH on the direction (minimize).

| Cloud store | Contents | Retention | Basis |
|---|---|---|---|
| Event log | Falls, long lie, bed exit, door events, escalations | 13 months rolling, then aggregate and purge raw events | Enables year over year trend while bounding the compellable and breachable corpus |
| Derived metric time series | Gait speed, sit to stand, nocturia count, life space, circadian indices, resting HR, respiration | 13 months rolling; downsample to weekly aggregates thereafter | MHMDA minimization; trend value preserved at coarser grain |
| Assistant transcripts (text) | Resident and caregiver dialogue turns | 30 days default, off by default for retention beyond the turn, resident opt in for longer | All party consent and MHMDA; audio never stored |
| Account and role graph | Identities, roles, capacity flags, consent grants and revocations | Life of account plus statutory tail, then delete | Consent auditability; deletion right honored |
| Backups | Encrypted snapshots of the above | Match primary retention; deletion propagates to backups within a defined window | `shared` section 6.3 deletion including backups |
| Raw video, raw audio, raw point cloud, raw waveform | None. These never reach the cloud in v1 | Not stored | The load bearing minimization claim |

Every deletion request purges primary and backup within the stated window. No raw modality is ever a cloud store row, which is the fact that makes section 2 provable and section 7 sayable.

---

## 2. PROVE OR DISPROVE: "NO VIDEO LEAVES THE DEVICE"

The claim is provable in the qualified form the shared file permits ("Raw video is processed on the device and is not sent to our servers"), and only if every code path below is affirmatively closed and audited. The absolute form ("your video never leaves your home") is not defensible, because residual paths (a crash dump, a compromised device) cannot be reduced to a mathematical zero. This matches `shared` section 7: state the enforced claim, not the absolute.

The architectural enabler is on sensor inference (Sony IMX500 class, `phase2_architecture` S16): pixels are consumed inside the sensor package and only a metadata tensor crosses to the application SoC. That removes the frame from the application processor entirely, which collapses most exfiltration paths at the hardware level rather than the policy level. This is the single most important control in the whole phase.

### 2.1 Every code path that could violate the claim, and the control that closes it

| # | Code path | How it could leak video | Control that closes it | Residual risk | Confidence |
|---|---|---|---|---|---|
| 1 | Normal inference path | App SoC reads a frame buffer to run the model | On sensor inference (IMX500 class): frames never leave the sensor die; app SoC receives only the metadata tensor. No frame buffer is exposed to application code | Near zero by construction | HIGH |
| 2 | Developer and debug builds | A debug build enables a frame dump, a live preview, or logs raw frames for tuning | Production signed image has no frame egress path compiled in; frame access is a debug only capability gated behind a hardware fuse or secure debug that is blown or disabled before shipment; separate firmware variants for lab and field | Low; depends on build hygiene and fuse discipline | MEDIUM |
| 3 | OTA update | A future signed update quietly adds a frame capture and upload capability | Signed firmware and signed OTA (section 5); a documented policy that no OTA may enable raw modality egress without a re consent event; code review gate on any camera pipeline change; reproducible builds so the shipped image is auditable | Low; this is a governance control, not a hardware one, so it is only as strong as the review process | MEDIUM |
| 4 | Crash dumps and telemetry | A core dump or diagnostic snapshot captures a frame buffer resident in RAM | With on sensor inference there is no frame in app SoC RAM to capture; additionally, crash dumps exclude any camera memory region and are scrubbed before upload; telemetry is schema allowlisted to derived fields only | Low; the IMX500 architecture removes the frame from the dumpable region | MEDIUM to HIGH |
| 5 | Remote support and live view | A support engineer requests a live camera view or a stored clip to diagnose an install | No remote video access capability is built. Support sees derived events and device health only. Any on device diagnostic image is viewable on device by the resident, never streamed off | Low; a deliberately absent feature cannot be abused, provided it is never added | HIGH |
| 6 | Local verification clip for false positive reduction | A short pre and post event clip is buffered to let a human or model confirm a fall, and that clip is uploaded | Design decision: no clip is uploaded. If a verification clip is buffered at all, it stays on device, encrypted to the secure element, auto deleted on a short timer, and is never a network payload. Preferred v1 posture: no clip buffer, radar plus pose event fusion for confirmation instead | Medium if a clip buffer is introduced; the safest build has none | MEDIUM |
| 7 | Model improvement data collection | Raw frames are harvested to retrain the detector | No raw frame collection. Model improvement uses on device metrics, synthetic data, or a separate explicit opt in program with its own consent and its own store, never the production telemetry path | Low if the no raw collection rule holds | MEDIUM |
| 8 | Physical device compromise | An attacker with the device extracts frames from memory or storage | Secure boot, encrypted storage, no persisted frames (section 5). Even a rooted device yields at most the in sensor rolling buffer, not a history | Low for history; a live compromised device is a single home exposure, not a corpus | MEDIUM |

### 2.2 Verdict

Provable, conditionally. "Raw video is processed on the device and raw video is not transmitted to our servers or our support staff" is true and defensible if and only if paths 1 through 8 are closed as specified and audited before any marketing uses the claim. The strongest single move is on sensor inference, which converts the promise from a policy assertion (path 4, 5) into a hardware property (path 1). The weakest links are the governance paths (OTA path 3, debug path 2), which no hardware can close and which require process discipline and code review as the control. The absolute unqualified claim is prohibited per `shared` section 7. Confidence HIGH on the verdict, MEDIUM on the field enforcement of the governance paths.

---

## 3. CONSENT ARCHITECTURE: THE RESIDENT IS NOT THE BUYER

This is a product design constraint and a market objection, not a compliance footnote. The resident is the data subject. The caregiver (adult child) is the buyer and the day to day user. Their interests diverge: the caregiver wants visibility, the resident may not want to be watched, and the resident may have fluctuating or diminished capacity to consent at all. A product that treats the buyer as the account owner and the resident as an object of that account is both legally exposed (covert or non consented surveillance of a competent adult) and commercially fragile (the resident unplugs it, or refuses it, which is the dominant churn and refusal mode in this category).

### 3.1 The design stance

The product implements a role and capacity model, not a single owner account. The resident is a first class principal with visibility and control, even when the caregiver pays. This is engineering work at G0 and G1, per `shared` section 5.2, restated here as a build requirement, not a policy document.

### 3.2 Four consent states the product must handle

| State | Who consents | Product behavior | Basis |
|---|---|---|---|
| Competent resident, willing | Resident, informed opt in | Full function. Resident sees what is captured and what is shared, and can pause or revoke. Visible active indicator on every sensing node | BIPA, CUBI, MHMDA consent runs to the data subject (`shared` 4); wiretap consent for audio (section 4) |
| Competent resident, unwilling or ambivalent | Resident controls scope | Resident can decline the camera and keep the mesh, decline audio, or decline sharing specific categories with the caregiver. The caregiver cannot override. Covert operation is not an available configuration | Covert monitoring of a competent adult is a distinct legal and ethical exposure (`shared` 5.2); MHMDA granular consent |
| Resident with diminished or fluctuating capacity | Resident assent plus surrogate consent | Solicit resident assent and show a visible, dignified active indicator even where legal consent flows through a surrogate. Capacity is presumed until shown otherwise and can fluctuate; the product must not assume the buyer can consent for the resident | Surrogate consent doctrine; MHMDA; ethical assent standard (`shared` 5.2) |
| Resident lacks capacity | Legally authorized representative | Consent flows through a surrogate in a defined priority order (see 3.3). The surrogate must follow the resident's known wishes and values, and absent those, the resident's best interest | State surrogate decision maker statutes (see 3.3) |

### 3.3 Who can consent for a cognitively impaired adult (the hardest case, verified)

Surrogate consent for a consumer monitoring product is not identical to clinical treatment consent, and the exact enforceable order is state specific and, for a non clinical consumer product, partly untested. The clinical and statutory hierarchy is the correct model to build to, because it is the order courts and states already recognize. Confidence MEDIUM on direct applicability to a consumer product, HIGH on the hierarchy itself.

| Priority | Surrogate | Authority | Source | Confidence |
|---|---|---|---|---|
| 1 | Agent under a health care power of attorney (durable POA for health care) | Designated in advance by the resident while competent | Arizona Rev. Stat. 36-3231 (surrogate decision makers, priorities), azleg.gov, accessed 2026-07-10; general default surrogate framework, Merck Manual "Default Surrogate Decision Making," merckmanuals.com, accessed 2026-07-10 | HIGH |
| 2 | Court appointed guardian of the person (where appointed for health decisions, may outrank the agent for its express purpose) | Court order | Illinois Health Care Surrogate Act priority order, Illinois Legal Aid Online, illinoislegalaid.org, accessed 2026-07-10 | HIGH |
| 3 | Spouse or domestic partner | Default statutory next of kin | Illinois Health Care Surrogate Act; Merck Manual default surrogate list, accessed 2026-07-10 | HIGH |
| 4 | Adult child | Default statutory next of kin | Same | HIGH |
| 5 | Parent | Default statutory next of kin | Same | HIGH |
| 6 | Adult sibling | Default statutory next of kin | Same | HIGH |

Named authorities: Arizona Rev. Stat. 36-3231 sets an explicit statutory priority (agent under health care POA first, then court appointed health care guardian, then spouse, adult child, parent, sibling). Illinois Health Care Surrogate Act sets a parallel order (guardian of the person, spouse, adult child, parent, sibling). The uniform decision standard across states: the surrogate must follow the resident's expressed wishes and known values, and where unknown, act in the resident's best interest. Sources: azleg.gov/ars/36/03231.htm (accessed 2026-07-10); illinoislegalaid.org healthcare surrogate (accessed 2026-07-10); merckmanuals.com default surrogate decision making (accessed 2026-07-10). Confidence HIGH on the hierarchy, MEDIUM on whether a consumer wellness product may rely on it directly without a clinical nexus, which is untested and belongs in the launch state legal review.

Build consequence: onboarding must capture the resident's role and capacity status and, where capacity is absent, the surrogate's authority basis (POA document, guardianship order, or attested next of kin standing in priority order), and must record which principal granted consent for what, revocably and auditable. A single "owner buys and controls everything" account is a defect, not a simplification.

### 3.4 The market objection stated plainly

The resident who does not want to be watched is not an edge case; the resident is the person the product lives or dies with. The architecture already answers this: the two private rooms have no camera (bathroom radar, bedroom mat or radar), the camera sits obliquely in one shared room with a visible active indicator, and no raw video leaves. The consent model turns that architecture into an adoption argument: the resident can see and control what is captured and shared, which is the difference between a product an older adult accepts and one an older adult unplugs. Confidence HIGH on the principle.

---

## 4. APPLICABLE LAW, APPLIED TO CONCEPT A

Inherits the full statutory analysis in `shared` section 4. Applied to this product's specific data (gait and whole body movement signatures, home activity patterns, contactless vitals, and an audio assistant) below.

### 4.1 State biometric and consumer health privacy law, applied

| Statute | Does it reach this product's data | Applied finding | Confidence |
|---|---|---|---|
| Illinois BIPA (740 ILCS 14) | Enumerated identifiers are face, voice, fingerprint, hand and iris geometry. A gait or whole body movement signature is not enumerated. A voiceprint from the assistant could be, if the product builds one | Gait likely outside BIPA's enumerated list; a voiceprint would be inside it. Do not build a voice template. Confirm gait non applicability before relying on it (`shared` Open Question 2) | MEDIUM |
| Texas CUBI (Bus. & Com. Code 503.001) | Same enumerated set as BIPA; AG only enforcement | Same as BIPA; no private right of action lowers acute litigation risk but not the compliance duty | MEDIUM |
| Washington MHMDA (RCW 19.373) | "Consumer health data" sweeps in home activity patterns, sleep, gait decline, nocturia, and any inference of health status, regardless of whether it is a biometric identifier | Binding constraint. This product's derived markers are consumer health data. Design to MHMDA opt in, separate sharing consent, minimization, and deletion, and BIPA and CUBI are cleared by margin (`shared` 4.3) | HIGH |

Net, unchanged from the shared file: MHMDA governs. The product's home activity and health inference data is squarely "consumer health data," so the whole consent and minimization architecture is built to MHMDA whether or not gait is a biometric identifier.

### 4.2 Audio triggers a separate regime: all party consent wiretap law

The assistant captures audio in a home where visitors, aides, and family members also speak. Recording a private conversation without the consent of all parties is a crime in the all party consent states. As of 2026, twelve states apply an all party (two party) consent rule: California, Connecticut, Delaware, Florida, Illinois, Maryland, Massachusetts, Montana, New Hampshire, Oregon, Pennsylvania, and Washington. Illinois is a felony; Washington is a gross misdemeanor (`shared` 4.4). Source: Recording Law, "Two Party Consent States for Recording (2026 Guide)," recordinglaw.com, accessed 2026-07-10; corroborated by worldpopulationreview.com two party consent states 2026. Confidence HIGH on the twelve state set, HIGH on Illinois and Washington penalties (primary statutes cited in `shared` 4.4).

Product consequence, restated as a build constraint: on device wake word processing with no pre wake audio retention; no ambient always on recording; post wake utterances not stored by default; explicit onboarding consent and a visible indicator; and a design that does not record a third party (an aide, a visitor) without a lawful basis. A device that silently records the household cannot lawfully operate in twelve states. This makes "no retained audio, wake word only" a national design floor, not a per state toggle. Confidence HIGH.

### 4.3 When HIPAA attaches: the channel decides

Restating `shared` section 3 applied to this product. HIPAA does not attach because the product touches health data; it attaches because of who the customer is.

| Channel | HIPAA status | BAA required | Effect on this product | Confidence |
|---|---|---|---|---|
| Direct to consumer (adult child buys for a parent) | Not a covered entity, not a business associate. HIPAA does not attach | No | FTC Health Breach Notification Rule plus MHMDA and state law govern. This is the base case | HIGH |
| Sold through or integrated by a home health agency, hospital, or health plan, handling data on their behalf | Business associate | Yes, before any PHI is exchanged | Full HIPAA Security Rule, BAA, and breach notification under 45 CFR 164.400 to 414 attach. Changes the compliance baseline entirely | HIGH |
| Reimbursed by a payer where the product performs a regulated function for the payer | Likely business associate | Yes | Same as above; analyze per deal | MEDIUM |

Strategic note carried from the concept brief and confirmed against primary sources in `shared` 3.3: a home health agency channel converts the product into a business associate and imposes the full Security Rule from day one. The DTC base case is governed by FTC HBNR (2024 amendments, effective 2024-07-29, `shared` 3.4) plus MHMDA, not by nothing. There is no unregulated state.

### 4.4 PERS emergency dispatch: liability and terms of service (concept specific, verified)

The concept escalates events to a designated contact and, in some designs, to emergency services. That escalation decision carries liability distinct from any privacy question, and it is the reason the concept brief (Phase 4 section 3.5, Phase 7 section 5) says do not build a 24 7 call center, buy it. Findings:

| Finding | Detail | Source | Confidence |
|---|---|---|---|
| A PERS provider that assumes the emergency response function assumes a duty of care | Courts have found subscribers rely on a PERS provider's representation that emergency response will be at least as good as calling 911 directly; a monitoring failure that delayed EMS created a triable duty of care question and summary judgment for the provider was denied | SDM Magazine, "Summary Judgement Denied: A Death Leads to a Cautionary PERS Saga," sdmmag.com, accessed 2026-07-10 (fetch 403 blocked; content via search extraction); Kirschenbaum & Kirschenbaum PERS legal guidance, kirschenbaumesq.com | MEDIUM |
| Monitoring failures during a live event drive the worst outcomes | A documented case: operator called 911 but did not relay that the subscriber was home alone behind locked doors and that contact was lost, delaying treatment by at least 18 minutes; the subscriber died | SDM Magazine (as above), accessed 2026-07-10 | MEDIUM |
| Limitation of liability clauses are standard and generally enforceable, but do not cover gross negligence or willful or wanton misconduct | Providers cap damages (a common cap is a nominal sum, for example $2,500), disclaim liability even for their own ordinary negligence, and require the subscriber to indemnify; under Georgia law such clauses are valid unless they purport to relieve gross negligence or willful or wanton misconduct | Medical Care Alert monitoring agreement, medicalcarealert.com (fetch 403; terms via search extraction), accessed 2026-07-10; SDM Magazine, "Limited Liability Clause Would Have Helped in Wrongful Death Lawsuit," sdmmag.com, accessed 2026-07-10 | MEDIUM |
| PERS is contractually positioned as not a substitute for 911 and not a lifesaving or medical device | Monitoring agreements state the service is not 100 percent reliable, is not a replacement for emergency services, and is not certified for emergency response | GeoArm and Medical Care Alert PERS monitoring terms, geoarm.com and medicalcarealert.com, accessed 2026-07-10 | MEDIUM |

Product consequence: the decision to call emergency services directly should sit with a licensed, insured monitoring center partner operating under its own terms of service and limitation of liability, not with the product company. This aligns the liability with the party that carries the insurance and the enforceable contract, and it keeps the product's own escalation to a notify the designated contact function plus a hard coded red flag layer (Phase 0 feature 18). The product's own terms must mirror the PERS posture: not a substitute for 911, not a medical device, not a guaranteed lifesaving system, with a limitation of liability clause that survives everything short of gross negligence. Note the tension: an automated fall alert with no human in the loop that dispatches 911 on a false positive imports the monitoring center's liability without the monitoring center's insurance, which is why the human verified partner path is preferred. Confidence MEDIUM (secondary sources; primary contract text was 403 blocked to the fetcher, same site side blocking noted in the shared file, and the substance is corroborated across multiple extractions).

---

## 5. THREAT MODEL: A BEDROOM OR BATHROOM SENSOR IS A HIGH VALUE TARGET

A sensing node in a private room of an older adult's home is among the highest value physical targets a consumer device can be. The bedroom and bathroom nodes in this architecture are non camera by design (radar, mat), which removes the image from the target, but a compromised radar or mat still exposes presence, sleep, vitals, and toileting patterns, and a compromised living area camera node is the crown jewel. The architecture's data minimization (no raw modality leaves, no cloud video corpus) means the worst case cloud breach exposes derived metrics, not video, and the worst case device breach exposes one home, not the base. That is the whole point of the edge posture. The controls below make it real.

### 5.1 Controls

| Control | Specification | Purpose | Confidence |
|---|---|---|---|
| Secure boot | Hardware root of trust; boot ROM verifies a signed bootloader, which verifies signed firmware, chain anchored in fuses. A device will not run an unsigned or modified image | Prevents persistent implant and rooted firmware that could add a frame egress path (section 2 path 8) | HIGH (standard practice), MEDIUM (per silicon feasibility, Phase 3) |
| Signed firmware and signed OTA | Every image and every update is signed; the device verifies the signature and rejects unsigned or downgraded images (anti rollback). Reproducible builds so the shipped image is auditable | Closes section 2 path 3; prevents a malicious or coerced update from enabling raw egress | HIGH |
| Encrypted storage | On device storage encrypted AES 256 (`shared` 1.3), keys held in a secure element, not in plaintext on flash. No raw frames, audio, point clouds, or waveforms persisted (section 1) | A stolen device yields no history, only what is in volatile memory | HIGH |
| Key management | Per device identity keys provisioned at manufacture into the secure element; per home or per tenant data keys; envelope encryption with a cloud KMS or HSM; documented rotation; keys never on the edge device in plaintext (`shared` 1.3) | Limits blast radius of a single device compromise to one home | MEDIUM |
| Transport security | TLS 1.3 device to cloud with certificate pinning; mutual authentication so a spoofed cloud cannot harvest a node | Prevents interception and node hijack | HIGH |
| Mesh security | Zigbee or Thread network with encrypted links; the gateway authenticates each node; no unauthenticated node joins | Prevents a rogue node injecting false events or eavesdropping the mesh | MEDIUM |
| Debug lockdown | Secure debug (JTAG, UART) fused off or authenticated before shipment; no production frame or audio egress capability compiled in (section 2 paths 2, 5) | Removes the developer path to raw modality | MEDIUM |
| Patch cadence | An SLA for security patching over signed OTA across the fleet; a device that cannot be patched is the weak point (`shared` section 2) | The edge posture's operational cost; edge is harder to keep patched than cloud | MEDIUM |

### 5.2 The breach scenario, and why the architecture bounds it

| Breach vector | What an attacker gets | Why it is bounded | Notification obligation |
|---|---|---|---|
| Cloud tier breach | Derived metrics, events, transcripts (text), account and consent graph for the whole base | No raw video, audio, point cloud, or waveform exists in the cloud to steal. Encryption to NIST standards renders the store unusable if key material is not also taken, engaging breach safe harbor (`shared` 1.3, 3.4) | DTC: FTC Health Breach Notification Rule (`shared` 3.4). Covered channel: HIPAA breach notification 45 CFR 164.400 to 414 |
| Single device compromise | One home's live derived stream, and at most an in sensor rolling buffer, not a history | Per home blast radius by key design; no persisted raw modality; secure boot limits persistence | Same regime as above, scoped to affected individuals |
| Mesh eavesdrop | Encrypted derived events for one home | Encrypted links; derived not raw | Same |
| Insider or support abuse | Derived data and device health; no video or audio access exists to abuse (section 2 path 5) | The remote video capability is deliberately absent | Same |

The breach story the architecture permits is materially better than a cloud video product: the company cannot leak video it never received, and cannot leak a corpus it never assembled. The residual exposure is a derived metrics breach, which is real and still notifiable, but is not the catastrophic home video exposure the category is known for. Confidence HIGH on the bounding logic, MEDIUM on the per silicon control feasibility (Phase 3).

---

## 6. APPROVED MARKETING CLAIM LANGUAGE

Per `shared` section 7: every privacy claim maps to an enforced control and a proven code path, or it is not said. A privacy promise the architecture does not enforce is an FTC deceptive practice. The table states what this architecture permits.

| Approved claim (permitted because the architecture enforces it) | Enforcing control | Prohibited or high risk version | Why |
|---|---|---|---|
| "There is no camera in your bedroom or bathroom." | Architecture: bathroom radar, bedroom mat or radar, no camera in private rooms | "Total privacy in every room." | Specific and true; absolutes invite a counterexample |
| "Raw video is processed on the device. Raw video is not sent to our servers." | On sensor inference (IMX500 class) plus section 2 paths closed and audited | "Your video never leaves your home." | The absolute cannot survive a crash dump or a compromised device (section 2 verdict); the qualified claim can |
| "Our staff cannot see a live video or a video clip from your home." | No remote video access capability built (section 2 path 5) | "No one can ever access your camera." | True as an absent feature; the absolute overreaches |
| "Encrypted in transit and at rest using AES 256 and TLS 1.3." | Section 5 controls, `shared` 1.3 | "Military grade encryption." | Specific and verifiable versus puffery FTC disfavors |
| "You decide what is captured and what your family can see, and you can change it at any time." | Role and capacity model, granular revocable consent (section 3) | "Fully HIPAA compliant" (in the DTC channel) | HIPAA does not attach DTC; claiming it misleads (`shared` 7) |
| "We do not sell your health data." | No sale, no broker path; MHMDA sale authorization not sought | "We will never share your data with anyone." | Lawful process can compel disclosure; an absolute never is false |
| "Fall detection runs on the device and works even if the internet is down." | T1 local fall path (`phase2_architecture` topology finding 1) | "Guaranteed to detect every fall" or "a lifesaving device" | Detection is not 100 percent reliable; and a lifesaving or medical claim exits the wellness lane and imports PERS liability (section 4.4) |
| "This is a wellness product, not a medical device, and not a replacement for calling 911." | Positioning (framework section 2); PERS posture (section 4.4) | Any implied emergency response guarantee | Mirrors the enforceable PERS terms of service posture |

Rule, restated: if a control does not enforce it and a code path does not prove it, it is not a claim. Confidence HIGH.

---

## Register Entries

Per framework section 9, sources land in `research/registers/sources.md`. This phase does not edit the registers (instructed scope limit). Staged for append below, including the site side 403 blocks noted (same automated fetcher blocking documented in `shared_privacy_security.md`; substance obtained via search extraction, primary URLs cited for the human reader).

### Sources consulted (stage into registers/sources.md)

| Source | Org | URL | Date accessed | Used for | Credibility |
|---|---|---|---|---|---|
| Two Party Consent States for Recording (2026 Guide) | Recording Law | recordinglaw.com/party-two-party-consent-states | 2026-07-10 | Full 12 state all party consent set for the audio assistant | MEDIUM (secondary, current) |
| Two Party Consent States 2026 | World Population Review | worldpopulationreview.com/state-rankings/two-party-consent-states | 2026-07-10 | Corroboration of the 12 state set | LOW (aggregator, corroborating) |
| Surrogate decision makers; priorities; limitations, Ariz. Rev. Stat. 36-3231 | Arizona Legislature | azleg.gov/ars/36/03231.htm | 2026-07-10 | Statutory surrogate priority order (POA agent, then guardian, then next of kin) | HIGH (primary statute) |
| Health Care Surrogate legal questions (Illinois Health Care Surrogate Act) | Illinois Legal Aid Online | illinoislegalaid.org/legal-information/healthcare-surrogate-legal-questions | 2026-07-10 | Illinois surrogate priority order | MEDIUM (secondary, on primary law) |
| Default Surrogate Decision Making | Merck Manual | merckmanuals.com/home/fundamentals/legal-and-ethical-issues/default-surrogate-decision-making | 2026-07-10 | General default surrogate hierarchy and best interest standard | MEDIUM (secondary, authoritative) |
| Summary Judgement Denied: A Death Leads to a Cautionary PERS Saga | SDM Magazine | sdmmag.com/articles/102697 | 2026-07-10 | PERS duty of care; monitoring failure delayed EMS 18 min; summary judgment denied | MEDIUM (trade press; fetch 403, via extraction) |
| Limited Liability Clause Would Have Helped in Wrongful Death Lawsuit | SDM Magazine | sdmmag.com/articles/93960 | 2026-07-10 | Enforceability of limitation of liability clauses in monitoring contracts | MEDIUM (trade press; fetch 403, via extraction) |
| PERS / Medical Alert / Personal Emergency Response | Kirschenbaum & Kirschenbaum | kirschenbaumesq.com/article/pers-medical-alert-personal-emergency-response | 2026-07-10 | PERS provider liability and contract protections | MEDIUM (law firm; fetch 403, via search snippet) |
| Monitoring Agreement | Medical Care Alert | medicalcarealert.com/monitoring-agreement | 2026-07-10 | Liability cap, not a substitute for 911, not a medical device language | MEDIUM (primary vendor terms; fetch 403, via extraction) |
| Medical Alert PERS Alarm Monitoring Services terms | GeoArm Security | geoarm.com/medical-alert-pers-alarm-monitoring-services.html | 2026-07-10 | PERS not 100 percent reliable, not certified emergency response | MEDIUM (vendor) |

### Sources rejected

| Source | Reason rejected |
|---|---|
| Various 911 dispatcher immunity articles (Texas, New Mexico, Alaska wrongful death) | About government 911 dispatcher sovereign immunity, not private PERS provider liability; off point for a commercial monitoring partner |
| Nimitai, ConvertAudioToText, getnextphone call recording law blogs | SEO aggregators; superseded by Recording Law and the primary statutes cited in `shared` 4.4 |
| Dementia end of life surrogate decision academic papers (Oxford, PMC clusters) | Clinical end of life decision literature; not consumer product consent authority |

Note: sdmmag.com, kirschenbaumesq.com, and medicalcarealert.com returned HTTP 403 to the automated fetcher (site side bot blocking, consistent with the pattern documented in `shared_privacy_security.md`, not an organization policy denial). Substance was obtained via search engine extraction of those same pages and corroborated across sources. Direct machine fetch of the full contract and case text is an open item.

## Open Questions

1. Whether a consumer wellness product (no clinical or HIPAA nexus in the DTC channel) may rely on the clinical and statutory surrogate consent hierarchy directly, and the exact enforceable order per launch state. The hierarchy is confirmed; its application to a non clinical consumer monitoring product is untested and belongs in launch state legal review. Does not block the architecture.
2. Whether a gait or whole body movement signature qualifies as a biometric identifier under BIPA or CUBI (carried from `shared` Open Question 2). Likely outside the enumerated list; MHMDA captures it regardless. Do not build a voice template, which would be inside BIPA. Confirm before relying on non applicability.
3. Field enforcement of the governance code paths in section 2 (OTA path 3, debug path 2) depends on process discipline and code review, which no hardware closes. The audit procedure that certifies the "no raw video leaves" claim before marketing uses it is a G2 to G3 deliverable, not settled here.
4. Whether v1 ships any local verification clip buffer at all (section 2 path 6). The safest build has none and confirms falls by radar plus pose fusion. If false positive rate at G2 forces a clip, the claim language must be requalified. Decide at G2 against the measured false positive rate.
5. Per silicon feasibility of secure boot, secure element, and fused debug lockdown on the selected camera and radar nodes is Phase 3, driven by the Phase 4 model and Phase 3 silicon choice.
6. Exact retention windows in section 1.2 are a product policy recommendation set to MHMDA minimization and the BIPA 3 year floor; confirm per launch state before G4.
7. Primary contract and case text for the PERS liability findings (section 4.4) was 403 blocked to the fetcher; verify the SDM cases and the Medical Care Alert terms against primary text before any partner contract negotiation.
8. Whether the emergency dispatch function is outsourced to a licensed monitoring center (recommended) or built. If built, the product imports PERS duty of care and liability without a monitoring center's insurance. Resolve in Phase 4 section 3.5 and Phase 7 section 5.

## Assumptions Made

1. Assumed the architecture is A1 as selected in Phase 2 (mesh, one oblique camera, T4 hybrid, T1 fall path, no in home inference hub in v1). If the A2 all radar fallback is adopted, the camera code paths in section 2 fall away entirely and the "no video leaves" question is moot, which strengthens the privacy posture. Impact if wrong: section 2 narrows, sections 5 and 6 unchanged.
2. Assumed on sensor inference (IMX500 class) is the camera node design, which is what makes section 2 path 1 a hardware property. If the camera node instead exposes frames to an application SoC, the "no raw video leaves" claim weakens from a hardware property to a policy assertion and section 2 paths 4 and 8 reopen. Impact if wrong: the headline privacy claim degrades. Confidence MEDIUM (silicon selection is Phase 3).
3. Assumed DTC as the base channel, with the home health agency and payer channels as variants that attach HIPAA (section 4.3). Impact if wrong (primary channel is a covered entity): HIPAA Security Rule and BAA become baseline from day one, raising compliance cost, which is the safe direction to plan for.
4. Assumed the assistant uses on device wake word with no retained audio and, preferably, on device speech to text. If cloud STT is used, the utterance audio transits and the all party consent and MHMDA analysis tightens. Impact if wrong: audio becomes a transiting sensitive modality, expanding section 2 and section 4.2 scope.
5. Assumed retention windows in section 1.2 as a minimization aligned recommendation, not a legal constant. Impact if wrong: windows adjust per launch state; direction (minimize) holds.
6. Assumed the emergency dispatch function, if offered, is outsourced to a licensed monitoring center partner under its own ToS. Impact if wrong (built in house): the product carries PERS duty of care and liability directly (section 4.4).
7. Legal findings assumed current as of 2026-07-10. The 12 state all party consent set, the surrogate hierarchy, and the PERS liability posture are stable; the two time sensitive items flagged in `shared` (HIPAA Security Rule NPRM, reproductive rule) do not bear on Concept A.

## Confidence Summary

Overall confidence: HIGH on the load bearing conclusions, MEDIUM on the specifics that depend on Phase 3 silicon and G2 field data.

- HIGH: the data flow minimization design (no raw modality leaves, no cloud video corpus); the verdict that "no raw video leaves the device" is provable only in the qualified form and only if the section 2 code paths are closed, with on sensor inference as the decisive control; MHMDA as the binding privacy constraint applied to this product's derived health data; the 12 state all party consent floor forcing a no retained audio, wake word only design nationally; HIPAA attaching through the channel not the product; the breach scenario bounding logic; the approved claim language mapping to enforced controls.
- MEDIUM: the exact surrogate consent order's direct applicability to a non clinical consumer product (open question 1); field enforcement of the governance code paths (open question 3); the PERS liability findings, which rest on trade press and vendor terms that were 403 blocked to the fetcher and corroborated via extraction (section 4.4); per silicon security control feasibility (Phase 3); the specific retention windows.
- LOW / weakest: whether gait qualifies as a biometric identifier (carried open question); whether v1 ships any local verification clip, which if introduced requalifies the headline claim.
- The single load bearing conclusion, HIGH confidence: the architecture makes the strongest privacy claim in the category defensible, because the company cannot leak video it never receives and cannot leak a corpus it never assembles, but only if on sensor inference is the camera design and every code path in section 2 is affirmatively closed and audited before the claim is marketed.
