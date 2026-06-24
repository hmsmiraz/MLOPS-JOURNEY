# Day 01 — Python Environment Setup

**Phase:** 0 — Foundations | **Week:** 1  
**Roadmap Topic:** Install Python 3.11+, set up virtual environment, install Jupyter/VS Code

---

## What I Did
Set up a clean, isolated Python environment for the entire MLOps journey.
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

### Step 2 — Create the project virtual environment
```bash
python3 -m venv ~/mlops-env
```
This creates an isolated environment — think of it like a Docker container
but for Python packages. Each project gets its own clean slate.

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
You will see `(mlops-env)` appear at the start of your terminal line.

---

### Step 4 — Install core packages
```bash
pip install ipykernel numpy pandas matplotlib
```

---

### Step 5 — Set up a quick activation alias (Linux/macOS)
```bash
echo 'alias mlenv="source ~/mlops-env/bin/activate"' >> ~/.bashrc
source ~/.bashrc
```
Now just type `mlenv` to activate anytime instead of the full command.

---

### Step 6 — VS Code setup
Install these two extensions:
- Python (by Microsoft)
- Jupyter (by Microsoft)

Then: `Ctrl+Shift+P` → "Select Kernel" → pick `mlops-env`
VS Code remembers this kernel for all future notebook work.

---

## Key Concepts Learned

### Virtual Environment = Docker Container (Mental Model)
| Docker | Virtual Environment |
|--------|-------------------|
| `docker build` | `python3 -m venv` |
| `docker run` | `source activate` |
| Isolated filesystem | Isolated packages |
| `rm container` | `rm -rf ~/env` |

This is the core insight — environment isolation in ML is the same
mindset as container isolation in DevOps. Reproducibility is the goal.

### Why NOT install packages system-wide?
- Different projects need different package versions
- System Python breaking = everything breaks
- No reproducibility = no MLOps

### Activation rule
Every new terminal session → activate venv → do work → close terminal → auto deactivated.
VS Code handles this automatically for notebooks once kernel is selected.

---

## Verification Test
```bash
# Create a test environment
python3 -m venv ~/test-env
source ~/test-env/bin/activate  # Linux/macOS

# Verify isolation
which python3
# Should show: /home/YOUR_USER/test-env/bin/python3

pip list
# Should show only: pip 24.0 (clean slate)

# Cleanup
deactivate
rm -rf ~/test-env
```

---

## Struggles / Questions
- Initial venv creation failed — missing `python3.12-venv` package on Ubuntu
- Fixed by: `sudo apt install python3.12-venv python3-pip -y`

---

## DevOps → MLOps Connection
In DevOps we use Docker for environment isolation.
In ML/Data work, virtual environments serve the same purpose at the Python level.
In Phase 3 (MLOps Core), both combine — Python env INSIDE a Docker container.
This week is laying the foundation for that.

---

## Tomorrow — Day 02
NumPy basics: arrays, shapes, broadcasting, vectorized operations vs Python loops.
Solve 10 array manipulation problems.
File: `notebooks/week-01/day02_numpy.ipynb`
