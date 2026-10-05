# Exercise A — User Manual Procedure

## Create and Activate a Python Virtual Environment and Install a Package

This procedure shows a beginner how to create an isolated Python environment, activate it, and install the `requests` package.

## Prerequisites

Before starting, you need:

- A computer with Python 3 installed.
- A terminal application: Command Prompt/PowerShell on Windows or Terminal on macOS/Linux.
- Basic knowledge of opening a terminal and typing commands.
- An internet connection for downloading the package.
- Permission to create files in the folder where you will work.

> **Note:** The commands below use `python`. If your computer uses `python3` to start Python, replace `python` with `python3`.

## Procedure

### 1. Open a terminal

**Action:** Open Command Prompt, PowerShell, or Terminal.

**Expected result:** A terminal window displays a command prompt where you can enter commands.

### 2. Create a working folder

**Action:** Run `mkdir python-project`.

**Expected result:** A folder named `python-project` is created in the current location.

### 3. Enter the working folder

**Action:** Run `cd python-project`.

**Expected result:** The terminal prompt now shows that the current working directory is `python-project`.

### 4. Create the virtual environment

**Action:** Run `python -m venv .venv`.

**Expected result:** A `.venv` folder is created inside `python-project` containing the files needed for the isolated Python environment.

### 5. Activate the virtual environment on Windows Command Prompt

**Action:** Run `.venv\\Scripts\\activate.bat`.

**Expected result:** The terminal prompt begins with `(.venv)`, showing that the virtual environment is active.

### 6. Activate the virtual environment on Windows PowerShell

**Action:** Run `.venv\\Scripts\\Activate.ps1`.

**Expected result:** The PowerShell prompt begins with `(.venv)`, showing that the virtual environment is active.

> Perform this step instead of Step 5 when using PowerShell.

### 7. Activate the virtual environment on macOS or Linux

**Action:** Run `source .venv/bin/activate`.

**Expected result:** The terminal prompt begins with `(.venv)`, showing that the virtual environment is active.

> Perform this step instead of Steps 5 and 6 when using macOS or Linux.

### 8. Upgrade pip

**Action:** Run `python -m pip install --upgrade pip`.

**Expected result:** pip is upgraded, or the terminal reports that the installed version already satisfies the requirement.

### 9. Install the requests package

**Action:** Run `python -m pip install requests`.

**Expected result:** pip downloads and installs `requests` and its required dependencies successfully.

### 10. Verify the installation

**Action:** Run `python -c "import requests; print(requests.__version__)"`.

**Expected result:** The terminal prints the installed `requests` version without an import error.

### 11. Deactivate the virtual environment

**Action:** Run `deactivate`.

**Expected result:** The `(.venv)` prefix disappears from the terminal prompt.

## Screenshot Description

**Screenshot to include:** A terminal window showing the completed installation and verification. The screenshot should show the `(.venv)` prompt, the command `python -m pip install requests` with a successful installation message, and the verification command printing a `requests` version number.

## Troubleshooting

### Error: `python is not recognized` or `python: command not found`

This usually means Python is not installed or the Python executable is not available through the system PATH.

**Fix:** Install Python 3 from the official Python distribution for your operating system, then close and reopen the terminal. On systems where Python is started with `python3`, repeat the procedure using `python3` in place of `python`.
