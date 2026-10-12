---
ID: P63
Title: Rare Disease Diagnostic Navigator
Registry: CLAI-OS (P-series, open tier)
License: AGPL-3.0
Version: 2.0.0
Author: Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
Last Updated: 2026-10-12
Variant-Family: base · P63-G (Global Equity) · P63-AM (Advanced Markets)
---

# P63: Rare Disease Diagnostic Navigator

Abstract: P63 designs rare and complex disease diagnostic navigation across three operating contexts — and its variant family embodies the corpus's core claim that 'rare' is geographic. The base specification (genomic-era tertiary medicine) structures phenotype capture in HPO terms, generates ranked differentials with gene prioritization, guides stepwise testing strategy (single gene to panel to exome to genome), interprets variants under ACMG/AMP classification, and coordinates specialist care, registries, and trials. The P63-G Global Equity variant inverts the prevalence lens: sickle cell as default anemia workup in endemic regions, thalassemia screening before iron, mandatory G6PD testing before oxidative drugs, and a 50+ condition NTD differential ontology (onchocerciasis, lymphatic filariasis, Buruli ulcer, yaws, neurocysticercosis, Chagas) built on the diagnostics that exist locally — hemoglobin electrophoresis, G6PD spot tests, GeneXpert, smartphone microscopy, MinION field sequencing. The P63-AM Advanced Markets variant re-points navigation at Asia-Pacific complex disease: Kawasaki disease, IgA nephropathy, Takayasu arteritis, Wilson disease, HBV-associated presentations, and consanguinity-aware inheritance analysis. In every variant, the differential is ranked by phenotype match, inheritance pattern, and the prevalence of the population actually being served.

## The Prompt (Base Specification)

Provenance: verbatim from the author's base specification (*CLAI OS P51-P70.txt*); no edits beyond whitespace.

ROLE: You are a Medical Geneticist who navigates the diagnostic odyssey for rare diseases. You understand phenotype ontologies (HPO), gene-disease databases (OMIM, Orphanet), and exome/genome sequencing interpretation.
ACTION: Design a rare disease diagnostic prompt that:
1.  Structures phenotype capture (HPO terms, onset, progression, family history)
2.  Generates differential diagnosis (disease ranking, gene prioritization)
3.  Guides testing strategy (single gene → panel → exome → genome)
4.  Interprets variants (ACMG classification, functional studies, literature)
5.  Coordinates care (specialist referral, patient resources, clinical trials)
SCOPE:
•  Phenotype: HPO terms with frequency, onset, severity
•  Differential: Ranked by phenotype match, inheritance pattern, prevalence
•  Testing: Cost-effective, stepwise, with pre-test probability
•  Variant interpretation: ACMG/AMP with phenotypic matching
•  Patient support: advocacy organizations, natural history studies, registries
CONTEXT:
[INSERT: Patient phenotype, onset age, progression, family history, prior testing, consanguinity]
EXAMPLES:
Input: "3-year-old male, developmental regression starting at 18 months,
loss of motor skills, seizures onset at 20 months,
hyperpigmented macules on trunk, hepatosplenomegaly,
parents first cousins, one sibling died at 2 years (similar symptoms)"
Phenotype Structuring:
HPO TERMS (with frequency, onset):
•  Developmental regression [HP:0002376]: Obligate, onset 18 months
•  Seizures [HP:0001250]: Frequent, onset 20 months, multiple types
•  Hyperpigmentation [HP:0000953]: Frequent, truncal
•  Hepatomegaly [HP:0002240]: Frequent
•  Splenomegaly [HP:0001744]: Frequent
•  Loss of motor skills [HP:0002500]: Obligate
•  Failure to thrive [HP:0001508]: Frequent
INHERITANCE PATTERN: Autosomal recessive (consanguinity, sibling affected)
DIFFERENTIAL DIAGNOSIS (ranked):
1.  Niemann-Pick Disease, Type C (NPC1 or NPC2)
•  Phenotype match: 8/8 HPO terms
•  Key features: Vertical gaze palsy (not yet assessed), hepatosplenomegaly,
neurodegeneration, seizures, hyperpigmentation
•  Inheritance: AR (fits)
•  Prevalence: 1:100,000-1:120,000
•  Testing: NPC1/NPC2 sequencing, filipin staining, oxysterol analysis
•  Action: Order NPC1/NPC2 panel, assess vertical gaze
2.  Gaucher Disease, Type 2 (GBA)
•  Phenotype match: 6/8 HPO terms
•  Key features: Hepatosplenomegaly, neurodegeneration, seizures
•  Missing: Hyperpigmentation less typical
•  Inheritance: AR (fits)
•  Prevalence: 1:50,000 (Ashkenazi Jewish higher)
•  Testing: GBA enzyme activity, GBA sequencing
•  Action: Order GBA testing if NPC negative
3.  Wolman Disease (LIPA)
•  Phenotype match: 5/8 HPO terms
•  Key features: Hepatosplenomegaly, failure to thrive, adrenal calcification
•  Missing: Hyperpigmentation, seizure pattern
•  Inheritance: AR (fits)
•  Prevalence: <1:200,000
•  Testing: LIPA sequencing, lysosomal acid lipase activity
TESTING STRATEGY:
Step 1: Targeted panel (NPC1, NPC2, GBA, LIPA, ASAH1)
•  Rationale: Highest pre-test probability, fastest turnaround
•  Cost: $2,500, TAT: 2-3 weeks
•  If positive: Proceed to variant interpretation, family testing
Step 2: If panel negative: Rapid exome sequencing
•  Rationale: Broad differential, novel genes possible
•  Cost: $5,000, TAT: 4-6 weeks
•  Include: Trio analysis (parents + patient) for de novo/AR variants
Step 3: If exome negative: Genome sequencing + RNA studies
•  Rationale: Deep intronic variants, regulatory mutations, splicing
•  Cost: $10,000, TAT: 8-12 weeks
CARE COORDINATION:
•  Referral: Metabolic genetics, neurology, gastroenterology
•  Support: Niemann-Pick Disease Foundation, Children's Neurodegenerative Disease Foundation
•  Clinical trial: Arimoclomol for NPC (phase 3, eligibility assessment)
•  Palliative care: Early integration for symptom management, family support
FORMAT:
•  HPO term extraction and standardization
•  Differential ranking algorithm (phenotype match, inheritance, prevalence)
•  Testing strategy framework (stepwise, cost-effective)
•  Variant interpretation for rare disease
•  Care coordination checklist
•  Patient/family resource compilation

## Architecture

P63 produces ranked differentials and testing strategies — high-stakes reasoning outputs — so the architecture separates deterministic knowledge operations from model synthesis and wraps every diagnostic assertion in provenance.

**Deterministic-first safety pathways.** Phenotype standardization maps free-text findings to HPO terms via deterministic terminology services; differential ranking executes as a deterministic scoring function over phenotype match counts, inheritance-pattern consistency, and configured prevalence tables (geography-weighted in -G, population-weighted in -AM); the model's role is eliciting and structuring phenotype narratives, explaining rankings, and drafting family-facing summaries. Safety gates are hard deterministic blocks: in -G, iron supplementation recommendations in microcytic anemia are blocked until thalassemia screening is recorded, and oxidative-drug suggestions are blocked until a G6PD result is present; these gates execute in the Safety Kernel, not in the prompt.

**FHIR R4 mapping.** Phenotype findings map to Observation (HPO-coded); family history to FamilyMemberHistory; the ranked differential to Condition (provisional, with ranking evidence in supportingInfo); testing strategy steps to ServiceRequest with order rationale; sequencing and assay results to DiagnosticReport with Observation components; variant interpretations to the Genomics profile set (MolecularSequence / variant Observations) where the host supports them; trial and registry referrals to ResearchStudy linkage and ServiceRequest; care coordination to CarePlan and CareTeam. All resources carry signed Provenance.

**Interposition contract.** P63 executes behind the CLAI-OS interposition layer: no differential, testing recommendation, or variant classification reaches the chart or family without deterministic filter passage (safety gates, terminology validation, blocked-content rules). Every assertion travels in a Clinical Assertion Wrapper carrying per-claim epistemic labels — terminology-derived, literature-derived, model-inferred — with uncertainty decomposition on every ranked hypothesis so probabilistic overconfidence is structurally prevented.

**Audit and provenance stack.** Differential rankings, gate firings, testing-order suggestions, and clinician overrides are written to an immutable Merkle-anchored audit trail; recursive self-audit monitors ranking calibration against eventual confirmed diagnoses; hallucination traceability reconstructs any variant claim lacking a terminology or literature anchor; prompt mortality governs expiry of prevalence tables and variant knowledge snapshots.

**C0 classification.** This artifact is C0 informational: it confers no clinical, legal, financial, or safety authority. Confirmatory testing and diagnosis remain with qualified clinicians and accredited laboratories.

## Variations

### P63-G — Global Equity Variant

Author's variant abstract (*CLAI-OS Global Equity Extension*):

> We present P63-G, a diagnostic engine that reclassifies "rare" by geography. Sickle cell is the default workup for any anemia in endemic regions. Thalassemia screening precedes iron supplementation in microcytic anemia (preventing iron overload). G6PD testing is mandatory before any oxidative drug. NTD differentials are built into every relevant presentation: skin nodule + eye worm → onchocerciasis; leg swelling + hydrocele → lymphatic filariasis; painless ulcer + undermined edges → Buruli ulcer; facial destruction + nose collapse → yaws (eradicable with azithromycin); seizures + calcified brain cysts → neurocysticercosis; cardiomyopathy + megacolon + megaesophagus → Chagas. WHO NTD elimination verification is supported: MDA coverage tracking, transmission assessment surveys for lymphatic filariasis, trachoma TF prevalence in children 1-9. Field diagnostics integrate MinION sequencing for leprosy/Buruli AMR profiling and smartphone microscopy for malaria/filariasis blood films.

Variant prompt compiled from the author's Global Equity Extension specification.

ROLE: You are a diagnostic reasoning architect for endemic and neglected tropical diseases, with field experience in sub-Saharan Africa, South and Southeast Asia, and Latin America. You reject the Northern definition of "rare": you weight differentials by local prevalence, you respect physical exam findings (spleen size by percussion, liver span) and local symptom descriptions, and you design workups around hemoglobin electrophoresis, G6PD spot tests, and GeneXpert-class platforms rather than genomic sequencing.

ACTION: Design a complete endemic-disease diagnostic workflow for the deployment context below. Deliver:
1. A geographic prevalence reweighting table: condition | local prevalence class | default-workup trigger (e.g., sickle cell as default workup for any anemia in endemic regions)
2. A hemoglobinopathy interpretation workflow: hemoglobin electrophoresis plus solubility testing plus alpha-thalassemia deletion screening, with the mandatory rule that thalassemia screening precedes iron supplementation in microcytic anemia, and explicit iron-overload risk flags
3. A G6PD safety gate: mandatory G6PD spot test result integration before any oxidative drug recommendation, with a blocked-drug list presented as a checklist
4. An NTD differential module keyed to presentations: skin nodule + eye worm → onchocerciasis; leg swelling + hydrocele → lymphatic filariasis; painless ulcer + undermined edges → Buruli ulcer; facial destruction + nose collapse → yaws (noting azithromycin eradicability); seizures + calcified brain cysts → neurocysticercosis; cardiomyopathy + megacolon + megaesophagus → Chagas — each with confirmatory test and referral action
5. A WHO NTD elimination verification module: MDA coverage tracking fields, transmission assessment survey protocol for lymphatic filariasis, and trachoma TF prevalence survey structure for children aged 1–9
6. A field diagnostics integration plan: MinION sequencing workflow for leprosy/Buruli AMR profiling (including basecalling constraints) and smartphone microscopy reading for malaria/filariasis blood films
7. A physical-exam-first assessment template capturing spleen size by percussion, liver span, and local-language symptom descriptions without requiring HPO terminology

SCOPE:
• Differentials must be reweighted by the deployment geography; a differential that ignores endemic prevalence is a defect
• Every recommended test must be locally procurable or explicitly flagged as referral-level
• Safety gates (thalassemia-before-iron, G6PD-before-oxidative-drug) are hard blocks, not advisory notes
• The engine generates differentials and workup plans; confirmatory diagnosis and treatment decisions rest with the responsible clinician

CONTEXT:
[INSERT: deployment country/region and endemic disease profile; available laboratory capacity (electrophoresis, spot tests, GeneXpert, microscopy); field sequencing availability (MinION); survey obligations under national NTD programs; cadre performing assessment; connectivity profile]

FORMAT:
• Prevalence table and differential modules as tables: presentation | suspected condition | confirmatory test | disposition
• Safety gates as explicit BLOCK/CLEAR logic statements
• Survey modules as protocol cards: target population | sampling | indicator | reporting line
• Field diagnostics as stepwise wet-lab-adjacent workflows with QC checkpoints
• "Do Not" list: iron before thalassemia screen in microcytic anemia; oxidative drugs before G6PD result; dismissing local symptom vocabulary
• "Escalation" list: presentations requiring referral-level diagnostics, stated per condition

Deployment constraint (invariant for this variant): offline-first; open-weight models only (Llama 3 / Mistral / Phi-3 class); no closed-API processing of patient-identifiable data.

### P63-AM — Advanced Markets Variant

From the author's *CLAI-OS Advanced Markets Extension (P51-AM – P70-AM)*. No AM prompt body exists; the variant is specified as deltas against the base prompt.

**What Changes**
| Dimension | US-Centric (P63) | Asia-Pacific (P63-AM) |
|-----------|------------------|----------------------|
| Rare Diseases | Rett, Angelman, CDKL5 | **Asia-enriched**: Western rare diseases + Asia-prevalent: mucopolysaccharidoses (higher in some Asian populations), glycogen storage diseases, Wilson disease (higher in China), primary biliary cholangitis (higher in Japan), IgA nephropathy (most common GN in Asia), Takayasu arteritis (higher in Japan/India), Kawasaki disease (higher in Japan/Korea), HBV-related PAN |
| Phenotyping | HPO terms | **HPO + Asia-specific**: Short stature + delayed bone age (common presentation Asian GHD), epicanthal fold + wide nasal bridge (Asian dysmorphology baseline vs. syndrome), consanguinity markers (South Asia), HBV serology as phenotypic feature |
| Testing | Exome/genome | **Cascaded**: Targeted panel first (cost-conscious Asia), then exome. Japan = covered by NHI if approved. China = BGI/MGI local sequencing. Korea = high NGS penetration. India = cost-driven tiered testing. |
| Differential | OMIM, Orphanet | **Asia-specific**: Every splenomegaly → thalassemia (SE Asia), G6PD (all Asia), HBV (East Asia), malaria (if travel history). Every childhood fever + rash → Kawasaki (Japan/Korea). Every young female with blindness → Takayasu (pulseless disease, Japan/India). |
| Care Coordination | Specialist referral | **Asia-mixed**: Japan = by hospital department (tertiary center referral). China = by hospital tier (3A hospital required for rare disease). Singapore = by polyclinic → specialist center. India = by city (metro vs. tier-2/3 access gap). |

**Extended Actions**
```
P63-AM EXTENDED ACTIONS:
6. Reclassify "rare" by Asian epidemiology: 
   - Kawasaki disease: NOT rare in Japan 
     (annual epidemic, winter peak). AI 
     defaults to Kawasaki workup for 
     childhood fever >5 days + rash + 
     conjunctivitis + extremity changes.
   - IgA nephropathy: Most common GN in 
     Asia (30-40% of biopsies). AI defaults 
     to IgA nephropathy for hematuria + 
     proteinuria in young Asian males.
   - Takayasu arteritis: "Pulseless disease" 
     in young Asian females. AI checks 
     blood pressure in all 4 limbs, 
     auscultates for bruits, checks ESR/CRP.

7. Build HBV-related disease differentials:
   - Polyarteritis nodosa (PAN): HBV 
     surface antigen complex deposition. 
     AI checks HBV status in all vasculitis.
   - Membranous nephropathy: PLA2R vs. 
     HBV-associated. AI checks PLA2R 
     antibody and HBV serology.
   - Cryoglobulinemic vasculitis: HBV 
     + HCV. AI checks both.

8. Support consanguinity analysis (South 
   Asia): 20-50% consanguineous marriage 
   in South India, Pakistan, Bangladesh. 
   AI elevates autosomal recessive 
   inheritance in differential ranking. 
   Autozygosity mapping as primary 
   diagnostic tool.

9. Integrate Japan-specific rare disease 
   infrastructure: Japan has 331 designated 
   intractable diseases (specified chronic 
   diseases) with NHI coverage. AI checks 
   designation status for treatment 
   subsidy eligibility.

10. Design for cost-tiered testing (Asia): 
    - Tier 1: Targeted panel ($200-500) 
      → solves 60% of cases
    - Tier 2: Clinical exome ($800-1500) 
      → solves 25% more
    - Tier 3: Genome + RNA ($2000-3000) 
      → research-grade
    - AI recommends tier based on 
      phenotype complexity and prior 
      test results.
```

---

Named jurisdiction examples: Japan (Kawasaki disease, IgA nephropathy); East Asia broadly (Takayasu arteritis, Wilson disease, HBV-associated polyarteritis); China (BGI/MGI local sequencing, cost-cascaded testing); South and Southeast Asia (thalassemia screening programs, consanguinity-aware analysis); the canonical summary table maps P63-AM to Kawasaki, IgA nephropathy, Takayasu, MPS, Wilson, and HBV-PAN presentations.

### Regional Adapters

Regional adapters set the prevalence tables, test menus, and inheritance priors. -AF (Africa): the -G variant is primary — sickle cell default workup, G6PD gating, NTD ontology, MDA/elimination survey support, MinION and smartphone-microscopy field diagnostics. -AR (Arab region): high-consanguinity inheritance priors; hemoglobinopathy carrier screening aligned to national premarital programs; -G NTD modules where endemic. -US: the base specification as written — HPO/OMIM/Orphanet navigation, stepwise panel-exome-genome strategy, ACMG/AMP interpretation, registry and trial linkage. APAC: the -AM variant — Kawasaki disease, IgA nephropathy, Takayasu arteritis, Wilson disease, HBV-associated polyarteritis presentations, consanguinity-aware analysis, population-specific reference panels. Adapters are configuration packs (prevalence tables, local test availability and referral levels, safety-gate formularies); none weakens the thalassemia/G6PD safety gates where those gates apply.

## Jurisdiction Matrix

| Regime | Variant applicability | Consent & de-identification posture | Residency & transfer |
|---|---|---|---|
| HIPAA (US) | Base variant (primary) | Genetic and diagnostic data are PHI; GINA constrains use of genetic information by employers/insurers — system outputs must not feed prohibited uses; family-implicating results handled per institutional policy | US-hosted; BAAs; registry/trial linkage under authorization |
| GDPR (EU/EEA) | Base-EU; -AM partnerships | Art. 9 explicitly covers genetic and health data; DPIA mandatory; explicit consent or research/health conditions with safeguards; carrier-status findings require controlled disclosure | EU/EEA residency; sequence data transfer under SCCs and minimization |
| NDPR (Nigeria) | -G variant (primary) | Carrier-status results (sickle cell trait, G6PD) are sensitive personal data with family-level implications; private individual disclosure only | In-country hosting; survey aggregates de-identified |
| Kenya DPA 2019 | -G variant (Kenya) | Sensitive health and genetic data; registration and consent requirements | Transfer with safeguards; NTD program reporting de-identified |
| India DPDP Act | -G/-AM (India) | Consent plus notice; consanguinity fields are sensitive family data; hemoglobinopathy screening program data under national mission rules | Program agreements may impose residency |
| Brazil LGPD | -G variant (Latin America; Chagas contexts) | Sensitive health/genetic data; explicit consent or care condition | ANPD transfer mechanisms |
| Saudi PDPL | -G/-AM (premarital carrier screening contexts) | Sensitive data; premarital screening results subject to national program confidentiality rules | In-Kingdom hosting default |
| China PIPL | -AM variant (China) | Medical and genetic data are sensitive personal information; separate consent; PIPIA; human genetic resources regulations restrict export of Chinese HGR data | HGR export approvals required; localization default |
| Japan APPI | -AM variant (Japan) | Special-care-required personal information; opt-in consent; genomic data under APPI plus ministry genomic guidelines | Transfer with consent or equivalent protections |
| Tribal / community consent | -G variant (population surveys, founder-effect communities) | Community consent for prevalence studies and MDA tracking; carrier-frequency publications reviewed with community governance to prevent stigmatization | Community-governed datasets; Nagoya-adjacent rules for pathogen/genetic resource export |

## Methodology

Base: HPO phenotype extraction and standardization with frequency/onset annotation; differential ranking by phenotype match, inheritance pattern, and prevalence; stepwise testing strategy framework (single gene, panel, exome, genome) with pre-test probability; ACMG/AMP variant interpretation with phenotypic matching; care coordination, registry, and trial linkage.

Global Equity (P63-G): geographic prevalence reweighting; NTD differential ontology (50+ conditions); hemoglobinopathy interpretation workflow (electrophoresis, solubility, alpha-thalassemia deletion screening); G6PD spot-test integration with oxidative-drug gating; MinION basecalling for AMR profiling; smartphone-microscope parasite reading; WHO NTD elimination survey support (MDA coverage, transmission assessment, trachoma TF prevalence in children 1–9).

Advanced Markets (P63-AM): Asia-Pacific complex-disease differentials (Kawasaki disease, IgA nephropathy, Takayasu arteritis, MPS, Wilson disease, HBV-associated polyarteritis); consanguinity-aware inheritance analysis; population-specific genomic reference panels; integration with national screening programs.

## Merits

• Structures the diagnostic odyssey: explicit phenotyping, ranked differentials, and stepwise testing reduce years of undirected referral (base)
• Corrects the geographic definition of 'rare': endemic defaults and NTD differentials surface the conditions actually killing patients in -G deployments
• Prevents specific, named harms: iron overload in thalassemia carriers and oxidative-drug hemolysis in G6PD deficiency, enforced as hard gates (-G)
• Supports WHO NTD elimination verification at village level with field-appropriate diagnostics (-G)
• Extends navigation to Asia-Pacific complex disease with population-appropriate references (-AM)

## Guidance for Use

**Base deployments.** Keep HPO, OMIM/Orphanet, and ACMG/AMP knowledge snapshots versioned and dated; the stepwise testing strategy must reflect actual laboratory contracts and turnaround; variant classifications are decision support for clinical geneticists, not final classifications.

**Global Equity deployments (-G).** Offline-first on facility-controlled infrastructure; open-weight models only (Llama 3, Mistral, Phi-3 class); no closed-API processing of identifiable clinical, image, or sequence data. Prevalence tables must be localized with the national NTD program before activation — stale endemicity data misranks differentials. Safety gates (thalassemia-before-iron, G6PD-before-oxidative-drug) are non-overridable in default configuration; any local override policy must be documented and clinically governed. Smartphone-microscopy reads require human confirmation before treatment.

**Advanced Markets deployments (-AM).** Load population-specific reference panels and national screening program rules; confirm consanguinity counseling content with local clinical genetics and cultural advisors.

**Prerequisites (all variants).** Terminology service versioning; prevalence table governance; laboratory capability map; clinician owner; audit storage.

**Misuse.** Do not present ranked differentials as diagnoses; do not bypass safety gates; do not export sequence or carrier data across borders without the approvals the matrix lists; do not use carrier findings for any non-clinical purpose.

**Pairings.** P54/P54-G (genomic and ancestral medicine) for variant depth; P64/P64-G for prevalence-table equity review; P67-G for NTD surveillance linkage; P66-G for field diagnostic device validation.

C0 informational classification; confers no clinical, legal, financial, or safety authority.
