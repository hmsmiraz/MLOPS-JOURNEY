# Day 01 — Python Environment Setup

**Phase:** 0 — Foundations | **Week:** 1  
**Roadmap Topic:** Install Python 3.11+, set up virtual environment, install Jupyter/VS Code

---

## What I Did
Set up a clean isolated Python environment for the entire MLOps journey.
Chose VS Code over Jupyter Notebook — VS Code handles both .ipynb and .py files,
which matters more in Phase 3+ when Docker and pipelines take over from notebooks.

---

## Setup Commands

### Step 1 — Install system dependencies
**Ubuntu/Debian:**
```bash
sudo apt install python3.12-venv python3-pip -y
```
**macOS:**
```bash
brew install python@3.12
```
**Windows:**
Download Python 3.12+ from https://python.org and check "Add to PATH" during install.

---

### Step 2 — Create the virtual environment
```bash
python3 -m venv ~/mlops-env
```

---

### Step 3 — Activate the environment
**Linux/macOS:**
```bash
source ~/mlops-env/bin/activate
```
**Windows (PowerShell):**
```powershell
~/mlops-env/Scripts/Activate.ps1
```
You will see `(mlops-env)` appear at the start of your terminal.

---

### Step 4 — Install core packages
```bash
pip install ipykernel numpy pandas matplotlib
```

---

### Step 5 — Register kernel for VS Code
```bash
python -m ipykernel install --user --name=mlops-env
```
This makes VS Code see `mlops-env` as a kernel option for notebooks.

---

### Step 6 — Quick activation alias (Linux/macOS)
```bash
echo 'alias mlenv="source ~/mlops-env/bin/activate"' >> ~/.bashrc
source ~/.bashrc
```
Now just type `mlenv` to activate anytime.

---

### Step 7 — VS Code setup
Install two extensions:
- Python (by Microsoft)
- Jupyter (by Microsoft)

Select kernel: `Ctrl+Shift+P` → "Select Kernel" → "Python Environments" → pick `mlops-env`

---

## Common Issues & Fixes

| Problem | Fix |
|---------|-----|
| venv creation fails | `sudo apt install python3.12-venv python3-pip -y` |
| `pip` not found | Make sure venv is activated — check for `(mlops-env)` in terminal |
| VS Code picks wrong kernel | Click kernel name top right → Select Another Kernel → mlops-env |
| `No module named numpy` | Wrong kernel selected in VS Code — switch to mlops-env |
| `.venv` auto-created by VS Code | Run `deactivate` then `mlenv` to switch back |

---

## Key Concepts

### Virtual Environment = Docker Container (Mental Model)
| Docker | Virtual Environment |
|--------|-------------------|
| `docker build` | `python3 -m venv` |
| `docker run` | `source activate` |
| Isolated filesystem | Isolated packages |
| `rm container` | `rm -rf ~/env` |

### Every Session Flow
Open terminal → mlenv → work → close terminal → auto deactivated


---

## DevOps → MLOps Connection
In DevOps we use Docker for environment isolation.
In ML, virtual environments serve the same purpose at the Python level.
In Phase 3 (MLOps Core), both combine — Python env INSIDE a Docker container.

---

## Tomorrow — Day 02
NumPy basics: arrays, shapes, broadcasting, vectorized operations vs Python loops.
File: `notebooks/week-01/day02_numpy.ipynb`