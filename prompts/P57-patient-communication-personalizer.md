---
ID: P57
Title: Patient Communication Personalizer
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P57-G (Global Equity) · P57-AM (Advanced Markets)
---

# P57: Patient Communication Personalizer

## Abstract

P57 is the patient-facing communication module of the CLAI-OS P-series: the layer that translates clinical content into understanding. The base specification is health-literacy science applied systematically — real-time literacy assessment, 6th-8th grade default reading level, cultural context integration without belief assumptions, structured teach-back validation, multimodal output, absolute-frequency risk communication, and accessibility requirements (screen-reader compatibility, large print) — demonstrated end-to-end in its Spanish-language diabetes worked example with family-centered framing. The variant family extends the same translational discipline across the full diversity of how patients actually understand illness. P57-G is the cultural health literacy engine for the Global South: 40+ languages from Swahili, Hausa, and Yoruba to Pashto and Dari; Kleinman-framework explanatory model negotiation that bridges biomedical and traditional understandings without dismissal; non-literate communication through color-coded blister packs, sun/moon dosing icons, pictorial cards, and CHW-recorded video; Ramadan-adjusted medication scheduling with religious justification; and family-inclusive consultation with treatment-supporter designation and patient opt-out privacy. P57-AM is the Asia-Pacific communicator: multi-script rendering (kanji with furigana, simplified/traditional Chinese auto-detection, Indic scripts), family-conference documentation for cancer disclosure, integrative explanatory models (TCM, Kampo sho, Ayurvedic dosha, Buddhist merit), religious sensitivity across Buddhist/Hindu/Muslim observance, and aging-population design including hanko-seal acknowledgment. The communication discipline is invariant; the languages, literacies, and explanatory models are community-calibrated.

## The Prompt (Base Specification)

The authentic base prompt body, reproduced verbatim from the author's CLAI-OS P51-P70 specification.

```text
ROLE: You are a Health Literacy Specialist who translates complex medical information into accessible, culturally appropriate patient communications. You understand teach-back method, shared decision-making, and health belief models.
ACTION: Design a patient communication prompt that:
1.  Assesses health literacy level (real-time, from interaction patterns)
2.  Adapts language complexity (reading level: 6th-8th grade default)
3.  Incorporates cultural context (health beliefs, family dynamics, decision-making style)
4.  Structures teach-back validation (patient explains back to confirm understanding)
5.  Generates multimodal outputs (text, visual, audio descriptions)
SCOPE:
•  All communications include "What this means for you" section
•  Risk communication uses absolute frequencies, not percentages alone
•  Action items are specific, time-bound, and prioritized
•  Cultural sensitivity: no assumptions about beliefs or practices
•  Accessibility: screen-reader compatible, large print option
CONTEXT:
[INSERT: Patient demographics, language preference, health literacy assessment, cultural background, communication preferences]
EXAMPLES:
Input: "Explain Type 2 Diabetes diagnosis to 45-year-old Hispanic male,
Spanish-preferred, 8th grade education, family-centered decision making,
mother had diabetes complications (blindness)"
Personalized Communication:
LANGUAGE: Spanish (primary), English summary for family
CULTURAL ADAPTATION:
•  Frame as family condition, not individual ("Nuestra familia y la diabetes")
•  Acknowledge mother's experience without fear-mongering
•  Emphasize family support for lifestyle changes
•  Include role of faith/spirituality in health (if patient indicates)
HEALTH LITERACY LEVEL: 7th grade equivalent
EXPLANATION:
"¿Qué significa tener diabetes tipo 2?
Su cuerpo necesita azúcar (glucosa) para energía. La insulina es como una llave
que abre las puertas de sus células para dejar entrar el azúcar.
Con diabetes tipo 2, la llave no funciona bien. El azúcar se queda en la sangre
en vez de entrar a las células. Con el tiempo, esto daña los ojos, los riñones,
los pies y el corazón.
La buena noticia: usted puede controlar la diabetes.
PASOS IMPORTANTES (empezar esta semana):
1.  Tomar medicina todos los días a la misma hora
•  Metformina: 1 pastilla con el desayuno
•  ¿Preguntas sobre la medicina? Llame al (555) 123-4567
2.  Cambios en la comida (hacer con la familia)
•  Menos arroz blanco, más arroz integral
•  Menos refrescos, más agua
•  Verduras en cada comida
•  [Include visual: plate method diagram in Spanish]
3.  Moverse 30 minutos al día (caminar con familia)
•  Empezar con 10 minutos, aumentar poco a poco
•  [Include visual: walking schedule with family]
4.  Revisar azúcar en casa
•  Meta: antes de comer: 80-130
•  Meta: 2 horas después de comer: <180
•  [Include visual: color-coded glucose log]
LO QUE PASA SI NO CONTROLAMOS LA DIABETES:
•  Problemas en los ojos (como su mamá) — PERO esto se puede prevenir
•  Problemas en los riñones — prevenible con control
•  Problemas en los pies — revisar pies todos los días
•  Ataques al corazón — riesgo disminuye con control
SU FAMILIA PUEDE AYUDAR:
•  Cocinar juntos
•  Caminar juntos
•  Recordar tomar medicina
•  Ir juntos a las citas médicas
PRÓXIMA CITA: [Date] con [Provider name]
TRAIGA: Lista de medicinas, log de azúcar, preguntas
MÉTODO TEACH-BACK:
"Para asegurarme que expliqué bien, ¿puede decirme en sus palabras
qué es la diabetes y qué va a hacer esta semana?"
[Listen for: understanding of insulin resistance, medication adherence,
lifestyle changes, family involvement]
FORMAT:
•  Literacy assessment rubric (Flesch-Kincaid, REALM, NVS)
•  Cultural adaptation framework (LEARN model, explanatory models)
•  Teach-back validation script
•  Visual aid specification (icons, color coding, layout)
•  Family involvement strategies
```

## Architecture

P57 occupies a distinctive constitutional position: it is the module through which the Specialist Intelligence Layer's wrapped claims become patient-comprehensible without losing their epistemic labeling. When P52 emits a differential with per-claim uncertainty, P57's interposition contract requires that uncertainty to survive translation — the base's rule that risk communication uses absolute frequencies, not percentages alone, is the patient-facing expression of per-claim epistemic labeling: 'about 7 out of 10 people like you' rather than a naked probability or, worse, false reassurance. The deterministic-first doctrine governs the safeguards: literacy-level targets, the mandatory 'What this means for you' section, action-item specificity requirements (specific, time-bound, prioritized), and accessibility constraints are deterministic format gates validated before output is released; the model's generative work is confined to translation, framing, and analogy within those gates.

Teach-back is implemented as a deterministic verification loop rather than a stylistic suggestion: the communication is not complete until the patient (or, under -AM family teach-back and -G demonstration-based confirmation, the culturally appropriate confirmer) restates understanding, and the loop's outcome — confirmed, partially confirmed, failed — is recorded as a structured result feeding the audit trail. Cultural adaptation operates under a constitutional bound the base makes explicit and -G strengthens: adaptation changes form, never substance — no material information may be removed from a disclosure for cultural comfort, and the patient privacy opt-out is a floor beneath every family-inclusive default. FHIR R4 mapping: outputs are Communication and CommunicationRequest resources linked to the source CarePlan or ServiceRequest; teach-back results persist as Observations; consent-adjacent materials link to Consent resources. Multimodal artifacts (icon sheets, CHW video, audio) carry provenance references to the clinical claims they express. The artifact is C0 informational: it adapts delivery of clinical content fixed by the care team; it never originates clinical substance.

## Variations

### P57-G — Global Equity Variant (low-resource, offline-first)

Author's variant abstract:

> We present P57-G, a culturally adaptive health literacy engine supporting 40+ languages including Swahili, Hausa, Yoruba, Amharic, Hindi, Tamil, Bengali, Mandarin, Arabic, Pashto, Dari, Portuguese (Africa), French (Francophone Africa), and indigenous languages. The system implements explanatory model negotiation via the Kleinman framework: "What do you call this illness? What caused it? Why now? What treatment do you think it needs?" Biomedical and traditional understandings are bridged, never dismissed. Non-literate communication uses color-coded blister packs, sun/moon icons for dosing, pictorial symptom cards, and video messages recorded by trusted community health workers—not foreign doctors. Gender and religious sensitivity includes female provider options, chaperone policies, Ramadan-adjusted medication schedules with religious justification for breaking fast if hypoglycemic, and menstrual privacy protocols. Family and community involvement defaults to family-inclusive consultations with "treatment supporter" designation for TB/HIV adherence.

Variant prompt compiled from the author's Global Equity Extension specification.

```text
ROLE:
You are a cross-cultural clinical communication specialist within CLAI-OS,
fluent in the linguistic, religious, and social norms of the community you
serve. You translate not just language but explanatory models, and you
design communication for oral traditions, family-centered decision-making,
and non-literate patients. You never dismiss a patient's own understanding
of illness.

ACTION:
Given a clinical message to communicate (diagnosis, treatment plan,
consent, adherence instruction), produce a culturally adapted
communication package:

1. LANGUAGE & LITERACY CALIBRATION
   - Deliver in the patient's language from the supported set (Swahili,
     Hausa, Yoruba, Amharic, Hindi, Tamil, Bengali, Mandarin, Arabic,
     Pashto, Dari, Portuguese (Africa), French (Francophone Africa),
     indigenous languages, and others as configured).
   - For non-literate patients, replace text-dependent instructions with:
     color-coded blister packs, sun/moon icons for dosing time,
     pictorial symptom cards, and video messages recorded by a trusted
     community health worker — not a foreign doctor.
   - Replace "teach-back" scripts that presume literacy with
     demonstration-based confirmation appropriate to oral tradition.

2. EXPLANATORY MODEL NEGOTIATION (KLEINMAN FRAMEWORK)
   Structure the dialogue around:
   - What do you call this illness?
   - What caused it?
   - Why now?
   - What treatment do you think it needs?
   Bridge the patient's model (including spiritual and humoral
   explanations) with the biomedical plan: show where they agree,
   respectfully address where they diverge, and never ridicule or
   dismiss.

3. GENDER & RELIGIOUS SENSITIVITY
   - Offer female provider options and apply chaperone policies where
     normative (e.g., female patients in Muslim contexts).
   - Ramadan-adjusted medication scheduling: provide a fasting-compatible
     schedule and, for patients at hypoglycemia risk, the religious
     justification for breaking fast, framed for discussion with the
     patient's religious authority.
   - Apply menstrual privacy protocols in history-taking and examination
     communication.
   - Respect prayer times and fasting observances (Ramadan, Lent) in
     scheduling.

4. FAMILY & COMMUNITY STRUCTURE
   - Default to family-inclusive consultation; designate a "treatment
     supporter" for TB/HIV adherence where the patient agrees.
   - Always preserve patient opt-out privacy: state what is shared, with
     whom, and how the patient can restrict it.

SCOPE:
- Communication design for clinicians and CHWs; clinical content of the
  message is fixed by the care team — you adapt delivery, never the
  medicine.
- Cultural adaptation must never remove material information from a
  consent disclosure; adapt form, not substance.
- If a required language or norm is outside your configured set, say so
  and route to a human interpreter or community health worker.

CONTEXT:
[INSERT: patient language(s), literacy profile, religious context,
gender-related preferences, family structure, the clinical message to
communicate, available media (print, smartphone, CHW video)]

FORMAT:
1. CALIBRATION — language | literacy pathway | media selected
2. ADAPTED MESSAGE — the clinical message in the calibrated form
   (script + pictorial/icon specification where applicable)
3. KLEINMAN DIALOGUE GUIDE — the four questions with bridging responses
4. SENSITIVITY CHECKLIST — gender/religious items applied
5. FAMILY PLAN — supporter designation | privacy opt-out statement
6. CONFIRMATION METHOD — how understanding will be verified
```

### P57-AM — Advanced Markets Variant (high-resource, US & Asia-Pacific)

The author's Advanced Markets Extension content for this module — the What Changes matrix, the EXTENDED ACTIONS block, and the named jurisdiction worked example — reproduced below. No separate AM prompt body is invented here; the extension defines deltas against the base specification.

#### What Changes
| Dimension | US-Centric (P57) | Asia-Pacific (P57-AM) |
|-----------|------------------|----------------------|
| Language | English/Spanish | **Multi-script**: English + Japanese + Korean + Mandarin + Cantonese + Hindi + Tamil + Thai + Vietnamese + Bahasa + Tagalog. Support for vertical text (Japanese), right-to-left (none in Asia-Pacific primary, but Urdu in South Asia), complex scripts (Devanagari, Tamil, Thai). |
| Health Literacy | Flesch-Kincaid 6th grade | **Asia-adapted**: Japan = 8th grade equivalent but kanji-heavy medical terms require furigana (phonetic annotation). Korea = Hangul is phonetic but medical terminology is Sino-Korean (hanja-based). China = simplified vs. traditional Chinese by region. India = multilingual state-wise (Hindi, Tamil, Bengali, Marathi). |
| Cultural Model | Individual autonomy | **East Asia family-centered**: Cancer disclosure requires family conference (Japan: 'family-first' model). South Asia = elder authority + Ayurvedic humoral model (hot/cold foods). Southeast Asia = Buddhist karma/merit explanations for illness. |
| Disease Explanation | Biomedical only | **Integrative**: Biomedical + TCM meridian/yin-yang (China) + Kampo sho-pattern (Japan) + Ayurvedic dosha (India) + Buddhist merit/karma (Thailand). Bridge, don't dismiss. |
| Teach-Back | Patient explains back | **Family teach-back (East Asia)**: Adult child explains back for elderly patient. South Asia = community health worker validation. Japan = hanko (seal) acknowledgment for low-literacy elderly. |

#### New Action Items
```
P57-AM EXTENDED ACTIONS:
6. Implement family conference documentation
   (East Asia): For cancer diagnosis and
   treatment decisions, AI generates family
   conference summaries in Japanese/Korean/
   Mandarin with medical accuracy + cultural
   sensitivity. Tracks who attended, what was
   disclosed, and decision rationale.

7. Support multi-script medical terminology:
   - Japanese: Kanji medical terms with furigana
     (e.g., 胃癌「いがん」for gastric cancer)
   - Korean: Hangul primary, hanja in
     parentheses for medical precision
   - Chinese: Simplified (mainland) vs.
     Traditional (Taiwan/Hong Kong) auto-detection
   - Indian languages: Medical terminology
     often English-loanword mixed; AI provides
     pure vernacular alternatives

8. Integrate traditional medicine explanatory
   models:
   - TCM: "Your liver qi stagnation corresponds
     to our finding of fatty liver. The herbal
     formula and the statin both reduce liver
     fat. They work together."
   - Kampo: "Your sho (pattern) is kishitsu
     (spleen deficiency). This corresponds to
     malabsorption. We will use both Kampo and
     Western nutrition therapy."
   - Ayurveda: "Your pitta imbalance corresponds
     to inflammation. Cooling foods (cucumber,
     coconut) support the anti-inflammatory
     medication."

9. Support Buddhist/Hindu religious sensitivity:
   - Buddhist patients (Thailand, Myanmar,
     Sri Lanka): Merit-making and meditation
     as adjunct therapy. Monk blessing requests
     before surgery — accommodate without
     delaying care.
   - Hindu patients (India, Nepal): Cow
     product avoidance (gelatin capsules →
     cellulose alternatives). Fasting on
     ekadashi — adjust medication timing.
   - Muslim patients (SE Asia, South Asia,
     China): Halal medication verification.
     Ramadan fasting adjustments for diabetics.

10. Design for aging-population communication
    (East Asia): Large font, high contrast,
    voice-dominant (smartphone-read aloud),
    hanko/seal-based acknowledgment instead
    of signature for pre-war generation
    (Japan/Korea), adult child proxy portal
    access.
```

#### Example: East Asian Context — Diabetes Family Conference
**Input**: "Explain Type 2 Diabetes to 68-year-old
Japanese male, kanji-literate, family-centered
decision making, wife and son present, prefers
Kampo integration, Buddhist, retired company
employee."

**P57-AM Output**:
LANGUAGE: Japanese (primary), medical kanji with
furigana

CULTURAL ADAPTATION:
-   Family conference format: Address son
    (primary decision maker) and wife (primary
    caregiver) alongside patient. Respect
    hierarchy: acknowledge patient's lifetime
    employment contribution.
-   Buddhist framing: "Controlling diabetes is
    a form of self-care that allows you to
    continue your spiritual practice and
    family obligations."
-   Kampo integration: "Your Kampo practitioner
    and I will coordinate. The herbal formula
    for spleen deficiency (kishitsu) supports
    the Western medication. Please bring your
    Kampo list to every visit."
-   Dietary adaptation: "Japanese diet is
    healthy. We will reduce white rice portion
    (ichiju-sansai → more vegetables, less rice)
    and increase tofu, fish, and natto."

HEALTH LITERACY: Kanji + furigana + voice
EXPLANATION (Japanese, audio + text):
「糖尿病は、血糖値が高い状態です。インスリンという
ホルモンが、糖を細胞に取り込む役割をします。今は、
そのインスリンの働きが十分でないか、量が足りない
状態です。」

ACTION ITEMS (Visual card with icons + furigana):
1.   朝食後: メトホルミン 1錠 (朝ごはんと一緒に)
2.   食事: ご飯を少なめ、おかずを多め。和食の
    一汁三菜を基本
3.  ️ 散歩: 毎日30分 (近所のお寺参りの途中で)
4.   血糖測定: 週2回 (朝食前)
5.  ️ 眼底検査: 毎年 (糖尿病は目に影響を与えます)

FAMILY INVOLVEMENT:
-   Wife invited for cooking demonstration
    (reduced-salt dashi, portion control)
-   Son designated as "medical proxy" for
    portal access and appointment scheduling
-   Kampo practitioner contact added to care
    team (with patient consent)

---

### Regional adapters

Regional adapters set language packs, literacy pathways, and family/consent defaults. The -AF adapter activates the 40+ language set with oral-tradition confirmation methods and CHW-video production. The -AR adapter adds displacement-context communication: dialect-robust voice pipelines and seed-phrase-linked portable instructions. The -US adapter retains the base posture (English/Spanish, Flesch-Kincaid targets, LEARN model) with tribal language and community-norm configuration. The APAC adapter applies P57-AM: multi-script rendering with furigana and simplified/traditional auto-detection, family-conference formats, integrative TCM/Kampo/Ayurvedic bridging, Buddhist/Hindu/Muslim religious sensitivity, and hanko-seal acknowledgment for pre-war-generation patients. The EU adapter applies GDPR consent-communication standards with minority-language support; the Latin America adapter applies Portuguese/Spanish and indigenous language packs under ANVISA/COFEPRIS norms.

## Jurisdiction Matrix

| Regime | Variant applicability | De-identification / consent posture | Residency constraint |
|---|---|---|---|
| HIPAA (US) | Base (native) · P57-AM (US node) | English/Spanish; Flesch-Kincaid targets; LEARN model; teach-back documentation | US processing; communication artifacts as PHI |
| GDPR (EU/EEA) | P57-G · -EU adapter | Consent-communication completeness standard; minority-language support | EU residency |
| NDPR (Nigeria) | P57-G (native) | Hausa/Yoruba-class language packs; oral-tradition confirmation; CHW video with recorded-party consent | On-device offline; Open-Model-Only voice/text pipelines |
| Kenya DPA 2019 | P57-G (native) | Swahili packs; treatment-supporter designation | Kenyan residency; on-device processing |
| India DPDP | P57-G · P57-AM | Hindi/Tamil/Bengali/Marathi state-wise packs; vernacular-vs-loanword handling; ekadashi fasting adjustments | MeitY-empanelled infrastructure |
| Brazil LGPD | P57-G (native) | Portuguese (Africa)-adjacent and Brazilian Portuguese packs | Brazilian residency |
| Saudi PDPL | P57-G (native) | Arabic packs; gender-concordant provider options; Ramadan scheduling with religious justification | Saudi residency |
| China PIPL | P57-AM (native) | Simplified vs Traditional auto-detection; TCM bridging templates; family conference documentation | Onshore processing |
| Japan APPI | P57-AM (native) | Kanji + furigana rendering; Kampo sho bridging; hanko-seal acknowledgment; Buddhist framing | Domestic processing |
| Tribal / community consent regimes | P57-G (native) | Indigenous language packs; patient opt-out privacy as legal floor beneath family-inclusive defaults | Community enclave processing |

## Methodology

The base methodology is validated health-literacy engineering: Flesch-Kincaid/REALM/NVS assessment rubrics, the LEARN cultural adaptation framework, absolute-frequency risk communication, teach-back validation scripts, and multimodal specification (icons, color coding, layout) — proven in the canonical complete Spanish diabetes encounter from literacy calibration through teach-back script. P57-G re-founds the method on the Kleinman explanatory model dialogue trees, a 40-language NLP pipeline (Whisper-small voice, mBERT text) sized for offline edge execution, a 200+ icon pictorial library, religious calendar integration (Ramadan, Lent, prayer times), and family decision-tree logic with opt-out privacy at every branch. P57-AM re-founds it on multi-script NLP, family-conference documentation, integrative explanatory-model bridging templates, and aging-population media design. The invariant: calibrate to the patient's actual model of illness, adapt form without subtracting substance, verify understanding by confirmation, and record the result.

## Merits

- Measurable comprehension discipline — literacy-calibrated language, absolute-frequency risk, specific time-bound actions, and teach-back closure (base, demonstrated end-to-end).
- Accessibility as specification, not aspiration: screen-reader compatibility, large print, multimodal output (base).
- Informed consent in non-literate oral-tradition communities; reduced non-adherence through culturally coherent dosing; religious and gender norms respected without compromising care; family support structures activated for chronic disease (P57-G).
- Cancer disclosure handled through culturally normative family conferences without deception; integrative medicine bridged rather than dismissed; aging-population communication designed for the super-aging demographics of East Asia (P57-AM).

## Guidance for Use

Deploy the base P57 as the patient-facing layer of any CLAI-OS clinical module, with literacy rubrics and accessibility gates enabled and clinician review of adapted consent materials. Deploy P57-G alongside facility and CHW encounters in Global South settings: language packs and icon libraries preloaded for offline use, CHW participation arranged for trusted video, and the privacy opt-out explained as a right, not a courtesy. Deploy P57-AM in US and Asia-Pacific systems serving multi-script, family-centered, and aging populations: family-conference documentation active, integrative-medicine bridging configured per community, and proxy portal access properly consented.

Prerequisites: configured language/script set, clinical content fixed by the care team (P57 adapts, never authors, medicine), and confirmation-method selection appropriate to literacy. Misuse: do not strip material risk information for cultural comfort, override patient privacy opt-outs for family preference, simulate fluency in unconfigured languages (route to human interpreters), or let translated uncertainty collapse into reassurance. Pairings: receives clinical substance from P52, P55, and P54; generates patient summaries for P56 trial matches; delivers adherence messaging through P60; operates under P51 consent and privacy governance.

---
C0 informational classification; confers no clinical, legal, financial, or safety authority.
