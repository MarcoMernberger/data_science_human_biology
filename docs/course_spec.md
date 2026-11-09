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
8. Knowledge section at the very end: Summary and explanation of the most important concepts and example solutions to the exercises.

Goal: apply concepts, write code, solve problems, use AI deliberately, identify and solve errors independently, solidify the knowledge

# Major didactic rules

- make the lectures not too long. They need to contain the relevant concepts in an understandable way and be usable as a reference later, but they should not be overloaded.
- Several blocks below list more topics than fit into 1.5 hours for complete beginners. The agent must NOT silently drop or silently squeeze topics. In the syllabus it flags overloaded blocks and proposes what to move (to another block, to an optional 'further reading' section, or to a mention only), and I decide.
- Only use Python concepts that were introduced in the current or an earlier block. If a library function requires a concept that has not been introduced yet, either avoid it or explain it briefly where it is first needed.
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

The block lists above do not mention the following topics, but later blocks and the learning goals depend on them. In the syllabus, the agent proposes in which block each one is introduced (and which block it takes time from), and I decide:

- `import`, modules and libraries (`import numpy as np`, installed packages versus the standard library). Needed before Block 05 at the latest, ideally earlier.
- String handling: indexing and slicing, common string methods (`upper()`, `count()`, `replace()`), f-strings. Needed for the DNA sequence functions in Block 04.
- List comprehensions (AI-generated code uses them constantly, and students must be able to read them).
- Reading tracebacks and recognising common exception types (`NameError`, `TypeError`, `KeyError`, `IndexError`, `ValueError`). A learning goal, but no block lists it.
- Simple test cases with `assert` (a learning goal, but no block lists it).
- Library versions: AI answers often use outdated idioms (for example older pandas or NumPy syntax). Students should learn to check the installed versions and the documentation.
- Git basics, if they are not covered completely by the setup instructions.

## Day 1 – Introduction to Python and Programming

**Objective:** Students understand the working environment and can write and follow simple Python instructions.

### Block 01 – Python, Jupyter and AI

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- What is Python? What is a programming language?
- Interpreters and scripts
- Jupyter Notebooks: kernels, cells, Markdown and code
- VS Code: interface, Python environment, Jupyter integration and file management
- Getting started: `print()`, comments and simple calculations
- reproducibility: what does it mean? why do analysis have to be repeatable at any time?
- jupyter notebooks, order of execution, why should we restart the kernel and rerun from time to time
- importance of documentation
- Jupyter shortcuts and useful features
- Introduction to AI-assisted programming: What can ChatGPT do, and what are its limitations?

**AI component:** 

- How do I formulate a good prompt? How can I ask AI to explain Python code? How can I generate code without blindly accepting it?
- Data privacy: Why patient data and confidential research data should not be entered carelessly into public AI systems.

### Block 02 – Variables, Data Types and Operators

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- Writing first Python instructions
- Defining variables and assigning values
- Integers, floats, strings and Booleans
- Exploring data types with `type()`
- Type conversion with `int()`, `float()` and `str()`
- Arithmetic and logical operators
- Comparison operators and Boolean expressions
- Simple biological calculations (e.g. dilutions, concentrations and age calculations)

**AI task:** Students use AI to generate a small calculator for a biological problem, review the code and test it with their own values.

## Day 2 – Programming with Python and Problem Solving

**Objective:** Students understand basic programming logic and can independently solve simple analytical tasks.

### Block 03 – Control Flow and Data Structures

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- Why do we need control structures?
- `if`, `elif`, `else`
- `for` and `while` loops
- `range()`, `enumerate()`, `break` and `continue`
- Lists and tuples
- Dictionaries and sets
- Iterables and iteration
- Nested data structures

**AI component:** Asking AI to explain code, generate loops and identify errors in existing code.

### Block 04 – Functions and Biological Programming Tasks

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- Creating custom functions with `def`
- Parameters, arguments and return values
- Default parameters
- Local variables
- `help()` and docstrings
- touch upon object-orientation: what is an object, what is a class? what are attributes and methods? difference between class and instance. Students need to know that this exists and later use class methods and attributes with pandas and seaborn. but they do not need to implement themselves.
- Writing small functions for sequence analysis:
  - Determining the length of a DNA sequence
  - Calculating GC content
  - Counting specific nucleotides
  - Generating the reverse complement of a DNA sequence
  - Reading .fasta

**AI task:** Develop a function to calculate GC content with the help of AI, test it and then extend it in a targeted way. Students should be able to explain what each line of code does.

## Day 3 – Scientific Data Analysis with NumPy and Pandas

**Objective:** Students can load, manipulate and analyse numerical data and tabular datasets.

### Block 05 – NumPy: Numerical Data Analysis

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- Why NumPy? Differences between NumPy arrays and Python lists
- Arrays, vectors and matrices
- Dimensions, shape and data types
- Creating arrays: `np.array()`, `np.zeros()`, `np.ones()`, `np.arange()`
- Indexing and slicing
- Boolean masking
- Element-wise calculations
- Raw counts vs. normalised/log-transformed expression 
- Mention `np.linspace()` and broadcasting
- Statistical functions: mean, median and standard deviation
- Random numbers with `np.random` and reproducible seeds (`np.random.seed()`, `random.seed()`)

**Biological context:** Gene expression data, experimental measurements and concentration series.

**AI component:** Generate NumPy code with AI and use small examples to understand what arrays and broadcasting actually do.

### Block 06 – Pandas: Working with Tables

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- What is Pandas?
- Series and DataFrames
- Reading CSV and TSV files (`read_csv`)
- handling different data formats (.csv, .tsv, excel). Focus on dataframes, demonstrate json and fasta.
- also mention .json, .fastq, .bam and .vcf files conceptually (but we will not use them here)
- Exploring data: `head()`, `info()`, `describe()`
- Selecting columns and rows
- Filtering and sorting
- cleaning data
- Identifying and handling missing values
- Calculating new columns
- Grouping with `groupby()`
- Summarising data with `agg()`

**Biological context:** Analysing a table containing gene expression values, sample information or qPCR measurements.

**AI task:** Explore an unfamiliar dataset with the help of AI. AI should suggest meaningful analyses; students then implement these suggestions and verify the results.

## Day 4 – Data Visualisation

**Objective:** Students can create meaningful visual representations of scientific data and interpret them.

### Block 07 – Matplotlib: Fundamentals of Data Visualisation

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- Why do we visualise data?
- Fundamentals of scientific plots
- Figures, axes and subplots
- Line plots, scatter plots, bar plots and histograms
- Axis labels, titles and legends
- Colours, markers and line styles
- Figure size and DPI
- Exporting and saving figures

**Biological context:** Time series, growth curves, gene expression data and experimental measurements.

**AI component:** Create and improve plots with AI assistance. AI should also explain which type of plot is suitable for a particular research question.

### Block 08 – Seaborn and Exploratory Data Visualisation

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- What is Seaborn, and how does it differ from Matplotlib?
- Histograms and distributions
- Boxplots and violin plots
- Scatter plots and regression
- Heatmaps, address Raw counts vs. normalised/log-transformed expression 
- Visualising correlations
- Comparing categories and groups
- Visualising multiple variables simultaneously

**Biological context:** Comparing control and treatment groups, gene expression profiles and correlations between experimental parameters.

**AI task:** Explore a dataset and use AI to develop suitable visualisations. Afterwards, assess whether the visualisations actually address the biological research question.

## Day 5 – Scientific Analysis, Statistics and AI

**Objective:** Students can work through an integrated analysis workflow using a biological dataset and make effective use of AI throughout the process.

### Block 09 – Data Quality, Statistics and Interpretation

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- Common challenges in biomedical datasets
- Data quality and plausibility checks
- Missing values, outliers and duplicates
- Descriptive statistics
- Mean, median, standard deviation and coefficient of variation
- Introduction to statistical tests: t-test and correlation (conceptually and practically)
- p-values and their interpretation
- biological versus technical replicates
- effect sizes
- statistical pitfalls: small sample size, multiple hypothesis testing, pseudoreplication, outliers, normal distribution assumption, correlation does not imply causation
- Reproducibility and documentation of analyses

**AI component**

- Using AI to support the selection of appropriate statistical methods
- Asking AI to help interpret results
- Critically reviewing AI-generated statistical statements

### Block 10 – AI-Assisted Biomedical Data Analysis

*Lecture 1.5 h + Hands-on 1.5 h*

**Topics**

- Loading an unfamiliar biological dataset
- Exploring its structure and data quality
- Formulating research questions
- Developing an analysis plan with AI
- Generating and executing Python code step by step
- Filtering and summarising data
- Creating suitable visualisations
- Interpreting results
- Critically reviewing AI-generated results
- Documenting the analysis in a reproducible and transparent way (clean documentation, reproducibility, separation of raw and processed data, version documentation and control)

**Final discussion:** What did AI do well? Where did it make mistakes? Which decisions did the students have to make themselves?


# Final examination after the course

To assess the students learning success, they have to pass a test and be graded. 
The idea is to give each student the assignment to analyze an unknown data set by creating an appropriate runnable jupyter notebook, that will analyze the data, find key insights and produce
appropriate plots and tables. The students need to answer some research questions about the dataset and may explicitly use AI assist to create these. 
In a final session, each student will present and explain their notebook and answer some questions about it in an oral presentation.

Evaluation will be according to the following criteria:

Part 1 – Generation of a notebook, practical application - 50% of the grade
Analysis of a small data set with python. Students need to submit a notebook with code, visualizations, results, documentation and interpretation. 

Part 2 – Oral presentation - 30% of the grade (5-10 minutes)
Students need to explain and guide us through their notebook and explain their reasoning, explain the central findings and insights.

Part 3 – Questions - 20% of the grade (5-7 minutes)
Specific questions regarding their own code, python concepts of the course, data analysis and usage of AI.

