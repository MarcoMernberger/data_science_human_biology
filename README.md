# Data Science in der Humanbiologie - Python Data Science Course

Welcome to the Python Data Science course for "Data Science in der Humanbiologie".

In this course, we will use Python to analyze, visualize, and interpret biological data.

We will work with:

- **Python** – programming language for data analysis
- **VS Code** – programming environment
- **Jupyter Notebooks** – interactive data analysis notebooks
- **Git** – downloading and updating course materials
- **uv** – managing the Python environment and required packages

The setup needs to be completed **once before the course starts**.

Please follow all steps carefully.

---

# Overview

At the end of the installation, your workflow will be:

```
GitHub repository
        |
        ↓
VS Code
        |
        ↓
Python environment (.venv)
        |
        ↓
Jupyter Notebook
        |
        ↓
Data analysis
```

---

# Step 1 - Install Visual Studio Code

Download and install Visual Studio Code:

https://code.visualstudio.com/

Install it with the default settings.

After installation, open VS Code once to make sure it starts correctly.

---

# Step 2 - Install Git

Git allows us to download and update the course materials.

Download Git:

https://git-scm.com/downloads

Install Git using the default settings.

After installation, open a terminal.

## Windows

Open:

```
Start Menu → PowerShell
```

## macOS

Open:

```
Applications → Utilities → Terminal
```

## Linux

Open your normal terminal.

Check that Git works:

```bash
git --version
```

You should see something similar to:

```
git version 2.x.x
```

If you see a version number, Git is installed correctly.

---

# Step 3 - Install Python

We use Python version 3.13.

Download Python:

https://www.python.org/downloads/

Install Python 3.13.

## Windows users: Important!

During installation, make sure to check:

```
☑ Add python.exe to PATH
```

before clicking "Install Now".

---

## Check Python installation

Open a new terminal and type:

```bash
python --version
```

You should see:

```
Python 3.13.x
```

If this works, Python is installed correctly.

---

# Step 4 - Install uv

uv manages the Python environment for this course.

It creates a separate environment containing exactly the packages we need.

---

## Windows

Open PowerShell and run:

```powershell
winget install --id=astral-sh.uv
```

---

## macOS / Linux

Open Terminal and run:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

---

Close the terminal completely and open a new one.

Check that uv works:

```bash
uv --version
```

You should see a version number.

Example:

```
uv 0.x.x
```

---

# Step 5 - Install VS Code extensions

Open VS Code.

Click the Extensions icon on the left side.

Install the following two extensions:

---

## Python

Publisher:

```
Microsoft
```

Extension:

```
Python
```

---

## Jupyter

Publisher:

```
Microsoft
```

Extension:

```
Jupyter
```

---

# Step 6 - Download the course materials

We now download the course repository.

Open a terminal.

Go to the location where you want to store the course.

Example:

```bash
cd Documents
```

Download the repository:

```bash
git clone https://github.com/DEIN-USERNAME/human-biology-python.git
```

Replace:

```
DEIN-USERNAME
```

with the actual GitHub username or organization name.

---

Now enter the course folder:

```bash
cd human-biology-python
```

You are now inside the course project.

---

# Step 7 - Create the Python environment

Inside the course folder, run:

```bash
uv sync
```

This command will:

- create a private Python environment
- install all required Python packages
- install the exact versions used in this course

The first installation may take several minutes.

After successful completion, a new folder called

```
.venv
```

will exist.

Do not modify or delete this folder.

---

# Step 8 - Open the course in VS Code

From the terminal, run:

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
human-biology-python
```

---

# Step 9 - Select the Python environment in VS Code

VS Code needs to know which Python installation to use.

Press:

## Windows/Linux

```
Ctrl + Shift + P
```

## macOS

```
Cmd + Shift + P
```

Search:

```
Python: Select Interpreter
```

Select the interpreter inside:

```
.venv
```

It should look similar to:

```
Python 3.13 (.venv)
```

---

# Step 10 - Test your installation

Open:

```
notebooks/00_setup_test.ipynb
```

At the top right of the notebook, select the Python kernel:

```
Python (.venv)
```

Then click:

```
Run All
```

The notebook should run without errors and display a test plot.

If you see the plot:

🎉 Congratulations!

Your Python environment is ready.

---

# Working with the course

## Open a notebook

Course exercises are stored as:

```
.ipynb
```

files.

Open them in VS Code and run the cells one by one.

---

## Updating course materials

If new materials are added during the course:

Open a terminal inside the course folder and run:

```bash
git pull
```

---

## Updating packages

If instructed by the lecturer, run:

```bash
uv sync
```

---

# Important rules

## Do not install Python packages manually

Do not use:

```bash
pip install package-name
```

The course environment is managed by:

```
pyproject.toml
```

and

```
uv.lock
```

Using other installation methods can break the environment.

---

## Do not delete the .venv folder

The folder:

```
.venv
```

contains your course-specific Python environment.

---

# Troubleshooting

## Problem: Python command not found

Check that Python is installed:

```bash
python --version
```

If this does not work:

- restart the terminal
- restart the computer
- reinstall Python and make sure "Add Python to PATH" is enabled (Windows)

---

## Problem: VS Code cannot find Python

Repeat:

```
Ctrl + Shift + P
```

(or `Cmd + Shift + P` on macOS)

Choose:

```
Python: Select Interpreter
```

and select:

```
.venv
```

---

## Problem: Something is broken

Try:

```bash
uv sync
```

Then restart VS Code.

If the problem remains, report:

1. Your operating system:
   - Windows
   - macOS
   - Linux

2. The command you executed

3. The complete error message

---

# Final checklist

Before the course starts, you should have:

☑ VS Code installed  
☑ Git installed  
☑ Python 3.13 installed  
☑ uv installed  
☑ VS Code Python extension installed  
☑ VS Code Jupyter extension installed  
☑ Course repository downloaded  
☑ `uv sync` completed successfully  
☑ Test notebook runs successfully  

You are ready for the course!