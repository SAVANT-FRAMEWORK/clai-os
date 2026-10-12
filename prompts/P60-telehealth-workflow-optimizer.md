---
ID: P60
Title: Telehealth Workflow Optimizer
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P60-G (Global Equity) · P60-AM (Advanced Markets)
---

# P60: Telehealth Workflow Optimizer

## Abstract

P60 is the virtual care orchestration module of the CLAI-OS P-series, managing the full telehealth arc from modality triage through post-visit follow-up. The base specification is operations-grade virtual care: modality selection by clinical acuity, technology access, and patient preference; pre-visit synthesis aggregating remote monitoring, EHR, pharmacy adherence, and care-gap data into a risk-flagged agenda with suggested orders; real-time documentation support with coding; automated post-visit care plans; and device-data integration (CGM, blood pressure, weight, activity) — demonstrated in its diabetes-hypertension worked example from CGM time-in-range through ICD-10-coded assessment. The variant family carries the same orchestration discipline into radically different bandwidth and device realities. P60-G is the asynchronous engine for 2G environments: sub-1KB text interactions, sub-100KB JPEG-2000 imaging, voice over video, CHW telepresenter protocols, store-and-forward dermatology with 24-hour specialist review, time-shifted batch review across time zones, and reply-coded SMS adherence with CHW home-visit escalation. P60-AM is the messaging-app-native engine for advanced Asia-Pacific markets: WeChat/Line/KakaoTalk-first telehealth, family-mediated proxy access for elderly patients, 4-to-24-hour store-and-forward dermatology, pharmacy-chain e-prescribing integration, and one-tap messaging adherence with family notification. The orchestration discipline is invariant; the channels, payloads, and escalation assets are infrastructure-calibrated.

## The Prompt (Base Specification)

The authentic base prompt body, reproduced verbatim from the author's CLAI-OS P51-P70 specification.

```text
ROLE: You are a Telehealth Operations Engineer who designs virtual care workflows. You understand synchronous video visits, asynchronous e-visits, remote patient monitoring, and digital therapeutics.
ACTION: Design a telehealth prompt that:
1.  Triage patients to appropriate modality (video, phone, async, in-person)
2.  Prepares pre-visit summaries (data aggregation, risk flags, suggested questions)
3.  Supports during-visit documentation (real-time note generation, order suggestions)
4.  Manages post-visit follow-up (care plan, prescription, referral, scheduling)
5.  Integrates remote monitoring data (continuous glucose, BP, weight, activity)
SCOPE:
•  Modality selection based on clinical acuity, technology access, patient preference
•  Pre-visit data from EHR, patient-reported, devices, labs
•  Documentation: structured notes, coding suggestions, quality measure capture
•  Follow-up: automated care plans, patient portal messages, device data review
CONTEXT:
[INSERT: Telehealth platform, patient population, device ecosystem, reimbursement model, state regulations]
EXAMPLES:
Pre-Visit Summary:
PATIENT: Maria Gonzalez, 58, Type 2 Diabetes, Hypertension
VISIT TYPE: Follow-up video visit (15 min scheduled)
PRE-VISIT DATA SYNTHESIS:
Remote Monitoring (last 30 days):
•  Blood pressure: Average 138/86 (last 7 days), trend: stable
•  Alert: 3 readings >140/90 (non-adherence to medication timing?)
•  Weight: 184 lbs → 182 lbs (-2 lbs, appropriate)
•  Steps: Average 4,200/day (goal: 6,000, not meeting)
•  Glucose: CGM data available, TIR 65% (goal: >70%)
EHR Review:
•  Last HbA1c: 7.8% (3 months ago, target <7.0%)
•  Medications: Metformin 1000mg BID, Lisinopril 10mg daily
•  Adherence (pharmacy data): Metformin 85%, Lisinopril 60% (concerning)
•  Care gaps: Missing eye exam (due 6 months ago), missing foot exam
RISK FLAGS:
•  BP trending up + medication non-adherence → Cardiovascular risk
•  HbA1c above target + low TIR → Diabetes progression risk
•  Missing eye exam → Retinopathy risk (undetected)
SUGGESTED VISIT AGENDA:
1.  BP review: Discuss home readings, medication timing
2.  Diabetes management: HbA1c review, CGM data interpretation
3.  Medication adherence: Explore barriers (cost, side effects, complexity)
4.  Preventive care: Schedule eye exam, foot exam
5.  Lifestyle: Step goal, weight maintenance
SUGGESTED ORDERS:
•  HbA1c (overdue)
•  BMP (metformin monitoring, last 6 months ago)
•  Ophthalmology referral (overdue)
•  Diabetes educator referral (adherence support)
DOCUMENTATION TEMPLATE:
[Chief Complaint]: "Follow-up for diabetes and blood pressure"
[History]: Pre-populated with remote monitoring data, adherence issues
[Assessment]:
6.  Type 2 Diabetes mellitus, uncontrolled (E11.9)
7.  Essential hypertension, uncontrolled (I10)
8.  Medication non-adherence (Z91.14)
[Plan]: Pre-populated with suggested orders and care plan
FORMAT:
•  Modality triage algorithm (clinical acuity, tech readiness, preference)
•  Pre-visit summary generator
•  Real-time documentation assistant
•  Post-visit workflow automation
•  Remote monitoring data integration specification
```

## Architecture

P60 is a Specialist Intelligence Layer orchestration module whose interposition contract governs time itself: it decides what must be synchronous, what tolerates asynchrony, and what can never wait. The deterministic-first doctrine draws that line constitutionally — red-flag screening in any intake channel (the base's risk flags, P60-G's SMS triage screen) is deterministic and fires immediate escalation regardless of queue state, implementing the architecture's red-flag latency bound (under 1 second target, 2 seconds maximum tolerable) and the Master Architecture's rule that asynchronous convenience never delays emergency care. Every workflow carries a declared worst-case latency and an emergency bypass; a store-and-forward package without both is constitutionally incomplete.

Modality triage, agenda synthesis, and adherence escalation are deterministic logic over structured inputs — acuity scores, device connectivity, response codes — with model reasoning reserved for summarization, documentation assistance, and agenda drafting within format gates. The adherence workflow's escalation chain (daily reply-coded message → non-response threshold → CHW visit under P60-G, family notification under P60-AM) is deterministic state-machine logic with every transition logged. FHIR R4 mapping: virtual encounters are Encounter resources with modality-type coding; pre-visit synthesis aggregates Observation (device metrics, labs), MedicationRequest with adherence extensions, and Flag resources for risk; documentation emits Composition and Condition (coded, as in the base's E11.9/I10/Z91.14 example); follow-up emits CarePlan, ServiceRequest, Communication, and Appointment resources; device data arrives as DeviceMetric-linked Observations. Queue persistence follows the Federated Synchronization Map's delayed-reconciliation pattern — durable, retryable messages rather than live sessions — and every message transition emits AuditEvents. The artifact is C0 informational: it coordinates care logistics and documentation; clinical decisions remain with the reviewing clinician.

## Variations

### P60-G — Global Equity Variant (low-resource, offline-first)

Author's variant abstract:

> We present P60-G, an asynchronous virtual care system optimized for <1KB text interactions, <100KB compressed images, and voice notes preferred over video. The architecture includes CHW-mediated telehealth: the CHW holds the tablet, video-calls the city specialist while the patient is present, acting as "telepresenter"—describing exam findings, translating, and managing camera angles. Store-and-forward dermatology enables 85% of skin condition diagnosis via smartphone photo uploaded async for specialist review within 24 hours. Time-shifted care allows a Nairobi clinician to review rural Kenya cases during city daytime hours; no synchronous appointment required. Medication adherence telehealth sends daily SMS: "Did you take your medication? Reply 1 for yes, 2 for no." Non-response triggers CHW home visit. All interactions are optimized for 2G: text-based triage, compressed imaging, voice-dominant communication.

Variant prompt compiled from the author's Global Equity Extension specification.

```text
ROLE:
You are an asynchronous care coordinator for low-bandwidth environments
within CLAI-OS. You design and run virtual care that works on 2G networks,
feature phones, and mismatched schedules — where 4G/5G will not exist for
a decade. Your unit of design is the store-and-forward interaction, not
the video call.

ACTION:
Given a virtual care request (triage, specialist consult, follow-up,
adherence support), select and execute the appropriate asynchronous
pattern:

1. CHANNEL SELECTION (BANDWIDTH-FIRST)
   - Budget: text interactions <1KB; images compressed to <100KB
     (JPEG-2000 pipeline); voice notes preferred over video; video only
     where a CHW-mediated link exists.
   - For each encounter, state the channel, its payload budget, and the
     fallback when even that channel fails.

2. TEXT-BASED TRIAGE
   - Structure 2G-compatible triage: structured symptom reporting via
     SMS/USSD-style interaction, with deterministic red-flag screening
     that escalates immediately regardless of review queue state.
   - Output a triage disposition with timeframe.

3. CHW-MEDIATED TELEHEALTH (TELEPRESENTER PROTOCOL)
   - When a specialist link is possible: the CHW holds the tablet and
     video-calls the specialist while the patient is present, acting as
     telepresenter — describing exam findings, translating, managing
     camera angles.
   - Provide the CHW telepresenter script: what to report, in what
     order, and which examination maneuvers to perform on instruction.

4. STORE-AND-FORWARD SPECIALTY REVIEW
   - Dermatology: smartphone photo (compressed <100KB) uploaded
     asynchronously for specialist review within 24 hours; 85% of skin
     conditions are diagnosable by this route. State image adequacy
     criteria and re-capture instructions.
   - Time-shifted care: batch cases for clinician review during the
     reviewing clinician's working hours (e.g., a Nairobi clinician
     reviewing rural cases in city daytime); no synchronous appointment
     is required. Apply time-zone optimization for batch review.

5. ADHERENCE TELEHEALTH & ESCALATION
   - Daily SMS: "Did you take your medication? Reply 1 for yes, 2 for
     no."
   - Non-response triggers a CHW home visit per the escalation logic;
     define the non-response threshold, the visit trigger, and the
     clinician notification path. Target: 90%+ adherence via SMS + CHW
     escalation.

SCOPE:
- Care coordination and communication architecture; diagnosis and
  treatment decisions rest with the reviewing clinician.
- Every asynchronous workflow must define its worst-case latency and its
  emergency bypass; red flags never wait in a store-and-forward queue.
- If the patient's only channel is a feature phone, the entire workflow
  must complete on SMS/USSD — design for it explicitly.

CONTEXT:
[INSERT: network profile (2G/3G coverage), patient device mix, CHW
availability and territory, specialist pool and time zones, condition
mix, existing SMS/USSD gateway]

FORMAT:
1. CHANNEL PLAN — encounter type | channel | payload budget | fallback
2. TRIAGE PROTOCOL — structured questions | red-flag screen | dispositions
3. TELEPRESENTER SCRIPT — CHW reporting sequence | exam maneuvers
4. STORE-AND-FORWARD PACKAGE — capture spec | compression | review SLA |
   adequacy criteria
5. ADHERENCE WORKFLOW — message spec | response coding | escalation
   logic | visit trigger
6. QUEUE & LATENCY TABLE — workflow | worst-case latency | emergency
   bypass
```

### P60-AM — Advanced Markets Variant (high-resource, US & Asia-Pacific)

The author's Advanced Markets Extension content for this module — the What Changes matrix and the EXTENDED ACTIONS block — reproduced below. The source extension provides no named jurisdiction worked example for this module; none is invented here. No separate AM prompt body is fabricated; the extension defines deltas against the base specification.

#### What Changes
| Dimension | US-Centric (P60) | Asia-Pacific (P60-AM) |
|-----------|------------------|----------------------|
| Modality | Video (synchronous) | **Asia-dominant**: Messaging app telehealth (WeChat China, Line Japan/Thailand, KakaoTalk Korea, WhatsApp India/Singapore). Store-and-forward (photo + text). AI chatbots for triage. Video only for specialist consults. |
| Pre-Visit Data | EHR + devices | **Asia-specific**: Wearables (Xiaomi, Huawei, Samsung Galaxy Watch — high penetration East Asia). Home BP monitors (Omron dominates Japan). Continuous glucose monitors (FreeStyle Libre growing in Japan/Korea). WeChat health mini-program self-reported data. |
| During Visit | Real-time video | **Mixed**: Synchronous video for specialist (dermatology, psychiatry). Async text for follow-up. Family-mediated video (adult child holds phone for elderly parent in Japan/Korea). |
| Post-Visit | EHR write-back | **Messaging app care plans**: WeChat/Line/KakaoTalk care plan cards. Medication reminders via messaging. Pharmacy pre-ordering (Japan Matsumoto Kiyoshi, China Alibaba Health). |
| Remote Monitoring | Dexcom, smart scale | **Asia-adapted**: Smartphone-connected BP (Omron, Xiaomi), non-invasive glucose (optical sensors in development, Japan/China), smart toilet health metrics (Toto, Japan), fall detection (Apple Watch + Samsung, high elderly adoption East Asia). |

#### New Action Items
```
P60-AM EXTENDED ACTIONS:
6. Optimize for messaging-app-first telehealth:
   In China, WeChat is primary health
   communication. In Japan, Line is dominant.
   AI delivers triage, care plans, and
   reminders via these platforms. Video is
   secondary, initiated from messaging
   thread.

7. Build family-mediated elderly telehealth:
   Adult child (40-60 years old, tech
   proficient) manages elderly parent's
   (70-90 years old) telehealth account.
   AI recognizes proxy access with
   patient consent. Family receives
   simplified summaries.

8. Implement store-and-forward dermatology:
   High smartphone camera quality in Asia
   enables 90%+ diagnostic accuracy for
   skin conditions. Patient photographs
   lesion, uploads via messaging app.
   Dermatologist reviews within 4 hours
   (Japan/Korea) or 24 hours (SE Asia).

9. Support pharmacy integration:
   Japan: Matsumoto Kiyoshi / Sugi Pharmacy
   e-prescribing. China: Alibaba Health /
   JD Health same-day delivery. Singapore:
   Guardian/Watsons integration. AI sends
   prescription directly to patient's
   preferred pharmacy chain.

10. Add medication adherence via messaging:
    Daily Line/WeChat/Kakao "Did you take
    your medication?" with one-tap reply.
    Non-response triggers family notification
    (East Asia) or CHW visit (South Asia).
```

---

### Regional adapters

Regional adapters configure channels, device ecosystems, and escalation assets. The -AF adapter activates the P60-G asynchronous stack: SMS/USSD triage, CHW telepresenter protocols, and community health worker home-visit escalation. The -AR adapter adds humanitarian operation: solar-powered queue nodes, camp-based telepresenter kiosks, and cross-border continuity via seed-phrase identity. The -US adapter retains the base video-and-RPM posture with state telehealth regulation configuration and tribal broadband realities addressed through the async fallback. The APAC adapter applies P60-AM: WeChat/Line/KakaoTalk/WhatsApp-first channels, family-mediated proxy access, Omron/Xiaomi/Huawei device integration, pharmacy-chain e-prescribing, and store-and-forward dermatology SLAs. The EU adapter applies GDPR-partitioned telehealth with national telemedicine act compliance; the Latin America adapter applies WhatsApp-dominant async patterns under LGPD residency.

## Jurisdiction Matrix

| Regime | Variant applicability | De-identification / consent posture | Residency constraint |
|---|---|---|---|
| HIPAA (US) | Base (native) · P60-AM (US node) | State telehealth regulation; platform BAAs; documented virtual encounters | US processing; 6-year encounter retention |
| GDPR (EU/EEA) | P60-G · -EU adapter | National telemedicine acts; GDPR-partitioned encounter data | EU residency |
| NDPR (Nigeria) | P60-G (native) | SMS/USSD minimum-data channels; encrypted queue for clinical detail; CHW telepresenter consent | In-country queue nodes; offline-first |
| Kenya DPA 2019 | P60-G (native) | Time-shifted review (Nairobi-rural pattern); SMS adherence webhooks | Kenyan residency |
| India DPDP | P60-G · P60-AM | WhatsApp-dominant channels; eSanjeevani alignment; ASHA/ANM escalation | MeitY-empanelled infrastructure |
| Brazil LGPD | P60-G (native) | WhatsApp async patterns under LGPD | Brazilian residency |
| Saudi PDPL | P60-G (native) | Gender-concordant telehealth options; family-mediated encounters with consent | Saudi residency |
| China PIPL | P60-AM (native) | WeChat-first telehealth; Alibaba Health/JD Health pharmacy integration | Onshore; messaging data localized |
| Japan APPI | P60-AM (native) | Line-dominant channels; family-mediated elderly proxy with consent; Matsumoto Kiyoshi/Sugi e-prescribing; 4-hour derm review SLA | Domestic processing |
| Tribal / community consent regimes | P60-G (native) | CHW-mediated encounters under community norms; family notification only with patient consent | Community enclave queues per P51 |

## Methodology

The base methodology is workflow systems engineering: acuity-tech-preference triage matrices, multi-source pre-visit synthesis (devices, EHR, pharmacy fills, care gaps), agenda and order suggestion with coding support, and closed-loop follow-up automation — demonstrated from CGM time-in-range analysis to ICD-10-coded documentation. P60-G re-founds the method on bandwidth reality: durable message-queue architecture (RabbitMQ-class), JPEG-2000 compression under 100KB, standardized CHW telepresenter protocols, store-and-forward dermatology validated at 85% diagnostic coverage, SMS adherence webhooks with deterministic escalation, and time-zone-optimized batch review. P60-AM re-founds it on platform reality: messaging-app-native channels, consented proxy state machines, 90%+ smartphone dermatology accuracy, and pharmacy API integration. The invariant: every workflow declares its latency class, every red flag bypasses every queue, and every non-response has a deterministic human consequence.

## Merits

- Complete virtual-care arc — triage, preparation, documentation, follow-up, monitoring — with demonstrated synthesis quality (adherence inference from BP patterns, CGM TIR against targets) (base).
- Documentation efficiency with coding-grade structure and quality-measure capture (base).
- Specialist dermatology without a dermatologist present; 90%+ medication adherence via SMS with CHW escalation; elimination of rural travel for synchronous appointments; full function on 2G networks that will persist for a decade or more (P60-G).
- Telehealth meeting patients on the messaging platforms they already use; elderly access solved through consented family mediation; same-day pharmacy fulfillment integration; 4-hour specialist review achievable in high-resource Asian markets (P60-AM).

## Guidance for Use

Deploy the base P60 within telehealth programs of integrated health systems: platform APIs connected, device data flowing, state telehealth regulations configured, and documentation reviewed by the clinician of record. Deploy P60-G in low-bandwidth Global South programs: queue, compression, and SMS/USSD gateway configured for local network reality; CHW telepresenters trained; specialist review pool committed to stated SLAs; emergency bypass protocol drilled. Deploy P60-AM in Asia-Pacific markets: messaging-platform channels consented and configured, proxy access state machines reviewed by compliance, and pharmacy integrations contracted.

Prerequisites: a declared channel inventory per population, an emergency bypass protocol, and clinician ownership of all clinical content. Misuse: do not let red-flag cases wait in asynchronous queues, send clinical detail over SMS beyond minimum workflow coding, promise review latencies the specialist pool cannot meet, or route patient messages and images through closed telehealth clouds. Pairings: P57 crafts the patient-facing messaging; P55 receives adherence signals for regimen review; P52 receives store-and-forward clinical questions; P58 persists encounters; P59 consumes aggregate telehealth utilization; P51 governs cross-border specialist review as data transfer.

---
C0 informational classification; confers no clinical, legal, financial, or safety authority.
