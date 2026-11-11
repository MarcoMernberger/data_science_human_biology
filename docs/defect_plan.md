# Defect plan (instructor only)

> Status: DRAFT (Phase 1). Planned data-quality problems per dataset. `instructor/generate_data.py`
> first writes the clean ground truth to `instructor/answer_keys/clean/`, then the defective copy to
> `data/raw/`, and writes a machine-readable answer key to `instructor/answer_keys/<file>_defects.csv`
> (columns: `file`, `rows` (row IDs), `columns`, `defect_type`, `disclosed`, `block_found`,
> `expected_handling`). Exact rows are fixed by seed when the data is generated (Phases 3–4).

## Principles

- Only defects that can be found and fixed with core concepts taught **up to** the block in which
  they are meant to be found.
- Progression: obvious with a hint (04–06) → visible in a plot (07–08) → subtle (09) →
  undisclosed, several kinds (10, exam).
- "Disclosed" = the exercise says that a problem exists (with a hint), not what it is.
- Students document what they found and how they handled it; silently deleting rows is never the
  expected handling.
- A dataset may carry defects for several blocks. Defects for a later block must not break the
  core code of an earlier block (e.g. no text in a numeric column that Block 06 core code
  calculates with).

## Per dataset

### `crc_amplicons.fasta` (Block 04)

| Defect | Detail | Disclosed | Found in | Expected handling |
|---|---|---|---|---|
| Lower-case sequence | 2 records completely in lower case | yes (hint: compare counts) | 04 | `.upper()` before counting; document |
| Ambiguous bases | 1 record with several `N` | yes | 04 | exclude `N` from the GC denominator or report the fraction of `N`; document |
| Trailing whitespace / empty line | spaces at line ends, one empty line between records | yes | 04 | `.strip()`, skip empty lines |

### `crc_counts_small.csv` (Block 05)

| Defect | Detail | Disclosed | Found in | Expected handling |
|---|---|---|---|---|
| Impossible value | 1 negative count | yes (hint: counts cannot be …) | 05 | find with a mask; report gene and sample; do not use that value |

(Low library size of one sample is a **teaching point**, not a defect: it shows why normalisation is needed.)

### `crc_patients.csv` (Block 06; reused in 07, 10)

| Defect | Detail | Disclosed | Found in | Expected handling |
|---|---|---|---|---|
| Exact duplicated rows | 2 patients appear twice | yes | 06 | `drop_duplicates()`; report how many |
| Inconsistent categories | `sex`: `F`, `female`, `Female `; `tp53_status`: `mutant`, `Mutant`, `MUT`; `tumour_stage`: `III` vs `3` | yes (hint: `value_counts()`) | 06 | standardise with `.str.strip()`, `.str.lower()`, `.replace()`; check with `value_counts()` |
| Random missing values | 4 missing `age_years`, 2 missing `kras_status` | yes | 06 | count with `isna()`; keep rows, exclude from the specific calculation; document |
| Impossible value | 1 negative age | yes (hint: `describe()`) | 06 | set to missing, document |

Block 07 uses `age_years` (histogram) and `tumour_stage` (bar plot): the Block 07 notebooks load the file and apply the
Block 06 cleaning steps (or read the cleaned file produced inside the same notebook), never a file
written by another notebook.

### `crc_samples.csv` (Block 06 AI challenge)

| Defect | Detail | Disclosed | Found in | Expected handling |
|---|---|---|---|---|
| Inconsistent categories | `tissue_type`: `tumour`, `Tumour`, `tumor`, `TUMOUR`, `normal ` | yes (general hint: "this table contains at least three kinds of problems") | 06 | standardise |
| Mixed-case IDs | 3 `sample_id`s in lower case (`p012_t`) | yes (same general hint) | 06 | `.str.upper()`; check uniqueness afterwards |
| Systematic missing values | `rin` missing for all samples of batch `B2` | yes (same general hint; question: "are missing values random?") | 06 | `groupby("batch")` + `isna()`; document that RIN is unknown for B2 rather than imputing |

### `crc_expression_counts.tsv` / `crc_expression_log2cpm.csv` (Blocks 08, 09)

| Defect | Detail | Disclosed | Found in | Expected handling |
|---|---|---|---|---|
| Technical outlier sample | 1 sample with a failed library: very low raw counts, extreme values after normalisation | yes (ex. 7: "a sample looks unusual") | 08 | identify in heatmap/boxplot; describe; exclusion discussed in 09 |
| Batch effect | all samples of batch `B3` shifted by about +0.8 log2 units in a subset of genes | yes (ex. 4: "is there a batch effect?") | 09 | boxplot by batch; document; discuss confounding with tissue type / status (batches are balanced so that it is not fully confounded) |
| Mislabelled sample | 1 sample labelled `normal` with a tumour expression profile (high *MKI67*, *MMP7*, low *GUCA2A*, *CA1*) and a *TP53* mutation in `crc_mutations.csv` / tumour-like status | yes, subtle hint (ex. 5) | 09 | identify with marker genes; do not silently relabel: report, exclude from tumour/normal comparison, document |

### `hct116_nutlin_viability.csv` (Blocks 07, 09)

| Defect | Detail | Disclosed | Found in | Expected handling |
|---|---|---|---|---|
| Unit mismatch | one experiment (`experiment_id` E3) entered in nM instead of µM in `concentration_uM` | yes (hint: compare experiments) | 07 | dose-response curve of E3 shifted by 3 log10 units; convert (÷ 1000), document |
| Impossible value | 1 negative viability | yes | 07 | set to missing; document |
| Not a defect | viability slightly above 100 % at the lowest concentrations | – | 07 | teaching point: plausible relative to DMSO control, keep |

### `hct116_growth_curves.csv` (Block 07)

| Defect | Detail | Disclosed | Found in | Expected handling |
|---|---|---|---|---|
| Impossible value | `confluence_percent` = 112 in one well | yes (ex. 8) | 07 | plot reveals it; filter; document |
| Missing time point | one replicate lacks the 72 h measurement | yes (hint: "count the points per line") | 07 | visible as a gap/shorter line; keep the replicate, document |

### `hct116_qpcr_wide.csv` / `hct116_qpcr_long.csv` (Block 09; long file only optional in 06)

| Defect | Detail | Disclosed | Found in | Expected handling |
|---|---|---|---|---|
| Numbers stored as text | `ct_MDM2` contains `Undetermined` in 2 wells, so the column is text | yes (ex. 1) | 09 | `pd.to_numeric(errors="coerce")`; document |
| Technical outlier | 1 failed well: Ct ~ 7 cycles higher than its two technical replicates | yes (ex. 2) | 09 | exclude that well before averaging technical replicates; document |
| Duplicated rows | 1 well exported twice | yes (part of the ex. 1 checklist: "check for duplicated wells") | 09 | `drop_duplicates()` |

The long file carries the same defects (generated from the same defective data), so the optional
pivot/melt sections show that format changes do not remove problems.

### `crc_mutations.csv` (optional sections, practice)

No planted defects in Phase 1 planning (used for optional `merge` and as the source of truth for the
mislabelled-sample check). Defects may be added in Phase 7 for practice exercises.

### `crc_organoid_screen.csv` (Block 10, all undisclosed)

| Defect | Detail | Expected handling |
|---|---|---|
| Duplicated rows | 3 rows | remove, report |
| Mixed-case / whitespace IDs | `organoid_id` with trailing spaces and lower case | standardise |
| Unit mismatch | one plate in nM | detect in dose-response plot, convert |
| Systematic missing values | all viability values of one plate missing | detect via groupby, document, do not impute |
| Impossible values | 2 negative viabilities, 1 value > 300 % | set to missing |
| Mislabelled annotation | 1 organoid annotated `TP53` wild type that responds to Nutlin-3a and oxaliplatin like the `TP53`-mutant organoids, not like the other wild-type organoids | discuss as a likely annotation error; report, do not silently change |

### Exam datasets

Defined in Phase 6 (one defect list per assignment, in `instructor/assignments/assignment_NN/`).
