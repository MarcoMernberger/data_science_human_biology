# Agent instructions: biomedical-data-science course

## 0. Working agreement (read this first, every session)

1. At the start of every session read `docs/course_spec.md` (the specification), `docs/instructor_notes.md` (my notes) and `docs/development_plan.md` (project status). Then tell me which phase we are in, according to `development_plan.md`. Do not infer the phase from the folder contents.
2. `docs/course_spec.md`, `docs/instructor_notes.md` and this file are **read-only** for you. If you think one of them should change, propose the change to me.
3. Work in the phases below. **Never start the next phase until I write "Phase N approved".** At the end of every phase: update `docs/development_plan.md`, summarise what you did, list your assumptions and open questions, and stop.
4. If an instruction is ambiguous or contradicts another one, ask me. Do not guess silently.
5. Do not install libraries, and do not edit `pyproject.toml`, `uv.lock` or the ruff configuration, without asking me first.
6. **Course language:** TODO (Marco: write "English" or "German" here). If this line still says TODO, ask me before starting Phase 1. Code, variable names and code comments are always in English.

## 1. Context

- Course: see `docs/course_spec.md`. 5 days, 10 blocks. **Every block has two notebooks**: a lecture (1.5 h) and a hands-on session (1.5 h).
- Students: bachelor students, biology background, **no programming experience**. They use VS Code and/or JupyterLab. Environment: `uv`, specified in `pyproject.toml`, set up as described in `README_SETUP.md`.
- Data: everything runs offline on local, synthetic, cancer-research-themed data. No internet connection and no external API may be needed.

## 2. Folder structure

```
biomedical-data-science/
├── AGENTS.md
├── CLAUDE.md                  (contains only: @AGENTS.md)
├── README.md
├── README_SETUP.md / README_SETUP.html
├── README_SETUP_german.md / README_SETUP_german.html
├── Makefile
├── pyproject.toml
├── uv.lock
├── .gitignore
├── data/
│   ├── raw/                   (generated once, never modified by notebooks)
│   ├── processed/             (written by notebooks only if the exercise says so)
│   └── README.md
├── scripts/
│   ├── generate_data.py       (creates ALL example data, fixed seeds, deterministic)
│   └── check_course.py        (the checks behind `make check`)
├── src/                       (SOURCE of all notebooks: Jupytext percent-format .py)
│   ├── day01/  Lecture_01.py  Hands_on_01.py  Lecture_02.py  Hands_on_02.py
│   ├── day02/  Lecture_03.py  Hands_on_03.py  Lecture_04.py  Hands_on_04.py
│   ├── day03/  Lecture_05.py  Hands_on_05.py  Lecture_06.py  Hands_on_06.py
│   ├── day04/  Lecture_07.py  Hands_on_07.py  Lecture_08.py  Hands_on_08.py
│   └── day05/  Lecture_09.py  Hands_on_09.py  Lecture_10.py  Hands_on_10.py
├── notebooks/                 (BUILD ARTIFACTS: same layout, .ipynb instead of .py)
├── outputs/                   (figures and files written by notebooks; git-ignored)
├── assignments/
│   └── assignment_01/ ... assignment_05/   (task, data, example solution each)
└── docs/
    ├── syllabus.md
    ├── datasets.md
    ├── development_plan.md
    ├── course_spec.md
    └── instructor_notes.md
```

Notebooks in `src/dayNN/` and `notebooks/dayNN/` are at the same depth, so the same relative data path (`../../data/raw/...`) works for both.

- `docs/syllabus.md`: the full syllabus (Phase 1).
- `docs/datasets.md`: every dataset in `data/`, what each file and column contains, how it was generated, and the biological rationale. **Maintain it continuously** from the moment a dataset is created.
- `docs/development_plan.md`: current phase, what is finished and approved, what is missing, open questions. A new session must be able to continue from this file alone.
- `docs/course_spec.md`: course structure, goals, audience, sessions, examination, AI didactics.
- `docs/instructor_notes.md`: my personal notes. Consult them in every phase.

## 3. Phases

### Phase 1 – Syllabus

Create `docs/syllabus.md` from `docs/course_spec.md`. For each of the 10 blocks include:

- concepts and terms **introduced** in this block;
- concepts **assumed** from earlier blocks;
- learning objective (what students can do afterwards);
- dataset or example idea, and exercise ideas;
- content of the AI corner (lecture) and the AI challenge (hands-on);
- time budget as a table of minutes for lecture and for hands-on. Each must add up to at most 90 minutes.

Also include:

- a **concept index**: for every concept, the block where it is first introduced. No concept may be used before it is introduced.
- a **data concept**: one consistent fictional study (cohort, sample types, columns, genes, mutation status) and which dataset is used in which block.
- the **cross-cutting topics** listed in `docs/course_spec.md`, with the block you propose for each.
- **overload flags**: if a block has more content than fits into 1.5 h for beginners, say so and propose what to move or cut. Never drop or squeeze content silently.

Update `docs/development_plan.md`. Wait for approval.

### Phase 2 – Project setup

Follow `README_SETUP.md` to create the environment. If the file is missing or a step fails, tell me instead of improvising. Create a `Makefile` with at least these targets, and test every one of them:

- `make setup`: create the environment from `pyproject.toml`/`uv.lock` (safe to run repeatedly)
- `make data`: run `scripts/generate_data.py`
- `make lint`: run ruff on `src/` and `scripts/`
- `make check`: all checks from section 5
- `make notebooks`: build `notebooks/` from `src/`
- `make clean`: remove generated files in `outputs/` and temporary files (never `data/raw`)
- `make help`: list the targets

Also create `.gitignore`. Update `docs/development_plan.md`. Wait for approval.

### Phase 3 – Pilot: first block

After I approved the syllabus and the environment works, create `Lecture_01` and `Hands_on_01`:

- as Jupytext percent-format `.py` files in `src/day01/`, following all rules in sections 4 to 6;
- create the data they need with `scripts/generate_data.py` and document it in `docs/datasets.md`;
- run `make check` and fix every problem in the code;
- then build the `.ipynb` files into `notebooks/`;
- run the self-review checklist (section 7) and report the result;
- tell me exactly how you hid the solution cells, so that I can verify it in both VS Code and JupyterLab.

I will review and refine the notebooks, and possibly this file. If so, we repeat this phase. Update `docs/development_plan.md`. Wait for approval.

### Phase 4 – Remaining blocks

Work **one day at a time** (two blocks, four notebooks), in the same way as Phase 3. After each day, update `docs/development_plan.md`, report deviations from the syllabus, and wait for my approval of that day before starting the next one. If a notebook has to deviate from the syllabus, say so; I decide whether the syllabus is updated. I may ask you to redo individual notebooks.

### Phase 5 – Course-wide quality review

After I approved the notebooks, do a consistency pass over the complete course. Do not change notebooks in this phase; report findings first.

- inconsistent terminology;
- inconsistent ordering (concept used before it is introduced);
- difficulty progression;
- time requirements per block;
- technical accuracy of explanations, including the biology;
- consistency of the example data theme.

If asked to repeat this phase, consult `docs/instructor_notes.md` and `docs/development_plan.md` to see what needs to change. Update `docs/development_plan.md`. Wait for approval.

### Phase 6 – Final assignments

Create 5 assignments for the final examination. Each lives in `assignments/assignment_NN/` and contains the task description, the data, and an example solution as a Jupytext percent-format `.py` file.

- Define a typical, not too extensive research question from biomedical research, mainly molecular cancer research, that is complex enough to require the concepts of this course. Students analyse an **unfamiliar** dataset (new columns, not simply a copy of the course data).
- Students must demonstrate that they can:
  - read and analyse data;
  - clean and filter data;
  - calculate appropriate scores, measurements and summaries;
  - generate appropriate visualisations (heatmaps, scatterplots, boxplots);
  - interpret results correctly in the biological and biomedical context;
  - document their solution.
- Students must document where and for what purpose they used which AI tool, which code was generated by AI, and where and why they modified it. Provide a short template for this (an AI usage log) in each assignment.
- Formulate the task explicitly so students know what is expected. State which course blocks each part draws on.
- Generate plausible synthetic data (see section 6) with `scripts/generate_data.py`.

Update `docs/development_plan.md`. Wait for approval.

### Phase 7 – Dataset documentation

Check that `docs/datasets.md` is complete and correct: every file in `data/` and `assignments/*/`, its columns, meaning, units, generation method and biological rationale. Update `docs/development_plan.md`.

## 4. Technical rules: building notebooks

- The `.py` files in `src/` are the only source. Never edit `.ipynb` files directly. Whenever a `.py` file changes, rebuild its `.ipynb` (`make notebooks`).
- Jupytext percent format: markdown cells are `# %% [markdown]`, code cells are `# %%`. Keep the cell order. All notebooks use the same jupytext header and the same kernelspec (`python3`, display name "Python 3 (ipykernel)"), so they work with whatever virtual environment the student selects.
- Lecture `.ipynb` files are built **with executed outputs** (students use them as a reference). Hands-on `.ipynb` files are built **with all outputs cleared**. (Marco: confirm or change.)
- Notebooks must run top to bottom in a fresh kernel in under 60 seconds.
- Do not use `try/except` and do not suppress exceptions to make checks pass. Fix the code instead.
- **Intentional errors** (traceback demonstrations, typical mistakes) are the only exception: such a cell is tagged `raises-exception`, is announced by a markdown cell ("the next cell fails on purpose"), and is placed at the end of its section. `make check` must verify that exactly these cells raise an error, and that every tagged cell really does.
- Notebooks may never overwrite files in `data/raw/`. Anything a notebook writes goes to `outputs/` or, where the exercise says so, `data/processed/`.

## 5. What `make check` must do

`scripts/check_course.py` and the Makefile implement the following, and `make check` fails if any of them fails:

1. Python syntax check of every `.py` in `src/`, `scripts/` and `assignments/`.
2. `make lint` (ruff) passes.
3. Every `.py` converts to `.ipynb` and executes top to bottom without errors (apart from the tagged cells above).
4. Execute each notebook twice and compare the cell outputs (apart from timings). Results must be identical, which proves fixed seeds.
5. Hash `data/raw/` before and after execution. It must be unchanged.
6. All files that a notebook reads exist under `data/`. No absolute paths, no URLs.
7. Every package imported by a notebook is declared in `pyproject.toml`.
8. Every notebook has the required sections (section 6), every exercise has a solution cell, and solution cells carry the `solution` tag.
9. No `try:` in notebook sources, no `input()`, no network access.
10. `notebooks/*.ipynb` match what is built from the current `src/*.py`.

**Ruff:** `pyproject.toml` selects all rules. Some of them conflict with what we teach, for example `NPY002` (legacy `np.random.seed`), `S311` (`random` module) and `S101` (`assert`). Do not change the code to satisfy such a rule if it makes it less readable for beginners, and do not edit the ruff configuration yourself. Collect these cases and ask me which ones to ignore.

## 6. Technical rules: content

**Both notebook types**

- Follow the structures in `docs/course_spec.md` (lecture: goals, introduction, concepts with commented code examples, biological examples, typical mistakes, AI corner, summary; hands-on: goals, recap, exercises, AI challenges, reflection questions, knowledge section).
- Every cell must have a didactic purpose.
- Code must be readable for beginners: explicit, simple, no clever one-liners. Only use Python concepts introduced in the current or an earlier block (see syllabus concept index).
- Show no dummy results. All numbers, tables and figures are computed by the code when the notebook runs.
- Do not rely on variables defined in other notebooks.
- Target the library versions installed through `pyproject.toml` (for example pandas 3.x). Avoid outdated idioms such as `inplace=True` and chained assignment, unless a cell shows them on purpose as a typical AI mistake.
- Calibrate the length from the time budget: as a starting point, 4 to 6 core concepts and about 25 code cells for a lecture, and 8 to 10 exercises for a hands-on session. We will adjust these numbers after the pilot.

**AI corner and AI challenges**

- Notebooks cannot call AI tools (no internet). A prompt is shown as markdown. An AI answer shown in a notebook is **written by you as an illustrative example**, labelled "Example of a typical AI answer; real answers differ", and its code is executed like any other code.
- When the point is that AI makes a mistake, the mistake must be realistic and subtle. Show that it is wrong with a computed check (for example, an `assert` or a comparison against a known value), not just by claiming it.
- AI challenges give students a prompt template, a place to paste the AI's code (commented out so the notebook still runs), and an AI usage log table to fill in.

**Hands-on notebooks**

- Hands-on notebooks must be executable as delivered. Incomplete code is valid Python and commented out, so that it raises no exception.
- Increasing difficulty ladder; mark the difficulty of each exercise. Include small problems that need independent thinking, not only recapitulation.
- Exercises must not depend on previous unfinished exercises.
- Solutions are placed only in the final section. Each solution cell is tagged `solution` and collapsed (`jupyter: {source_hidden: true, outputs_hidden: true}`), so that neither code nor output is visible until expanded. Each solution is self-contained and uses its own variable names (for example with the suffix `_solution`), so it does not collide with the students' variables.

**Example data**

- All data is created by `scripts/generate_data.py` (fixed seeds, deterministic, no manually entered data) and lives under `data/`. Formats: `.tsv`, `.csv`, Excel, `.fasta`.
- Data is synthetic but biologically and scientifically plausible:
  - tumour samples have cancer-related genes with higher or lower expression than normal samples;
  - a mutation can be associated with an expression pattern;
  - technical replicates are similar, unless flawed measurements are the point;
  - biological replicates show realistic variation;
  - missing values and outliers are added deliberately for didactic purposes.
- Use real gene symbols with known cancer roles and the correct direction of change. Record the rationale in `docs/datasets.md`. If you are unsure about a biological claim, mark it for my review instead of asserting it.
- State in every data README and in the notebooks that the data is simulated and not real patient data.
- One consistent theme throughout the course, as defined in the syllabus.

## 7. Self-review checklist (run before presenting any notebook)

- Does it follow the structure in the course spec, and does every cell have a purpose?
- Is every concept either introduced here or listed as introduced earlier in the syllabus?
- Does the time budget fit (90 minutes)?
- Could a student with no programming experience follow each code cell?
- Are all results computed, and do solutions run?
- Is every AI example labelled and checked?
- Is the biology correct and plausible?
- Does `make check` pass without any suppressed errors?
