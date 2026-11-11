# Development plan

## Current status

**Phase 1 (Syllabus): approved** (revision 6). Next: Phase 2 (project setup). Do not start Phase 2
until the instructor gives the go-ahead in a new instruction.

## Phase 1 – done (approved)

- `docs/syllabus.md` (revision 6): per-block concepts (core/optional), assumed concepts, learning
  objectives, datasets, exercise ideas, AI corner and AI challenge, AI log columns, core time
  budgets; data concept (fictional CRC-P53 study); cross-cutting topics; complete concept index
  (every function, method, attribute, operator, keyword, magic command and library in core code,
  per block); learning-goal coverage. This is the detailed instructor version.
- `docs/defect_plan.md`: planted defects per dataset and block (revision 3: the mislabelled
  organoid is now detectable via Nutlin-3a and oxaliplatin).
- `docs/datasets.md`: planning draft of the gene panel, simulated effects, cell-line data and
  organoid screen; all biological claims reviewed and accepted (revision 3: oxaliplatin depends on
  wild-type p53, 5-FU has no TP53 association).
- Removed the old draft `notebooks/01_python_jupyter_first_steps.ipynb` (instructor's decision).

### Core time budgets (minutes, after revision 6)

| Block | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| Lecture | 86 | 83 | 88 | 85 | 87 | 89 | 80 | 76 | 88 | 86 |
| Hands-on | 90 | 89 | 90 | 90 | 90 | 90 | 90 | 90 | 90 | 90 |

## Decisions taken (instructor)

- Theme: TP53-centred CRC cohort + HCT116 TP53 wt/ko with Nutlin-3a; real cell-line and compound
  names allowed, data labelled as simulated.
- AI is shown only briefly in lectures (e.g. prompts for tracebacks, explaining/generating code);
  students choose free ChatGPT or Claude.
- Daily order: Lecture A, Hands-on A, Lecture B, Hands-on B.
- Core datasets are single tables; `merge`/`melt` stay optional, but example data for them is
  generated. The exam cannot require `merge`/`melt`.
- Lecture notebooks are built with executed outputs, hands-on notebooks with cleared outputs.
- P1: variables, assignment, naming rules, literals vs. variables and arithmetic with variables are
  formal core content in Block 01; `None` stays in Block 04; built-in-names trap in Block 03.
- P2: indexing and slicing (lists, tuples, strings) in Block 03.
- P3: list comprehensions strictly optional (reading level, Block 03).
- P4: `import` first contact in Block 02 (`math`), formal in Block 05.
- P5: `.iloc` optional; `pd.to_numeric` in Block 09.
- P6: Cohen's d optional; normality assumption conceptual only.
- O1: "interpreters and scripts" is a short mention in Block 01.
- O2: error categories inside the traceback section; `import math` inside the biological
  calculations (Block 02).
- O4: `split()`/`join()` inside the FASTA section; shorter `help()` section (Block 04).
- O5: `np.zeros()`/`np.ones()` as a short mention. `np.argsort()` is **core** in Block 05, as in
  the spec (revision 6; hands-on exercise 8 uses it; sorting section 5 min, lecture 87 min).
- Block 01 hands-on has 8 core exercises (revision 6): all seven pool ideas are used (five as
  exercises, two as the AI challenge), plus shortcut drill, valid names and a `?print` exercise.
- Every hands-on notebook has 4 optional stretch exercises, used depending on the time available
  (spec and AGENTS.md updated by the instructor).
- C1–C3: `assert` in Block 04; exception types in Blocks 03–06; library versions in Blocks 05–06.
- [V]: vocabulary additions accepted (`abs()`, `.lower()`, `in`/`not in`, `+=`,
  `sum()`/`min()`/`max()`, `&`/`|` for masks, `pd.DataFrame({...})`, `.isin()`,
  `fig.tight_layout()`, `.T`, `.quantile()` with the 1.5 × IQR rule).
- Q1: Block 01 covers keywords and "don't reuse `print`"; the `list`/`sum`/`max` trap is in Block 03.
- Q2: the restart demo and keyword misuse show errors as a preview; tracebacks are taught in Block 02.
- Q3: Block 01 Markdown core = a heading plus text.
- AI usage log: the "Tool" column is used from Block 01 on. Blocks 01–02: `#`, Task, Tool, Prompt,
  Result; Blocks 03–06: + How I checked it; Block 07 on and the exam: + What I changed and why.
- Nutlin-3a molar mass 581.5 g/mol (C30H30Cl2N4O4); bench calculator with a 10 mM stock and 10, 5,
  1 µM working solutions.
- Biology reviews in `docs/datasets.md` accepted; oxaliplatin is TP53-dependent, 5-FU is not.
- Block 05: "array with a single number" is core element-wise calculation; broadcasting optional.
- P7: Block 07 gets a core section on the Figure and Axes objects (anatomy of a figure; `ax.` vs.
  `plt.` interface, the latter at reading level). Block 08 gets `sns.relplot()` and `sns.displot()`
  as core (figure-level vs. axes-level functions, panels with `col=`/`row=`, `height`/`aspect`,
  `g.set_axis_labels()`, `g.savefig()`). Both lectures keep at least a 10-minute buffer (80 and 76 min).
- P8: Block 10 no longer teaches step-by-step code generation in the lecture. The AI corner is one
  section (15 min) on developing and critiquing an analysis plan with AI, followed by a recap of
  the AI lessons of Blocks 01–09 (7 min). Lecture: 86 min.

- P9 (decided): Block 07 shows colours/markers/line styles inside the line and scatter sections
  and mentions `Series.plot()` briefly; Block 08 teaches "comparing categories and groups" inside
  the boxplot and panel sections.
- Q4 (decided): the spec now describes Block 10 as "Executing an analysis step by step; recap of
  earlier AI corners; practice in the hands-on".

## Pending (decided later)

- **O3 (Block 03), after the pilot:** if the lecture runs late, `del` and `.pop()` become a mention
  (optional section); `.append()`, item assignment and `.update()` stay core.
- **Block 06 fallback, after the pilot:** if the lecture runs late, duplicates move to Block 09.
## Consistency check (revision 6)

Earlier fixes (revision 5) remain in place: Block 01 AI challenge independent of the exercises;
data table corrected; `df.columns[a:b]` in the concept index; all defects before Block 10 disclosed
with a hint; growth curves measured as confluence (%).

Resolved since revision 5: `np.argsort()` core again; "Tool" column from Block 01 (spec updated);
Block 10 wording (spec updated); stretch exercises now 4 per block (spec and AGENTS.md updated);
Block 01 has 8 core exercises.

Remaining points:

1. **Block 01 hands-on is tight.** To fit two more exercises into 90 minutes, the exercise slots
   were shortened by 1–2 minutes each and the AI challenge from 20 to 18 minutes; reflection and
   AI log have 8 minutes. If the pilot shows it does not fit, exercise 8 (Notebook detective)
   could become a stretch exercise again.
2. **Spec vs. AGENTS.md wording on stretch exercises:** the spec says "4 optional stretch
   exercises", AGENTS.md says "at least 4". The syllabus uses exactly 4, which satisfies both.
3. **Block 07 (minor):** the spec says "Figures, axes and subplots"; the syllabus has a dedicated
   section on the Figure and Axes objects (P7). Optionally make this explicit in the spec.
4. **Exercise dependencies (Phases 3–4):** some exercises build on each other by nature (Block 05
   ex. 5→6, Block 09 ex. 2→3, the Block 10 mini-project). Each such exercise will start from a
   provided cell that creates the state it needs (AGENTS.md §6).
5. **Optional share ≤ ~20% (Phases 3–4):** Blocks 06 (six optional topics) and 09 (eight) are at
   risk; their optional sections will be kept very short.

## Notes and to-dos

- **Student-facing syllabus:** `docs/syllabus.md` stays the detailed instructor version. A brief
  student-facing version (only the topics covered in lectures and exercises) for ILIAS may be
  derived from it later.
- **Before the course:** check the Nutlin-3a molar mass against the supplier's datasheet.
- "Practised in at least two blocks" is interpreted as: the hands-on of the introducing block
  counts. SciPy and "critical interpretation" are thin (09, 10 only); mitigation via practice
  notebooks (Phase 7).

## Next phases

- Phase 2: environment, Makefile, `.gitignore`s (not started; next).
- Phases 3–10: not started.
