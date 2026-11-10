# Data Science in Human Biology - Python Data Science Course

Welcome to the Python course **Data Science in Human Biology**.

In this course, we use Python to analyze, visualize, and scientifically evaluate biological data.

We work with:

- **Python** – programming language for data analysis
- **Visual Studio Code (VS Code)** – development environment
- **Jupyter Notebooks** – interactive environment for data analysis
- **Git** – for downloading and updating course materials
- **uv** – management of the Python environment and required packages

The installation only needs to be performed **once before the practical course starts**.

Please follow all steps in the order given.

---

# Overview

After successful installation, your workflow will look like this:

```
GitHub Repository
        |
        ↓
Visual Studio Code
        |
        ↓
Python environment (`.venv`)
        |
        ↓
+----------------+
|                |
VS Code      JupyterLab
|                |
+----------------+
        |
        ↓
Data analysis
```

---


# Requirements

You need:

☑ Computer running Windows, macOS, or Linux  
☑ Internet connection (for the installation; the course notebooks themselves work offline)

The following software will be installed:

☑ Visual Studio Code  
☑ Git  
☑ uv  
☑ Required VS Code extensions  

The Python version and all Python packages are automatically managed by `uv`.

---

# Step 1 - Install Visual Studio Code

Download Visual Studio Code:

[Visual Studio Code](https://code.visualstudio.com/)

Install VS Code using the default settings.

Open VS Code once after installation to make sure it works correctly.

---

# Step 2 - Install Git

Git is required to download the course materials and update them later.

Download Git:

[Git](https://git-scm.com/downloads)

Install Git using the default settings.

On Linux you can also install Git with your package manager, for example on Ubuntu or Debian:

```bash
sudo apt install git -y
```

---

## Test Git installation

Open a terminal.

### Windows

Open:

```
Start Menu → PowerShell
```

### macOS

Open:

```
Applications → Utilities → Terminal
```

### Linux

Open your terminal.

Enter:

```bash
git --version
```

You should see output similar to:

```
git version 2.x.x
```

If a version number appears, Git has been installed successfully.

---

# Step 3 - Install uv

uv manages the complete Python environment for this course.

It:

* installs the correct Python version
* creates an isolated environment
* installs all required packages
* ensures that all students use the same environment

---

## Windows

Open PowerShell and run:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

If this does not work, you can try `winget` instead:

```powershell
winget install --id=astral-sh.uv -e
```

---

## macOS and Linux

Open a terminal:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

If `curl` is missing on Linux (Ubuntu or Debian):

```bash
sudo apt install curl -y
```

---

Close the terminal completely and open a new terminal.

Test the installation:

```bash
uv --version
```

Example:

```
uv 0.x.x
```

---

# Step 4 - Install VS Code Extensions

Open VS Code.

Click the "Extensions" icon on the left:

![Extensions](assets/extensions.svg)

Install the following extensions:


| Extension | Publisher | Extension ID (Search for) | Purpose |
|---|---|---|---|
| Python | Microsoft | `ms-python.python` | Python support, selecting the interpreter, running Python code |
| Jupyter | Microsoft | `ms-toolsai.jupyter` | Opening and running Jupyter notebooks (`.ipynb`) |
| Data Wrangler | Microsoft | `ms-toolsai.datawrangler` | Interactive exploration and preparation of datasets |
| Ruff | Astral Software | `charliermarsh.ruff` | Automatic code analysis and formatting |

---


# Step 5 - Download Course Materials

Open a terminal.

Navigate to the location where you want to store the course materials.

Example:

```bash
cd Documents
```

Download the repository:

```bash
git clone https://github.com/MarcoMernberger/data_science_human_biology.git
```

Change into the course directory:

```bash
cd data_science_human_biology
```

Check the contents:

Linux or macOS:

```bash
ls -al
```

Windows:

```powershell
dir
```

You should see files and folders including:

```
README.md
pyproject.toml
uv.lock
notebooks
data
assets
outputs
```

---


# Step 6 - Create the Python Environment

Inside the course directory, run:

```bash
uv sync
```

This command:

- creates a dedicated Python environment
- installs all required Python packages
- installs exactly the versions used in the course

The first installation may take several minutes.

After successful installation, a new folder exists:

```
.venv
```

This folder contains your course environment.

Please do not delete or modify this folder.

---

# Step 7 - Open the Course in VS Code

In the terminal:

```bash
code .
```

Alternatively:

1. Open VS Code
2. Select:

```
File → Open Folder
```

3. Choose:

```
data_science_human_biology
```

---

# Step 8 - Select the Python Environment in VS Code

VS Code needs to know which Python version should be used.

Press:

## Windows/Linux

```
Ctrl + Shift + P
```

## macOS

```
Cmd + Shift + P
```

Search for:

```
Python: Select Interpreter
```

Select the entry that belongs to the `.venv` folder of the course, for example:

```
Python 3.12.x (.venv)
```

or

```
Python 3.13.x (.venv)
```

The exact version number does not matter, as long as `.venv` is part of the entry.

![Select Python Interpreter](assets/select_interpreter.svg)

---

# Step 9 - Test JupyterLab

Depending on the number of installed extensions and available resources, VS Code can use a considerable amount of system resources.

If VS Code runs slowly on your computer, the course can also be completed directly using JupyterLab.

JupyterLab runs in your web browser and requires fewer resources than a full development environment.


## Start JupyterLab

Open a terminal inside the course directory:

```bash
uv run jupyter lab
```

A browser window with JupyterLab will open automatically.

If no browser opens automatically, copy the displayed URL into your browser.

Example:

[http://localhost:8888/lab](http://localhost:8888/lab)

In JupyterLab, the kernel `Python 3 (ipykernel)` is the correct one, because JupyterLab was started with `uv run`.

## Stop JupyterLab

In the terminal press:

`Ctrl + C`

---


# Step 10 - Test the Installation

Open:

```
notebooks/00_setup_test.ipynb
```

In VS Code, click "Select Kernel" in the upper right corner of the notebook and select the entry that belongs to `.venv`:

```
Python Environments... → Python 3.x.x (.venv)
```

![Select Kernel](assets/select_kernel.svg)


Then click:

```
Run All
```

The notebook should run without errors.

At the end, a success message should appear and the test plot should be visible.

If you can see the plot:

🎉 Your Python environment has been successfully configured.

---


# Working During the Course

## Opening notebooks

The course notebooks are provided as files with the extension:

```
.ipynb
```

These files can be opened directly in VS Code or in JupyterLab.

Code can be executed using the ▶ button.

## Work in your own copy

Please do **not** work directly in the folder `notebooks`. Otherwise your changes can collide with updates of the course material (see "Updating Course Materials" below).

Instead, copy the folder of the day to the folder `my_work` and work there. For example for day 1:

Linux or macOS:

```bash
mkdir -p my_work
cp -r notebooks/day01 my_work/
```

Windows (PowerShell):

```powershell
New-Item -ItemType Directory -Force my_work
Copy-Item -Recurse notebooks\day01 my_work\
```

You can also copy and paste the folder in the VS Code file explorer.

Important:

- Keep the folder structure: `my_work/day01`, not `my_work` directly. The notebooks load their data using relative paths (`../../data/...`), which only work at this depth.
- The folder `my_work` is ignored by Git. Your own work is never changed or deleted by updates.
- Do the same with the folder `notebooks/practice`, if you want to work on the practice exercises.

---

# Updating Course Materials

If new or updated materials are provided:

Open a terminal inside the course directory and run:

```bash
git pull
```

---

# Updating Python Packages

The course environment is centrally managed using `pyproject.toml` and `uv.lock`.

If new Python packages are added to the course, they will be provided through the course repository.

After updating the course materials:

```bash
git pull
uv sync
```

# Adding Your Own Python Packages

During the course, please do not add packages yourself. All students must have exactly the same environment.

If you want to use additional packages later for your own projects, create a separate project folder outside the course folder and use `uv` there:

```bash
uv init my_project
cd my_project
uv add <package>
```

`uv add` automatically updates `pyproject.toml` and `uv.lock` of that project.

If you share your own project with others, both files must be included:

```
pyproject.toml
uv.lock
```

---

# Important Rules

## Do not install packages using other methods

Please do not use:

```bash
pip install <package>
```

The course environment is managed automatically through:

```
pyproject.toml
```

and

```
uv.lock
```

Manual installations may cause compatibility problems.

---

## Do not delete the .venv folder

The folder:

```
.venv
```

contains your personal Python environment for this course.

---

# Troubleshooting

## Problem: VS Code cannot find Python

Open the Command Palette:

Windows/Linux:

```
Ctrl + Shift + P
```

macOS:

```
Cmd + Shift + P
```

Select:

```
Python: Select Interpreter
```

and choose the entry that belongs to:

```
.venv
```

---

## Problem: A notebook cannot find a data file (`FileNotFoundError`)

The notebooks load their data using relative paths. Check that your copy is located at the correct depth, for example `my_work/day01/` and not directly in `my_work/`.

---

## Problem: `git pull` reports "Your local changes would be overwritten"

You have changed a file in the folder `notebooks`. Copy your changed notebook into your folder `my_work` first (see "Work in your own copy"). Then run:

```bash
git restore notebooks
git pull
```

---

## Problem: Something does not work

Try first:

```bash
uv sync
```

and restart VS Code.

If the problem persists, note:

1. Operating system:
   - Windows
   - macOS
   - Linux

2. The command you executed

3. The complete error message

---

# Checklist Before the Practical Course

Before the course starts, the following should be completed:

☑ VS Code installed

☑ Git installed

☑ uv installed

☑ Python VS Code extension installed

☑ Jupyter VS Code extension installed

☑ Course repository downloaded

☑ uv sync completed successfully

☑ VS Code and JupyterLab started once

☑ Test notebook executed successfully

You are now ready for the course!
