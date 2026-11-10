# Course Concept: Data Science with Python for Biomedical Students

I want to teach a python and data analysis course for bachelor students using a combination of jupyter notebooks that i use in a lecture to demonstrate the basic concepts followed by a hands-on session, where the people can explore this by themselves.
The course is a one week block course intended for the level of bachelor students without practical python experience. They do however have a basic knowledge of biology, medical research, genetics and DNA sequencing. Rather than teaching Python for its own sake, we teach Python as a tool for biomedical data analysis, with AI as an integral part of the entire workflow. Students need to be able to generate code (with AI assistance) and execute it, but also be able to assess, whether the analysis is scientifically sound.

We are mostly working with molecular cancer research data. 
More precisely NGS data (RNAseq, scRNAseq, mutations), Time-series, growth-curve, dose-response, qPCR data, counts data and whatever other biological data might be reasonable for showcasing certain concepts.
For the course, which is a block course in one week, the students should use some free version of either chatGPT or Claude as assistant for their tasks.
They also learn how to critically review AI-generated code and avoid blindly accepting its results.
As the goal is to teach the students the best way to utilize the AI agents and judge the quality of the produced code, they need to learn
the relevant python concepts for that. They should be able at the end to understand the python code, write it without and with AI assistance and
correct AI generated code on their own.
Each new concept is introduced, whenever possible, using biological or biomedical examples.
Tools we will use: vscode, JupyterLab, git and uv. AI assistance is not dependent on a specific tool and should only utilize free tools (e.g. chatGPT or claude free) without a subscription plan.

# Learning goals - Students should learn:

- Python from the ground up, no prior knowledge required.
- to formulate prompts and translate a scientific question into a specific data analysis task
- to work with tabular data using pandas
- to comprehend code and identify used python concepts
- to debug code, read tracebacks and exceptions, use AI for troubleshooting
- to create test cases and check the validity of the code with them
- to perform basic statistic analysis and calculations using numpy and scipy
- to create visualizations of scientific data using matplotlib and seaborn 
- to generate and modify python code with and without AI assistance
- to assess, if data analysis and calculations are valid and appropriate
- to spot erroneous AI suggestions and correct them
- to interpret and critically reflect results scientifically without trusting AI
- how to analyse and visualise data independently.
- to document the code, AI usage, analysis design transparently 
- to use AI effectively for programming, debugging and interpretation

A major AI assisted workflow for the students to grasp should be:

1. Define the problem
   
   Formulate the biological research question. Identify the data, the required analysis and the expected output.
   
   Human responsibility: Define what needs to be solved.

2. Provide context and prompt the AI
   
   Explain the biological problem, data structure, variable names, data types, constraints and desired outcome.
   
   AI skill: Context-aware prompting.

3. Generate and understand the code
   
   Ask AI to generate code in manageable steps. Request explanations of unfamiliar syntax, functions and Python concepts.
   
   AI skill: Code generation and code comprehension.

4. Execute the code
   
   Run the code in Jupyter. Inspect outputs, intermediate results and data structures.
   
   Human responsibility: Never assume generated code works correctly.

5. Debug and improve
   
   Use error messages and tracebacks to identify problems. Ask AI for explanations and possible fixes. Test the proposed changes.
   
   AI skill: Debugging and iterative problem solving.

6. Test and validate
   
   Check calculations against known examples, inspect assumptions, verify statistical methods and assess biological plausibility.
   
   Human responsibility: Establish whether the result is actually correct.

7. Interpret and document
   
   Interpret the results in the biological context. Document analytical decisions, AI assistance, code modifications and limitations.
   
   Human responsibility: Own the scientific conclusions.
   
With ten course blocks, each consisting of a 1.5-hour lecture followed by a practical exercise, we need to build a clear progression.


# Block structure and didactic rules

For each course block, I need two jupyter notebooks. The first one should be the lecture notebook. 
This is intended as a digital lecture script. 
While it should contain executable code to illustrate the concepts (I will execute the cells as I go along the lecture), it is also intended as lookup for the students containing the relevant information they need, so that they can revisit that at any time later. So for the sake of reusability, we want to explain the concepts thoroughly so that they are self-explanatory without my narrative.
The second notebook is a Hands-On notebook, where the students should test out the newly introduced concepts with given exercises.


**General structure/content of a lecture notebook**

1. goals of the lecture: What should the students know after the lecture
2. Short introduction to the topic and its relevance for data science and data analysis
3. Step by Step introduction and explanation of python concepts
4. each concept section is followed by a code example section with thorough comments
5. and biological or biomedical examples
6. typical mistakes and traps, if applicable
7. AI corner: How can AI be used to help with these topics?
8. Summary of the most important concepts.

Goal: explaining concepts, demonstrate code, show examples, explain AI possibilities, address typical mistakes and pitfalls, communicate knowledge

An example for the AI corner:

Explain how AI can help with a topic and showcase it:
1. Which benefit can AI give with this concept?
2. What is a good prompt?
3. What is a bad or incomplete prompt?
4. How can I check the AI answer?
5. Which mistakes can the AI make?

Example for Python functions:

AI Corner: Generating and understanding Python functions

Show a simple function for GC content calculation.

The prompt:
"I am analysing DNA sequences in a biomedical research context.

Write a Python function that calculates the GC content
of a DNA sequence as a percentage.

Requirements:
- The input is a DNA sequence represented as a string.
- The function should be case-insensitive.
- Ignore whitespace.
- Return the GC percentage.
- Explain each line of the code.
- Include at least three test cases.
- Explain how the function handles invalid input.
"


**General structure/content of the Hands-on Notebook**

1. Goals of the Exercise
2. Short recap of the most relevant concepts
3. exercises with biological or biomedical context
4. code cells with partial code to be completed (insert as 'commented out' code, so that it does not raise exceptions during testing).
5. exercises where the students need to write their own code
6. AI challenges: exercises where the students should use AI explicitly
7. Questions for reflection: What does the code? Why does it work?
8. AI usage log: the students document their AI use (see 'AI usage documentation' below)
9. Knowledge section at the very end: Summary and explanation of the most important concepts and example solutions to the exercises.

Beginners work at very different speeds. Therefore every hands-on notebook also contains:

- **2 optional stretch exercises** (clearly marked as optional and harder) for fast students.
- **Tiered hints** for the exercises, collapsed by default: hint 1 points to the relevant concept, hint 2 shows the approach. The full solution stays in the knowledge section.
- **A fallback for every AI challenge**: a saved example answer of an AI tool (clearly labelled as an example), so that students can continue if their free tool is unavailable, rate-limited or not working.

Goal: apply concepts, write code, solve problems, use AI deliberately, identify and solve errors independently, solidify the knowledge

# Major didactic rules

- make the lectures not too long. They need to contain the relevant concepts in an understandable way and be usable as a reference later, but they should not be overloaded.
- Several blocks below list more topics than fit into 1.5 hours for complete beginners. The agent must NOT silently drop or silently squeeze topics. In the syllabus it flags overloaded blocks and proposes what to move (to another block, to an optional 'further reading' section, or to a mention only), and I decide.
- Only use Python concepts that were introduced in the current or an earlier block. If a library function requires a concept that has not been introduced yet, either avoid it or explain it briefly where it is first needed.
- Free AI tools change, hit rate limits and answer differently every time. Students will therefore NOT get the same answers as shown in the notebooks. The notebooks teach the process of checking an answer (against known values, small test cases, the documentation), not specific AI outputs. Every AI exercise must be solvable by checking whatever answer the tool returns, and must say how to check it.
- the lecture should communicate the concepts. The exercises forces the students to apply the concepts.
- hands-on exercises should not be just a recapitulation, but also contain small problems that demands independent and problem-solving thinking.
- construct the exercises with an increasing difficulty ladder, starting with simple exercises and becoming more demanding.
- example data used throughout the course should follow a consistent theme and build upon each lesson. It should represent typical cancer research data and contain:
  -- Patient and sample information
  -- Tumor- and control samples
  -- gene expression data
  -- mutation status of selected genes
  -- experimental measurements
  -- Time-series data 
  -- growth-curves 
  -- dose-response 
  -- qPCR data


# Example data: deliberately planted data-quality problems

Real data is messy, and recognising problems is a learning goal. The synthetic datasets therefore contain **deliberately planted defects** that students have to find, document and handle. "Planted" means: the data generator inserts the defects on purpose (with a fixed seed) and records exactly what it inserted, so that cleaning exercises and the final examination can be checked objectively.

How it works:

- The generator creates a **clean ground-truth version** of each dataset first, then inserts defects into a copy. That copy is the dataset students receive.
- It writes an **answer key** (machine-readable): file, affected rows/columns, type of defect, and how it should be handled. With the clean version, the answer key lets us verify automatically that a cleaning step recovers the truth.
- The answer key and the clean version are instructor-only and never part of the student repository.

Examples of defects (to be matched to what the students have learned in the respective block):

- duplicated rows or duplicated sample IDs;
- missing values: random, and systematic (for example all missing in one batch);
- impossible values: negative age, negative counts, percentages above 100;
- inconsistent categories and IDs: "Tumor", "tumor", "TUMOUR", trailing whitespace, mixed case in sample IDs;
- numbers stored as text, decimal commas;
- unit mismatches: part of a concentration column in nM, the rest in µM;
- technical outliers, such as a failed qPCR well, as opposed to biological outliers;
- a mislabelled sample: labelled "normal", but known marker genes and mutation status say "tumour";
- a batch effect: samples from one batch or date are shifted, visible in a boxplot by batch.

Rules:

- Only plant defects that students can detect and fix with the concepts taught up to that block.
- Difficulty increases over the course: obvious defects with a hint in early blocks (duplicates, missing values, inconsistent categories), visible-in-a-plot defects in Block 07 and 08 (outliers, unit mismatch), subtle defects in Block 09 (batch effect, mislabelled sample), and several **undisclosed** defects of different kinds in Block 10 and in the examination datasets.
- Students must document what they found and how they handled it. Silently deleting rows is not a solution.
- Each exam assignment has its own list of planted defects, which is used in grading (found? handled sensibly? documented? effect on the result discussed?).

# AI usage documentation (from day 1)

The examination requires students to document how they used AI. They must practise this from Block 01 on, in every hands-on session, so that it is a habit by the time of the exam.

**1. Mark AI code in the notebook.** The first line of every code cell that contains AI-generated code is a comment:

- `# AI-generated` for code used as it came, or
- `# AI-modified: <what I changed and why>` for code the student changed.

Code the students wrote themselves needs no mark.

**2. AI usage log.** A markdown table at the end of each hands-on notebook (before the knowledge section), filled in by the student. One row per AI interaction (one problem, even if it took several messages).

- **Students log their prompts** (copy and paste, verbatim). Prompt quality is a learning goal, and the examiner must be able to see what was asked. Full AI answers do not have to be logged, only what was taken from them.
- Never paste real patient data or confidential research data into the prompt or the log (see data privacy, Block 01).
- The log is built up gradually so it does not become a burden:
  - Blocks 01–02: Task, Prompt, Result (accepted / modified / rejected).
  - Blocks 03–06: additionally "How I checked it".
  - from Block 07 on and in the examination: the full table, including "What I changed and why".

Full table, with an example row:

| # | Task | Tool | Prompt (verbatim) | Result | How I checked it | What I changed and why |
|---|------|------|-------------------|--------|------------------|------------------------|
| 1 | GC content of a DNA string | ChatGPT (free) | "Write a Python function that calculates the GC content of a DNA sequence as a percentage. ..." | modified | ran 3 test cases; a lowercase sequence returned 0 % | added `.upper()` before counting, because the function was case-sensitive |

# Core and optional content

Every topic in the block descriptions below is flagged **[core]** or **[optional]**.

- **Core** content is presented in the live lecture, practised in the hands-on exercises, and available as a basis for later blocks and for the examination. The core content of a block, including the AI component or AI task, must fit into 1.5 hours of lecture and 1.5 hours of hands-on session.
- **Optional** content is for self-study at home. It is included in the lecture notebook in clearly marked "Optional" sections, but it is not presented in the lecture and not needed for the core exercises. Optional topics may appear in the optional stretch exercises and in the practice notebooks. Examination questions draw only on core content.
- No core content may depend on optional content. A student who skips every optional section must still be able to follow all later blocks.
- The optional topics also include additional context that helps understanding but cannot be addressed during the course.
- The AI component and the AI task of a block are always core.
- Optional sections stay short. They should add no more than about 20% to the length of a lecture notebook.
- If, when planning a block, the agent finds that the core content does not fit into the time, it proposes in the syllabus which core topics should become optional. I decide. The agent never moves topics silently and never promotes optional content to core.

# Course Structure: Data Science with Python for Biomedical Students

**5 days · 10 blocks**

**10** – Course blocks. Each block = one 1.5-hour lecture followed by one 1.5-hour hands-on session (2 notebooks per block, 20 notebooks in total)

**15 hours** – Total lecture time (10 × 1.5 h)

**15 hours** – Total hands-on time (10 × 1.5 h)

**30 hours** – Total contact time

**How to read the block descriptions below**

- Every block below has BOTH a lecture notebook (`Lecture_NN`) and a hands-on notebook (`Hands_on_NN`). The topic list of a block applies to the whole block: the lecture teaches the concepts, the hands-on session practises them.
- **AI component** = content for the "AI corner" of the lecture notebook. **AI task** = content for the "AI challenge" in the hands-on notebook. Where a block names only one of the two, the other one is derived from it by the agent and proposed in the syllabus for my approval.

## Cross-cutting topics the syllabus must cover

The block lists above do not mention the following topics, but later blocks and the learning goals depend on them. All of them are **core**, except git basics, which are optional. In the syllabus, the agent proposes in which block each one is introduced (and which block it takes time from), and I decide:

- `import`, modules and libraries (`import numpy as np`, installed packages versus the standard library). Needed before Block 05 at the latest, ideally earlier.
- String handling: indexing and slicing, common string methods (`upper()`, `count()`, `replace()`), f-strings. Needed for the DNA sequence functions in Block 04.
- List comprehensions (AI-generated code uses them constantly, and students must be able to read them).
- More exception types beyond the first introduction (`KeyError`, `IndexError`, and later the errors typical for arrays and DataFrames). How to read an error message is fixed for Block 02 (see there). The agent proposes where the further exception types go.
- Simple test cases with `assert` (a learning goal, but no block lists it).
- Library versions: AI answers often use outdated idioms (for example older pandas or NumPy syntax). Students should learn to check the installed versions and the documentation.
- **[optional]** Git basics (commit, history), if they are not covered completely by the setup instructions.

## Learning goals: planned coverage by block

This table shows where each learning goal is introduced, practised and assessed. It is a proposal. In the syllabus the agent checks it against the final block contents, refines it, and flags every goal that is not introduced in at least one block and practised in at least two (for example `scipy`, which currently only appears in Block 09).

| Learning goal | Introduced | Practised | Assessed in the exam |
|---|---|---|---|
| Python from the ground up | 01–04 | 05–10 | notebook |
| Formulate prompts, translate a scientific question into an analysis task | 01 | AI tasks in 02–10, central in 10 | notebook, questions |
| Work with tabular data using pandas | 06 | 07–10 | notebook |
| Comprehend code and identify the Python concepts used | 03, 04 | "what does this code do?" questions in every hands-on | questions |
| Debug code, read tracebacks, use AI for troubleshooting | 02 (reading error messages), 03 | 04, 06, 10 | questions (errors) |
| Create test cases and check code with them | 04 | 06, 09, 10 | questions |
| Basic statistics and calculations with numpy and scipy | 05 (numpy), 09 (scipy) | 09, 10 | notebook |
| Visualise scientific data with matplotlib and seaborn | 07, 08 | 09, 10 | notebook |
| Generate and modify code with and without AI | 01 | 02–10 (core exercises without AI, AI challenges with AI) | notebook, questions |
| Assess whether analyses and calculations are valid and appropriate | 06 (cleaning), 09 | 10 | notebook, presentation |
| Spot and correct erroneous AI suggestions | 01 | AI corners with realistic errors in 03–09, 10 | questions |
| Interpret and critically reflect on results without trusting AI | 08, 09 | 10 | presentation, notebook |
| Analyse and visualise data independently | 08 | 10 | notebook |
| Document code, AI usage and analysis design transparently | 01 | AI usage log in every hands-on, 10 | notebook |
| Use AI effectively for programming, debugging and interpretation | 01 | AI corners and AI tasks in every block | questions (AI) |

## Preparation before the course

Before the course starts, I meet the students and set up their computers. `README_SETUP.md` (and its German version) and `notebooks/00_setup_test.ipynb` already exist, have been tested and are maintained by me. The agent does not create or change them.

## Course material and distribution

- Per block: a lecture notebook and a hands-on notebook (`notebooks/dayNN/`).
- **Practice material:** additional, optional, ungraded practice notebooks (`notebooks/practice/`) with new exercises for all topics, enough to keep a beginner busy for about 2 hours. Students do not have to do them.
- `notebooks/Table_of_Contents.ipynb` links to all notebooks. `notebooks/00_setup_test.ipynb` checks the environment.
- `assets/` contains example figures and images that I provide as illustrations for the notebooks.
- Students work in their own copy of a day's folder in `my_work/dayNN/`, not in the `notebooks` folder itself, so that updates of the material never collide with their work.
- **Two repositories:** a private one for me (all work in progress, including sources, private documents and exam material) and a student repository that contains only `assets`, `notebooks`, `outputs`, `data` and `assignments` plus the files needed for the setup (`README.md`, `README_SETUP*`, `pyproject.toml`, `uv.lock`). The exam assignments are added to the student repository only at the exam date.
- The material is also provided through the online platform ILIAS (for example HTML versions of the lecture notebooks and the syllabus). The syllabus and the detailed dataset description are not part of the student repository.
- **Language:** all course material is in English. (`README_SETUP_german.md` is a translation of the setup instructions for convenience.)
- The hands-on sessions are done together with me, so the example solutions can stay in the hands-on notebooks (collapsed). Students can look them up later.

## Day 1 – Introduction to Python and Programming

**Objective:** Students understand the working environment and can write and follow simple Python instructions.

### Block 01 – Python, Jupyter and AI

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** What is Python? What is a programming language?
- **[core]** Interpreters and scripts
- **[core]** Jupyter Notebooks: kernels, cells, Markdown and code
- **[core]** VS Code: interface, Python environment, Jupyter integration and file management
- **[core]** Getting started: `print()`, comments and simple calculations
- **[core]** reproducibility: what does it mean? why do analysis have to be repeatable at any time?
- **[core]** jupyter notebooks, order of execution, why should we restart the kernel and rerun from time to time
- **[core]** importance of documentation
- **[optional]** Jupyter shortcuts and useful features (beyond running, adding and deleting cells, which are core)
- **[core]** Introduction to AI-assisted programming: What can ChatGPT do, and what are its limitations?
- **[optional]** Markdown cheat sheet: headings, lists, emphasis, formulas
- **[optional]** The Python ecosystem for biomedical data analysis (overview of libraries such as Biopython and scanpy)

**AI component:** 

- How do I formulate a good prompt? How can I ask AI to explain Python code? How can I generate code without blindly accepting it?
- Data privacy: Why patient data and confidential research data should not be entered carelessly into public AI systems.

### Block 02 – Variables, Data Types and Operators

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** Writing first Python instructions
- **[core]** Defining variables and assigning values
- **[core]** Integers, floats, strings and Booleans
- **[core]** Exploring data types with `type()`
- **[core]** Type conversion with `int()`, `float()` and `str()`
- **[core]** Arithmetic and logical operators
- **[core]** Comparison operators and Boolean expressions
- **[core]** Simple biological calculations (e.g. dilutions, concentrations and age calculations)
- **[core]** Reading an error message: what a traceback shows (error type, message, line number), the typical beginner errors (`SyntaxError`, `NameError`, `TypeError`, `ValueError`) and how to fix them. Errors are normal and part of programming. This is a dedicated short section of the lecture and has its own hands-on exercise.
- **[optional]** Floating-point precision: why `0.1 + 0.2` is not exactly `0.3`, and `round()`
- **[optional]** Naming conventions for variables (PEP 8)
- **[optional]** Integer division and remainder (`//`, `%`)

**AI task:** Students use AI to generate a small calculator for a biological problem, review the code and test it with their own values.

## Day 2 – Programming with Python and Problem Solving

**Objective:** Students understand basic programming logic and can independently solve simple analytical tasks.

### Block 03 – Control Flow and Data Structures

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** Why do we need control structures?
- **[core]** `if`, `elif`, `else`
- **[core]** `for` loops
- **[optional]** `while` loops
- **[core]** `range()`
- **[optional]** `enumerate()`, `break` and `continue`
- **[core]** Lists and tuples
- **[core]** Dictionaries
- **[optional]** Sets
- **[core]** Iterables and iteration
- **[optional]** Nested data structures
- **[optional]** Mutable and immutable objects: why `b = a` does not copy a list
- **[optional]** Sorting with `sorted()` and `.sort()`

**AI component:** Asking AI to explain code, generate loops and identify errors in existing code.

### Block 04 – Functions and Biological Programming Tasks

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** Creating custom functions with `def`
- **[core]** Parameters, arguments and return values
- **[core]** Default parameters and keyword arguments
- **[core]** Local variables
- **[core]** `help()` and docstrings
- **[core]** touch upon object-orientation: what is an object, what is a class? what are attributes and methods? difference between class and instance. Students need to know that this exists and later use class methods and attributes with pandas and seaborn. but they do not need to implement themselves.
- **[core]** Writing small functions for sequence analysis:
  - **[core]** Determining the length of a DNA sequence
  - **[core]** Calculating GC content
  - **[core]** Counting specific nucleotides
  - **[optional]** Generating the reverse complement of a DNA sequence
  - **[core]** Reading .fasta
- **[optional]** Lambda functions (you will meet them in AI-generated pandas code)
- **[optional]** Type hints in function definitions (you will see them in AI-generated code)

**AI task:** Develop a function to calculate GC content with the help of AI, test it and then extend it in a targeted way. Students should be able to explain what each line of code does.

## Day 3 – Scientific Data Analysis with NumPy and Pandas

**Objective:** Students can load, manipulate and analyse numerical data and tabular datasets.

### Block 05 – NumPy: Numerical Data Analysis

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** Why NumPy? Differences between NumPy arrays and Python lists
- **[core]** Arrays, vectors and matrices
- **[core]** Dimensions, shape and data types
- **[core]** Creating arrays: `np.array()`, `np.zeros()`, `np.ones()`, `np.arange()`
- **[core]** Indexing and slicing
- **[core]** Boolean masking
- **[core]** Element-wise calculations
- **[core]** Raw counts vs. normalised/log-transformed expression 
- **[optional]** Mention `np.linspace()` and broadcasting
- **[core]** Statistical functions: mean, median and standard deviation
- **[core]** Random numbers with a seeded generator (`rng = np.random.default_rng(42)`, then `rng.normal()`, `rng.integers()`, `rng.choice()`) and why a fixed seed makes results reproducible
- **[optional]** The legacy interface `np.random.seed()` and the `random` module: you will meet them in older tutorials and in AI-generated code
- **[optional]** Row-wise and column-wise statistics with the `axis` argument
- **[optional]** Missing values in NumPy (`np.nan`, `np.nanmean`)

**Biological context:** Gene expression data, experimental measurements and concentration series.

**AI component:** Generate NumPy code with AI and use small examples to understand what arrays and broadcasting actually do.

### Block 06 – Pandas: Working with Tables

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** What is Pandas?
- **[core]** Series and DataFrames
- **[core]** Reading CSV and TSV files (`read_csv`)
- **[core]** handling different data formats (.csv, .tsv). Focus on dataframes. (Reading .fasta is covered in Block 04.)
- **[optional]** also mention .json, .fastq, .bam and .vcf files conceptually (but we will not use them here)
- **[core]** Exploring data: `head()`, `info()`, `describe()`
- **[core]** Selecting columns and rows
- **[core]** Filtering and sorting
- **[core]** cleaning data
- **[core]** Identifying and handling missing values
- **[core]** Calculating new columns
- **[core]** Grouping with `groupby()` and simple summaries such as `mean()` and `count()`
- **[optional]** Summarising data with `agg()` (several statistics at once)
- **[core]** Saving a table with `to_csv`
- **[optional]** Reading Excel files (`read_excel`)
- **[optional]** Merging tables with `merge()` (for example sample information and expression values)
- **[optional]** Wide versus long table format (`melt`, `pivot`)

**Biological context:** Analysing a table containing gene expression values, sample information or qPCR measurements.

**AI task:** Explore an unfamiliar dataset with the help of AI. AI should suggest meaningful analyses; students then implement these suggestions and verify the results.

## Day 4 – Data Visualisation

**Objective:** Students can create meaningful visual representations of scientific data and interpret them.

### Block 07 – Matplotlib: Fundamentals of Data Visualisation

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** Why do we visualise data?
- **[core]** Fundamentals of scientific plots
- **[core]** Figures, axes and subplots
- **[core]** Line plots, scatter plots, bar plots and histograms
- **[core]** Axis labels, titles and legends
- **[core]** Colours, markers and line styles
- **[optional]** Figure size and DPI
- **[core]** Exporting and saving figures
- **[optional]** Error bars (mean ± standard deviation)
- **[optional]** Logarithmic axes (`set_yscale`) for expression and dose-response data
- **[optional]** Colour-blind-friendly palettes and misleading axes (truncated or dual axes)

**Biological context:** Time series, growth curves, gene expression data and experimental measurements.

**AI component:** Create and improve plots with AI assistance. AI should also explain which type of plot is suitable for a particular research question.

### Block 08 – Seaborn and Exploratory Data Visualisation

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** What is Seaborn, and how does it differ from Matplotlib?
- **[core]** Histograms and distributions
- **[core]** Boxplots
- **[optional]** Violin plots
- **[core]** Scatter plots
- **[optional]** Regression lines (`regplot`)
- **[core]** Heatmaps, address Raw counts vs. normalised/log-transformed expression 
- **[core]** Visualising correlations
- **[core]** Comparing categories and groups
- **[optional]** Visualising multiple variables simultaneously (for example pair plots)
- **[optional]** Clustered heatmaps with `clustermap`

**Biological context:** Comparing control and treatment groups, gene expression profiles and correlations between experimental parameters.

**AI task:** Explore a dataset and use AI to develop suitable visualisations. Afterwards, assess whether the visualisations actually address the biological research question.

## Day 5 – Scientific Analysis, Statistics and AI

**Objective:** Students can work through an integrated analysis workflow using a biological dataset and make effective use of AI throughout the process.

### Block 09 – Data Quality, Statistics and Interpretation

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** Common challenges in biomedical datasets
- **[core]** Data quality and plausibility checks
- **[core]** Missing values, outliers and duplicates
- **[core]** Descriptive statistics
- **[core]** Mean, median and standard deviation
- **[optional]** Coefficient of variation
- **[core]** Introduction to statistical tests: t-test and correlation (conceptually and practically)
- **[core]** p-values and their interpretation
- **[core]** biological versus technical replicates
- **[core]** effect sizes
- **[core]** statistical pitfalls: small sample size, multiple hypothesis testing, pseudoreplication, outliers, normal distribution assumption, correlation does not imply causation
- **[optional]** Reproducibility and documentation of analyses (covered in Blocks 01 and 10)
- **[optional]** Paired versus unpaired t-test (for example tumour and normal tissue from the same patient)
- **[optional]** Non-parametric alternative: Mann-Whitney U test
- **[optional]** Checking the normality assumption (histogram, Q-Q plot, Shapiro-Wilk test)
- **[optional]** Multiple testing correction in practice (Benjamini-Hochberg with `statsmodels`)
- **[optional]** Confidence intervals

**AI component**

- Using AI to support the selection of appropriate statistical methods
- Asking AI to help interpret results
- Critically reviewing AI-generated statistical statements

### Block 10 – AI-Assisted Biomedical Data Analysis

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- **[core]** Loading an unfamiliar biological dataset
- **[core]** Exploring its structure and data quality
- **[core]** Formulating research questions
- **[core]** Developing an analysis plan with AI
- **[core]** Generating and executing Python code step by step
- **[core]** Filtering and summarising data
- **[core]** Creating suitable visualisations
- **[core]** Interpreting results
- **[core]** Critically reviewing AI-generated results
- **[core]** Documenting the analysis in a reproducible and transparent way (clean documentation, reproducibility, separation of raw and processed data)
- **[optional]** Version control with git (commit, history, why it matters for reproducibility)
- **[optional]** Writing a short methods paragraph and figure legends for an analysis
- **[optional]** Exporting a notebook to HTML or PDF for sharing

**Final discussion:** What did AI do well? Where did it make mistakes? Which decisions did the students have to make themselves?


# Block Summaries – Purpose, Learning Priorities and Boundaries

These summaries give direction and boundaries. The topic lists in the block descriptions above remain authoritative for the content, and their core/optional flags apply. If a summary and a topic list seem to disagree, ask me.

## Block 01 – Python, Jupyter and AI

- **Purpose:** Establish the working environment and introduce Python as a practical tool for biomedical data analysis. Students should become comfortable navigating and executing notebooks, which is essential for all subsequent practical work and the notebook-based exam.
- **The one thing that must land:** A Jupyter notebook is an executable document, and the order in which cells are executed matters. Students must understand the difference between code, output and explanatory Markdown.
- **Not in scope:** Installing or configuring complex development environments, advanced Python syntax, software engineering practices or detailed AI theory.
- **Fit:** Establishes the tools and working habits needed for Block 02. Introduces AI as an assistant whose output must always be checked, not as a replacement for understanding.
- **Common traps:** Executing cells out of order, assuming displayed output reflects the current code, confusing Markdown and code cells, and copying AI-generated code without understanding what it does.

## Block 02 – Variables, Data Types and Operators

- **Purpose:** Give students the basic building blocks needed to represent and manipulate values in Python. These concepts underpin every calculation and analysis later in the course.
- **The one thing that must land:** Variables store values, and the type of a value determines which operations can be performed on it. Students should be able to follow simple calculations and recognise type-related problems.
- **Not in scope:** Advanced type systems, complex data structures, object-oriented programming or mathematical programming beyond simple biomedical calculations.
- **Fit:** Builds directly on the first executable Python examples in Block 01 and prepares students for more structured logic and data organisation in Block 03.
- **Common traps:** Confusing assignment (`=`) with comparison (`==`), mixing strings and numbers, overlooking integer versus floating-point values, and assuming Python automatically converts incompatible types.

## Block 03 – Control Flow and Data Structures

- **Purpose:** Introduce the mechanisms that allow students to make decisions, repeat operations and organise multiple values. This is the transition from isolated commands to small, meaningful programs.
- **The one thing that must land:** Conditions control which instructions are executed, while loops repeat instructions. Lists, tuples and dictionaries provide different ways to organise related data.
- **Not in scope:** Advanced algorithms, recursion, complex nested data structures, algorithmic optimisation or extensive treatment of sets, or writing `try`/`except` blocks (reading error messages is in scope).
- **Fit:** Uses the variables, types and operators from Block 02. Prepares students to write reusable functions and process biological sequences in Block 04.
- **Common traps:** Indentation errors, incorrect condition logic, off-by-one errors in loops, confusing list indices with values, and modifying a data structure without understanding the consequences.

## Block 04 – Functions and Biological Programming Tasks

- **Purpose:** Show students how to structure code into reusable units and apply basic programming concepts to biological problems. Functions provide a manageable way to develop, test and reuse analysis steps.
- **The one thing that must land:** A function receives inputs, performs a defined task and can return a result. Students should understand the difference between defining a function and calling it.
- **Not in scope:** Advanced object-oriented programming, class implementation, decorators, generators, complex software architecture or sophisticated sequence-analysis algorithms.
- **Fit:** Combines the variables, control flow and data structures from Blocks 02 and 03. Prepares students to work with numerical arrays and larger datasets in Blocks 05 and 06.
- **Common traps:** Forgetting to return a result, confusing `print()` with `return`, using variables outside their scope, and writing functions that work for one example but fail for other valid inputs.

## Block 05 – NumPy: Numerical Data Analysis

- **Purpose:** Introduce efficient numerical data handling as the foundation for scientific computing. Students should understand why numerical biomedical data are often represented as arrays rather than ordinary Python lists.
- **The one thing that must land:** NumPy arrays support element-wise numerical operations and allow students to select and analyse data using indexing and Boolean masks. Students must understand array shape and dimensions.
- **Not in scope:** Advanced linear algebra, matrix decompositions, numerical optimisation, complex broadcasting rules or machine-learning algorithms.
- **Fit:** Applies the programming foundations from Blocks 01–04 to numerical biomedical measurements. Prepares students for structured tabular data analysis with Pandas in Block 06.
- **Common traps:** Confusing array dimensions and shapes, mixing up rows and columns, misunderstanding Boolean masks, and treating raw RNA-seq counts as if they were directly comparable normalised expression values.

## Block 06 – Pandas: Working with Tables

- **Purpose:** Teach students to inspect, select, filter, clean and summarise realistic biomedical datasets. This block introduces the table-based workflow that will be used throughout the remainder of the course and in the final assessment.
- **The one thing that must land:** A DataFrame is a structured table with labelled rows and columns. Students must be able to inspect a dataset, select relevant information, filter observations and calculate basic summaries.
- **Not in scope:** Complex database systems, advanced data engineering, large-scale data pipelines, extensive file-format coverage or sophisticated multi-table data modelling.
- **Fit:** Builds on NumPy's numerical foundations and introduces the practical data-handling skills needed for visualisation in Blocks 07 and 08.
- **Common traps:** Confusing column names with row indices, overlooking missing values, applying filters incorrectly, and assuming that a successful import means the data are clean and meaningful.

## Block 07 – Matplotlib: Fundamentals of Data Visualisation

- **Purpose:** Establish the principles and practical skills needed to create clear, scientifically useful figures. Students should be able to turn analysed data into plots that communicate the relevant information.
- **The one thing that must land:** A plot is not just a visual output; it must represent the data correctly and make its meaning understandable through appropriate axes, labels, scales and legends.
- **Not in scope:** Advanced figure design, publication-specific formatting, complex customisation, animation or interactive visualisation libraries.
- **Fit:** Uses the data structures and summaries developed in Blocks 05 and 06. Provides the plotting foundations for the more specialised statistical visualisations in Block 08.
- **Common traps:** Missing axis labels or units, inappropriate plot types, misleading axis scales, confusing categories and numerical values, and creating figures without checking whether they support the intended scientific message.

## Block 08 – Seaborn and Exploratory Data Visualisation

- **Purpose:** Expand students' visualisation skills towards exploratory analysis and comparison of biological groups. Students should learn to use visualisations to identify patterns, variability and potential relationships in biomedical data.
- **The one thing that must land:** Different visualisation types answer different questions. Students must be able to select a suitable plot for the data and research question and interpret what the plot actually shows.
- **Not in scope:** Advanced statistical modelling, machine learning, complex clustering algorithms or treating visual patterns as proof of biological mechanisms.
- **Fit:** Extends the Matplotlib foundations from Block 07 and prepares students to assess data quality, statistical evidence and biological interpretation in Block 09.
- **Common traps:** Overinterpreting correlations, ignoring sample size and variability, comparing groups without considering the experimental design, and confusing visual differences with statistically or biologically meaningful effects.

## Block 09 – Data Quality, Statistics and Interpretation

- **Purpose:** Develop the critical judgement needed to assess whether an analysis is reliable and whether its conclusions are justified. This block is particularly important for the final exam because students must explain and defend their analytical decisions.
- **The one thing that must land:** Statistical results do not speak for themselves. Students must connect data quality, experimental design, statistical methods, effect sizes and biological context before drawing conclusions.
- **Not in scope:** Advanced statistical theory, complex regression models, survival analysis, specialised bioinformatics statistics or mathematical derivations of statistical tests.
- **Fit:** Builds on the data handling and visualisation skills from Blocks 05–08. Prepares students to apply the complete analytical workflow independently in Block 10.
- **Common traps:** Confusing technical and biological replicates, interpreting p-values as measures of biological importance, ignoring small sample sizes or multiple testing, treating correlation as causation, and applying statistical tests without checking whether their assumptions are reasonable.

## Block 10 – AI-Assisted Biomedical Data Analysis

- **Purpose:** Integrate the programming, data analysis, visualisation and critical reasoning skills developed throughout the course into a complete biomedical analysis workflow. This block directly prepares students for the practical notebook assessment and the oral examination.
- **The one thing that must land:** AI can support an analysis, but the student remains responsible for every analytical decision, every generated code section and every scientific conclusion. Students must be able to explain, test and defend their workflow.
- **Not in scope:** Introducing major new Python libraries, advanced machine learning, fully automated analysis pipelines or expecting students to solve complex research problems independently without guidance.
- **Fit:** Consolidates all previous blocks. It should primarily apply and connect established concepts rather than introduce substantial new programming content.
- **Common traps:** Accepting AI-generated code or interpretations without verification, running an entire analysis without checking intermediate results, overlooking data-quality problems, confusing statistical significance with biological relevance, and being unable to explain one's own notebook.


# Final examination after the course

To assess the students learning success, they have to pass a test and be graded. 
The idea is to give each student the assignment to analyze an unknown data set by creating an appropriate runnable jupyter notebook, that will analyze the data, find key insights and produce
appropriate plots and tables. The students need to answer some research questions about the dataset and may explicitly use AI assist to create these. 
In a final session, each student will present and explain their notebook and answer some questions about it in an oral presentation.

Evaluation will be according to the following criteria:

**Part 1 – Notebook, practical application – 50% of the grade**

Analysis of a small, unknown data set with Python. Students submit a notebook with code, visualisations, tables, results, documentation and interpretation. Suggested weighting within Part 1:

| Criterion | Weight within Part 1 |
|---|---|
| Runnability: the notebook runs top to bottom in a fresh kernel without errors, uses relative paths and fixed seeds | 20% |
| Correct analysis: all scientific questions are answered correctly | 30% |
| Plots and tables: correct, appropriate type, labelled and readable | 20% |
| Interpretation in the biological context, including limitations | 15% |
| Documentation: markdown explanations, comments, handling of data problems, AI usage documented as described above | 15% |

**Part 2 – Oral presentation – 30% of the grade (5–10 minutes)**

Students guide us through their notebook and explain what they did and why: the analysis plan, the reasons for their choices, the central findings and insights, and the limitations.

**Part 3 – Questions – 20% of the grade (5–7 minutes)**

Questions on the student's own code, the Python concepts of the course, data analysis and the use of AI. They come in four types:

- *Change the code:* "How would you change your code to calculate ...?"
- *Change the strategy:* "How would you adjust your strategy to answer this different question ...?"
- *Errors:* "What errors could occur if ...?"
- *AI:* "How would you use AI to ...?"

For each assignment, the agent prepares a question bank with expected answers (see the agent instructions).

**What the top grade (1.0, "A") requires**

- A perfectly runnable notebook that answers all scientific questions and produces plots and tables correctly.
- A presentation in which the student can explain what they did and why.
- Correct answers to the questions of Part 3 (all four types).

**Passing the course**

The exact requirements, including the point thresholds, are listed under "Grading scale and passing requirements" below. In short:

- The course is passed with a complete notebook, a presentation in which the student can explain their approach, and the required points.
- If the notebook contains errors, the student must fix them and hand in the corrected notebook. Errors do not cause a fail. They lower the grade through the runnability criterion in Part 1.
- The course is failed if no notebook is handed in, if the notebook is incomplete (not all tasks are addressed), or if the student cannot explain the approach they took.

### Grading scale and passing requirements

The examination is graded on a 100-point scale. The final grade is based on the following weighting:

| Examination part | Weight | Maximum points |
|---|---:|---:|
| Part 1 – Notebook, practical application | 50% | 50 |
| Part 2 – Oral presentation | 30% | 30 |
| Part 3 – Questions | 20% | 20 |
| **Total** | **100%** | **100** |

**Proposed grading scale:**

| Points | Grade |
|---:|---:|
| 95–100 | 15 |
| 90–94 | 14 |
| 85–89 | 13 |
| 80–84 | 12 |
| 75–79 | 11 |
| 70–74 | 10 |
| 65–69 | 9 |
| 60–64 | 8 |
| 55–59 | 7 |
| 50–54 | 6 |
| 45–49 | 5 |
| 40–44 | 4 |
| 35–39 | 3 |
| 30–34 | 2 |
| 25–29 | 1 |
| 0–24 | 0 |

**Passing requirements:**

To pass the examination, students must:

- Achieve at least 50 out of 100 points overall.
- Achieve at least 40% of the available points in each of the three examination parts.
- Submit a complete notebook addressing all required tasks.
- Demonstrate a basic understanding of their own analysis, code and scientific conclusions during the oral examination.

Minor technical errors in the notebook reduce the score for runnability but do not automatically result in failure. If a notebook contains errors, students may be asked to correct and resubmit it, subject to the applicable examination regulations.

An incomplete submission or a failure to demonstrate a basic understanding of the submitted analysis may result in failing the examination.

**Principles of grading:**

- Scientific correctness and appropriate analytical decisions are more important than code complexity.
- Students are not expected to write sophisticated Python code from memory. Appropriate use of AI assistance is permitted and encouraged.
- AI-generated code is evaluated according to whether the student understands, tests, validates and appropriately adapts it.
- Students are not penalised for using AI, provided its use is transparently documented and the student takes responsibility for the submitted work.
- Different valid approaches to a research question are accepted if they are scientifically justified and produce correct results.


**Organisation**

- Format of Part 1: take-home assignment, duration: 2 hours, AI may be used but must be documented as discussed in the Lectures.
- Number of students: 5, with 5 different assignments: each student receives a different assignment. If there are ever more students than assignments, the generator creates seeded variants of the assignment datasets (same structure and questions, different data, individually planted defects), so that every student works on a genuinely unknown dataset and results cannot be copied.
- Example solutions, question banks and answer keys are instructor-only material and never part of the student repository. Task descriptions and data of the assignments are released at the exam date.
