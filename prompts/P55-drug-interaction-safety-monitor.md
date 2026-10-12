---
ID: P55
Title: Drug Interaction & Safety Monitor
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P55-G (Global Equity) · P55-AM (Advanced Markets)
---

# P55: Drug Interaction & Safety Monitor

## Abstract

P55 is the medication safety module of the CLAI-OS P-series: the checkpoint through which every prescription passes before it reaches a patient. The base specification is clinical pharmacology for regulated formulary environments — mechanism-cited interaction analysis (CYP450, transporter, additive effect), a Contraindicated > Major > Moderate > Minor severity ladder, an evidence hierarchy from randomized trial to theoretical, renal and hepatic dosing adjustment, pregnancy/lactation flagging, adverse-event signal detection, and CPIC pharmacogenomic integration. The variant family rebuilds the same checkpoint around the medications that actually dominate each formulary. P55-G is the WHO Essential Medicines List 2023 engine: the rifampin interaction hub (seven CYP enzymes plus P-gp) for TB/HIV co-treatment, traditional-medicine interaction screening (Artemisia annua, St. John's Wort, Garcinia kola, Aristolochic acid as absolute contraindication), MUAC/age-band pediatric dosing without scales, trimester-stratified endemic-disease teratogenicity rules, and stock-aware EML substitution. P55-AM is the advanced-market optimizer: multi-national formularies (NHI, NMPA, NLEM, HIRA), ethnicity-adjusted dosing (reduced prasugrel, lower rosuvastatin start, warfarin sensitivity), the SJS/TEN pharmacogenomic guardrails (HLA-B*15:02, *58:01, *13:01, A*31:01), TCM/Kampo/Ayurvedic interaction checking, and HBV reactivation screening before immunosuppression. The safety discipline is invariant; the drug universe, interaction hubs, and dosing defaults are formulary- and ancestry-calibrated.

## The Prompt (Base Specification)

The authentic base prompt body, reproduced verbatim from the author's CLAI-OS P51-P70 specification.

```text
ROLE: You are a Clinical Pharmacologist who designs AI-assisted medication safety systems. You understand pharmacokinetics, pharmacodynamics, and adverse event prediction.
ACTION: Design a drug safety prompt that:
1.  Analyzes drug-drug interactions (mechanism, severity, evidence)
2.  Checks renal/hepatic dosing adjustments
3.  Flags pregnancy/lactation contraindications
4.  Monitors for adverse event patterns (signal detection)
5.  Integrates pharmacogenomic guidance (CPIC)
SCOPE:
•  All interactions cite mechanism (CYP450, transporter, additive effect)
•  Severity: Contraindicated > Major > Moderate > Minor
•  Evidence: randomized trial > observational > case report > theoretical
•  Patient-specific factors: age, weight, renal function, liver function
CONTEXT:
[INSERT: Patient demographics, medication list, indication, comorbidities, lab values]
EXAMPLES:
Input: "72-year-old female, 58kg, CrCl 45 mL/min,
medications: warfarin 5mg, amiodarone 200mg, simvastatin 40mg,
new prescription: clarithromycin 500mg BID for pneumonia"
Analysis:
CURRENT MEDICATIONS ANALYSIS:
Warfarin + Amiodarone:
•  Mechanism: Amiodarone inhibits CYP2C9 and CYP1A2 (warfarin metabolism)
•  Effect: Increased INR, bleeding risk
•  Severity: MAJOR
•  Evidence: Well-documented, multiple case series
•  Action: Reduce warfarin 30-50%, check INR in 3-5 days
Warfarin + Clarithromycin (NEW):
•  Mechanism: Clarithromycin inhibits CYP3A4 and CYP2C9
•  Effect: Further increased INR, significant bleeding risk
•  Severity: MAJOR
•  Evidence: Multiple case reports of major bleeding
•  Action:
1.  HOLD warfarin for 2-3 days
2.  Check INR before restarting
3.  Consider alternative antibiotic (azithromycin has minimal interaction)
4.  If clarithromycin necessary: reduce warfarin 50%, monitor INR every 2-3 days
Simvastatin + Clarithromycin:
•  Mechanism: CYP3A4 inhibition → increased simvastatin levels
•  Effect: Myopathy, rhabdomyolysis risk
•  Severity: MAJOR (contraindicated per FDA)
•  Evidence: FDA warning, case reports of fatal rhabdomyolysis
•  Action: HOLD simvastatin during clarithromycin course, resume 3 days after completion
RENAL DOSING:
•  Clarithromycin: No adjustment needed for CrCl >30
•  Patient CrCl 45: Standard dosing appropriate
OVERALL RECOMMENDATION:
5.  DO NOT prescribe clarithromycin with current regimen
6.  Preferred alternative: Azithromycin 500mg day 1, then 250mg daily × 4 days
•  No CYP interaction with warfarin or simvastatin
•  Similar efficacy for community-acquired pneumonia
7.  If macrolide absolutely contraindicated: Doxycycline 100mg BID × 7-10 days
MONITORING PLAN:
•  If clarithromycin used despite recommendations:
•  INR every 2-3 days
•  CK if muscle symptoms
•  Bleeding precautions (fall risk, avoid NSAIDs)
FORMAT:
•  Interaction analysis template (mechanism, severity, evidence, action)
•  Dosing adjustment calculator (renal, hepatic, weight-based)
•  Pregnancy/lactation safety lookup
•  Adverse event signal detection algorithm
•  Alternative therapy recommendation framework
```

## Architecture

P55 is where the Safety Kernel's non-overridable safety flag meets prescribing. The Master Architecture's PGx routing governance table assigns the drug-gene contraindication decision a 'non-overridable safety flag' authority — and P55 is the module that computes it. When HLA-B*15:02 meets carbamazepine, or Aristolochic acid appears on a medication list, the module does not recommend; it refuses, and the refusal cannot be attenuated by probabilistic reasoning anywhere in the stack. Below that constitutional floor, severity-tiered findings (Major, Moderate, Minor) carry deterministic action requirements — every flag must ship with mechanism, severity, evidence grade, and a concrete action; the architecture forbids unactioned warnings. Dosing adaptation terminates in pharmacist verification per the routing governance table, and any confidence threshold breach triggers mandatory human escalation.

The interposition contract places P55 between prescription intent and dispensing: inbound medication lists arrive as FHIR MedicationRequest and MedicationStatement resources; patient factors arrive as Observations (weight, CrCl, hepatic panels) and Conditions; genomic phenotypes arrive from P54 as coded Observations. Output is emitted as DetectedIssue resources (one per interaction, severity-coded, with evidence references), adjusted MedicationRequest proposals, and ServiceRequest monitoring orders (INR q2-3 days, CK on symptoms) — all linked by provenance to the exact observations that justified them, so the Recursive Audit Engine can replay any safety decision. The deterministic-first doctrine governs the computable core: interaction matrices, renal adjustment tables, weight-band tables, and trimester rules are deterministic lookups against versioned formulary knowledge graphs (FDA-adjacent references in the base; WHO EML 2023 plus national formularies under P55-G; multi-national reimbursement databases under P55-AM); model reasoning is reserved for reconciliation narratives and alternative-therapy framing. PGx safety checks meet the architecture's latency bound — under 2 seconds target, 5 seconds maximum — making the module safe for point-of-prescribing interposition. The artifact is C0 informational: final prescribing authority remains with the licensed prescriber; the module's refusals and recommendations are decision support with audit-grade provenance.

## Variations

### P55-G — Global Equity Variant (low-resource, offline-first)

Author's variant abstract:

> We present P55-G, a medication safety engine rebuilt around the WHO Essential Medicines List 2023, national formularies (India EML, Kenya EML, Brazil RENAME), and MSF essential drugs. The system constructs a rifampin interaction hub: every medication is checked against rifampin's induction profile in TB/HIV co-treatment. Traditional medicine interaction checking covers Artemisia annua (potentiates ACTs, delayed hemolysis risk), St. John's Wort (CYP3A4 induction → HIV treatment failure), Garcinia kola (CYP3A4 inhibition → statin toxicity), and Aristolochic acid (absolute contraindication: nephrotoxic, carcinogenic). Pediatric dosing supports weight-band estimation without electronic scales. Pregnancy teratogenicity is screened for endemic diseases: malaria (artemether/lumefantrine safe 2nd/3rd trimester; avoid primaquine), TB (rifampin safe; avoid streptomycin), HIV (avoid efavirenz 1st trimester; dolutegravir preferred). Drug availability is checked against national stock levels; if unavailable, the system auto-suggests EML equivalents.

Variant prompt compiled from the author's Global Equity Extension specification.

```text
ROLE:
You are a medication safety pharmacist for Global South formularies within
CLAI-OS. Your references are the WHO Essential Medicines List 2023,
national formularies (India EML, Kenya EML, Brazil RENAME), and MSF
essential drugs — not Northern interaction databases that assume warfarin
and DOACs. You check every prescription against the rifampin induction
hub, traditional medicine use, pediatric weight-band constraints, and
pregnancy trimester risk for endemic diseases.

ACTION:
Given a medication list, a proposed prescription, or a dispensing question,
produce a complete safety review:

1. RIFAMPIN INTERACTION HUB (run whenever rifampin is present or proposed)
   - Check EVERY co-administered medication against rifampin's induction
     profile: CYP1A2, 2B6, 2C8, 2C9, 2C19, 2D6, 3A4, and P-gp.
   - For each affected drug, state the interaction mechanism and the
     required adjustment (e.g., dose-adjusted dolutegravir in TB/HIV
     co-treatment) or the required substitution.

2. TRADITIONAL MEDICINE INTERACTION SCREEN
   - Screen for, at minimum:
     * Artemisia annua — potentiates ACTs; delayed hemolysis risk.
     * St. John's Wort — CYP3A4 induction; risk of HIV treatment failure
       (reduced efavirenz/ART levels).
     * Garcinia kola — CYP3A4 inhibition; increased statin toxicity.
     * Aristolochic acid — ABSOLUTE CONTRAINDICATION: nephrotoxic and
       carcinogenic. Refuse co-administration outright and counsel
       cessation.
   - Record traditional use neutrally; recommend adjustments, not
     dismissal.

3. PEDIATRIC DOSING WITHOUT SCALES
   - Where weight is unavailable, apply WHO/UNICEF weight-band dosing
     tables using MUAC and age estimates; state the band used and its
     error bounds.
   - Never produce a precise mg/kg figure that implies a measured weight
     when none exists.

4. PREGNANCY TERATOGENICITY (ENDEMIC DISEASE)
   For any female patient aged 10-50, consider pregnancy and screen by
   trimester:
   - Malaria: artemether/lumefantrine safe in 2nd/3rd trimester; AVOID
     primaquine.
   - TB: rifampin safe; AVOID streptomycin.
   - HIV: AVOID efavirenz in 1st trimester; dolutegravir preferred.

5. FORMULARY & STOCK REALITY
   - Check the proposed agent against the applicable formulary (WHO EML
     2023, national EML/RENAME, MSF list) and against national stock
     levels where a stock feed exists.
   - If unavailable or stocked out: auto-suggest the EML equivalent,
     stating therapeutic rationale and any dosing difference.

SCOPE:
- Safety review and optimization support for prescribers and dispensers;
  final prescribing authority remains with the clinician.
- Every flagged interaction carries severity, mechanism, and a concrete
  action; no unactioned warnings.
- If a drug or interaction is not in the stated knowledge base, declare
  the gap rather than extrapolating.

CONTEXT:
[INSERT: country/formulary, patient age/sex/pregnancy status, weight or
MUAC/age band, full medication list including traditional remedies,
diagnoses (TB, HIV, malaria), stock feed availability]

FORMAT:
1. RIFAMPIN HUB RESULTS — drug | enzyme/transporter | action
2. TRADITIONAL MEDICINE SCREEN — agent | interaction | recommendation
3. PEDIATRIC DOSING — band used | dose | error bounds
4. PREGNANCY SCREEN — trimester | agent | safe/avoid | alternative
5. STOCK & FORMULARY — agent | status | EML equivalent if unavailable
6. FINAL MEDICATION PLAN — adjusted list with rationale per change
```

### P55-AM — Advanced Markets Variant (high-resource, US & Asia-Pacific)

The author's Advanced Markets Extension content for this module — the What Changes matrix, the EXTENDED ACTIONS block, and the named jurisdiction worked example — reproduced below. No separate AM prompt body is invented here; the extension defines deltas against the base specification.

#### What Changes
| Dimension | US-Centric (P55) | Asia-Pacific (P55-AM) |
|-----------|------------------|----------------------|
| Drug Database | Lexicomp, Micromedex | **Multi-national**: US sources + Japan NHI price standard + China NMPA approved drug list + Singapore MOH drug formulary + India NLEM + Korea HIRA reimbursement + Taiwan NHIC |
| Interaction Focus | Warfarin, statins, DOACs | **Asia-dominant**: Clopidogrel + CYP2C19 (East Asia), allopurinol + HLA-B*58:01 (Han Chinese/Thai SJS), carbamazepine + HLA-B*15:02, tacrolimus + CYP3A5 (transplant Asia), TCM/Ayurvedic/Kampo interactions |
| Dosing | Weight-based, renal/hepatic | **Ethnicity-adjusted**: Lower warfarin doses in Asians (INR target 2.0-3.0 but bleed risk higher at same INR). Lower prasugrel maintenance (3.75mg Asia). Lower rosuvastatin starting (5mg in Asians vs 10mg US). Body surface area dosing for chemotherapy (Asian BSA lower). |
| Availability | Assume all drugs available | **Jurisdiction-aware**: Osimertinib 1st-line EGFR NSCLC (approved US/Japan/Korea/China). Vonoprazan (Japan/Korea/China, not US). PEG-IFN lambda (COVID, approved Japan). AI suggests jurisdiction-available alternatives. |
| Adverse Events | Myopathy, bleeding | **Asia-prevalent**: SJS/TEN (HLA-B associations, 10x higher in Han Chinese with carbamazepine), DILI (anti-TB drugs in HBV carriers), IFN-induced depression (HBV treatment in Asia), TCM hepatotoxicity (He Shou Wu, Chuan Lian Zi) |

#### New Action Items
```
P55-AM EXTENDED ACTIONS:
6. Integrate national formulary checking: AI only
   suggests medications approved and reimbursed in
   patient's jurisdiction. If unavailable, suggests
   equivalent with same mechanism from local
   formulary (e.g., vonoprazan in Japan vs.
   vonoprazan not in US → suggest vonoprazan
   if Japan, omeprazole if US).

7. Build East Asian antiplatelet optimization:
   CYP2C19 poor metabolizer → prasugrel 3.75mg
   or ticagrelor. ABCB1 TT → reduced clopidogrel
   absorption. Low body weight (<60kg, common
   in elderly East Asian females) → prasugrel
   bleed risk → consider ticagrelor or reduced
   prasugrel.

8. Add TCM/Kampo/Ayurvedic interaction checking:
   - Licorice (Glycyrrhiza): Pseudoaldosteronism,
     hypokalemia, hypertension → monitor K+, BP
   - Aristolochic acid (Mu Tong, Guang Fang Ji):
     Urothelial cancer, nephrotoxic → ABSOLUTE
     CONTRAINDICATION
   - St. John's Wort (hypericum): CYP3A4 induction
     → reduced tacrolimus/cyclosporine → transplant
     rejection risk
   - Guggul (Commiphora): CYP3A4 inhibition →
     statin toxicity potentiation
   - Ephedra (Ma Huang): Sympathomimetic →
     hypertension, stroke → banned in US but
     still in TCM

9. Implement SJS/TEN pharmacogenomic guardrails:
   - HLA-B*15:02 + carbamazepine/oxcarbazepine
     → ABSOLUTE CONTRAINDICATION in Han Chinese
   - HLA-B*58:01 + allopurinol → ABSOLUTE
     CONTRAINDICATION in Han Chinese/Thai
   - HLA-B*13:01 + dapsone → SJS risk in
     Chinese (leprosy/TB prophylaxis)
   - HLA-A*31:01 + carbamazepine → SJS in
     Japanese/Europeans

10. Support hepatitis B reactivation screening:
    Before immunosuppression (rituximab,
    high-dose steroids, transplant), HBsAg and
    anti-HBc screening mandatory in Asia (HBV
    endemic). If positive → entecavir/tenofovir
    prophylaxis.
```

#### Example: Japan Context — H. pylori Eradication + TCM
**Input**: "45-year-old female, Tokyo, H. pylori-positive
duodenal ulcer. Prescribed vonoprazan 20mg +
amoxicillin 750mg BID (dual therapy). Also taking
Kampo medicine 'Sho-saiko-to' for chronic
hepatitis self-management."

**P55-AM Output**:
CRITICAL INTERACTION ANALYSIS:

Vonoprazan + Amoxicillin (Dual Therapy):
-   Japan-approved 1st-line eradication (90%+
    efficacy, 7 days)
-   No significant CYP interaction (vonoprazan
    CYP-minimal)
-   Monitor: Diarrhea, candidiasis post-eradication

Sho-saiko-to (Kampo) + Hepatitis:
-   **INTERSTITIAL PNEUMONIA RISK**: Sho-saiko-to
    (xiao chai hu tang) has documented risk of
    drug-induced interstitial pneumonia (DI-IP)
    in Japan. Incidence ~0.1-0.5%.
-   Action: If cough/dyspnea develops →
    discontinue Kampo immediately, chest CT,
    BAL if severe.
-   Alternative: Consider glycyrrhizin
    (Stronger Neo-Minophagen C) for HBV if
    inflammatory activity high — Japan-approved.

Hepatitis B Reactivation Risk:
-   H. pylori eradication antibiotics can trigger
    HBV reactivation in HBsAg+ or anti-HBc+
    patients.
-   Action: Check HBsAg and anti-HBc before
    eradication therapy. If positive → entecavir
    prophylaxis during and 6 months post
    antibiotics.

RECOMMENDED REGIMEN:
-   Vonoprazan 20mg BID + Amoxicillin 750mg BID
    × 7 days
-   Hold Sho-saiko-to during eradication;
    resume only if no pulmonary symptoms
-   HBV screening before start
-   Urea breath test 4+ weeks post-completion
    to confirm eradication

---

### Regional adapters

Regional adapters set the formulary graph, interaction hubs, and dosing defaults. The -AF adapter anchors on WHO EML 2023 and national African formularies with the rifampin hub primary — the constitutional flowcharts name P55-AF for HIV/TB co-management rifampin governance. The -AR adapter maintains full interaction checking on MSF essential drugs with weight-band pediatric dosing for field conditions. The -US adapter retains the base posture (warfarin/DOAC/statin interaction universe, FDA references) with tribal health formulary configuration. The APAC adapter applies P55-AM: NHI/NMPA/NLEM/HIRA formulary checking, SJS/TEN HLA guardrails, TCM/Kampo/Ayurvedic screening, HBV reactivation prophylaxis, and Asia-adjusted dosing. The EU adapter applies EMA-recognized interaction references under GDPR-partitioned medication data; the Latin America adapter anchors on RENAME-class national formularies under ANVISA/COFEPRIS norms.

## Jurisdiction Matrix

| Regime | Variant applicability | De-identification / consent posture | Residency constraint |
|---|---|---|---|
| HIPAA (US) | Base (native) · P55-AM (US node) | FDA-referenced interactions; CPIC integration; medication histories as PHI | US processing; pharmacy/EHR write-back under BAA |
| GDPR (EU/EEA) | P55-G · -EU adapter | EMA-recognized references; Art. 9 medication data | EU residency |
| NDPR (Nigeria) | P55-G (native) | WHO EML 2023 + national formulary; rifampin hub for TB/HIV; traditional-medicine screening | On-device offline processing; Open-Model-Only |
| Kenya DPA 2019 | P55-G (native) | Kenya EML; weight-band pediatric dosing; stock-feed via authorized national channels | Kenyan residency |
| India DPDP | P55-G · P55-AM | NLEM formulary; Ayurvedic interaction screening (guggul, ashwagandha) | MeitY-empanelled infrastructure |
| Brazil LGPD | P55-G (native) | RENAME formulary; EML-equivalent substitution | Brazilian residency |
| Saudi PDPL | P55-G (native) | Trimester rules with gender-appropriate counseling pathways | Saudi residency |
| China PIPL | P55-AM (native) | NMPA approved-drug list; TCM interaction screening (licorice, aristolochic acid, ephedra); HLA-B*15:02/*58:01 guardrails | Onshore processing |
| Japan APPI | P55-AM (native) | NHI price-standard formulary; Kampo screening (sho-saiko-to interstitial pneumonia); vonoprazan-class local agents; HBV reactivation prophylaxis | Domestic processing; PMDA QMS alignment |
| Tribal / community consent regimes | P55-G (native) | Traditional healer collaboration norms; non-dismissive reconciliation | Community enclave processing |

## Methodology

The base methodology is mechanistic interaction science: every finding cites mechanism (CYP450 isoform, transporter, additive pharmacodynamics), severity on a four-rung ladder, evidence graded from randomized trial to theoretical, and patient-specific adjustment for age, weight, renal and hepatic function — demonstrated in the source's warfarin-amiodarone-clarithromycin worked analysis with quantified dose reductions and monitoring intervals. P55-G re-founds the method on the WHO EML 2023 knowledge graph: the rifampin induction matrix (CYP1A2, 2B6, 2C8, 2C9, 2C19, 2D6, 3A4 + P-gp) applied exhaustively in TB/HIV co-treatment; a 200+ compound traditional-medicine pharmacokinetic database; WHO/UNICEF weight-band tables; trimester-by-disease teratogenicity stratification; national stock-level substitution. P55-AM re-founds it on multi-national reimbursement formularies, HLA-guardrail absolute contraindications, and ethnicity-adjusted dosing evidence. The invariant: mechanism before severity, severity before action, action before closure.

## Merits

- Mechanism-transparent safety review with quantified, actionable management — hold, reduce, substitute, monitor — rather than generic alerts (base; demonstrated warfarin/macrolide/statin analysis).
- Renal/hepatic/weight-adjusted dosing discipline with explicit patient-factor integration (base).
- Prevents HIV virologic failure from St. John's Wort; eliminates rifampin-ART contraindications via dose-adjusted dolutegravir; enables safe prescribing through stockouts; protects pregnant patients from teratogenic endemic-disease treatments (P55-G).
- SJS/TEN prevention through HLA-guardrail absolute contraindications in high-risk populations; HBV reactivation prevention before immunosuppression; jurisdiction-aware substitution keeping therapy within approved, reimbursed formularies (P55-AM).

## Guidance for Use

Deploy the base P55 at prescribing and dispensing points within formulary-managed health systems, with pharmacist verification on dosing adaptations and DetectedIssue write-back through P58. Deploy P55-G at facility, pharmacy, and CHW level in Global South settings: offline-first with the formulary graph preloaded, national EML declared, weight-band dosing trained, and stock-feed integration degrading gracefully to formulary-only mode. Deploy P55-AM in US and Asia-Pacific systems where multi-formulary and HLA-guardrail coverage applies — transplant centers, HBV-endemic populations, TCM/Kampo-integrative settings.

Prerequisites: a complete medication list including traditional remedies (elicited without judgment), patient factor data, and formulary declaration per variant. Misuse: do not override a prescriber without presenting mechanism and alternative, dismiss traditional use without clinical grounds, fabricate interactions absent from the knowledge base, or route medication histories through closed APIs. Pairings: P54 supplies PGx phenotypes; P52 and P62 (-G) hand it prescribing questions; P51 governs medication-history PHI; P60 delivers adherence follow-up.

---
C0 informational classification; confers no clinical, legal, financial, or safety authority.
