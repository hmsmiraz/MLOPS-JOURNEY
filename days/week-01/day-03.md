# Day 03 — Matplotlib Basics

**Phase:** 0 — Foundations | **Week:** 1  
**Roadmap Topic:** Line plots, histograms, scatter plots for data visualization

---

## What is Matplotlib?
Matplotlib turns numbers into charts so you can see patterns in data.
In ML you cannot debug a model by staring at 10,000 numbers — you need to visualize.
Every ML project starts with visualizing data before training anything.

---

## Core Chart Types

### 1. Line Plot — for trends over time
```python
plt.plot(x, y, color='blue', linewidth=2, linestyle='--')
plt.title("Title")
plt.xlabel("X axis")
plt.ylabel("Y axis")
plt.grid(True)
plt.show()
```
Use for: training loss over epochs, CPU usage over time, stock prices.

---

### 2. Histogram — for data distribution
```python
plt.hist(data, bins=30, color='steelblue', edgecolor='black', alpha=0.7)
```
Use for: seeing if data is normal, skewed, or has outliers.
`bins` = how many bars. `alpha` = transparency.

---

### 3. Scatter Plot — for relationships between variables
```python
plt.scatter(x, y, color='green', alpha=0.6, label='Class 0')
plt.legend()
```
Use for: seeing if two features are related, visualizing class separation.

---

### 4. Subplots — multiple charts together
```python
fig, axes = plt.subplots(rows, cols, figsize=(width, height))
axes[row, col].plot(...)   # access each chart by position
plt.tight_layout()         # fix spacing automatically
```

---

## Key Parameters Cheatsheet

| Parameter | What it does |
|-----------|-------------|
| `color=` | line/bar color |
| `linewidth=` | thickness of line |
| `linestyle='--'` | dashed line |
| `alpha=` | transparency (0=invisible, 1=solid) |
| `bins=` | number of bars in histogram |
| `label=` | name for legend |
| `edgecolor=` | border color of bars |
| `figsize=(w,h)` | chart size in inches |
| `dpi=` | image quality when saving |
| `grid(True, alpha=0.3)` | faint grid lines |

---

## Real ML Use Cases Built Today

### Training vs Validation Loss
```python
plt.plot(epochs, train_loss, label='Train Loss')
plt.plot(epochs, val_loss,   label='Val Loss')
plt.axvline(x=best_epoch, color='green', linestyle='--', label='Best Epoch')
```
Shows overfitting visually — when val_loss stops improving but train_loss keeps going down.

### Anomaly Detection on CPU Metrics
```python
threshold = cpu.mean() + 2 * cpu.std()
plt.axhline(y=threshold, color='red', linestyle='--')
plt.scatter(anomalies, anom_values, color='red', s=100)
```
Mean + 2 standard deviations = anything above this is unusual.
Directly relevant to Phase 5 AIOps work.

### Feature Distribution Before vs After Scaling
```python
fig, axes = plt.subplots(1, 2)
axes[0].hist(raw_data,    bins=40, color='tomato')
axes[1].hist(scaled_data, bins=40, color='steelblue')
```
Shows why feature scaling matters — same data, completely different range.

### MLOps Monitoring Dashboard (2x2 grid)
```python
fig, axes = plt.subplots(2, 2, figsize=(14, 10))
fig.suptitle("MLOps Monitoring Dashboard")
# 4 charts: training loss, CPU anomaly, distribution, class scatter
```

---

## Saving Charts
```python
plt.savefig("../../assets/images/chart.png", dpi=150, bbox_inches='tight')
```
`../../` goes up two folders from notebook location to repo root.
`bbox_inches='tight'` removes empty whitespace around the chart.

---

## Key Takeaways
- `plt.plot()` → line (trends)
- `plt.hist()` → histogram (distributions)
- `plt.scatter()` → scatter (relationships)
- `plt.subplots()` → dashboard of multiple charts
- Always add title, xlabel, ylabel
- `alpha` controls transparency — useful when overlapping charts
- `axhline()` draws threshold lines — key for anomaly detection

---

## DevOps → MLOps Connection
In DevOps we read Grafana dashboards to monitor systems.
In ML we build similar dashboards with Matplotlib to monitor model health.
Phase 5 AIOps combines both — ML models monitoring DevOps metrics.

---

## Notebook
[day03_matplotlib.ipynb](../../notebooks/week-01/day03_matplotlib.ipynb)

---

## Tomorrow — Day 04
Pandas basics: Series, DataFrame, reading CSV, indexing, filtering rows.
File: `notebooks/week-01/day04_pandas.ipynb`