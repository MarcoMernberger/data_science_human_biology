# Datasets (instructor documentation)

> Status: Phase 1 planning draft. No data has been generated yet. This file is completed file by
> file as `instructor/generate_data.py` creates the datasets (from Phase 3 on). Planned files and
> their use per block: see `syllabus.md` ("Data concept"); planted defects: see `defect_plan.md`.
> All biological claims below were reviewed and accepted by the instructor (Phase 1, revision 3).

## The fictional CRC-P53 study

- 60 patients with colorectal cancer (CRC), IDs `P001`–`P060`; tumour (`_T`) and matched normal
  mucosa (`_N`) sample per patient → 120 samples in 3 sequencing batches (`B1`–`B3`), balanced
  for tissue type and *TP53* status.
- Mutation frequencies (approximately as in CRC): *APC* ~75 %, *TP53* ~55 %, *KRAS* ~40 %
  (independent draws, seeded). Normal samples carry no somatic mutations.
- Cell lines: HCT116 *TP53* wild type (`HCT116_TP53_wt`) and HCT116 *TP53* knockout
  (`HCT116_TP53_ko`), an isogenic pair. HCT116 is *KRAS* G13D mutant and *TP53* wild type.
- Compound: Nutlin-3a (MDM2 inhibitor; molar mass 581.5 g/mol), stabilises wild-type p53.

## Planned gene panel and simulated effects

Expression is simulated on the log2 scale (per-gene baseline + group effects + biological noise),
converted to counts with sample-specific library sizes (negative binomial), and normalised to
log2(CPM + 1).

| Gene | Role | Tumour vs. normal | Other simulated association |
|---|---|---|---|
| *CDKN1A* (p21) | p53 target | ≈ | lower in *TP53*-mutant than wild-type tumours (about 1 log2 unit) |
| *MDM2* | p53 target, negative feedback | ≈ | lower in *TP53*-mutant tumours |
| *BAX* | p53 target (apoptosis) | ≈ | lower in *TP53*-mutant tumours (smaller effect) |
| *RRM2B* | p53 target | ≈ | lower in *TP53*-mutant tumours (smaller effect) |
| *TP53* | tumour suppressor | ≈ | unchanged by status (missense mutants keep mRNA) (simplification: truncating mutations could lower mRNA via NMD) |
| *MKI67* | proliferation | ↑ | – |
| *TOP2A* | proliferation | ↑ | correlated with *MKI67* |
| *MYC* | Wnt target, oncogene | ↑ | – |
| *AXIN2* | Wnt target | ↑ | – |
| *LGR5* | Wnt target, stem-cell marker | ↑ | – |
| *MMP7* | Wnt target, invasion | ↑ (strong) | – |
| *CEACAM5* (CEA) | tumour marker | ↑ (moderate) | – |
| *GUCA2A* | differentiated colonocytes | ↓ (strong) | – |
| *CA1* | differentiated colonocytes | ↓ (strong) | – |
| *CLCA4* | differentiated colonocytes | ↓ | – |
| *DUSP6* | MAPK pathway output | ↑ (small) | higher in *KRAS*-mutant tumours |
| *ETV5* | MAPK pathway output | ≈ | higher in *KRAS*-mutant tumours |
| *CDH1* | epithelial adhesion | ≈ / slight ↓ | – |
| *VIM* | mesenchymal/stromal | variable | high between-sample variance (stroma content) |
| *EGFR* | receptor tyrosine kinase | ≈ | – |
| *GAPDH* | reference | ≈ | stable |
| *ACTB* | reference | ≈ | stable |

## Planned cell-line data

- **Dose response** (`hct116_nutlin_viability.csv`): 4-parameter log-logistic curves.
  IC50 ≈ 2 µM for `HCT116_TP53_wt`, > 30 µM for `HCT116_TP53_ko` (published values
  for HCT116 are roughly 1–5 µM, with strongly reduced sensitivity in p53-null cells);
  concentrations 0.01–30 µM, 3 experiments × 3 technical replicates; viability in % of DMSO.
- **Growth curves** (`hct116_growth_curves.csv`): logistic growth of confluence (%) over 0–120 h every 24 h,
  DMSO vs. 5 µM Nutlin-3a; Nutlin-3a strongly slows wt growth (p53-dependent G1 arrest), slight
  or no effect on ko.
- **qPCR** (`hct116_qpcr_wide.csv`, `hct116_qpcr_long.csv`): *CDKN1A*, *MDM2*, reference
  *GAPDH*; 0, 4, 8, 24 h after 10 µM Nutlin-3a; 3 biological × 3 technical replicates. Induction
  in wt (*CDKN1A* up to ~8-fold, *MDM2* ~4-fold by 8–24 h), none in ko.

## Planned organoid screen (Block 10)

Patient-derived organoids from about 20 cohort patients; drugs 5-FU, oxaliplatin, Nutlin-3a,
cetuximab; viability per concentration. Simulated associations: Nutlin-3a effective only in
*TP53*-wild-type organoids; cetuximab effective mainly in *KRAS*-wild-type organoids (established
anti-EGFR resistance of *KRAS*-mutant CRC); oxaliplatin more effective in *TP53*-wild-type
organoids (its activity depends largely on functional p53 signalling for cell-cycle arrest and
apoptosis; instructor decision); 5-FU without an association with *TP53* status or any other
mutation.

Consequence for the planted defect "mislabelled TP53 annotation" (`defect_plan.md`): the
mislabelled organoid is detectable from **two** drugs (no response to Nutlin-3a and a weak response
to oxaliplatin, unlike the other *TP53*-wild-type organoids).

## Sequences

`crc_amplicons.fasta`: simulated amplicons (150–300 bp, wrapped at 60 characters) named
`<patient>_<gene>_<region>`. The sequences are random with gene-specific GC content and are **not**
real reference sequences; this is stated in the student-facing README.
