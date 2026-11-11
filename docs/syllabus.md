# Syllabus: Data Science with Python for Biomedical Students

> **Status: approved (Phase 1, revision 6).** Two fallbacks (Blocks 03 and 06) are decided only
> after the pilot and are recorded in `development_plan.md`.

## About this course

A one-week block course (5 days, 10 blocks) for bachelor students with a background in biology and
no programming experience. Python is taught as a tool for biomedical data analysis, with AI
assistants (free ChatGPT or free Claude, the student's choice) as part of the whole workflow.
Students learn to write code with and without AI, and above all to **check** code and results.

All data in this course are **simulated**. They imitate a cancer research study but contain no
real patient data.

### Daily schedule

Every day has two blocks. Every block has a 90-minute lecture and a 90-minute hands-on session,
in the order Lecture A, Hands-on A, Lecture B, Hands-on B.

| Day | Theme | Block A | Block B |
|---|---|---|---|
| 1 | Introduction to Python and programming | 01 Python, Jupyter and AI | 02 Variables, data types and operators |
| 2 | Programming and problem solving | 03 Control flow and data structures | 04 Functions and biological programming tasks |
| 3 | Scientific data analysis with NumPy and pandas | 05 NumPy | 06 pandas |
| 4 | Data visualisation | 07 Matplotlib | 08 Seaborn and exploratory visualisation |
| 5 | Scientific analysis, statistics and AI | 09 Data quality, statistics and interpretation | 10 AI-assisted biomedical data analysis |

### How to read this syllabus

- **Core** content is presented in the lecture, practised in the hands-on session and may be
  used in later blocks and in the examination.
- **Optional** content is for self-study. It sits in clearly marked "Optional" sections of the
  lecture notebooks and is not needed for any core exercise, later block or exam question.
  Optional content may appear in the optional stretch exercises. Every hands-on notebook has 4
  optional stretch exercises, used depending on the time available.
- Time tables count **core content only** and add up to at most 90 minutes.
- The AI corner (lecture) and the AI challenge (hands-on) are always core. The instructor shows
  AI tools only briefly and live (for example prompts for reading tracebacks and for explaining or
  generating code). Every notebook contains a saved example answer, labelled as an example, so
  nothing depends on a live AI answer.
- The **concept index** at the end is the complete core vocabulary: every function, method,
  operator, keyword, magic command and library that core code may use, with the block where it is
  introduced.

### The AI-assisted workflow used throughout the course

1. **Define the problem**: the biological question, the data, the expected output (human).
2. **Provide context and prompt the AI**: data structure, column names, types, constraints.
3. **Generate and understand the code** in small steps; ask for explanations.
4. **Execute the code**: inspect outputs and intermediate results (human).
5. **Debug and improve**: read tracebacks, ask for explanations, test the fix.
6. **Test and validate**: known values, small test cases, plausibility (human).
7. **Interpret and document**: biological context, AI use, changes, limitations (human).

Blocks 01–04 practise steps 2–5 on small pieces of code, Blocks 05–09 add step 6 with real
checks, and Block 10 runs the whole loop.

---

## Data concept: one fictional study

All datasets belong to one fictional study, the **CRC-P53 study**. It combines a patient cohort
with cell-line experiments.

**Research theme.** The tumour suppressor p53 (gene *TP53*) is mutated in roughly half of all
colorectal cancers (CRC). The study asks how *TP53* mutation status relates to gene expression in
patient tumours, and how cells with and without functional p53 respond to the MDM2 inhibitor
Nutlin-3a, which activates wild-type p53.

**Patient cohort.** 60 patients with colorectal cancer. For every patient: a tumour sample and a
matched normal mucosa sample (120 samples), clinical information (age, sex, height, weight, tumour
stage, tumour site) and the mutation status of *TP53*, *KRAS* and *APC*. RNA sequencing of a panel
of about 22 genes: p53 target genes, proliferation genes, Wnt target genes, colon differentiation
genes, MAPK/KRAS-related genes and reference genes.

**Cell-line experiments.** The isogenic cell line pair HCT116 *TP53* wild type and HCT116
*TP53* knockout:

- dose-response of cell viability to Nutlin-3a;
- growth curves with and without Nutlin-3a;
- qPCR time course of the p53 targets *CDKN1A* (p21) and *MDM2* after Nutlin-3a, with a
  reference gene, biological and technical replicates.

**Sequences.** Simulated amplicon sequences from the patients (FASTA), used for sequence functions.

**Organoid screen (Block 10).** A new, unfamiliar dataset: drug responses of patient-derived
tumour organoids from the same cohort.

### Planned data files and where they are used

All files live in `data/raw/`. The exact columns are fixed when a dataset is generated and are
documented in `data/README.md`.

| File | Content | Format | Core in blocks | Optional use |
|---|---|---|---|---|
| `crc_amplicons.fasta` | simulated amplicon sequences per patient and gene | FASTA | 04 | |
| `crc_counts_small.csv` | raw RNA-seq counts, small gene × sample matrix | CSV | 05 | |
| `crc_library_sizes_small.csv` | total sequenced reads and tissue type per sample of the small matrix | CSV | 05 | |
| `crc_patients.csv` | one row per patient: clinical data and mutation status | CSV | 06, 07, 10 | |
| `crc_patients.xlsx` | the same table as an Excel file | Excel | | 06 (`read_excel`) |
| `crc_samples.csv` | sample sheet: sample, patient, tissue type, batch, RNA quality, library size | CSV | 06 | 06 (`merge`) |
| `crc_mutations.csv` | long table: one row per mutation (gene, protein change, allele frequency) | CSV | | 06 (`merge`), practice |
| `crc_expression_counts.tsv` | raw counts, one row per sample, one column per gene | TSV | 08 | 06 (`merge`, `melt`) |
| `crc_expression_log2cpm.csv` | normalised expression (log2 CPM) with sample annotation, one row per sample | CSV | 08, 09, 10 | 08 (`melt`, `clustermap`) |
| `hct116_nutlin_viability.csv` | dose-response: viability (% of DMSO control) per concentration and replicate | CSV | 07, 09 | |
| `hct116_growth_curves.csv` | confluence over time per cell line, treatment, replicate | CSV | 07, 08 | |
| `hct116_qpcr_wide.csv` | qPCR Ct values, one row per well-sample, one column per gene | CSV | 09 | |
| `hct116_qpcr_long.csv` | the same qPCR data as a long table (one row per well) | CSV | | 06 (`pivot`, `melt`) |
| `crc_organoid_screen.csv` | organoid drug screen (Block 10, unfamiliar dataset) | CSV | 10 | |

**Wide and long formats.** Core content works with one table at a time, in the layout that the
analysis needs. The optional sections of Block 06 (and Block 08) use the paired files
(`crc_samples.csv` + `crc_expression_counts.tsv`, `hct116_qpcr_wide.csv` + `hct116_qpcr_long.csv`,
`crc_mutations.csv`) to show `merge()`, `melt()` and `pivot()`. Exam assignments do not require them.

**Small values in code.** Blocks 01–03 use small values written directly in the code (for
example the molar mass of Nutlin-3a or five Ct values in a list). From Block 04 on, the notebooks
read files from `data/raw/`.

**Data quality.** The datasets contain realistic data-quality problems. Discovering, handling and
documenting them is part of the exercises, with increasing difficulty: obvious problems with a
hint in Blocks 04–06, problems that become visible in plots in Blocks 07–08, subtle problems in
Block 09, and undisclosed problems in Block 10.

---

## Block 01 – Python, Jupyter and AI (Day 1)

**Learning objective.** Students can open, run, edit and restart a Jupyter notebook in VS Code
(or JupyterLab), switch between command and edit mode and use the essential keys, get help with
`?print`, store values in well-named variables and calculate with them, explain why the execution
order and the kernel state matter for reproducibility, document their work in Markdown, and write
a prompt that asks an AI to explain code without sharing confidential data.

**The one thing that must land:** a notebook is an executable document, and the order in which
cells run matters.

**Concepts introduced**

| Concept | Flag |
|---|---|
| What is a programming language, what is Python | core |
| Interpreter vs. script (`.py`) vs. notebook (short mention only) | core |
| Jupyter notebook: kernel, code cell, Markdown cell, output; the last expression of a cell is shown as output | core |
| Command mode and edit mode (`Esc`, `Enter`); essential keys: run (`Shift+Enter`), add (`A`, `B`), delete (`D`,`D`), cell type (`M`, `Y`) | core |
| VS Code (short): selecting the `.venv` kernel, Jupyter integration, file explorer, working in `my_work/dayNN/`; JupyterLab as the lightweight alternative | core |
| `print()` (one or several values), comments (`#`) | core |
| Literals: whole numbers, decimal numbers and text in quotes (data types formally in Block 02) | core |
| Simple calculations with `+ - * / **` and parentheses | core |
| Getting help: `?print` | core |
| Variables, assignment (`=`), literals vs. variables, calculating with variables | core |
| Naming variables: allowed characters, case sensitivity, descriptive names (snake_case); reserved keywords (two shown: `class`, `for`) cannot be names; do not reuse names that Python already uses, such as `print` (the trap with `list`, `sum`, `max` follows in Block 03) | core |
| Kernel state, execution order, execution counter, stale variables, running a cell twice | core |
| Restart kernel and run all; reproducibility | core |
| Errors are normal: `NameError` after a restart and `SyntaxError` for a keyword as name are *shown* (reading tracebacks is taught in Block 02) | core (preview) |
| Documentation: Markdown cell with a heading and text; comments | core |
| AI-assisted programming: what LLM assistants can and cannot do | core |
| Prompting basics: context, task, constraints, output format; asking for an explanation | core |
| Data privacy with public AI tools | core |
| Further Jupyter and VS Code shortcuts and features (split/merge cells, multi-cursor, command palette) | optional |
| Markdown cheat sheet: lists, emphasis, tables, formulas | optional |
| The Python ecosystem for biomedical data analysis (Biopython, scanpy, …) | optional |

**Concepts assumed:** none (setup done before the course with `README_SETUP.md`).

**Not in scope:** `import`, data types beyond what simple calculations need.

**Dataset / examples.** No files. Values in code: cell numbers, Nutlin-3a stock solution, Ct values.

**Hands-on exercises (selection from the pool in the course specification)**

| # | Exercise (from the pool) | Difficulty |
|---|---|---|
| 1 | **Shortcut drill** (core shortcuts): build a mini lab notebook only with the keyboard: Markdown heading, two code cells, change a cell type, delete a cell, run all. | easy |
| 2 | **Growth by re-running**: `cells = 1000`, then `cells = cells * 2`. Predict, run twice by accident, explain the result, restart and run all. | easy |
| 3 | **Valid names?** Decide which of ten names are valid and which are bad style; try one keyword and see what Python says. | easy |
| 4 | **Ask Jupyter first**: use `?print` to answer two questions about `print()` (what happens with several values, and what is printed between them); compare with what you observe. | easy |
| 5 | **Bench calculator for tomorrow's experiment**: mass of Nutlin-3a for 1 mL of a 10 mM stock (molar mass 581.5 g/mol, C30H30Cl2N4O4), and volumes of stock for 10, 5 and 1 µM working solutions in 2 mL medium. | medium |
| 6 | **qPCR fold change**: `2 ** (ct_control - ct_sample)`; which sample expresses more, and why does a lower Ct mean higher expression? (Normalisation to a reference gene follows in Block 09.) | medium |
| 7 | **Fix the lab notebook**: shuffled cells; restore the order, document with Markdown, finish with restart and run all. | medium |
| 8 | **Notebook detective**: a notebook with out-of-order execution counts and a stale variable; why did two people get different results? Write the explanation in a Markdown cell. | medium |

All seven ideas of the pool are used: five as core exercises (2, 5, 6, 7, 8) and two as the AI
challenge (**Prompt duel**, **Explain this code**). Exercises 1, 3 and 4 practise the core topics
shortcuts, naming and `?print`.

Stretch (optional, used depending on the time available):

1. Use the optional shortcuts (split and merge cells, command palette) to restructure a notebook.
2. Document the bench calculator with the Markdown cheat sheet: a table of the working solutions and the formula C1·V1 = C2·V2.
3. Starting with 1000 cells that double every 24 h: how many doublings until a flask with 10⁶ cells is full? Find out by re-running a cell and counting, then check with a calculation.
4. Python ecosystem: find out what Biopython is for and name one task from this course it could do.

**AI corner (lecture).** What an AI assistant is (it predicts text, it does not run your code, it
can be confidently wrong, its answers vary). Good vs. bad prompt for the same task. Asking the AI
to *explain* code line by line. Never paste patient data or confidential data; describe the
structure instead. Example of a typical AI answer with a wrong dilution calculation; the correct
value is recalculated in a code cell and the difference is printed.

**AI challenge (hands-on).** **Prompt duel** (pairs, different AI tools): a good and a bad prompt
for the same dilution task; compare the answers and numbers with the reference values that a
provided cell computes (independent of exercise 5).
**Explain this code**: let the AI explain a five-line snippet with unfamiliar syntax; change one
value to test one of its claims. Fallback: saved example answers. First entries in the AI usage log.

**AI usage log columns:** `#`, Task, Tool, Prompt (verbatim), Result (accepted / modified / rejected).

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals, how the course works | 3 | Copy to `my_work`, open, select kernel | 5 |
| Tools: what is Python; interpreters and scripts (short mention) | 2 | Exercise 1 (shortcuts) | 8 |
| Tools: Jupyter kernel, cells, Markdown vs. code | 7 | Exercises 2–4 | 17 |
| Tools: command and edit mode, essential keys | 5 | Exercise 5 | 12 |
| Tools: VS Code (short) | 5 | Exercise 6 | 7 |
| `print()`, comments, calculations, `?print` | 8 | Exercises 7–8 | 15 |
| Variables, literals, naming, keywords | 10 | AI challenge | 18 |
| Kernel state, execution order, restart & run all, reproducibility | 12 | Reflection questions, AI usage log | 8 |
| AI-assisted programming (incl. brief live demo, data privacy) | 25 | | |
| Documentation | 5 | | |
| Summary | 4 | | |
| **Total** | **86** | **Total** | **90** |

Compared with the time guide of the specification: tools 19 min (plus 8 min first code),
variables and kernel state 22 min, AI 25 min, documentation and recap 9 min. "Interpreters and
scripts" is only a short mention, which leaves a 4-minute buffer on the first morning.

---

## Block 02 – Variables, Data Types and Operators (Day 1)

**Learning objective.** Students can determine and convert data types, compute biological
quantities (dilutions, concentrations, ages, fold changes) with arithmetic, comparison and logical
operators in the correct order of precedence, use the `math` module for logarithms and square
roots, format results with f-strings and string methods, distinguish syntax, runtime and logical
errors, and read a traceback to fix the four typical beginner errors.

**Concepts introduced**

| Concept | Flag |
|---|---|
| Recap: variables vs. literals; keywords and naming errors | core (recap) |
| `int`, `float`, `str`, `bool`; `True`, `False`; `type()` | core |
| Type conversion (casting): `int()`, `float()`, `str()` | core |
| Arithmetic operators `+ - * / **`, unary minus; `abs()` | core |
| Comparison operators `== != < > <= >=`, Boolean expressions | core |
| Logical operators `not`, `and`, `or` | core |
| Precedence: arithmetic before comparison before `not` before `and` before `or`; rule: use parentheses when in doubt | core |
| Strings: `+` concatenation, f-strings (incl. `:.2f`) | core |
| String methods `.upper()`, `.lower()`, `.count()`, `.replace()`; method = function attached to a value (dot syntax) | core |
| First contact with `import`: `import math`, `math.log10()`, `math.log2()`, `math.sqrt()` (pattern only, shown inside the biological calculations) | core |
| Simple biological calculations (C1·V1 = C2·V2, molarity, age, fold change) | core |
| Syntax errors, runtime errors, logical errors (inside the traceback section) | core |
| Reading a traceback: error type, message, line; `SyntaxError`, `NameError`, `TypeError`, `ValueError` | core |
| Floating-point precision, `round()` | optional |
| PEP 8 style conventions beyond the basic naming rules | optional |
| Integer division and remainder (`//`, `%`) | optional |

**Concepts assumed:** Block 01 (variables, literals, naming, calculations, `print()`, `?print`, run order).

**Dataset / examples.** Values in code: Nutlin-3a stock solution, dilution series, birth years,
Ct values read as text (`"24.7"`), a short DNA string.

**Exercise ideas (hands-on)** – more practice, as the specification asks:

1. Types and casting: convert measurements stored as text into numbers; why does `int("24.7")` fail? (easy)
2. Dilution with C1·V1 = C2·V2. (easy)
3. Mass of Nutlin-3a for a stock solution of a given molarity and volume. (medium)
4. Boolean checks with precedence: predict `not a or b and c`, then add parentheses that make the intention explicit; is a patient older than 50 *and* (stage III *or* IV)? (medium)
5. f-string sample report with formatted numbers. (easy)
6. String methods on a DNA string: upper case, count `G` and `C`, replace `T` with `U`. (easy)
7. `math`: log2 fold change from two expression values; doubling time from a growth rate. (medium)
8. Error hunt: four commented-out broken cells (`SyntaxError`, `NameError`, `TypeError`, `ValueError`); uncomment, read the traceback, fix. (medium)
9. Logical error: a dilution cell runs but gives a wrong result; find it with a value calculated by hand. (medium)
10. Small problem: from a cell count, a counting-chamber factor and a dilution, compute the volume needed to seed 200 000 cells. (hard)

Stretch (optional, used depending on the time available):

1. Floating-point surprise: why is `0.1 + 0.2 == 0.3` `False`? Use `round()` to report a concentration.
2. Split an incubation time in minutes into hours and minutes with `//` and `%`.
3. Serial dilution: how many 1:10 steps are needed to go from a 10 mM stock to below 1 nM? Calculate it with `math.log10()` and check the result with `**`.
4. Rename the badly named variables of a given calculation following PEP 8, without changing the result.

**AI corner (lecture).** Prompt patterns for (a) explaining a traceback (paste the code and the full
error, ask for an explanation, not only a fix) and (b) generating a small calculation. Example of a
typical AI answer that converts with `int()` and silently truncates a concentration; a computed
comparison with a hand-calculated value reveals it.

**AI challenge (hands-on).** Let the AI build a small calculator for a biological problem (e.g.
stock volumes for a dilution series). Review the code, test it with own values and one known case
calculated by hand. Fallback: saved example answer.

**AI usage log columns:** `#`, Task, Tool, Prompt (verbatim), Result.

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals | 2 | Recap | 4 |
| Recap: variables vs. literals, naming errors | 5 | Exercises 1–4 | 22 |
| Data types, `type()` | 8 | Exercises 5–7 | 15 |
| Type conversion | 6 | Exercise 8 (error hunt) | 10 |
| Arithmetic operators | 6 | Exercises 9–10 | 12 |
| Comparison operators, Boolean expressions | 7 | AI challenge | 18 |
| Logical operators and precedence | 7 | Reflection questions, AI usage log | 8 |
| Strings: f-strings, string methods | 10 | | |
| Biological calculations, incl. first contact with `import math` | 10 | | |
| Reading a traceback; syntax, runtime and logical errors | 12 | | |
| AI corner | 8 | | |
| Summary | 2 | | |
| **Total** | **83** | **Total** | **89** |

The time freed by moving variables to Block 01 is used in the lecture by the topics the
specification added (precedence of `not`/`and`/`or`, `import math`, error categories). The extra
practice happens in the hands-on session (10 exercises).

---

## Block 03 – Control Flow and Data Structures (Day 2)

**Learning objective.** Students can write conditions (`if`/`elif`/`else`) and `for` loops with
correct indentation, organise values in lists, tuples and dictionaries, index and slice lists,
tuples and strings, unpack tuples, add, change and delete elements of containers, use `len()` and
`range()`, avoid reusing built-in names, and recognise `IndexError`, `KeyError` and
`IndentationError`.

**Concepts introduced**

| Concept | Flag |
|---|---|
| Why control structures | core |
| `if`, `elif`, `else`; `:` and indentation; `IndentationError` | core |
| Lists `[...]` and tuples `(...)` | core |
| Indexing (incl. negative) and slicing `[start:stop]` of lists, tuples and strings | core |
| Tuple unpacking (`gene, ct = pair`) | core |
| Dictionaries `{key: value}`: lookup `d[key]`, `.keys()`, `.values()`, `.items()` | core |
| Modifying containers: `.append()`, item assignment, `del`, `.pop()`, `.update()` | core |
| Membership `in`, `not in` (lists, strings, dictionary keys) | core |
| `for` loops, iterables and iteration; unpacking in `for gene, ct in pairs` and `for key, value in d.items()` | core |
| Accumulator pattern; augmented assignment `+=` | core |
| `len()`, `range()` | core |
| Built-ins `sum()`, `min()`, `max()` | core |
| Trap: never reuse built-in names such as `list`, `sum` or `max` as variable names | core |
| `IndexError`, `KeyError` | core |
| `while` loops | optional |
| `break`, `continue`, `pass` | optional |
| `enumerate()` | optional |
| Sets | optional |
| List comprehensions (reading level only) | optional |
| Nested data structures | optional |
| Mutable vs. immutable; why `b = a` does not copy a list | optional |
| Sorting with `sorted()` and `.sort()`; slicing with a step | optional |
| `dict.get()` | optional |

**Concepts assumed:** Blocks 01–02 (variables, types, operators, precedence, Booleans, f-strings, string methods, tracebacks).

**Dataset / examples.** Values in code: lists of Ct values, patient ages, a dictionary of gene →
mutation status for one patient, `(gene, ct)` tuples, a short DNA string, tumour stages.

**Exercise ideas (hands-on).**

1. Classify a Ct value as "detected", "late" or "not detected" with `if`/`elif`/`else`. (easy)
2. Index and slice a list of patient IDs: first, last, first three. (easy)
3. Slice a DNA string: extract a codon; is it a start codon? (easy)
4. Unpack `(gene, ct)` tuples in a `for` loop and print a classification for each. (medium)
5. **Growth by re-running, as a loop** (Block 01 problem): double 1000 cells for `range(n)` generations. (medium)
6. Count patients older than 65 (accumulator, `+=`); compare with `sum()` on a prepared list. (medium)
7. Dictionary of gene → mutation status: look up, add, change, delete; loop over `.items()`. (medium)
8. Error hunt: `IndexError` (off-by-one), `KeyError` (gene spelled differently), `IndentationError`, and `sum = 0` that breaks a later `sum()`. (medium)
9. Small problem: from two lists (sample IDs and Ct values) build a dictionary and report all samples with Ct > 35. (hard)

Stretch (optional, used depending on the time available):

1. Count the codons of a DNA string with a `while` loop.
2. Read a list comprehension and rewrite it as a `for` loop; check that both give the same list.
3. Find the positions of all `ATG` start codons in a DNA string with `enumerate()` (or a `while` loop).
4. Mutated genes of two patients: which genes are mutated in both, which in only one? Use sets.

**AI corner (lecture).** Ask the AI to explain a loop line by line; generate a loop from a precise
prompt; find the error in existing code. Example of a typical AI answer with `range(1, len(x))`
that skips the first sample; a computed count against the known number reveals it.

**AI challenge (hands-on).** Give the AI a buggy loop (accumulator reset inside the loop) and ask
it to find the error; check the fixed code with a small test list whose answer is known. Then let
it generate a loop that counts mutated genes; verify on a dictionary with a known count.
Fallback: saved example answer.

**AI usage log columns:** `#`, Task, Tool, Prompt (verbatim), Result, How I checked it.

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals, why control structures | 3 | Recap | 5 |
| `if` / `elif` / `else`, indentation, `IndentationError` | 12 | Exercises 1–4 | 18 |
| Lists and tuples | 7 | Exercises 5–7 | 18 |
| Indexing and slicing (lists, tuples, strings) | 10 | Exercise 8 (error hunt) | 8 |
| Tuple unpacking | 3 | Exercise 9 | 8 |
| Dictionaries | 10 | AI challenge | 20 |
| Modifying containers | 8 | Reflection questions, AI usage log | 13 |
| `for` loops, iteration, accumulator, `+=` | 12 | | |
| `len()`, `range()`, `sum()`/`min()`/`max()` | 5 | | |
| Trap: built-in names | 2 | | |
| `IndexError`, `KeyError` | 4 | | |
| AI corner | 10 | | |
| Summary | 2 | | |
| **Total** | **88** | **Total** | **90** |

---

## Block 04 – Functions and Biological Programming Tasks (Day 2)

**Learning objective.** Students can define (signature and body) and call functions with
parameters, default values and return values, document them with docstrings, test them with
`assert`, explain what objects, classes, attributes and methods are, recognise `try`/`except` and
`raise` in AI-generated code, read a FASTA file line by line (using `split()` and `join()`), and
write small sequence-analysis functions.

**Concepts introduced**

| Concept | Flag |
|---|---|
| `def`: signature (name, parameters) and body; defining vs. calling | core |
| Parameters, arguments, `return`; `return` vs. `print()`; `None` | core |
| Default parameters and keyword arguments | core |
| Local variables (scope) | core |
| `help()`, docstrings (`"""..."""`; a docstring in every function from the start) | core |
| Objects, classes, instances, attributes, methods (concept only; `obj.attribute` vs. `obj.method()`) | core |
| String methods `.split()` and `.join()` (taught inside the FASTA section) | core |
| Simple test cases with `assert`; `AssertionError` | core |
| Sequence functions: length, GC content, counting nucleotides | core |
| Reading a text file: relative paths (`../../data/raw/...`), `with open(..., encoding="utf-8") as f:`, looping over lines, `.strip()`, `.startswith()`; `FileNotFoundError` | core |
| FASTA format; reading a FASTA file into a dictionary | core |
| Recognising `try`/`except` and `raise` in AI-generated code; why a bare `except: pass` hides errors (AI corner, 3 min, reading level) | core |
| Reverse complement | optional |
| Lambda functions | optional |
| Type hints | optional |
| Writing `try`/`except` and `raise ValueError` | optional |

**Concepts assumed:** Blocks 02–03 (strings and string methods, indexing, loops, conditions,
lists, dictionaries, unpacking, tracebacks).

**Dataset.** `crc_amplicons.fasta`.

**Exercise ideas (hands-on).**

1. Function `sequence_length(seq)`; call it on three sequences. (easy)
2. Function `count_nucleotide(seq, base="G")` with a default; call it with a keyword argument. (easy)
3. Add a docstring; view it with `help()`. (easy)
4. Objects: identify the object, the attribute and the method in three given lines. (easy)
5. `return` vs. `print()`: fix a function that prints but returns `None`. (medium)
6. `split()` a FASTA header (`>P001_TP53_ex5`) into patient, gene and region; `join()` wrapped sequence lines. (medium)
7. Write three `assert` tests for `gc_content()` (including a known value and lower-case input). (medium)
8. Read `crc_amplicons.fasta` with the reading function from the lecture; report length and GC content per sequence. Some sequences need attention (hint given): handle and document. (medium)
9. Small problem: function that returns the IDs of all sequences with GC content above a threshold (keyword argument with a default). (hard)

Stretch (optional, used depending on the time available):

1. Reverse complement of a sequence (dictionary of base pairs, slicing with a step).
2. Validate a sequence: `raise ValueError` for invalid bases, and catch it with `try`/`except`.
3. Sort the sequences by GC content with `sorted(..., key=lambda ...)`.
4. GC content in sliding windows of 20 bases along an amplicon; report the window with the highest GC content.

**AI corner (lecture).** The GC content prompt from the course specification. Example of a typical
AI answer that counts only upper-case `G`/`C` or divides by a length that includes `N` bases;
`assert` tests with known values expose it. Recognising `try`/`except` and `raise` in AI code: an
example wraps the calculation in a bare `except: pass`; the next cell shows the sequence it
silently skipped (cells tagged `error-handling`).

**AI challenge (hands-on).** Develop a GC content function with AI, test it with at least three
own test cases, extend it in a targeted way (e.g. ignore `N`), and explain every line in a
Markdown cell. Fallback: saved example answer.

**AI usage log columns:** `#`, Task, Tool, Prompt (verbatim), Result, How I checked it.

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals | 2 | Recap | 5 |
| `def`: signature and body, defining vs. calling | 10 | Exercises 1–4 | 15 |
| Parameters, arguments, `return`, `None` | 10 | Exercises 5–7 | 20 |
| Default and keyword arguments | 6 | Exercises 8–9 | 15 |
| Local variables | 5 | AI challenge | 22 |
| `help()`, docstrings | 3 | Reflection questions, AI usage log | 13 |
| Objects, classes, attributes, methods | 6 | | |
| `assert` and test cases | 7 | | |
| Sequence functions | 10 | | |
| Reading files and FASTA, incl. `split()` and `join()` | 14 | | |
| AI corner (incl. 3 min `try`/`except`/`raise`) | 10 | | |
| Summary | 2 | | |
| **Total** | **85** | **Total** | **90** |

---

## Block 05 – NumPy: Numerical Data Analysis (Day 3)

**Learning objective.** Students can import libraries in the common ways and check their versions,
create and inspect arrays (shape, dimensions, data type), select values by indexing, slicing and
Boolean masks, calculate element-wise, normalise raw counts to CPM and log2 values and detect
`-inf`, sort values and find the order of genes, compute mean, median and standard deviation, and
generate reproducible random numbers with a seeded generator.

**Concepts introduced**

| Concept | Flag |
|---|---|
| Formal `import`: `import x`, `import x as y`, `from x import y`; standard library vs. installed packages; `__version__`; reading the documentation | core |
| Why NumPy; arrays vs. lists | core |
| Vectors and matrices; attributes `.ndim`, `.shape`, `.dtype` | core |
| Creating arrays: `np.array()`, `np.arange()`; `np.zeros()`, `np.ones()` as a short mention | core |
| Loading a numeric text file: `np.loadtxt()` (recipe with `delimiter`, `skiprows`, `usecols`, `dtype=str`) | core |
| Indexing and slicing (1D, 2D `[row, column]`, `[:, j]`) | core |
| Boolean masks; combining masks with `&` and `\|` (parentheses) | core |
| Element-wise calculations, including array with a single number | core |
| `np.log2()`, `np.log10()`, `np.isinf()` | core |
| Raw counts vs. normalised (CPM) and log-transformed expression | core |
| Sorting: `np.sort()`, `np.argsort()`; indexing with an array of positions | core |
| `np.sum()`, `np.mean()`, `np.median()`, `np.std()` (incl. `ddof=1`), `np.min()`, `np.max()`; method forms `.sum()`, `.mean()` (reading) | core |
| Seeded random generator: `np.random.default_rng(42)`, `.normal()`, `.integers()`, `.choice()` | core |
| Array errors: shape mismatch (`ValueError`), `IndexError` | core |
| `np.linspace()`, `np.concatenate()`, broadcasting (e.g. normalising a whole matrix at once) | optional |
| Legacy `np.random.seed()` and the `random` module | optional |
| Row-/column-wise statistics with `axis` | optional |
| Missing values: `np.nan`, `np.nanmean()` | optional |

**Concepts assumed:** Blocks 02–04 (`import math`, types, operators, lists, loops, functions, keyword arguments, objects/attributes/methods, file paths).

**Dataset.** `crc_counts_small.csv` (genes × samples), `crc_library_sizes_small.csv`.

**Exercise ideas (hands-on).**

1. Create arrays of Ct values and concentrations; inspect `shape`, `ndim`, `dtype`. (easy)
2. Load the count matrix; how many genes and samples? (easy)
3. Select one gene, one sample, a block of genes × samples. (easy)
4. Boolean mask: which samples have more than *n* counts for *MKI67*, and which of them are tumours? (medium)
5. Normalise one gene to CPM with the library sizes; then log2(CPM + 1); what happens without `+ 1` (`np.isinf()`)? (medium)
6. Compare raw counts and CPM between two samples with very different library sizes; explain. (medium)
7. Find impossible values in the matrix with a mask (hint given). (medium)
8. Sort the genes of one sample by expression with `np.argsort()`; name the three highest-expressed genes. (medium)
9. Simulate 3 biological replicates with a seeded generator; rerun and show the result is identical. (easy)
10. Small problem: fraction of genes whose log2 expression in a tumour sample exceeds that of its matched normal sample. (hard)

Stretch (optional, used depending on the time available):

1. Normalise the whole count matrix to CPM at once with broadcasting; compare with the gene-by-gene result.
2. Per-gene and per-sample means with the `axis` argument.
3. A measurement is missing (`np.nan`): compare `np.mean()` and `np.nanmean()` and explain.
4. Build a Nutlin-3a concentration series with `np.linspace()` on a log10 scale and join two replicate arrays with `np.concatenate()`.

**AI corner (lecture).** Generate NumPy code with AI and understand it with tiny arrays whose
result can be checked by hand (element-wise operations, masks, normalisation; no broadcasting
needed). Example of a typical AI answer that uses `np.log` instead of `np.log2`, omits the `+ 1`
(producing `-inf`, found with `np.isinf()`) and uses the legacy `np.random.seed()`; a known value
exposes the first, the documentation and the installed version explain the last.

**AI challenge (hands-on).** Ask the AI for a mask that selects highly expressed genes and for a
CPM normalisation; check both on a 2 × 3 test array with hand-calculated results. Ask the AI why
`np.std()` and other tools may give different standard deviations; verify with a tiny example.
Fallback: saved example answer.

**AI usage log columns:** `#`, Task, Tool, Prompt (verbatim), Result, How I checked it.

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals | 2 | Recap | 5 |
| `import` formally, libraries, versions | 7 | Exercises 1–3 | 13 |
| Why NumPy, arrays vs. lists | 5 | Exercises 4–6 | 20 |
| Arrays, shape, dimensions, dtype | 8 | Exercises 7–9 | 15 |
| Creating and loading arrays | 5 | Exercise 10 | 7 |
| Indexing and slicing | 9 | AI challenge | 20 |
| Boolean masks | 9 | Reflection questions, AI usage log | 10 |
| Element-wise calculations, array errors | 6 | | |
| Raw counts vs. normalised/log, `np.isinf()` | 9 | | |
| Sorting: `np.sort()`, `np.argsort()` | 5 | | |
| Mean, median, standard deviation | 5 | | |
| Seeded random numbers | 7 | | |
| AI corner | 8 | | |
| Summary | 2 | | |
| **Total** | **87** | **Total** | **90** |

---

## Block 06 – Pandas: Working with Tables (Day 3)

**Learning objective.** Students can read CSV and TSV files into a DataFrame, explore its structure
and index, select columns and rows, filter and sort, find and handle missing values, duplicates and
inconsistent categories (and document what they did), calculate new columns, summarise groups with
`groupby()` and save the result.

**Concepts introduced**

| Concept | Flag |
|---|---|
| What is pandas; `import pandas as pd`; `pd.__version__` | core |
| Series and DataFrame; index (row labels) and columns; `.index`, `.columns`; creating a small DataFrame from a dictionary (`pd.DataFrame({...})`) for checks | core |
| `pd.read_csv()` for `.csv` and `.tsv` (`sep="\t"`) | core |
| Exploring: `.head()`, `.info()`, `.describe()`, `.shape`, `.dtypes`, `.value_counts()` | core |
| Selecting columns (`df["col"]`, `df[["a", "b"]]`, a range of columns via `df.columns[a:b]`) and rows (`.loc` with labels and conditions) | core |
| Filtering with conditions, `&`, `\|`, parentheses; `.isin()`; `.sort_values()` | core |
| Missing values: `.isna()`, `.sum()` of a Boolean column, `.dropna()`, `.fillna()`; documenting the decision | core |
| Cleaning: `.str.strip()`, `.str.lower()`, `.str.upper()`, `.replace()`, `.duplicated()`, `.drop_duplicates()` | core |
| Calculating new columns | core |
| Series statistics: `.mean()`, `.median()`, `.std()`, `.min()`, `.max()`, `.count()` | core |
| `.groupby()` with `.mean()`, `.count()`, `.size()` | core |
| `.to_csv(..., index=False)` (to `outputs/` or `data/processed/`, never `data/raw/`) | core |
| `KeyError` for columns; pandas 3 idioms (no `inplace=True`, no chained assignment) | core |
| Position-based selection `.iloc` | optional |
| Other formats (`.json`, `.fastq`, `.bam`, `.vcf`) conceptually | optional |
| `.agg()` | optional |
| `pd.read_excel()` | optional |
| `pd.merge()` | optional |
| Wide vs. long format (`.melt()`, `.pivot()`) | optional |

**Concepts assumed:** Blocks 02–05 (types, Booleans, functions, keyword arguments, objects/attributes/methods, Boolean masks with `&`/`|`, NumPy statistics, `import`).

**Dataset.** Lecture: `crc_patients.csv` (new column example: body-mass index from height and
weight). Hands-on: `crc_patients.csv`; AI challenge: `crc_samples.csv` (unfamiliar). Optional
sections: `crc_patients.xlsx`, `crc_samples.csv` + `crc_expression_counts.tsv` (merge),
`hct116_qpcr_long.csv` (pivot / melt), `crc_mutations.csv`.

**Exercise ideas (hands-on).**

1. Load `crc_patients.csv`; number of rows and columns, data types. (easy)
2. `describe()` and `value_counts()`: what looks implausible? (easy)
3. Select patients with stage III or IV; sort by age. (easy)
4. Missing values: count per column; decide and document how to handle them. (medium)
5. Inconsistent categories (hint given): standardise and check with `value_counts()`. (medium)
6. Duplicates: find, remove, document. (medium)
7. New column: age group (`age_years >= 65`). (medium)
8. `groupby()`: number of patients and mean age by *TP53* status. (medium)
9. Small problem: proportion of *KRAS*-mutant patients per tumour stage, after cleaning; save the cleaned table to `data/processed/`. (hard)

Stretch (optional, used depending on the time available):

1. Merge the sample sheet with the patient table (`merge()`) and count tumour samples per stage.
2. Several statistics per group at once with `agg()`.
3. Read `crc_patients.xlsx` with `read_excel()` and check that it equals the CSV version.
4. Convert the long qPCR table to wide format with `pivot()` and back with `melt()`; check the number of rows.

**AI corner (lecture).** Exploring an unfamiliar table with AI without uploading it: share the
column names and `dtypes`, ask for analysis suggestions, then check each suggestion yourself.
Example of a typical AI answer with outdated pandas (`inplace=True`, chained assignment that does
nothing in pandas 3); a computed comparison before and after shows the table did not change. How to
check the installed version and the documentation.

**AI challenge (hands-on).** Explore the unfamiliar `crc_samples.csv` with AI suggestions;
implement them, verify each result independently (e.g. `value_counts()` against the AI's claim,
`shape` before and after filtering). Fallback: saved example answer.

**AI usage log columns:** `#`, Task, Tool, Prompt (verbatim), Result, How I checked it.

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals, what is pandas, import, version | 4 | Recap | 5 |
| Series, DataFrame, index | 7 | Exercises 1–3 | 13 |
| Reading CSV/TSV | 5 | Exercises 4–6 | 20 |
| Exploring | 8 | Exercises 7–8 | 10 |
| Selecting columns and rows | 10 | Exercise 9 | 8 |
| Filtering and sorting | 10 | AI challenge | 22 |
| Missing values | 8 | Reflection questions, AI usage log | 12 |
| Cleaning: categories, duplicates | 9 | | |
| New columns | 5 | | |
| `groupby()` | 8 | | |
| `to_csv()` | 3 | | |
| AI corner | 10 | | |
| Summary | 2 | | |
| **Total** | **89** | **Total** | **90** |

`.iloc` is optional; "numbers stored as text" (`pd.to_numeric`) is taught in Block 09.

---

## Block 07 – Matplotlib: Fundamentals of Data Visualisation (Day 4)

**Learning objective.** Students can explain how a Matplotlib figure is built (a Figure that
contains one or more Axes, each with its own axes, ticks, labels and legend) and why we draw with
`ax.` methods rather than `plt.` functions, choose a suitable basic plot type for a question, create
line plots, scatter plots, bar plots and histograms (including subplots and `figsize`), plot
directly from pandas, draw one line per group with a `groupby` loop, label plots completely (axes
with units, title, legend), style them with colours, markers and line styles, and show and save them.

**Concepts introduced**

| Concept | Flag |
|---|---|
| Why we visualise; which plot answers which question | core |
| Fundamentals of scientific plots: units, readable labels, honest axes, show the data | core |
| `import matplotlib.pyplot as plt` | core |
| **The Figure and Axes objects:** anatomy of a figure (Figure → Axes → x/y axis, ticks, tick labels, title, legend); `fig, ax = plt.subplots()` (recap of tuple unpacking) | core |
| The two interfaces: `ax.` methods (used in this course) vs. `plt.` functions (`plt.plot()`, `plt.title()`, … – recognise in AI code; why `plt.title()` titles only the last subplot) | core |
| Subplots grid (`nrows`, `ncols`, indexing `axes[0]`); figure size `figsize=(width, height)` | core |
| `ax.plot()`, `ax.scatter()`, `ax.bar()`, `ax.hist()` (`bins`) | core |
| `color=`, `marker=`, `linestyle=` (shown inside the line and scatter sections) | core |
| `ax.set_xlabel()`, `ax.set_ylabel()`, `ax.set_title()`, `label=` and `ax.legend()` | core |
| `plt.show()`, `fig.savefig()` to `outputs/`, `fig.tight_layout()` | core |
| Plotting from pandas: `df.plot(...)` (`kind=`, `x=`, `y=`, `ax=`; it returns an Axes); `Series.plot()` as a short mention | core |
| Iterating over groups: `for name, group in df.groupby(...)` (new: iterating a `groupby` object) | core |
| Dose on a log scale via a computed `np.log10()` column | core |
| DPI | optional |
| Error bars (mean ± SD) | optional |
| Logarithmic axes (`set_xscale`, `set_yscale`) | optional |
| Colour-blind-friendly palettes; misleading axes (truncated, dual) | optional |

**Concepts assumed:** Blocks 03–06 (tuple unpacking, `for` loops, objects/attributes/methods, arrays, `np.log10()`, DataFrames, filtering, `groupby`, `value_counts()`).

**Dataset.** `hct116_growth_curves.csv`, `hct116_nutlin_viability.csv`; histogram of ages and bar
plot of stages from `crc_patients.csv` (cleaned in the same notebook with Block 06 steps).

**Exercise ideas (hands-on).**

1. Line plot of one growth curve with labelled axes and units. (easy)
2. Histogram of patient ages with `df.plot()`; change the number of bins; what changes? (easy)
3. Bar plot of patients per tumour stage from `value_counts()` with `.plot()`. (easy)
4. All replicates of both cell lines with `for name, group in df.groupby(...)`: one line per replicate, colour by cell line, legend. (medium)
5. Scatter plot of viability vs. log10 concentration for both cell lines. (medium)
6. **Figure and Axes:** two subplots side by side (DMSO vs. Nutlin-3a) with a suitable `figsize`. A given cell uses `plt.title()` and titles the wrong subplot: fix it with the right Axes; show and save to `outputs/`. (medium)
7. Something in the dose-response plot looks wrong (hint: compare experiments): find the cause in the data and document it. (medium)
8. Something in the growth curves is impossible: find it with a plot and a filter. (medium)
9. Small problem: decide which plot type answers "Does Nutlin-3a slow the growth of TP53 wild-type cells more than of knockout cells?" and build it. (hard)

Stretch (optional, used depending on the time available):

1. Growth curves as mean ± SD with error bars (groupby mean and SD).
2. Dose-response with a logarithmic x axis (`set_xscale`) instead of a log10 column.
3. Redraw a figure with a colour-blind-friendly palette.
4. A bar chart with a truncated y axis exaggerates a difference: show it, then fix it.

**AI corner (lecture).** Ask the AI which plot type suits a research question, and to improve an
existing plot (labels, units, legend). Example of a typical AI answer that mixes `plt.` and `ax.`
calls and connects unsorted time points into a zig-zag line; checking which Axes received the
title, plotting the sorted data and counting the points per line show the problems.

**AI challenge (hands-on).** Let the AI create a growth-curve figure; check that every replicate
and time point is shown (compare the number of plotted points with the number of rows), that the
axes carry units, and that the figure answers the question. Fallback: saved example answer.
From this block on, the full AI usage log is used.

**AI usage log columns (full):** `#`, Task, Tool, Prompt (verbatim), Result, How I checked it, What I changed and why.

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals, why visualise, plot types | 7 | Recap | 5 |
| Fundamentals of scientific plots | 5 | Exercises 1–3 | 13 |
| The Figure and Axes objects; `ax.` vs. `plt.` | 9 | Exercises 4–6 | 19 |
| Subplots grid, `figsize` | 5 | Exercises 7–8 | 12 |
| Line plots, incl. colours, markers, line styles | 8 | Exercise 9 | 8 |
| Scatter plots (log10 column), incl. colours and markers | 6 | AI challenge | 20 |
| Bar plots and histograms | 8 | Reflection questions, AI usage log | 13 |
| Labels, titles, legends | 6 | | |
| Showing and saving figures | 4 | | |
| Groups: `for name, group in df.groupby(...)` | 6 | | |
| Plotting from pandas (`df.plot()`; `Series.plot()` mentioned) | 4 | | |
| AI corner | 10 | | |
| Summary | 2 | | |
| **Total** | **80** | **Total** | **90** |

The lecture keeps a 10-minute buffer. Colours, markers and line styles are shown inside the line
and scatter sections, and `Series.plot()` is a short mention.

---

## Block 08 – Seaborn and Exploratory Data Visualisation (Day 4)

**Learning objective.** Students can use seaborn with DataFrames to plot distributions, compare
groups with boxplots (showing the individual points), relate two variables in scatter plots,
split a figure into panels by a category with the figure-level functions `relplot()` and
`displot()`, display expression data and correlation matrices as heatmaps, explain why heatmaps of
raw counts mislead, and state what a plot does and does not show.

**Concepts introduced**

| Concept | Flag |
|---|---|
| What is seaborn; `import seaborn as sns`; `data=`, `x=`, `y=`, `hue=`, `order=` | core |
| Axes-level functions (draw into one Matplotlib Axes, `ax=`) vs. figure-level functions (create their own Figure with one or more panels; size with `height=` and `aspect=`, not `figsize`) | core |
| `sns.histplot()`, `sns.kdeplot()` | core |
| `sns.displot()` (`kind="hist"` / `"kde"`, `col=`) | core |
| `sns.boxplot()` with the individual points (`sns.stripplot()`) | core |
| `sns.scatterplot()` | core |
| `sns.relplot()` (`kind="scatter"` / `"line"`, `col=`, `row=`) | core |
| Working with the returned figure object: `g.set_axis_labels()`, `g.savefig()` | core |
| `sns.heatmap()` (`cmap`, `vmin`, `vmax`, `annot`); `.set_index()`; transposing with `.T`; raw counts vs. log-normalised values | core |
| Correlation: `.corr()` (Pearson; Spearman as a concept via `method="spearman"`), correlation heatmap | core |
| Comparing categories and groups (`hue=`, panels with `col=`); sample size per group | core |
| What a plot does and does not show (n, variability, overplotting, visual vs. real effect) | core |
| Violin plots | optional |
| Regression lines (`regplot`) | optional |
| Pair plots | optional |
| Clustered heatmaps (`clustermap`), z-scores per gene | optional |
| Long format for seaborn (`melt`) | optional |

**Concepts assumed:** Blocks 05–07 (log transformation, DataFrames, selecting, slicing of column labels, groupby, the Figure and Axes objects, labels, `figsize`, saving).

**Dataset.** `crc_expression_log2cpm.csv`, `crc_expression_counts.tsv`; `hct116_growth_curves.csv`
for `relplot(kind="line")`.

**Exercise ideas (hands-on).**

1. Distribution of one gene's expression: `displot()` with one panel per tissue type (`col=`). (easy)
2. Boxplot with points: *MKI67* in tumour vs. normal. (easy)
3. Boxplot of a p53 target gene by *TP53* status in tumours only. (medium)
4. Scatter plot of two genes with `relplot()`, coloured by tissue type, one panel per *TP53* status; set axis labels and save. (medium)
5. Heatmap of raw counts vs. log2 CPM for the same samples; explain the difference. (medium)
6. Correlation heatmap of the gene panel; pick the strongest pair and plot it as a scatter. (medium)
7. A sample looks unusual in the plots: find it and describe what is special (no removal yet). (medium)
8. Interpretation: which statements does a given plot support, and which not? (medium)
9. Small problem: choose and build the figure that best answers "Is *KRAS* mutation associated with a MAPK target gene in tumours?"; justify the choice. (hard)

Stretch (optional, used depending on the time available):

1. Clustered heatmap with z-scores per gene (`clustermap`).
2. Pair plot of four genes, coloured by tissue type.
3. Violin plot vs. boxplot with points for the same gene: what does each show and hide?
4. Regression line for *MDM2* vs. *CDKN1A* with `regplot()`; what does the line add, what does it not prove?

**AI corner (lecture).** Use AI to propose visualisations for a question and check whether they
answer it. Example of a typical AI answer that builds a heatmap from raw counts (dominated by a few
highly expressed genes), includes an ID-like numeric column in a correlation matrix, and passes
`figsize` to a figure-level function; computed checks (value ranges per gene, the column list of
the matrix, the size of the saved figure) expose all three.

**AI challenge (hands-on).** Explore `crc_expression_log2cpm.csv` with AI-proposed
visualisations; for each figure, write down the research question it answers, check the number of
samples shown, and decide whether it supports the conclusion the AI suggests. Fallback: saved
example answer.

**AI usage log columns (full):** see Block 07.

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals, seaborn vs. Matplotlib | 5 | Recap | 5 |
| Axes-level vs. figure-level functions | 4 | Exercises 1–4 | 18 |
| Distributions: `histplot()`, `kdeplot()`, `displot()` | 8 | Exercises 5–6 | 14 |
| Boxplots with points; comparing groups | 9 | Exercises 7–8 | 12 |
| Scatter plots: `scatterplot()`, `relplot()` with panels | 8 | Exercise 9 | 8 |
| Heatmaps; raw vs. normalised | 13 | AI challenge | 20 |
| Correlation | 10 | Reflection questions, AI usage log | 13 |
| What a plot shows and does not show | 6 | | |
| AI corner | 10 | | |
| Summary | 3 | | |
| **Total** | **76** | **Total** | **90** |

The lecture keeps a buffer of more than 10 minutes. To fit `relplot()` and `displot()`, "comparing
categories and groups" is taught inside the boxplot section (`hue=`) and the `relplot()`/`displot()`
panels (`col=`) instead of in a separate section.

---

## Block 09 – Data Quality, Statistics and Interpretation (Day 5)

**Learning objective.** Students can check a dataset systematically for plausibility, missing
values, numbers stored as text, duplicates, outliers and batch effects; distinguish technical from
biological replicates and avoid pseudoreplication; describe data with mean, median and SD; run and
interpret a t-test and a correlation test with SciPy; report an effect size; and name the main
statistical pitfalls.

**Concepts introduced**

| Concept | Flag |
|---|---|
| Common challenges in biomedical datasets; a data-quality checklist | core |
| Plausibility checks (ranges, `.describe()`, `.value_counts()`); batch effects (boxplot by batch) | core |
| Numbers stored as text: `pd.to_numeric(..., errors="coerce")` | core |
| Missing values, outliers (technical vs. biological; `.quantile()` and the 1.5 × IQR rule), duplicates – recap and decisions | core |
| Descriptive statistics: mean, median, SD (robustness; sample SD) | core |
| Biological vs. technical replicates; pseudoreplication; averaging technical replicates (`.groupby()` with two columns, `.reset_index()`) | core |
| `from scipy import stats`; hypothesis, null hypothesis; `stats.ttest_ind(..., equal_var=False)` (Welch); result attributes `.statistic`, `.pvalue` | core |
| p-values and their interpretation | core |
| Effect sizes: difference of means, log2 fold change | core |
| Correlation tests: `stats.pearsonr()`, `stats.spearmanr()` | core |
| Pitfalls: small n, multiple testing (shown by simulation with a seeded generator), pseudoreplication, outliers, normality assumption (conceptual), correlation ≠ causation | core |
| Standardised effect size (Cohen's d) | optional |
| Coefficient of variation | optional |
| Paired vs. unpaired t-test (tumour vs. matched normal) | optional |
| Mann-Whitney U test | optional |
| Checking normality (histogram, Q-Q plot, Shapiro-Wilk) | optional |
| Benjamini-Hochberg correction with `statsmodels` | optional |
| Confidence intervals | optional |
| Reproducibility and documentation (see Blocks 01 and 10) | optional |

**Concepts assumed:** Blocks 05–08 (`from x import y`, statistics in NumPy, seeded rng, pandas cleaning and groupby, boxplots, scatter plots, correlation).

**Dataset.** `crc_expression_log2cpm.csv`, `hct116_qpcr_wide.csv`, `hct116_nutlin_viability.csv`.

**Exercise ideas (hands-on).**

1. Data-quality checklist on `hct116_qpcr_wide.csv`: types, ranges, text in numeric columns. (easy)
2. Technical replicates: find a failed well; decide and document. (medium)
3. Average technical replicates, then compute ΔCt and ΔΔCt per biological replicate. (medium)
4. Boxplot of expression by batch: is there a batch effect? Describe it. (medium)
5. A "normal" sample does not look normal (hint: marker genes and mutation status): find it and document what you would do. (hard)
6. t-test: *CDKN1A* expression in *TP53*-wild-type vs. mutant tumours; report p-value and log2 fold change. (medium)
7. Correlation between *MDM2* and *CDKN1A*; Pearson vs. Spearman. (medium)
8. Pseudoreplication: t-test on technical vs. biological replicates; compare p-values and explain. (medium)
9. Multiple testing: test all genes; how many would be "significant" by chance? (hard)

Stretch (optional, used depending on the time available):

1. Paired t-test on matched tumour/normal samples; compare with the unpaired result.
2. Benjamini-Hochberg correction of the all-genes test with `statsmodels`.
3. Mann-Whitney U test vs. t-test on data with one outlier.
4. Check the normality assumption with a histogram, a Q-Q plot and the Shapiro-Wilk test.

**AI corner (lecture).** Ask the AI to suggest a statistical method (with context: design,
replicates, sample size), to interpret a result, and critically review its statements. Example of
a typical AI answer that runs a t-test on technical replicates and calls a tiny p-value a "strong
biological effect"; recomputing on biological replicates and reporting the effect size shows the
problem. A simulation with a seeded generator shows that 20 tests on pure noise produce about one
"significant" result.

**AI challenge (hands-on).** Ask the AI which test answers "Does Nutlin-3a induce *CDKN1A* more
strongly in TP53 wild-type cells?"; check the replicate level, run the test, compute the effect
size, and rate three AI interpretation statements as correct, overstated or wrong. Fallback:
saved example answer.

**AI usage log columns (full):** see Block 07.

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals, common challenges | 4 | Recap | 5 |
| Plausibility checks, batch effects, numbers as text | 9 | Exercises 1–3 | 18 |
| Missing values, outliers, duplicates | 7 | Exercises 4–5 | 12 |
| Descriptive statistics | 4 | Exercises 6–8 | 17 |
| Biological vs. technical replicates | 8 | Exercise 9 | 6 |
| Hypothesis testing and t-test | 12 | AI challenge | 20 |
| p-values | 7 | Reflection questions, AI usage log | 12 |
| Effect sizes | 6 | | |
| Correlation tests | 6 | | |
| Statistical pitfalls | 12 | | |
| AI corner | 10 | | |
| Summary | 3 | | |
| **Total** | **88** | **Total** | **90** |

Cohen's d is optional; the normality assumption is treated conceptually.

---

## Block 10 – AI-Assisted Biomedical Data Analysis (Day 5)

**Learning objective.** Students can run a complete analysis of an unfamiliar dataset with AI
assistance: explore its structure and quality, formulate research questions, develop and critique
an analysis plan with AI, carry it out (filter, summarise, visualise, test), interpret the results
critically, and document the analysis and their AI use reproducibly, applying the checks for AI
output learned in Blocks 01–09. This is the rehearsal for the examination.

**Concepts introduced**

| Concept | Flag |
|---|---|
| The complete AI-assisted workflow (7 steps) applied end to end | core |
| Exploring an unfamiliar dataset; finding undisclosed data-quality problems | core |
| Formulating research questions | core |
| Developing an analysis plan with AI: giving context (question, data structure, design, known data problems), asking the AI to critique a plan, checking the plan against the data and the question | core |
| Recap: the AI lessons of Blocks 01–09 as one checklist (prompt with context, ask for explanations, read tracebacks, test with known values and `assert`, check library versions, check plots against the table, check the replicate level and the choice of test, never trust an interpretation unchecked) | core (recap) |
| Carrying out the plan: filtering and summarising; suitable visualisations; interpretation | core |
| Critically reviewing AI-generated code, figures and conclusions | core |
| Reproducible, transparent documentation: raw vs. processed data, restart & run all, Markdown structure, full AI usage log | core |
| What the examination expects (structure of the assignments) | core |
| Version control with git (commit, history) | optional |
| Methods paragraph and figure legends | optional |
| Exporting a notebook to HTML or PDF | optional |

No new functions or libraries in core code. Generating and checking code with AI step by step is
not taught again as a separate lecture topic: it was covered in the AI corners of Blocks 01–09, is
revisited in the recap, and is practised in the hands-on mini-project.

**Concepts assumed:** all core content of Blocks 01–09.

**Dataset.** Lecture: worked example on `crc_patients.csv` + `crc_expression_log2cpm.csv` (one
question end to end). Hands-on: `crc_organoid_screen.csv` (unfamiliar, with undisclosed problems).

**Exercise ideas (hands-on).** A guided mini-project in numbered parts, mirroring the exam:

1. Explore structure and quality; list every problem found and how it was handled. (medium)
2. Formulate two research questions (one given, one own). (medium)
3. Write an analysis plan; ask the AI to critique it; decide which suggestions to accept and why. (medium)
4. Clean and summarise the data. (medium)
5. Create two suitable figures. (medium)
6. Test one hypothesis and report an effect size. (hard)
7. Interpret the results, including limitations. (hard)
8. Restart & run all; complete the AI usage log. (easy)

Stretch (optional, used depending on the time available):

1. Write a short methods paragraph and figure legends for the mini-project.
2. Export the notebook to HTML.
3. Commit the notebook with git and look at the history.
4. Answer a second, own research question on another drug of the organoid screen.

**AI corner (lecture), one section: AI for the analysis plan.** Live (briefly): a prompt that
gives the research question, the column names and types, the design (tumour/normal pairs,
replicates, batches) and the known data problems, and asks for an analysis plan with reasons; then
a prompt that asks the AI to critique a given plan. Example of a typical AI plan that tests all
genes with t-tests on all samples, ignores the batch information and the data-quality step, and
does not mention multiple testing; computed checks (samples per group and batch, number of planned
tests, expected false positives at p < 0.05) show what the plan misses. The section closes with the
recap checklist of the earlier AI lessons.

**AI challenge (hands-on).** The whole mini-project is an AI challenge: every AI interaction is
logged in the full table; every AI result is checked with the recap checklist (row counts, known
values, plots against the table). Fallback: saved example answers per part. **Final discussion
(15 min):** What did AI do well? Where did it make mistakes? Which decisions did students have to
make themselves?

**AI usage log columns (full):** see Block 07.

**Time budget (core only)**

| Lecture | min | Hands-on | min |
|---|---:|---|---:|
| Goals, the workflow end to end | 6 | Introduction to the mini-project | 5 |
| Loading, exploring and checking the quality of an unfamiliar dataset | 15 | Parts 1–3 (explore, questions, plan) | 22 |
| Research questions | 7 | Parts 4–5 (clean, summarise, figures) | 20 |
| AI corner: developing and critiquing an analysis plan with AI | 15 | Parts 6–7 (test, interpret) | 15 |
| Recap: the AI lessons of Blocks 01–09 | 7 | Part 8 (run all, AI log) | 8 |
| Carrying out the plan: filtering, summarising, visualising | 10 | Final discussion | 15 |
| Interpreting and critically reviewing results | 10 | Reflection questions | 5 |
| Documentation and reproducibility | 8 | | |
| What the examination expects | 5 | | |
| Summary | 3 | | |
| **Total** | **86** | **Total** | **90** |

---

## Cross-cutting topics

| Topic | Block | Status | Takes time from |
|---|---|---|---|
| `import`: first contact (`import math`, `math.log10/log2/sqrt`) | 02 (inside the biological calculations) | decided | Block 02 |
| `import`: formal (`as`, `from … import`, standard library vs. packages, versions) | 05 | decided | Block 05 (7 min) |
| f-strings, `.upper()`, `.lower()`, `.count()`, `.replace()` | 02 | decided | Block 02 |
| Indexing and slicing of strings, lists, tuples | 03 | decided | Block 03 (10 min) |
| `.split()`, `.join()` | 04 (inside the FASTA section) | decided | Block 04 |
| List comprehensions (reading level) | 03 | decided: optional | – |
| `SyntaxError`, `NameError`, `TypeError`, `ValueError`; syntax / runtime / logical errors | 02 | decided | Block 02 |
| `IndentationError`, `IndexError`, `KeyError` | 03 | decided | Block 03 (4 min + in the indentation section) |
| `AssertionError`, `FileNotFoundError` | 04 | decided | Block 04 (within the `assert` and file sections) |
| Array errors (shape mismatch `ValueError`, `IndexError`) | 05 | decided | Block 05 (within the element-wise section) |
| DataFrame errors (`KeyError` for columns), pandas 3 chained assignment | 06 | decided | Block 06 (AI corner) |
| Test cases with `assert` | 04 | decided | Block 04 (7 min); reused in 05, 06, 09, 10 |
| Library versions, documentation, outdated idioms in AI answers | 05 (`__version__`, legacy `np.random`), 06 (pandas 3) | decided | AI corners of 05 and 06 |
| Git basics | optional section in Block 10 | decided: optional | – |

---

## Concept index (complete core vocabulary)

Every function, method, attribute, operator, keyword, magic command and library that core code may
use, with the block of its first introduction. Later phases may use only these in core code, and
only from the listed block on. "Preview" means shown before its formal treatment. Optional entries
may be used only in optional sections, stretch exercises and practice notebooks.

### Block 01

| Entry | Kind | Flag |
|---|---|---|
| Python, programming language, interpreter, script (`.py`) | concept | core |
| Notebook, kernel, code cell, Markdown cell, output, execution counter | concept | core |
| The last expression of a cell is displayed | concept | core |
| Command mode / edit mode; `Esc`, `Enter`, `Shift+Enter`, `A`, `B`, `D`,`D`, `M`, `Y` | keys | core |
| Restart kernel and run all | menu action | core |
| `.venv` kernel selection, file explorer, `my_work/dayNN/`, JupyterLab | tool | core |
| `print()` (one or several values, separated by commas) | function | core |
| `#` comment | syntax | core |
| `?print` | IPython help | core |
| Number literals (`1000`, `0.5`), text literals in quotes (`"P001"`) | literal | core |
| `=` assignment; variable | operator | core |
| `+`, `-`, `*`, `/`, `**`, `( )` | operator | core |
| Naming rules, snake_case; keywords `class`, `for` as examples of reserved words | concept | core |
| `NameError`, `SyntaxError` (shown, not yet explained) | exception | core (preview) |
| Markdown: heading (`#`) and text | Markdown | core |
| Reproducibility, documentation, prompting, data privacy | concept | core |
| Further shortcuts (split/merge cells, multi-cursor, command palette) | keys | optional |
| Markdown lists, emphasis, tables, formulas | Markdown | optional |
| Biopython, scanpy (overview only) | library | optional |

### Block 02

| Entry | Kind | Flag |
|---|---|---|
| `int`, `float`, `str`, `bool` | type | core |
| `True`, `False` | keyword | core |
| `type()` | function | core |
| `int()`, `float()`, `str()` | function | core |
| Unary `-`; `abs()` | operator / function | core |
| `==`, `!=`, `<`, `>`, `<=`, `>=` | operator | core |
| `not`, `and`, `or` | keyword / operator | core |
| Operator precedence; parentheses | concept | core |
| `+` for strings (concatenation) | operator | core |
| f-strings `f"..."`, format spec `:.2f` | syntax | core |
| `.upper()`, `.lower()`, `.count()`, `.replace()` | str method | core |
| Method / dot syntax (preview of objects) | concept | core |
| `import math` (pattern only) | keyword | core |
| `math.log10()`, `math.log2()`, `math.sqrt()` | function | core |
| Syntax / runtime / logical errors; traceback | concept | core |
| `SyntaxError`, `NameError`, `TypeError`, `ValueError` | exception | core |
| `round()`; floating-point precision | function / concept | optional |
| `//`, `%` | operator | optional |
| PEP 8 beyond naming | concept | optional |

### Block 03

| Entry | Kind | Flag |
|---|---|---|
| `if`, `elif`, `else` | keyword | core |
| `:` and indentation; `IndentationError` | syntax / exception | core |
| `for … in …` | keyword | core |
| `in`, `not in` (membership) | operator | core |
| `[...]` list, `(...)` tuple | literal | core |
| `[i]`, `[-1]`, `[start:stop]` on lists, tuples, strings | syntax | core |
| Tuple unpacking `a, b = pair`; in `for` loops | syntax | core |
| `{key: value}` dictionary; `d[key]` | literal / syntax | core |
| `.keys()`, `.values()`, `.items()` | dict method | core |
| `.append()`, `.pop()` | list method | core |
| Item assignment `lst[i] = x`, `d[key] = x` | syntax | core |
| `del` | keyword | core |
| `.update()` | dict method | core |
| `+=` | operator | core |
| `len()`, `range()` | function | core |
| `sum()`, `min()`, `max()` | function | core |
| Built-in names must not be reused | concept | core |
| `IndexError`, `KeyError` | exception | core |
| `while` | keyword | optional |
| `break`, `continue`, `pass` | keyword | optional |
| `enumerate()` | function | optional |
| `set()`, `{a, b}` | type | optional |
| List comprehensions | syntax | optional |
| Nested structures; mutability; `b = a` aliasing | concept | optional |
| `sorted()`, `.sort()`; slicing with a step `[::step]` | function / method / syntax | optional |
| `.get()` | dict method | optional |

### Block 04

| Entry | Kind | Flag |
|---|---|---|
| `def`; signature and body | keyword | core |
| Parameters, arguments, default parameters, keyword arguments | concept | core |
| `return` | keyword | core |
| `None` | keyword | core |
| Local variables (scope) | concept | core |
| `help()` | function | core |
| Docstring `"""..."""` | syntax | core |
| Object, class, instance, attribute, method | concept | core |
| `.split()`, `.join()` | str method | core |
| `assert`; `AssertionError` | keyword / exception | core |
| `open(path, encoding="utf-8")` | function | core |
| `with … as …:` | keyword | core |
| Looping over the lines of a file | concept | core |
| `.strip()`, `.startswith()` | str method | core |
| Relative paths `../../data/raw/...`; `FileNotFoundError` | concept / exception | core |
| FASTA format | concept | core |
| `try`, `except`, `raise` (recognise in AI code; reading level only) | keyword | core (reading) |
| Reverse complement | concept | optional |
| `lambda` | keyword | optional |
| Type hints | syntax | optional |
| Writing `try`/`except`, `raise ValueError(...)` | keyword | optional |

### Block 05

| Entry | Kind | Flag |
|---|---|---|
| `import x`, `import x as y`, `from x import y` | keyword | core |
| Standard library vs. installed packages | concept | core |
| `__version__` | attribute | core |
| NumPy (`import numpy as np`) | library | core |
| `np.array()`, `np.arange()` | function | core |
| `np.zeros()`, `np.ones()` (short mention) | function | core |
| `np.loadtxt()` (`delimiter`, `skiprows`, `usecols`, `dtype`) | function | core |
| `.ndim`, `.shape`, `.dtype` | attribute | core |
| `arr[i]`, `arr[i, j]`, `arr[:, j]`, `arr[a:b, c:d]` | syntax | core |
| Boolean mask `arr[arr > x]`; `&`, `\|` with parentheses | syntax / operator | core |
| Element-wise `+ - * / **` with arrays and single numbers | operator | core |
| `np.log2()`, `np.log10()`, `np.isinf()` | function | core |
| `np.sort()`, `np.argsort()`; indexing with an array of positions | function / syntax | core |
| `np.sum()`, `np.mean()`, `np.median()`, `np.std()` (`ddof`), `np.min()`, `np.max()` | function | core |
| `.sum()`, `.mean()` (method forms, reading) | method | core |
| `np.random.default_rng()`; `.normal()`, `.integers()`, `.choice()` | function / method | core |
| Shape-mismatch `ValueError`; array `IndexError` | exception | core |
| `np.linspace()`, `np.concatenate()`, broadcasting | function / concept | optional |
| `np.random.seed()`, `random` module | function / library | optional |
| `axis=` | argument | optional |
| `np.nan`, `np.nanmean()` | constant / function | optional |

### Block 06

| Entry | Kind | Flag |
|---|---|---|
| pandas (`import pandas as pd`), `pd.__version__` | library | core |
| `pd.Series`, `pd.DataFrame`; `pd.DataFrame({...})` | class / function | core |
| `.index`, `.columns`, `.shape`, `.dtypes` | attribute | core |
| `pd.read_csv()` (`sep`) | function | core |
| `.head()`, `.info()`, `.describe()`, `.value_counts()` | method | core |
| `df["col"]`, `df[["a", "b"]]`; a list of gene columns from slicing `df.columns[a:b]` | syntax | core |
| `.loc[...]` | indexer | core |
| `df[mask]` with `&`, `\|` | syntax | core |
| `.isin()` | method | core |
| `.sort_values()` (`by`, `ascending`) | method | core |
| `.isna()`, `.dropna()` (`subset`), `.fillna()` | method | core |
| `.sum()` on a Boolean column (counting) | method | core |
| `.str.strip()`, `.str.lower()`, `.str.upper()` | string accessor | core |
| `.replace()` | method | core |
| `.duplicated()`, `.drop_duplicates()` | method | core |
| `df["new"] = ...` | syntax | core |
| `.mean()`, `.median()`, `.std()`, `.min()`, `.max()`, `.count()` | method | core |
| `.groupby()`; `.size()` | method | core |
| `.to_csv()` (`index=False`) | method | core |
| `KeyError` for column names | exception | core |
| `.iloc[...]` | indexer | optional |
| `.agg()` | method | optional |
| `pd.read_excel()` | function | optional |
| `pd.merge()` | function | optional |
| `.melt()`, `.pivot()` | method | optional |
| `.json`, `.fastq`, `.bam`, `.vcf` (concept) | concept | optional |

### Block 07

| Entry | Kind | Flag |
|---|---|---|
| Matplotlib (`import matplotlib.pyplot as plt`) | library | core |
| Figure and Axes objects; anatomy of a figure (axis, ticks, tick labels, title, legend) | class / concept | core |
| `plt.subplots()` (`nrows`, `ncols`, `figsize`); `fig`, `ax`, `axes[i]` | function | core |
| `plt.plot()`, `plt.title()`, `plt.xlabel()` … (pyplot interface; recognise in AI code, not used in course code) | function | core (reading) |
| `ax.plot()`, `ax.scatter()`, `ax.bar()`, `ax.hist()` (`bins`) | method | core |
| `color=`, `marker=`, `linestyle=`, `label=` | argument | core |
| `ax.set_xlabel()`, `ax.set_ylabel()`, `ax.set_title()`, `ax.legend()` | method | core |
| `plt.show()` | function | core |
| `fig.savefig()`, `fig.tight_layout()` | method | core |
| `df.plot()` (`kind`, `x`, `y`, `ax`; returns an Axes); `Series.plot()` (short mention) | method | core |
| `for name, group in df.groupby(...)` | syntax | core |
| `dpi=` | argument | optional |
| `ax.errorbar()` | method | optional |
| `ax.set_xscale()`, `ax.set_yscale()` | method | optional |
| Colour-blind palettes, misleading axes | concept | optional |

### Block 08

| Entry | Kind | Flag |
|---|---|---|
| seaborn (`import seaborn as sns`) | library | core |
| `data=`, `x=`, `y=`, `hue=`, `order=`, `ax=` | argument | core |
| `sns.histplot()`, `sns.kdeplot()` | function | core |
| `sns.boxplot()`, `sns.stripplot()` | function | core |
| `sns.scatterplot()` | function | core |
| Axes-level vs. figure-level functions | concept | core |
| `sns.displot()` (`kind`, `col`) | function | core |
| `sns.relplot()` (`kind`, `col`, `row`) | function | core |
| `height=`, `aspect=` (size of figure-level plots) | argument | core |
| `g.set_axis_labels()`, `g.savefig()` (returned figure object) | method | core |
| `sns.heatmap()` (`cmap`, `vmin`, `vmax`, `annot`) | function | core |
| `.set_index()` | method | core |
| `.T` (transpose) | attribute | core |
| `.corr()` (`method="pearson"`, `"spearman"`) | method | core |
| `sns.violinplot()` | function | optional |
| `sns.regplot()` | function | optional |
| `sns.pairplot()` | function | optional |
| `sns.clustermap()` (`z_score`) | function | optional |

### Block 09

| Entry | Kind | Flag |
|---|---|---|
| `pd.to_numeric()` (`errors="coerce"`) | function | core |
| `.quantile()`; 1.5 × IQR rule | method / concept | core |
| `.groupby([...])` with two columns; `.reset_index()` | method | core |
| SciPy (`from scipy import stats`) | library | core |
| `stats.ttest_ind()` (`equal_var=False`) | function | core |
| `stats.pearsonr()`, `stats.spearmanr()` | function | core |
| `.statistic`, `.pvalue` | attribute | core |
| Effect size: difference of means, log2 fold change | concept | core |
| Multiple testing, pseudoreplication, small n, normality assumption, correlation vs. causation | concept | core |
| Cohen's d; coefficient of variation; confidence intervals | concept | optional |
| `stats.ttest_rel()`, `stats.mannwhitneyu()`, `stats.shapiro()`, `stats.probplot()` | function | optional |
| statsmodels (`multipletests`) | library | optional |

### Block 10

| Entry | Kind | Flag |
|---|---|---|
| (no new code vocabulary) | – | – |
| `git commit`, `git log` | shell command | optional |
| Notebook export to HTML/PDF | tool | optional |

---

## Learning-goal coverage

"Introduced" = taught in a lecture. "Practised" = hands-on exercises (including the hands-on
session of the introducing block) and the practice notebooks. A goal is flagged if it is not
practised in at least two blocks.

| Learning goal | Introduced | Practised (hands-on) | Assessed in the exam | Flag |
|---|---|---|---|---|
| Python from the ground up | 01–04 | 01–10 | notebook | ok |
| Formulate prompts; translate a scientific question into an analysis task | 01 (prompts), 07 (question → plot), 10 (question → plan) | AI challenges 01–10; 07 ex. 9, 08 ex. 9, 10 | notebook, questions | ok |
| Work with tabular data using pandas | 06 | 06, 07, 08, 09, 10 | notebook | ok |
| Comprehend code and identify the Python concepts used | 03, 04 | reflection questions in every hands-on; 01 AI challenge ("Explain this code"), 04 ex. 4 | questions | ok |
| Debug code, read tracebacks, use AI for troubleshooting | 02, 03 | 01 (first errors, preview), 02 ex. 8–9, 03 ex. 8, 04 ex. 5, 05 (shape errors), 06 (`KeyError`, AI corner), 10 | questions (errors) | ok |
| Create test cases and check code with them | 04 | 04, 05 (test arrays), 06 (independent checks), 09, 10 | questions | ok |
| Basic statistics with NumPy and SciPy | 05 (NumPy), 09 (SciPy) | 05, 06 (groupby), 09, 10 | notebook | **thin for SciPy**: only 09 and 10. Mitigation: a statistics practice notebook (Phase 7). No earlier SciPy block is proposed, because Blocks 05–08 are full. |
| Visualise scientific data with Matplotlib and seaborn | 07, 08 | 07, 08, 09, 10 | notebook | ok |
| Generate and modify code with and without AI | 01 | 01–10 (core exercises without AI, AI challenges with AI) | notebook, questions | ok |
| Assess whether analyses and calculations are valid and appropriate | 06 (cleaning), 09 | 02 ex. 9 (logical error), 06, 07 (defects in plots), 08, 09, 10 | notebook, presentation | ok |
| Spot and correct erroneous AI suggestions | 01 | AI corners/challenges 01–10 (each with a realistic, computed AI error) | questions | ok |
| Interpret and critically reflect on results without trusting AI | 08, 09 | 08 ex. 8–9, 09, 10 | presentation, notebook | **thin**: practised only late in the week (08–10). Mitigation: "AI critique" exercises in the practice notebooks. |
| Analyse and visualise data independently | 08 | 07 ex. 9, 08 ex. 9, 09, 10 | notebook | ok |
| Document code, AI usage and analysis design transparently | 01 | AI usage log in every hands-on; data-cleaning documentation 04–10; 10 | notebook | ok |
| Use AI effectively for programming, debugging and interpretation | 01 | AI corners and challenges in every block | questions (AI) | ok |

---

## AI usage documentation per block

In every hands-on notebook, AI code is marked in the first line of the cell with `# AI-generated`
or `# AI-modified: <what I changed and why>`. The log is a Markdown table before the knowledge
section, one row per AI interaction, with a filled example row. Prompts are logged verbatim. Never
paste real patient data or confidential data into a prompt or into the log. The "Tool" column
(e.g. "ChatGPT (free)", "Claude (free)") is used from Block 01 on; the other columns are added
gradually.

| Blocks | Columns |
|---|---|
| 01–02 | `#`, Task, Tool, Prompt (verbatim), Result (accepted / modified / rejected) |
| 03–06 | `#`, Task, Tool, Prompt (verbatim), Result, How I checked it |
| 07–10 and the examination | `#`, Task, Tool, Prompt (verbatim), Result, How I checked it, What I changed and why |

---

## Examination

The final examination is a 2-hour take-home analysis of an unfamiliar dataset (one assignment per
student), followed by an oral presentation and questions. It draws on core content only. Details
are given to students at the exam date.
