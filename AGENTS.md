# Agent instructions: data_science_human_biology course

## 0. Working agreement (read this first, every session)

1. At the start of every session read this file, `docs/development_plan.md` (project status) and `docs/instructor_notes.md` (my notes). Then read `docs/course_spec.md` (the specification) as needed for the phase: all of it in Phases 1, 5 and 6; in the notebook phases (3, 4, 7) everything except the section "Final examination", with special attention to the blocks you work on; in Phases 2, 8, 9 and 10 the parts relevant to the task. Then tell me which phase we are in, according to `development_plan.md`. Do not infer the phase from the folder contents.
2. `docs/course_spec.md`, `docs/instructor_notes.md` and this file are **read-only** for you. If you think one of them should change, propose the change to me.
3. Work in the phases below. **Never start the next phase until I write "Phase N approved".** At the end of every phase: update `docs/development_plan.md`, summarise what you did, list your assumptions and open questions, and stop.
4. If an instruction is ambiguous or contradicts another one, ask me. Do not guess silently.
5. Do not install libraries, and do not edit `pyproject.toml`, `uv.lock` or the ruff configuration, without asking me first.
6. **Course language: English.** All notebook text, code, comments, variable names and documentation are in English. The only German file is `README_SETUP_german.md`.

## 1. Context

- Course: see `docs/course_spec.md`. 5 days, 10 blocks. **Every block has two notebooks**: a lecture (1.5 h) and a hands-on session (1.5 h).
- Students: bachelor students, biology background, **no programming experience**. They use VS Code and/or JupyterLab. Environment: `uv`, specified in `pyproject.toml`, set up as described in `README_SETUP.md`.
- Data: everything runs offline on local, synthetic, cancer-research-themed data. No internet connection and no external API may be needed.

## 2. Folder structure and repositories

This (private) repository contains everything. The student repository contains only the parts marked "public".

```
data_science_human_biology/
├── AGENTS.md                      private
├── CLAUDE.md                      private (contains only: @AGENTS.md)
├── Makefile                       private
├── README.md                      public
├── README_SETUP.md / .html        public
├── README_SETUP_german.md / .html public
├── pyproject.toml                 public
├── uv.lock                        public
├── .gitignore                     private (the student repository gets its own, see below)
├── assets/                        public: example figures and images that illustrate the notebooks (provided by me)
├── data/                          public
│   ├── raw/                       generated once, never modified by notebooks
│   ├── processed/                 written by notebooks only if the exercise says so
│   └── README.md                  student-facing: what each file contains (columns, units, "simulated data")
├── notebooks/                     public: BUILD ARTIFACTS, same layout as src/, .ipynb instead of .py
│   ├── 00_setup_test.ipynb        instructor-made environment test (the only hand-made notebook)
│   ├── Table_of_Contents.ipynb    created in Phase 9
│   ├── day01/ ... day05/          Lecture_NN.ipynb, Hands_on_NN.ipynb
│   └── practice/                  Practice_NN_<topic>.ipynb
├── outputs/                       public but empty (only .gitkeep): figures and files written by notebooks
├── assignments/                   public, but only from the exam date on
│   └── assignment_01/ ... assignment_05/   task description, data, AI usage log template
├── docs/                  private
│   ├── course_spec.md
│   ├── syllabus.md                created in Phase 1
│   ├── datasets.md                detailed description of all datasets
│   ├── development_plan.md
│   ├── instructor_notes.md
│   ├── defect_plan.md             planted data-quality problems per dataset (Phase 1)
│   └── instructor_guides/         lecture and hands-on guides for me only (Phase 10)
├── src/                           private: SOURCE of all notebooks, Jupytext percent-format .py
│   ├── day01/  Lecture_01.py  Hands_on_01.py  Lecture_02.py  Hands_on_02.py
│   ├── day02/  Lecture_03.py  Hands_on_03.py  Lecture_04.py  Hands_on_04.py
│   ├── day03/  Lecture_05.py  Hands_on_05.py  Lecture_06.py  Hands_on_06.py
│   ├── day04/  Lecture_07.py  Hands_on_07.py  Lecture_08.py  Hands_on_08.py
│   ├── day05/  Lecture_09.py  Hands_on_09.py  Lecture_10.py  Hands_on_10.py
│   ├── practice/                  Practice_NN_<topic>.py
│   └── Table_of_Contents.py
├── scripts/                       private
│   ├── check_course.py            the checks behind `make check`
│   └── student.gitignore          becomes the .gitignore of the student repository
└── instructor/                    private
    ├── generate_data.py           creates ALL example, practice and exam data; fixed seeds, deterministic
    ├── answer_keys/               planted-defect answer keys and clean ground-truth datasets
    └── assignments/               assignment_01 ... assignment_05: example solution, question bank, defect answer key, grading notes
```

**Student repository.** It contains exactly the folders `assets/`, `notebooks/`, `outputs/`, `data/`, and `assignments/` (only from the exam date on; I decide when), plus the root files `README.md`, `README_SETUP.md/.html`, `README_SETUP_german.md/.html`, `pyproject.toml`, `uv.lock` and a `.gitignore` made from `scripts/student.gitignore`. That `.gitignore` ignores `.venv/`, `my_work/`, `outputs/*` (except `outputs/.gitkeep`), `__pycache__/` and `.ipynb_checkpoints/`. Everything else is never published. `make student_repo` assembles it in `build/student_repo/`. Students clone it, so everything in it is visible to them: nothing public may reveal solutions, planted defects or exam content, and nothing public may reference a private folder. The course material is also published on the ILIAS platform (see `make html`).

**`assets/`** contains example figures and JPEGs that I provide purely as illustrations for the notebooks and the READMEs. Never modify, rename or add files there. Notebooks may embed them with relative paths (`../../assets/<file>`). If you need an image that does not exist, ask me.

**Depth rule:** every notebook that reads data or images sits exactly two levels below the repository root (`src/dayNN/`, `src/practice/`, `notebooks/dayNN/`, `notebooks/practice/`). Students work in copies at `my_work/dayNN/`, which have the same depth, so `../../data/...` and `../../assets/...` work everywhere.

**Documentation files:**

- `docs/syllabus.md`: the full syllabus (Phase 1). I may give it to students through ILIAS, so it should read cleanly, but it is not part of the student repository.
- `docs/datasets.md`: every dataset, what each file and column contains, how it was generated, and the biological rationale. **Maintain it continuously** from the moment a dataset is created. Students get only the short `data/README.md`, which describes each file, its columns and units, and states that the data is simulated. It must not give away the biological structure that exercises ask students to discover, and no planted defect.
- `docs/development_plan.md`: current phase, what is finished and approved, what is missing, open questions. A new session must be able to continue from this file alone.
- `docs/course_spec.md`: course structure, goals, audience, sessions, examination, AI didactics.
- `docs/instructor_notes.md`: my personal notes. Consult them in every phase.
- `docs/defect_plan.md`: which planted data-quality problems each dataset contains (Phase 1).
- `docs/instructor_guides/`: my private guides for lecturing and supervising (Phase 10).

## 3. Phases

### Phase 1 – Syllabus

Create `docs/syllabus.md` from `docs/course_spec.md`. For each of the 10 blocks include:

- concepts and terms **introduced** in this block, each flagged **core** or **optional** as in `docs/course_spec.md`;
- concepts **assumed** from earlier blocks;
- learning objective (what students can do afterwards);
- dataset or example idea, and exercise ideas;
- content of the AI corner (lecture) and the AI challenge (hands-on);
- time budget as a table of minutes for lecture and for hands-on. It counts **core content only** and must add up to at most 90 minutes each. Optional content is not counted.

Also include:

- a **concept index**: for every concept, the block where it is first introduced and whether it is core or optional. It must be **complete**: it lists every function, method, operator, keyword, magic command (such as `?print`) and library that appears in core code, one entry each, and it is the vocabulary that all later phases may use. No concept may be used before it is introduced, and no core content may depend on optional content.
- a **data concept**: one consistent fictional study (cohort, sample types, columns, genes, mutation status) and which dataset is used in which block.
- the **cross-cutting topics** listed in `docs/course_spec.md`, with the block you propose for each.
- a **learning-goal coverage table** that refines the planned coverage in `docs/course_spec.md`. Every learning goal must be introduced in at least one block and practised in at least two. Flag gaps.
- the **AI usage documentation** per block (which columns of the log apply, see the spec).
- **overload flags**: if a block has more content than fits into 1.5 h for beginners, say so and propose what to move or cut, in particular which core topics could become optional. Never drop, squeeze or move content silently, and never promote optional content to core. Report these flags to me and record them in `docs/development_plan.md`. Once I have decided, `docs/syllabus.md` shows only the final version.

Write the **defect plan** (which planted data-quality problems each dataset contains and in which block students find them) to `docs/defect_plan.md`, not into the syllabus.

Update `docs/development_plan.md`. Wait for approval.

### Phase 2 – Project setup

Create the environment using the relevant steps of `README_SETUP.md` (`uv` and `uv sync`; do not install VS Code or its extensions) and verify it by executing `notebooks/00_setup_test.ipynb`. That notebook and the README are instructor-made and tested: do not modify them, report problems to me. If a file is missing or a step fails, tell me instead of improvising. Create a `Makefile` with at least these targets, and test every one of them:

- `make setup`: create the environment from `pyproject.toml`/`uv.lock` (safe to run repeatedly)
- `make data`: run `instructor/generate_data.py`
- `make lint`: run ruff on `src/`, `scripts/` and `instructor/`
- `make check`: all checks from section 5
- `make notebooks`: build `notebooks/` from `src/` (including `notebooks/practice/` and the table of contents)
- `make clean`: remove generated files in `outputs/` and temporary files (never `data/raw`)
- `make student_repo`: assemble `build/student_repo/` from the whitelist in section 2 and nothing else (without `assignments/`, unless called with `RELEASE_ASSIGNMENTS=1`). Create `outputs/.gitkeep`, write the student `.gitignore`, and fail if a public file references a private path (`src/`, `scripts/`, `instructor/`, `docs/`).
- `make student_check`: in a fresh copy of `build/student_repo/`, run `uv sync` and execute every notebook. This proves that the student repository works without any private file.
- `make html`: export the lecture notebooks as HTML into `build/html/` (for ILIAS; readable without a Python environment). Lecture notebooks only, never hands-on notebooks.
- `make readme_html`: regenerate `README_SETUP.html` and `README_SETUP_german.html` from the `.md` files (package `markdown` from the dev group).
- `make help`: list the targets

The Makefile is for you and for me only. Students never need `make` (it is not available on Windows by default); everything they need is in `README_SETUP.md`.

Also create the private `.gitignore` (`.venv/`, `build/`, `my_work/`, `outputs/*` except `outputs/.gitkeep`, `__pycache__/`, `.ipynb_checkpoints/`; `instructor/` and `docs/` are tracked in this private repository) and `scripts/student.gitignore`. Update `docs/development_plan.md`. Wait for approval.

### Phase 3 – Pilot: first block

After I approved the syllabus and the environment works, create `Lecture_01` and `Hands_on_01`:

- as Jupytext percent-format `.py` files in `src/day01/`, following all rules in sections 4 to 6;
- create the data they need with `instructor/generate_data.py` and document it in `docs/datasets.md`;
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

Create 5 assignments for the final examination. Each has a student part in `assignments/assignment_NN/` (task description, data, AI usage log template) and an instructor part in `instructor/assignments/assignment_NN/` (example solution as a Jupytext percent-format `.py` file, question bank, defect answer key, grading notes). Follow the examination rules in `docs/course_spec.md` (rubric, planted defects, question types).

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
- Structure the task as numbered parts. In the grading notes, list which parts must be present for a submission to count as complete. A missing or incomplete notebook means failing the course. Errors in an otherwise complete notebook do not: the student fixes them (see `docs/course_spec.md`).
- Generate plausible synthetic data (see section 6) with `instructor/generate_data.py`, including planted defects and their answer key.
- Write a **question bank** of about 10 questions per assignment with expected answers, covering the four question types of Part 3 (change the code, change the strategy, possible errors, use of AI), tied to that assignment's data and solution.
- The student part is published only at the exam date (I decide when; until then `make student_repo` leaves `assignments/` out). Solution, question bank and answer key never leave `instructor/`.
- There are 5 students and 5 assignments: each student gets a different assignment, so no per-student variants are needed. If I tell you there are more students than assignments, add seeded variants of the data.
- Each assignment must be solvable in about 2 hours as a take-home task, including the use and documentation of AI. Do not make it more extensive than that.

Update `docs/development_plan.md`. Wait for approval.

### Phase 7 – Practice exercises

Create additional practice material for students who want more training. It is optional and ungraded. Together it must keep a beginner busy for about **2 hours**.

**Step 1: plan, no notebooks yet.** Propose 4 to 6 practice notebooks. For each give the title, the blocks it practises, the number of exercises, the difficulty (easy, medium, hard) and an estimated time per exercise and per notebook for a beginner. The total must be 120 to 150 minutes, so that students can choose. Wait for my approval of the plan.

**Step 2: create the notebooks** as `src/practice/Practice_NN_<topic>.py`, built to `notebooks/practice/`, following all rules in sections 4 to 6 (hands-on rules, hidden solutions, tiered hints, no dummy results). In addition:

- New problems, not copies of the hands-on exercises: the same concepts in new biological contexts. Use the course datasets in `data/`. New small datasets are created only through `instructor/generate_data.py` and documented in `docs/datasets.md`.
- Cover all blocks, with the most weight on what the examination needs: pandas, cleaning, summaries, visualisation, basic statistics and interpretation.
- Include integrated mini-analyses that combine several blocks (load, clean, summarise, plot, interpret).
- Include "find the error" exercises with code that looks like typical AI output but contains a realistic mistake, and "AI critique" exercises (an AI-generated analysis that is scientifically questionable: what is wrong?).
- Every exercise states its estimated time and how students can check their own result (expected shape, value range, plausibility). Solutions are collapsed and explained.
- The AI usage log is optional here.

Run the self-review checklist (section 7) and `make check`. Update `docs/development_plan.md`. Wait for approval.

### Phase 8 – Dataset documentation

Check that `docs/datasets.md` is complete and correct: every file in `data/` (including the practice data), its columns, meaning, units, generation method and biological rationale. Check that the student-facing `data/README.md` is consistent with it and reveals neither planted defects nor the biological structure that exercises ask students to discover. Exam datasets and the defect answer keys are documented in `instructor/`. Update `docs/development_plan.md`. Wait for approval.

### Phase 9 – Table of contents

Create `src/Table_of_Contents.py`, built to `notebooks/Table_of_Contents.ipynb`: a navigation notebook that links to all notebooks. Markdown only.

- A short welcome, and a note that students work in their own copy in `my_work/dayNN/` (see `README_SETUP.md`) and use the links only for reading and navigation.
- A link to `00_setup_test.ipynb`.
- One section per day. For each block, links to the lecture and the hands-on notebook, a one-sentence description, the learning objective and the time, taken from `docs/syllabus.md`.
- A section for the practice notebooks, with the estimated time of each.
- Only relative links (for example `day01/Lecture_01.ipynb`), and no link to anything outside the public folders.
- Check that the links open the notebooks in JupyterLab, and tell me how they behave in VS Code so that I can verify it. `make check` verifies that every link target exists and that every notebook in `notebooks/` is listed exactly once.

Update `docs/development_plan.md`, run `make student_repo` and `make student_check`, and report. Wait for approval.

### Phase 10 – Instructor guides (private, final phase)

Guides for me only. They live in `docs/instructor_guides/` and are never part of the student repository. Write them in English.

For each of the 10 blocks create `Block_NN_guide.md` containing:

- **Lecture timeline:** a minute-by-minute plan for the 90 minutes, which core sections to present, which cells to run live, and where to stop and check understanding.
- **If I run late:** what can be skipped (optional content first, then the least important core parts) and what must never be skipped.
- **Key explanations:** the clearest wording or analogy for the hardest concepts.
- **Likely student questions** with short answers, and common misunderstandings.
- **AI corner:** prompts to try live, what to expect, and what to do if the tool is down or answers differently (the fallback in the notebook).
- **Hands-on session:** timing, which exercises to do together, where students typically get stuck and what to say, common errors and how to spot them quickly while walking around, and which stretch exercises suit fast students.
- **Preparation checklist:** data present, environment test, kernel, anything to open beforehand.

Also create `Course_overview_guide.md`: the plan for the week, the dependencies between blocks, and the places where the schedule is most at risk.

Update `docs/development_plan.md`. Wait for approval. This is the final phase.

## 4. Technical rules: building notebooks

- The `.py` files in `src/` are the only source. Never edit `.ipynb` files directly. The only hand-made notebook is `notebooks/00_setup_test.ipynb`: do not modify or rebuild it, and `make clean` must not delete it. Whenever a `.py` file changes, rebuild its `.ipynb` (`make notebooks`).
- Jupytext percent format: markdown cells are `# %% [markdown]`, code cells are `# %%`. Keep the cell order. All notebooks use the same jupytext header and the same kernelspec (`python3`, display name "Python 3 (ipykernel)"), so they work with whatever virtual environment the student selects.
- Lecture `.ipynb` files are built **with executed outputs** (students use them as a reference). Hands-on `.ipynb` files are built **with all outputs cleared**.
- Notebooks must run top to bottom in a fresh kernel in under 60 seconds.
- Do not use `try/except` and do not suppress exceptions to make checks pass. Fix the code instead.
- **Error-handling teaching cells** are the second exception: Block 04 shows `try`/`except` and `raise` (reading level in the AI corner, writing level in an optional section). Such cells are allowed only where the syllabus lists this topic, are tagged `error-handling`, and must not hide a failure of the notebook itself. Never use a bare `except:` or `except: pass`, except in a cell that shows it on purpose as a bad AI example (also tagged `error-handling`, and the following cell must demonstrate what it hides).
- **IPython-only syntax** (`?print`, `%` magics, `!` shell commands) is used only where the syllabus lists it (Block 01 shows `?print`). It is not valid Python, so in the `.py` source it must be stored in the form Jupytext uses (commented), and the syntax check, ruff and the build must still pass. Verify the round trip `.py` to `.ipynb`; if it does not work, tell me instead of working around it.
- **Intentional errors** (traceback demonstrations, typical mistakes) are the only exception: such a cell is tagged `raises-exception`, is announced by a markdown cell ("the next cell fails on purpose"), and is placed at the end of its section. `make check` must verify that exactly these cells raise an error, and that every tagged cell really does.
- Notebooks may never overwrite files in `data/raw/`. Anything a notebook writes goes to `outputs/` or, where the exercise says so, `data/processed/`.

## 5. What `make check` must do

`scripts/check_course.py` and the Makefile implement the following, and `make check` fails if any of them fails:

1. Python syntax check of every `.py` in `src/`, `scripts/` and `instructor/`.
2. `make lint` (ruff) passes.
3. Every `.py` converts to `.ipynb` and executes top to bottom without errors (apart from the tagged cells above). `notebooks/00_setup_test.ipynb` executes without errors too.
4. Execute each notebook twice and compare the cell outputs (apart from timings). Results must be identical, which proves fixed seeds.
5. Hash `data/raw/` before and after execution. It must be unchanged.
6. All files that a notebook reads exist under `data/`. No absolute paths, no URLs.
7. Every package imported by a notebook is declared in `pyproject.toml` (map import names to distribution names, for example `Bio` to `biopython` and `sklearn` to `scikit-learn`).
8. Every notebook has the required sections (section 6), every exercise has a solution cell, and solution cells carry the `solution` tag.
9. No `try:` in notebook sources, except in cells tagged `error-handling` (only in Block 04 and only if the syllabus lists it). No `input()`, no network access.
10. `notebooks/*.ipynb` (except the setup test) match what is built from the current `src/*.py`.
11. No notebook, doc or README in the public folders references a private path (`src/`, `scripts/`, `instructor/`, `docs/`).
12. Once it exists: every link in `notebooks/Table_of_Contents.ipynb` points to an existing file, and every notebook in `notebooks/` is listed exactly once.
13. Every notebook that reads from `data/` or `assets/` sits exactly two levels below the repository root and uses relative paths only (`../../data/...`).
14. Remove all cells tagged `optional` from a copy of each notebook and execute it again. It must still run, which proves that no core content depends on optional content.

**Ruff:** `pyproject.toml` selects all rules and relaxes the ones that conflict with teaching code through per-file ignores (`src/**`; `notebooks/**` and `my_work/**` are excluded completely, because the students' editors read this configuration too). Fix every other finding in the code, for example by using `np.random.default_rng` instead of the legacy `np.random` functions (`NPY002`). Deliberate mistakes that a notebook shows as "typical AI errors" get a `# noqa: <rule>` comment on that line. Do not edit the ruff configuration yourself. If a finding would make the code less readable for beginners, collect these cases and ask me which rules to ignore.

## 6. Technical rules: content

**Both notebook types**

- Follow the structures in `docs/course_spec.md` (lecture: goals, introduction, concepts with commented code examples, biological examples, typical mistakes, AI corner, summary; hands-on: goals, recap, exercises, AI challenges, reflection questions, knowledge section).
- Every cell must have a didactic purpose.
- **Core and optional content:** follow the flags in the approved syllabus. In lecture notebooks, every optional section starts with a markdown cell titled "Optional: <topic>" with a one-line note that it is for self-study, and all its cells carry the cell tag `optional`. Optional sections add no more than about 20% to a notebook. They must run without errors like all other cells. Core exercises in hands-on notebooks use core content only; the optional stretch exercises may use optional content.
- Code must be readable for beginners: explicit, simple, no clever one-liners. Only use Python concepts introduced in the current or an earlier block (see syllabus concept index).
- Random numbers: always use a seeded generator (`rng = np.random.default_rng(seed)`). Do not use the legacy `np.random.seed()` / `np.random.rand()` interface or the `random` module, except where a notebook shows them on purpose as legacy code.
- Show no dummy results. All numbers, tables and figures are computed by the code when the notebook runs.
- Do not rely on variables defined in other notebooks.
- Target the library versions installed through `pyproject.toml` (for example pandas 3.x). Avoid outdated idioms such as `inplace=True` and chained assignment, unless a cell shows them on purpose as a typical AI mistake.
- Calibrate the length from the time budget: as a starting point, 4 to 6 core concepts and about 25 code cells for a lecture, and 8 to 10 exercises for a hands-on session. We will adjust these numbers after the pilot.

**AI corner and AI challenges**

- Notebooks cannot call AI tools (no internet). A prompt is shown as markdown. An AI answer shown in a notebook is **written by you as an illustrative example**, labelled "Example of a typical AI answer; real answers differ", and its code is executed like any other code.
- When the point is that AI makes a mistake, the mistake must be realistic and subtle. Show that it is wrong with a computed check (for example, an `assert` or a comparison against a known value), not just by claiming it.
- AI challenges give students a prompt template, a place to paste the AI's code (commented out so the notebook still runs), a **fallback** (a saved example answer, labelled as such) for when their tool is unavailable, and the AI usage log (below).
- A student's AI answer will not look like the example. Every AI exercise must be solvable by checking whatever answer comes back (against known values or small test cases) and must say how to check it.

**Hands-on notebooks**

- Hands-on notebooks must be executable as delivered. Incomplete code is valid Python and commented out, so that it raises no exception.
- Increasing difficulty ladder; mark the difficulty of each exercise. Include small problems that need independent thinking, not only recapitulation.
- Exercises must not depend on previous unfinished exercises.
- Every hands-on notebook contains at least 4 optional stretch exercises (marked as optional) and collapsed tiered hints (hint 1: the concept, hint 2: the approach).
- Every hands-on notebook contains an **AI usage log** (markdown table) before the knowledge section, with the columns for that block as defined in `docs/course_spec.md` (section "AI usage documentation"), and tells students to mark AI code with `# AI-generated` or `# AI-modified: <why>`. Show a filled example row.
- Solutions are placed only in the final section. Each solution cell is tagged `solution` and collapsed (`jupyter: {source_hidden: true, outputs_hidden: true}`), so that neither code nor output is visible until expanded. Each solution is self-contained and uses its own variable names (for example with the suffix `_solution`), so it does not collide with the students' variables.

**Example data**

- All data is created by `instructor/generate_data.py` (fixed seeds, deterministic, no manually entered data) and lives under `data/`. Formats: `.tsv`, `.csv`, Excel, `.fasta`.
- Data is synthetic but biologically and scientifically plausible:
  - tumour samples have cancer-related genes with higher or lower expression than normal samples;
  - a mutation can be associated with an expression pattern;
  - technical replicates are similar, unless flawed measurements are the point;
  - biological replicates show realistic variation;
  - missing values and outliers are added deliberately for didactic purposes.
- Use real gene symbols with known cancer roles and the correct direction of change. Record the rationale in `docs/datasets.md`. If you are unsure about a biological claim, mark it for my review instead of asserting it.
- State in every data README and in the notebooks that the data is simulated and not real patient data.
- One consistent theme throughout the course, as defined in the syllabus.
- Students use Windows, macOS and Linux. Data files and notebooks must work on all of them: UTF-8 encoding (pass `encoding="utf-8"` whenever a text file is opened), forward-slash relative paths, and no special characters (µ, ä, spaces) in file names or column names.
- **Planted defects:** insert documented data-quality problems as described in `docs/course_spec.md`. `instructor/generate_data.py` first creates the clean ground-truth dataset, then the defective copy that students get, and writes an answer key (file, rows/columns, defect type, expected handling) to `instructor/answer_keys/`. Only plant defects that students can find and fix with concepts taught by that block.

## 7. Self-review checklist (run before presenting any notebook)

- Does it follow the structure in the course spec, and does every cell have a purpose?
- Is every concept either introduced here or listed as introduced earlier in the syllabus? Is every function, method, operator and keyword used in core code listed in the concept index (and nothing from a later block)?
- Does the core content fit into 90 minutes, and are all optional sections flagged and tagged `optional`?
- Could a student with no programming experience follow each code cell?
- Are all results computed, and do solutions run?
- Is every AI example labelled and checked?
- Is the biology correct and plausible?
- Does `make check` pass without any suppressed errors?
