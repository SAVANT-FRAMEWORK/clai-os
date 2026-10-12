---
ID: P61
Title: Mental Health Triage & Safety System
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P61-G (Global Equity) · P61-AM (Advanced Markets)
---

# P61: Mental Health Triage & Safety System

Abstract: P61 designs AI-assisted mental health triage and safety systems across three operating contexts. The base specification (US crisis infrastructure) administers validated instruments — PHQ-9, GAD-7, PCL-5, AUDIT — assesses suicide and self-harm risk through the Columbia Suicide Severity Rating Scale structure (ideation, plan, intent, means, protective factors), triages to levels of care (outpatient, intensive outpatient, partial hospitalization, inpatient), generates collaborative safety plans, and escalates deterministically to crisis services (988, mobile crisis, emergency department) under duty-to-warn logic. The P61-G Global Equity variant re-founds the same safety spine on cultural psychiatry: SRQ-20 and cross-culturally validated PHQ-9, idioms of distress, war-trauma and gender-based-violence screening, traditional healer collaboration, and WHO mhGAP task-shifting where no hotline or crisis team exists. The P61-AM Advanced Markets variant adapts the spine to Asia-Pacific advanced systems: Asia-validated instruments, hikikomori and exam-stress detection, karoshi prevention, family-mediated distress, and super-aging elderly depression. In every variant the constitutional rule holds: risk is assessed by validated scales and structured protocol, never by model inference alone, and escalation for imminent risk is non-bypassable.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are a Crisis Intervention Specialist who designs AI-assisted mental health triage. You understand PHQ-9, GAD-7, Columbia Suicide Severity Rating Scale, and duty to warn protocols.
ACTION: Design a mental health prompt that:
1.  Administers validated screening instruments (PHQ-9, GAD-7, PCL-5, AUDIT)
2.  Assesses suicide/self-harm risk (ideation, plan, intent, means, protective factors)
3.  Triages to appropriate level of care (outpatient, intensive outpatient, partial hospitalization, inpatient)
4.  Generates safety plans (warning signs, coping strategies, support contacts, safe environment)
5.  Escalates to crisis services (988, mobile crisis, emergency department)
SCOPE:
•  All risk assessments use validated scales, not AI inference alone
•  Suicide risk: assess ideation, plan, intent, means, previous attempts
•  Duty to warn: automatic escalation for imminent risk to self or others
•  Cultural sensitivity: stigma, help-seeking barriers, family involvement
•  Follow-up: automated check-ins, referral tracking, outcome monitoring
CONTEXT:
[INSERT: Setting (primary care, ED, school, workplace), population, available resources, state laws]
EXAMPLES:
Suicide Risk Assessment:
SCREENING: PHQ-9 Question 9 ("Thoughts you would be better off dead...")
Response: "Nearly every day" (3/3)
FOLLOW-UP QUESTIONS (Columbia Scale):
1.  Have you wished you were dead or wished you could go to sleep and not wake up?
Response: "Yes, every day this week"
2.  Have you actually had any thoughts about killing yourself?
Response: "Yes"
3.  Have you thought about how you might do this?
Response: "Yes, I've thought about taking my pills"
4.  Have you had any intention of acting on these thoughts?
Response: "I'm not sure, sometimes I feel like I can't go on"
5.  Have you ever done anything, started to do anything, or prepared to do anything to end your life?
Response: "No, I've never actually tried"
RISK ANALYSIS:
•  Ideation: Present, frequent (daily)
•  Plan: Vague (pills available, no specific plan)
•  Intent: Ambivalent (not definite, but distress high)
•  Means: Available (prescription medications)
•  Protective factors: No previous attempts, some ambivalence, family support (mentioned mother)
•  Risk level: MODERATE-HIGH
TRIAGE DECISION:
•  Not imminent (no definite plan, no immediate intent)
•  Requires same-day evaluation
•  Options:
6.  Mobile crisis team dispatch (if available, <2 hour response)
7.  Urgent outpatient psychiatry (same day)
8.  ED if mobile crisis unavailable and patient unable to contract for safety
SAFETY PLAN (generated with patient):
9.  Warning signs: "When I feel hopeless, can't sleep, isolate from family"
10.  Internal coping: "Listen to music, walk outside, pray"
11.  Social support: "Call my mother (555-0100), call my best friend Maria"
12.  Professional help: "Crisis line 988, my therapist Dr. Chen (555-0200)"
13.  Safe environment: "Give pills to mother to hold, remove sharp objects"
14.  Reason for living: "My mother, my niece's graduation next year"
DOCUMENTATION:
•  Risk assessment completed using Columbia Scale
•  Safety plan developed collaboratively
•  Patient verbalized understanding and agreement
•  Follow-up: Automated check-in in 24 hours, therapist notified
•  Crisis resources provided (988, local mobile crisis: 555-0300)
FORMAT:
•  Validated screening instrument administration
•  Structured risk assessment protocol
•  Triage decision tree
•  Safety plan template
•  Crisis escalation automation
•  Follow-up scheduling

## Architecture

P61 is safety-critical by construction: its outputs include suicide-risk stratification and crisis escalation, so the deployment architecture places every consequential decision on deterministic pathways and confines model inference to language understanding, rapport, and documentation support.

**Deterministic-first safety pathways.** Risk scores are computed deterministically from validated instrument responses (PHQ-9 item 9, GAD-7, PCL-5, AUDIT, Columbia Scale items) using fixed scoring rules — never estimated by the model. The triage decision tree (outpatient / intensive outpatient / partial hospitalization / inpatient / emergency) is encoded as deterministic logic over structured assessment outputs. Escalation for imminent risk to self or others is a non-bypassable deterministic trigger per the CLAI-OS Safety Kernel: the model cannot suppress, defer, or soften an escalation, and duty-to-warn routing fires regardless of model confidence. The model's legitimate roles are eliciting narrative, phrasing follow-up questions with cultural sensitivity, drafting safety-plan language for clinician confirmation, and generating documentation.

**FHIR R4 mapping.** Screening administration maps to Questionnaire / QuestionnaireResponse (PHQ-9, GAD-7, PCL-5, AUDIT); computed risk scores and Columbia assessment findings map to Observation (with LOINC-coded panels where available); the safety plan maps to CarePlan with goal and activity entries; crisis and service referrals map to ServiceRequest and Task; follow-up check-ins map to Communication plus Task scheduling; active risk status maps to Flag on the Patient resource; consent and disclosure authorizations (including family involvement and duty-to-warn notices) map to Consent. All resources carry Provenance records signed by the hosting node.

**Interposition contract.** P61 executes behind the CLAI-OS interposition layer: no model-generated content reaches a patient, family member, or chart without passing the Safety Kernel's deterministic filters (red-flag lexicon, escalation state, prohibited-content rules). Every clinical assertion is emitted inside a Clinical Assertion Wrapper — a cryptographically signed container carrying per-claim epistemic labels (instrument-derived, clinician-entered, model-drafted) so downstream consumers can distinguish scored findings from drafted text.

**Audit and provenance stack.** All escalations, overrides, and safety-plan edits are written to an immutable, Merkle-anchored audit trail; recursive self-audit monitors drift in triage distributions and override patterns; hallucination traceability reconstructs any drafted content contradicted by instrument data; prompt mortality governs version expiry so stale risk logic cannot persist silently.

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Deployment confers no crisis-service status; local clinical governance must adopt and own every pathway.

## Variations

### P61-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P61-G, a cultural psychiatry triage system integrating locally validated tools (SRQ-20, cross-culturally validated PHQ-9 in 30+ languages) and idioms of distress: "thinking too much" (kufungisisa, Shona), "heart distress" (hwa-byung, Korean), "nerves" (nervios, Latin America), and "spirit attack" (various cultures)—recognized as depression, anxiety, or psychotic episodes without dismissal. Trauma-informed systems for conflict zones screen for war trauma, displacement, and gender-based violence, using Narrative Exposure Therapy (NET) validated in refugee settings. Traditional healer collaboration is structured: AI provides referral pathways distinguishing medical causes (psychosis, epilepsy, substance use) from spiritual explanations, enabling parallel treatment rather than replacement. Structural determinants (food insecurity, unemployment, discrimination) are flagged and connected to social services, not just psychiatric medication. Low-resource psychiatry deploys task-shifting: nurses and CHWs deliver WHO mhGAP structured psychological interventions supervised asynchronously by psychiatrist via telehealth.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are a cultural psychiatry and contextual crisis triage architect with field experience in humanitarian mental health, refugee settings, and low-resource district health systems. You design screening, triage, and referral logic that respects local explanatory models of distress while enforcing medical safety nets. You do not pathologize culture, and you do not dismiss spiritual frameworks; you route care.

ACTION: Design a complete cultural psychiatry triage and crisis-response workflow for the deployment context below. Deliver:
1. A screening instrument plan selecting locally validated tools (SRQ-20, cross-culturally validated PHQ-9 in the deployment language) with language, literacy, and administration-mode constraints stated explicitly
2. An idiom-of-distress mapping table: local idiom | language/culture | candidate clinical correlates (depression, anxiety, psychotic episode, none excluded) | required follow-up questions | explicitly prohibited responses (e.g., correcting or dismissing the idiom)
3. A trauma screening module for conflict and displacement settings covering war trauma, displacement, and gender-based violence, with a digital adaptation of Narrative Exposure Therapy referral steps
4. A traditional healer collaboration decision tree routing presentations to medical evaluation (psychosis, epilepsy, substance use) versus parallel traditional-plus-medical care, with referral language that preserves the healer relationship
5. A structural determinants screen (food insecurity, unemployment, discrimination, violence) with referral pathways to social services, sequenced before or alongside any pharmacological recommendation
6. A task-shifting supervision workflow in which nurses and CHWs deliver WHO mhGAP structured psychological interventions, supervised asynchronously by a psychiatrist via telehealth, including escalation triggers and review cadence
7. A crisis response plan for contexts with no hotline and no mobile crisis team: family watch protocols, community volunteer sitters, community elder and religious leader engagement, and transport-to-district-hospital decision criteria

SCOPE:
• All screening logic must be executable offline by a nurse or CHW with a basic device or paper fallback
• Stigma is managed at community level, not only as individual privacy; state the community-level stigma strategy
• Etiology assessment must include war trauma, gender-based violence, economic precarity, and spiritual/ancestral explanatory models
• Suicide risk response must not assume 988-style hotlines; specify the local substitute chain explicitly
• The system recommends referral pathways and task-shifted interventions; it does not diagnose and does not prescribe

CONTEXT:
[INSERT: deployment country/region and languages; conflict or displacement exposure; available cadres (nurses, CHWs, traditional healers); district hospital distance and transport options; existing community and religious structures; connectivity profile]

FORMAT:
• Screening plan as a table: instrument | language | validation population | administrator | cutoff action
• Idiom table as specified in ACTION item 2
• Referral decision tree as indented text or ASCII flow, one branch per line, with terminal actions
• Supervision workflow as a numbered protocol with escalation triggers and asynchronous review SLA
• "Do Not" list: prohibited responses (idiom dismissal, forced hospitalization without capacity assessment, breach of community-level confidentiality)
• "Handoff Summary" template: one paragraph per patient for the supervising psychiatrist, de-identified

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P61-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists in the source; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P61) | Asia-Pacific (P61-AM) |
|-----------|------------------|----------------------|
| Screening Tools | PHQ-9, GAD-7, Columbia | **Asia-validated**: PHQ-9 (validated in Japanese, Korean, Mandarin, Hindi), GAD-7 (validated across Asia), K6 (Japan), SRQ-20 (WHO, valid across Asia), culturally specific: hikikomori (Japan), exam stress/suicide (Korea/China), somatization (all Asia), family conflict-related distress |
| Suicide Risk | 988 hotline | **Asia-specific**: Japan (Lifelink, Yorisoi Hotline), Korea (129, 119), China (400-161-9995), Singapore (SOS), India (Kiran 1800-599-0019). Crisis response: family watch (East Asia), community volunteer (South Asia), ED hold (Singapore/Japan). |
| Crisis Response | Mobile crisis team, ED hold | **Asia-mixed**: Japan = home visit nursing (kaigo) + community mental health center. Korea = 24h community mental health center. Singapore = IMH emergency. Rural China/India = family + village doctor. |
| Stigma | Individual privacy | **Family honor (East/South Asia)**: Mental illness affects marriageability, employment, family reputation. Anonymous digital screening preferred. Group therapy disguised as "stress management workshop." Workplace EAP (high adoption Japan/Korea). |
| Etiology | Biopsychosocial | **Asia-enriched**: Biopsychosocial + academic pressure (Korea/China/Japan), workplace karoshi (death by overwork, Japan), family obligation burden (filial piety), social hierarchy stress (senior-junior dynamics Korea/Japan), hikikomori (social withdrawal, Japan). |

**Extended Actions**
```
P61-AM EXTENDED ACTIONS:
6. Integrate hikikomori screening (Japan): 
   AI recognizes prolonged social withdrawal 
   (>6 months at home, no work/school). 
   Distinct from depression or agoraphobia. 
   Intervention: non-confrontational outreach 
   via family, gradual re-socialization 
   programs, no forced hospitalization.

7. Build academic pressure / exam stress 
   detection (Korea/China): High-stakes 
   university entrance exams (CSAT, Gaokao). 
   AI flags sleep deprivation, anxiety spikes, 
   suicidal ideation during exam seasons. 
   Intervention: school counselor referral, 
   family stress reduction, sleep hygiene.

8. Support workplace mental health (Japan/
   Korea): Karoshi (overwork death) prevention. 
   AI monitors work hours, sleep, and stress 
   markers. Flags "black company" indicators. 
   EAP referral + labor standards board 
   notification if illegal overtime detected.

9. Address family-mediated distress: In 
   East Asia, family conflict (daughter-in-law 
   / mother-in-law, elder care burden) is 
   primary stressor. AI screens for family 
   functioning, not just individual symptoms. 
   Family therapy referral (culturally 
   adapted structural family therapy).

10. Design for elderly depression (super-
    aging Asia): Japan/Korea elderly 
    depression is underdiagnosed (somatized 
    as pain, fatigue). AI screens via 
    somatic symptom cluster + social 
    isolation markers. Home visit nursing 
    (kaigo) referral for isolated elderly.
```

---

Named jurisdiction examples (from the source): Japan (K6 instrument, Lifelink and Yorisoi hotlines, home-visit nursing/kaigo, hikikomori); Korea (129/119 crisis lines, 24-hour community mental health centers, CSAT exam-stress screening); China (400-161-9995, Gaokao stress, family plus village doctor in rural areas); Singapore (SOS, IMH emergency); India (Kiran 1800-599-0019, somatized presentations).

### Regional Adapters

Regional adapters carry the base safety spine into local crisis infrastructure. -AF (Africa): the -G variant is primary — SRQ-20/mhGAP task-shifting, family watch and community elder intervention chains, district-hospital referral by distance. -AR (Arab region): family-mediated intake with privacy-preserving anonymous screening; conflict-zone trauma screening per the -G module; humanitarian coordination (ICRC-class) data rules. -US: the base specification as written — 988, mobile crisis, state duty-to-warn statutes, 42 CFR Part 2 segmentation for substance-use records. APAC: the -AM variant — national crisis lines (Lifelink/Yorisoi, 129/119, 400-161-9995, SOS Singapore, Kiran 1800-599-0019), home-visit nursing (kaigo) referral, workplace EAP integration. Each adapter is a configuration pack (instrument set, crisis-resource map, escalation endpoints, consent language); none relaxes the deterministic escalation contract.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Mental-health PHI; psychotherapy notes receive heightened protection; AUDIT/substance-use records may fall under 42 CFR Part 2 requiring segmented consent; duty-to-warn disclosures under permitted-safety exceptions | US-hosted covered-entity systems; BAAs for any service layer; Part 2 records isolated from general chart |
| GDPR (EU/EEA) | Base-EU deployments; -AM partnerships | Art. 9 special-category (health; beliefs where spiritual-explanatory fields used); explicit consent or care provision condition; DPIA mandatory before deployment | EU/EEA residency; SCCs or adequacy for any transfer; de-identified supervision payloads only |
| NDPR (Nigeria) | -G variant (primary) | Sensitive personal data; explicit consent; verbal/witnessed consent where literacy limited; community stigma programs must never disclose individual results | In-country hosting; cross-border only de-identified |
| Kenya DPA 2019 | -G variant (Kenya deployments) | Sensitive health data; controller/processor registration; consent with plain-language notice; data subject access rights apply to safety plans | Transfer only with adequacy or safeguards; local copy retained |
| India DPDP Act | -G/-AM (India) | Consent plus notice for personal data; health data processed by fiduciaries with security safeguards; Kiran helpline integration is a service mapping, not data sharing | No blanket localization bar in the Act, but sectoral rules and state health-mission agreements may impose residency; confirm per program |
| Brazil LGPD | -G variant (Latin America; nervios idiom contexts) | Sensitive health data; explicit consent or care/tutela condition; ANPD oversight; family involvement documented as authorized sharing | International transfer per ANPD mechanisms; local processing preferred |
| Saudi PDPL | -G/-AM (Arab-region deployments) | Sensitive data; consent-based with care exceptions; strict transfer controls and regulator approval pathways | In-Kingdom hosting default; transfers only under PDPL transfer articles |
| China PIPL | -AM variant (China) | Sensitive personal information (medical health); separate consent; DPIA-equivalent (PIPIA); crisis data sharing with family per local practice must be consent-anchored | Localization for large-volume handlers; CAC security assessment for export |
| Japan APPI | -AM variant (Japan) | Special-care-required personal information; opt-in consent; workplace EAP data flows require explicit employee consent separating employer from clinical content | Cross-border transfer with consent or APPI-equivalent protections |
| Tribal / community consent | -G variant (indigenous and communal settings) | Collective consent (CARE principles, community advisory boards) precedes individual consent; elder/religious-leader intervention chains require community data-handling agreements | Community-governed storage; withdrawal rights honored at community and individual level |

## Methodology

Base: validated screening instrument administration (PHQ-9, GAD-7, PCL-5, AUDIT); structured Columbia Scale risk assessment (ideation, plan, intent, means, protective factors); level-of-care triage decision tree; collaborative safety-plan generation; deterministic crisis escalation (988, mobile crisis, ED); automated follow-up scheduling and referral tracking.

Global Equity (P61-G): idiom-of-distress multilingual NLP classifier; SRQ-20 and local scale integration with validated cutoffs; Narrative Exposure Therapy protocol digital adaptation; traditional healer referral decision tree (medical versus spiritual cause routing with parallel-care option); structural determinant screening (hunger, employment, violence); mhGAP task-shifting supervision workflow with asynchronous psychiatrist review.

Advanced Markets (P61-AM): Asia-validated instrument localization (PHQ-9/GAD-7 Asian-language validations, K6, SRQ-20); hikikomori social-withdrawal screening; exam-season stress and sleep-deprivation detection; workplace overwork (karoshi) monitoring with labor-standards referral; family-functioning screening; super-aging somatized-depression detection with home-visit nursing (kaigo) referral.

## Merits

• Structures suicide-risk assessment on validated instruments and explicit protocol rather than conversational inference, producing auditable, reproducible triage decisions
• Makes crisis escalation deterministic and non-bypassable — the single most important safety property in this domain
• Extends the same safety spine to settings with no hotline (-G: family watch, elders, mhGAP task-shifting) and to Asia-Pacific presentations that Western-only screening misses (-AM: hikikomori, exam stress, karoshi, somatized elderly depression)
• Manages stigma at the level each context requires: individual privacy (base), community-level programming without disclosure (-G), family-honor-preserving anonymous screening (-AM)
• Produces documentation and provenance suitable for clinical governance review in every variant

## Guidance for Use

**Base deployments (US-style infrastructure).** Configure the crisis-resource map first: 988, mobile crisis coverage and response times, ED locations, state duty-to-warn statutes. Do not activate until every escalation endpoint in the prompt resolves to a real, staffed service.

**Global Equity deployments (-G).** Offline-first on facility-controlled hardware; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of patient-identifiable data. Validate instrument cutoffs and idiom mappings with local clinicians, traditional healers, and community representatives before activation. Supervision handoffs de-identified by default.

**Advanced Markets deployments (-AM).** Map national crisis lines and EAP pathways per jurisdiction; confirm instrument validation for the deployment language; workplace and school integrations require explicit consent architectures separating employer/school from clinical content.

**Prerequisites (all variants).** Named accountable clinician owner; tested escalation endpoints; local-language instrument validation; audit trail storage; incident review process.

**Misuse.** Do not use to replace clinical judgment, to autonomously diagnose, to suppress or delay escalation, to conduct surveillance of employees or students, or to infer risk from passive data without validated instruments. The model never contracts for safety with a patient; that is a human clinical act.

**Pairings.** P57/P57-G (Cultural Health Literacy) for patient-facing language; P64/P64-G for equity audit of triage distributions; P58 for FHIR exchange into the host EHR; P67-G for population-level distress surveillance in humanitarian settings.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
