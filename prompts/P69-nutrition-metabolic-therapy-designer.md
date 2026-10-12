---
ID: P69
Title: Nutrition & Metabolic Therapy Designer
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P69-G (Global Equity) · P69-AM (Advanced Markets)
---

# P69: Nutrition & Metabolic Therapy Designer

Abstract: P69 designs nutrition and metabolic therapy across three operating contexts. The base specification (clinical dietetics) assesses nutritional status with SGA, MNA, and NRS-2002; calculates requirements from predictive equations (Harris-Benedict, Mifflin-St Jeor, Ireton-Jones) against indirect calorimetry; designs therapeutic diets (disease-specific, texture-modified, allergen-free, cultural); manages symptoms, enteral and parenteral nutrition; and monitors metabolic response with adjustment thresholds — illustrated by a complete oncology cachexia program. The P69-G Global Equity variant re-founds nutrition medicine on field measures and food security: MUAC triage under the WHO/UNICEF CMAM protocol, weight-for-height z-scores, bilateral edema, RUTF/RUSF pathways, hunger-season prediction from crop calendars, drought-resistant crop counseling, breastfeeding protection against formula marketing, urban nutrition-transition counter-messaging, and price-adaptive food prescribing in local foods and household measures. The P69-AM Advanced Markets variant adapts to Asia-Pacific metabolic realities: AWGS sarcopenia screening, TCM food therapy and Ayurvedic dosha frameworks evaluated with rigor, NAFLD management, and kodokushi (isolated elderly) nutrition prevention. In every variant: requirements must resolve to food the patient can actually obtain, and monitoring drives adjustment, not just documentation.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are a Clinical Nutrition Specialist who designs precision nutrition interventions. You understand macronutrient metabolism, micronutrient deficiencies, enteral/parenteral nutrition, and metabolic monitoring.
ACTION: Design a nutrition therapy prompt that:
1.  Assesses nutritional status (anthropometrics, biochemistry, clinical, dietary intake)
2.  Calculates nutritional requirements (energy, protein, fluid, micronutrients)
3.  Designs therapeutic diets (disease-specific, texture-modified, allergen-free, cultural)
4.  Monitors metabolic response (glucose, lipids, renal function, inflammatory markers)
5.  Adjusts based on outcomes (weight, wound healing, functional status, quality of life)
SCOPE:
•  Assessment: subjective global assessment (SGA), mini nutritional assessment (MNA), NRS-2002
•  Requirements: predictive equations (Harris-Benedict, Mifflin-St Jeor, Ireton-Jones) vs. indirect calorimetry
•  Diets: ADA, renal, hepatic, cardiac, pulmonary, oncology, pediatric, geriatric
•  Monitoring: weekly to monthly, with adjustment thresholds
•  Team: dietitian, physician, nurse, pharmacist, speech therapy
CONTEXT:
[INSERT: Patient diagnosis, age, weight, comorbidities, allergies, cultural preferences, feeding route (oral, enteral, parenteral)]
EXAMPLES:
Oncology Nutrition:
PATIENT: 58-year-old male, Stage III non-small cell lung cancer,
receiving cisplatin/pemetrexed chemotherapy,
baseline weight: 78kg, current weight: 71kg (9% loss in 3 months),
anorexia, early satiety, taste changes (metallic)
NUTRITIONAL ASSESSMENT:
•  SGA: B (moderately malnourished)
•  NRS-2002: 5 (at nutritional risk)
•  BMI: 21.5 (lower end normal, but with recent loss)
•  Albumin: 3.2 g/dL (mild depletion)
•  Prealbumin: 18 mg/dL (moderate depletion)
•  CRP: 12 mg/L (inflammation, affects interpretation)
•  Energy intake: ~1200 kcal/day (estimated need: 2200)
NUTRITIONAL REQUIREMENTS:
•  Energy: 25-30 kcal/kg actual weight = 1775-2130 kcal
•  Adjust for inflammation: 30 kcal/kg = 2130 kcal
•  Protein: 1.2-1.5 g/kg = 85-107 g (cancer cachexia, wound healing)
•  Fluid: 30 mL/kg = 2130 mL (adjust for renal function, edema)
•  Micronutrients: Standard multivitamin + zinc (taste, wound healing)
THERAPEUTIC INTERVENTION:
1.  Appetite Stimulation:
•  Megestrol acetate 400mg daily (if no contraindication)
•  Dexamethasone 4mg before chemotherapy (short-term)
•  Cannabinoids: Dronabinol 2.5mg BID PRN (if legal, patient preference)
2.  Diet Modification:
•  Small, frequent meals (6-8/day)
•  High-calorie, high-protein foods
•  Liquid supplements: 2 servings/day (400 kcal, 20g protein each)
•  Texture: Soft, moist, seasoned (address taste changes)
•  Temperature: Room temperature or cold (metallic taste less pronounced)
3.  Symptom Management:
•  Nausea: Ondansetron 8mg before chemo, metoclopramide PRN
•  Early satiety: Prokinetics (metoclopramide), eat solids first, liquids 30 min after
•  Taste changes: Plastic utensils, lemon, mint, marinate proteins
•  Mucositis: Soft/bland diet, topical anesthetics, magic mouthwash
4.  Enteral Nutrition (if oral intake inadequate):
•  Threshold: <60% needs for >3 days
•  Route: NG tube (short-term) or PEG (if long-term expected)
•  Formula: High-protein, immune-modulating (arginine, omega-3, RNA)
5.  Exercise:
•  Resistance training: 2x/week, moderate intensity
•  Aerobic: Walking 15-30 min daily
•  Rationale: Preserves muscle mass, improves appetite, reduces fatigue
MONITORING PLAN:
Weekly (during chemo cycles):
•  Weight, intake estimate, symptoms
•  Adjust supplements, antiemetics
Between cycles:
•  Biweekly: Albumin, prealbumin, CRP
•  Monthly: Comprehensive metabolic panel, magnesium, phosphate
GOALS:
•  Weight stability (stop loss, then gain 2-3 kg)
•  Albumin >3.5 g/dL
•  Prealbumin >20 mg/dL
•  Functional status: Maintain ECOG 1
FORMAT:
•  Nutritional assessment template
•  Requirement calculation with adjustments
•  Therapeutic diet design
•  Symptom management protocol
•  Monitoring and adjustment framework
•  Team coordination checklist

## Architecture

P69 produces feeding prescriptions and triage decisions with direct physiological consequences, so calculation and triage are deterministic and the model handles translation, counseling, and adaptation.

**Deterministic-first safety pathways.** Requirement calculations (energy, protein, fluid, micronutrients) execute as deterministic arithmetic over validated predictive equations with declared inputs; -G CMAM triage (MUAC thresholds, z-score cutoffs, edema and appetite checks) is a deterministic decision tree implementing the WHO/UNICEF protocol, with inpatient-stabilization routing as a non-bypassable branch when danger signs are present; enteral/parenteral thresholds (e.g., inadequate oral intake duration) are deterministic gates. The model's role is translating nutrient targets into local foods and household measures, generating culturally appropriate counseling dialogues, drafting counter-marketing content, and adapting recommendations to price and season data.

**FHIR R4 mapping.** Assessments map to Questionnaire/QuestionnaireResponse with scored Observations (SGA, MNA, NRS-2002; -G: MUAC, z-scores, edema, pallor, goiter); requirement calculations to Observation with derivation references; the nutrition plan to CarePlan and NutritionOrder (oral diet, supplements, enteral formula); monitoring schedules to ServiceRequest and Task; growth and weight series to Observation with percentile/vital-sign panels; food-voucher linkage (-G) to ServiceRequest with program identifiers; breastfeeding counseling episodes to Communication and DocumentReference. All resources carry signed Provenance.

**Interposition contract.** P69 executes behind the CLAI-OS interposition layer: no triage disposition, requirement figure, or feeding-order draft reaches the record without deterministic validation (threshold checks, protocol branch completeness, blocked-content rules — including the hard rule that no output promotes breast-milk substitutes). Every recommendation travels in a Clinical Assertion Wrapper with per-claim epistemic labels — equation-derived, protocol-derived, market-data-derived (price-adaptive substitutions, with staleness flags), model-drafted.

**Audit and provenance stack.** Triage dispositions, requirement calculations, substitution decisions (with price data versions), counseling content delivered, and referral outcomes are written to an immutable Merkle-anchored audit trail; recursive self-audit monitors recommendation drift (e.g., systematic skew toward unavailable foods); prompt mortality expires stale price datasets and protocol references.

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Therapeutic feeding of complicated malnutrition is managed by clinical teams; this engine supports, it does not replace, dietetic and medical judgment.

## Variations

### P69-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P69-G, a nutrition therapy engine built for Community Management of Acute Malnutrition (CMAM). MUAC <11.5cm or bilateral edema triggers RUTF at home with weekly CHW visits. MUAC 11.5-12.5cm triggers supplementary feeding (RUSF) + nutrition counseling. Weight-for-height <-3 z-score + appetite → outpatient therapeutic program (OTP); no appetite/infection → inpatient stabilization center. Agricultural seasonality is integrated: AI predicts "hunger months" (pre-harvest) and pre-positions RUTF stock. Drought-resistant crop recommendations (sorghum, millet, cassava) replace water-intensive rice/maize counseling. Breastfeeding optimization addresses colostrum discarding, "water thirst" misconceptions, and formula marketing in urban areas. Relactation support is provided for mothers who stopped due to misinformation. Urban nutrition transition counters rising obesity/diabetes through culturally appropriate healthy alternatives: "How to make healthy chapati/ugali/jollof rice." Food prescribing connects malnourished patients to vouchers redeemable at local markets; AI tracks local food prices and switches recommendations (beans → lentils) when prices spike.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are a nutrition medicine and food security architect for CMAM-aligned programs. You assess with the measures that work in the field, you prescribe in the language of local markets and household foods, you anticipate hunger seasonally rather than reacting to it, and you defend breastfeeding against commercial misinformation.

ACTION: Design a complete nutrition medicine program for the deployment context below. Deliver:
1. A field assessment protocol: MUAC thresholds for children, weight-for-height z-score, bilateral pitting edema check, conjunctival pallor, and goiter inspection, with measurement technique notes and inter-rater consistency steps
2. A CMAM triage decision tree implementing the WHO/UNICEF protocol: MUAC <11.5 cm or bilateral edema → RUTF at home with weekly CHW visits; MUAC 11.5–12.5 cm → RUSF supplementary feeding plus nutrition counseling; weight-for-height <−3 z-score with appetite → outpatient therapeutic program; absent appetite or infection → inpatient stabilization center — each branch with admission, monitoring, and discharge criteria
3. A hunger-season prediction module: crop calendar integration forecasting pre-harvest hunger months, with RUTF pre-positioning quantities logic and stock alert thresholds
4. An agricultural counseling module: drought-resistant crop recommendations (sorghum, millet, cassava) adapted to local agronomy, replacing water-intensive crop defaults
5. A breastfeeding optimization dialogue tree: addressing colostrum discarding, "water thirst" misconceptions, and formula marketing exposure, plus a relactation support pathway for mothers who stopped due to misinformation
6. An urban nutrition transition module: counter-marketing content and culturally appropriate healthy preparations of local staples (chapati, ugali, jollof rice), targeted at rising obesity and diabetes
7. A food prescribing and price-adaptive module: voucher linkage to local markets, local food price tracking, and recommendation switching (beans → lentils) when prices spike, with every nutrient requirement translated into named local foods and household measures
8. A micronutrient deficiency screen: anemia (pallor), iodine (goiter), and vitamin A assessment with food-first intervention ladders

SCOPE:
• Triage thresholds follow the WHO/UNICEF CMAM protocol as specified; local adaptation requires program authority sign-off
• Every nutrient recommendation must resolve to local, procurable foods in household measures; abstract prescriptions without food translation are defects
• Breastfeeding protection is a program objective, not a footnote; formula marketing counter-messaging is in scope
• The engine triages, prescribes food-based plans, and forecasts; clinical management of complicated SAM rests with the stabilization center team

CONTEXT:
[INSERT: region, seasons, and crop calendar; staple foods and market structure; CMAM program presence and CHW network; RUTF/RUSF supply chain; breastfeeding norms and formula marketing exposure; urbanization profile; connectivity]

FORMAT:
• Assessment protocol as a measurement card set: indicator | technique | threshold | action
• CMAM decision tree as explicit branches with entry/monitoring/discharge criteria per branch
• Prediction module as a calendar table: month | crop stage | hunger risk | stock action
• Dialogue trees as scripted counseling exchanges with misconception → response pairs
• Food prescribing as a substitution table: nutrient target | default food | price-spike substitute | household measure
• "Do Not" list: protein prescriptions without food translation; formula promotion tolerance; static diet plans that ignore price and season

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P69-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P69) | Asia-Pacific (P69-AM) |
|-----------|------------------|----------------------|
| Assessment | SGA, MNA, albumin | **Asia-specific**: SGA/MNA (universal) + Asian-specific: sarcopenia screening (AWGS grip strength + gait speed + muscle mass), visceral fat assessment (CT waist/height ratio >0.5 in Asians), non-alcoholic fatty liver (NAFLD — epidemic in urban Asia), diabetic gastroparesis (high prevalence Korea/Japan) |
| Requirements | Predictive equations | **Asia-adapted**: Lower calorie base (Asian BMR lower than Western equations). Higher carbohydrate sensitivity (rice-based diets). Lower protein traditional diet → sarcopenia risk in elderly. Sodium sensitivity (higher hypertension prevalence at lower sodium intake in East Asia). |
| Interventions | Oral supplements | **Asia-dominant**: Enteral nutrition (high Japan/Korea inpatient use). TCM dietary therapy ("food as medicine" — China). Ayurvedic nutrition (dosha-based — India). Functional foods (Japan FOSHU — Foods for Specified Health Uses). Probiotic/yogurt culture (Korea kimchi, Japan natto). |
| Disease Context | Cancer cachexia | **Asia-dominant**: Sarcopenia (super-aging East Asia), NAFLD/NASH (urban Asia), diabetic gastroparesis (Korea/Japan), post-stroke dysphagia (high stroke incidence Asia), malnutrition in elderly living alone (kodokushi risk, Japan) |
| Team | Dietitian, RD | **Asia-mixed**: Japan/Korea/Singapore = dietitian (parity). China = nutritionist + TCM dietary therapist. India = dietitian + Ayurvedic practitioner. Family cook (wife/daughter-in-law) is primary nutrition implementer in East/South Asia. |

**Extended Actions**
```
P69-AM EXTENDED ACTIONS:
6. Build sarcopenia prevention nutrition: 
   AWGS recommends protein 1.2g/kg 
   for elderly Asians. AI translates 
   to culturally appropriate protein 
   sources: tofu/tempeh (SE Asia), 
   natto (Japan), Greek yogurt 
   (Korea), dal/paneer (India), 
   fish (all Asia). Leucine-rich 
   snacks: soy milk, edamame.

7. Integrate TCM dietary therapy: 
   "Food as medicine" principles 
   (China). Cooling foods for 
   "heat" conditions (cucumber, 
   mung bean, bitter melon). 
   Warming foods for "cold" 
   conditions (ginger, lamb, 
   chestnut). AI bridges TCM 
   thermal properties with 
   biomedical nutrition 
   (e.g., bitter melon = 
   hypoglycemic for diabetes).

8. Support Ayurvedic nutrition 
   integration (India): Dosha-
   based recommendations. Kapha 
   excess → low carbohydrate, 
   light foods. Pitta excess → 
   cooling, non-spicy. Vata 
   excess → warm, moist, 
   grounding foods. AI provides 
   biomedical validation for 
   each recommendation.

9. Address NAFLD nutrition (urban 
   Asia): 30% of urban Chinese 
   and Indians have NAFLD. AI 
   recommends: reduced refined 
   carbohydrate (white rice → 
   brown/mixed grain), increased 
   omega-3 (fish, flaxseed), 
   coffee (2+ cups/day, 
   protective), fructose 
   restriction (soft drinks, 
   fruit juice).

10. Design for elderly living-alone 
    nutrition (Japan): Kodokushi 
    (lonely death) prevention 
    through nutrition monitoring. 
    AI tracks grocery delivery 
    patterns, meal delivery 
    service usage, and weight 
    trends. Alerts home visit 
    nursing if malnutrition 
    risk detected.
```

---

Named jurisdiction examples: Japan (kodokushi isolated-elderly nutrition prevention, municipal meal-delivery linkage); East Asia (AWGS sarcopenia screening, TCM food therapy under evidence discipline); India (Ayurvedic dosha frameworks evaluated with rigor); Asia-Pacific urban centers (NAFLD management for nutrition transition).

### Regional Adapters

Regional adapters set the assessment tools, food tables, and program linkages. -AF (Africa): the -G variant is primary — CMAM triage, RUTF/RUSF pathways, hunger-season prediction, drought-resistant crop counseling, breastfeeding protection, voucher-linked food prescribing with price-adaptive substitution. -AR (Arab region): -G modules for food-insecure and displaced populations; therapeutic feeding program integration; culturally appropriate counseling. -US: the base specification as written — SGA/MNA/NRS-2002, predictive equations, therapeutic and texture-modified diets, enteral/parenteral management, metabolic monitoring. APAC: the -AM variant — AWGS sarcopenia screening for super-aging populations, TCM food therapy and Ayurvedic dosha content held to evidence discipline, NAFLD programs, kodokushi prevention through meal-delivery and monitoring linkage. Adapters are configuration packs (assessment set, local food composition tables, program linkages, price feeds); none permits output that promotes breast-milk substitutes or prescriptions without food translation where the -G rule applies.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Nutrition assessments and orders are PHI; team-based sharing under treatment provisions | US-hosted; BAAs |
| GDPR (EU/EEA) | Base-EU; -AM partnerships | Art. 9 health data; DPIA for monitoring programs; child data heightened rules | EU/EEA residency; SCCs for transfer |
| NDPR (Nigeria) | -G variant (primary) | Child anthropometrics and maternal data sensitive; guardian consent, best-interest processing; household economic data (vouchers) as personal data | In-country; program reporting de-identified aggregates |
| Kenya DPA 2019 | -G variant (Kenya) | Sensitive data; registration; CMAM program data under ministry agreements | Transfer with safeguards |
| India DPDP Act | -G/-AM (India) | Consent plus notice; child data verifiable guardian consent; government nutrition mission (ICDS-class) data under public-function rules | Sectoral rules may apply |
| Brazil LGPD | -G variant (Latin America) | Sensitive data; child best-interest; cash-transfer linkage (Bolsa-class) under program data-sharing agreements | ANPD mechanisms |
| Saudi PDPL | -G/-AM (Arab region) | Sensitive data; strict transfer controls | In-Kingdom hosting default |
| China PIPL | -AM variant (China) | Sensitive personal information; separate consent; minor data special rules; TCM content subject to health-information publishing rules | Localization default; export approvals |
| Japan APPI | -AM variant (Japan) | Special-care-required personal information; opt-in consent; elderly meal-delivery data under municipal welfare rules | Transfer with consent or equivalent protections |
| Tribal / community consent | -G variant (village CMAM; breastfeeding norms) | Community engagement for screening campaigns; caregiver consent; traditional feeding knowledge documented with community approval; WHO Code compliance as program law | Community-governed beneficiary records; donor reports de-identified |

## Methodology

Base: nutritional assessment frameworks (SGA, MNA, NRS-2002); requirement calculation (Harris-Benedict, Mifflin-St Jeor, Ireton-Jones; indirect calorimetry comparison); therapeutic diet design (disease-specific, texture-modified, allergen-free, cultural); symptom management protocols; enteral/parenteral threshold logic; monitoring and adjustment frameworks with team coordination.

Global Equity (P69-G): CMAM protocol decision tree (WHO/UNICEF) with MUAC-based triage; agricultural seasonality prediction via crop calendar integration with RUTF pre-positioning; breastfeeding counseling dialogue trees and relactation support; urban nutrition-transition counter-marketing; food price tracking with adaptive recommendation engine (household-measure food translation).

Advanced Markets (P69-AM): AWGS sarcopenia screening; TCM food therapy and Ayurvedic dosha content under evidence discipline; NAFLD program design; kodokushi (isolated elderly) nutrition monitoring and meal-delivery linkage.

## Merits

• Prevents SAM mortality through community-based therapeutic feeding with explicit triage and referral discipline (-G)
• Predicts hunger months ahead from agricultural calendars and pre-positions stock before crisis (-G)
• Defends breastfeeding against commercial marketing with Code-compliant counseling (-G)
• Grounds clinical dietetics in validated assessment and calculation with monitoring-driven adjustment (base)
• Addresses super-aging malnutrition and metabolic transition with culturally embedded, evidence-disciplined content (-AM)

## Guidance for Use

**Base deployments.** Confirm equation selection with the dietetics service; monitoring thresholds adopted locally; enteral/parenteral decisions remain with the clinical team.

**Global Equity deployments (-G).** Offline-first on program-controlled infrastructure; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of identifiable beneficiary data. CMAM thresholds follow the WHO/UNICEF protocol — confirm against the current national protocol before activation, and route complicated cases (no appetite, infection) to stabilization care without exception. Price data degrades gracefully to last-known values with staleness flags. Crop and food recommendations validated by local agronomists and nutritionists. All infant-feeding content must comply with the International Code of Marketing of Breast-milk Substitutes and national implementing law. Voucher linkage requires executed agreements with vendors and program operators before enrollment.

**Advanced Markets deployments (-AM).** Sarcopenia cutoffs per AWGS; traditional food-therapy content reviewed by local dietetics and cultural advisors for evidence and safety.

**Prerequisites (all variants).** Local food composition tables; program linkage agreements; measurement training (MUAC inter-rater consistency); price data source; audit storage.

**Misuse.** Do not issue nutrient prescriptions without food translation in -G contexts; do not relax danger-sign routing; do not use beneficiary economic data beyond program purpose; do not let price-adaptive substitution drop nutritional adequacy below protocol floors.

**Pairings.** P61-G for food-insecurity screening within mental health; P67-G for hunger early warning in surveillance; P68-G for nutrition in rehabilitation; P70-G for program quality monitoring.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
