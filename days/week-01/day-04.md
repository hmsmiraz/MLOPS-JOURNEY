# Day 04 — Pandas Basics

**Phase:** 0 — Foundations | **Week:** 1  
**Roadmap Topic:** Series, DataFrame, reading CSV/JSON, indexing, filtering rows

---

## What is Pandas?
Pandas is built on NumPy but made for **tabular data** — rows and columns,
like Excel or a database table. This is the library you use most in ML —
for loading, cleaning, and exploring data before training any model.

---

## Core Concepts

### Series — 1D labeled array
```python
s = pd.Series([10, 20, 30], index=['a', 'b', 'c'])
s['b']        # access by label
```

### DataFrame — 2D table
```python
df = pd.DataFrame({
    "Name": ["Alice", "Bob"],
    "Age": [25, 30]
})
df.shape      # (rows, cols)
df.columns    # column names
df.dtypes     # data type per column
```

---

### Quick Inspection
```python
df.head()       # first 5 rows
df.tail()       # last 5 rows
df.info()       # types, nulls, memory
df.describe()   # stats: mean, std, min, max
```

---

### Reading & Saving Files
```python
df.to_csv("file.csv", index=False)
pd.read_csv("file.csv")

df.to_json("file.json", orient='records')
pd.read_json("file.json")
```
Pandas can also read directly from a URL — no download step needed.

---

### `.loc` vs `.iloc`
| | Access by |
|---|---|
| `.loc` | label/name |
| `.iloc` | position/number |

```python
df.loc[0, 'Name']     # label-based
df.iloc[0, 0]          # position-based
```

---

### Filtering Rows
```python
df[df['Salary'] > 70000]                          # single condition
df[(df['Age'] < 30) & (df['Salary'] > 60000)]      # multiple — use & and ()
df[df['City'].isin(['NYC', 'LA'])]                 # multiple values
```

---

### Selecting Columns
```python
df['Name']               # single column → Series
df[['Name', 'Salary']]   # multiple columns → DataFrame
```

---

### Adding Columns
```python
df['Bonus'] = df['Salary'] * 0.1
df['Senior'] = df['Age'] > 30
```

---

## Advanced — GroupBy & Aggregation
```python
titanic.groupby('Pclass')['Age'].mean()                     # single stat
titanic.groupby('Pclass')['Age'].agg(['mean','min','max'])  # multiple stats
titanic.groupby(['Pclass','Sex'])['Survived'].mean()        # multi-column group
```

## Pivot Table
```python
titanic.pivot_table(values='Survived', index='Pclass', columns='Sex', aggfunc='mean')
```

## Handling Missing Data
```python
titanic.isna().sum()
titanic['Age'] = titanic['Age'].fillna(titanic['Age'].median())
titanic.dropna(subset=['Embarked'])
```

## Merging Tables (like SQL JOIN)
```python
orders.merge(customers, on='customer_id', how='left')
```

---

## Mini Project — Titanic EDA
Loaded the Titanic dataset and analyzed survival patterns:

- Survival rate by class, gender, and family size
- Engineered new features: `FamilySize`, `IsAlone`, `Title` (extracted from Name)
- Built a 2x2 dashboard visualizing all key findings

**Key findings:**
- Women had ~74% survival rate vs ~19% for men
- 1st class passengers survived at ~63% vs ~24% for 3rd class
- Family size of 2–4 had the highest survival rate; solo travelers and large families fared worse

---

## Mini Project — Server Log Anomaly Detection
Simulated server logs (timestamp, status code, response time, CPU%) and detected anomalies:

```python
threshold = logs['response_time_ms'].mean() + 3 * logs['response_time_ms'].std()
anomalies = logs[logs['response_time_ms'] > threshold]
```
Visualized anomalies as red dots against a threshold line — same pattern
used in real AIOps monitoring (Phase 5, Week 27).

---

## Errors I Fixed Today
- `OSError: Cannot save file into a non-existent directory` → created missing folders with `mkdir -p`
- `NameError` on `plt`/`titanic`/`logs` → forgot to import matplotlib at the top, and cells must run in order. Fixed using **Run All**.

---

## Key Takeaways
- `.loc` = label-based, `.iloc` = position-based
- Always wrap conditions in `()` when combining with `&` or `|`
- `groupby()` + aggregation is the most-used pattern for data analysis
- `merge()` is pandas' SQL JOIN — critical for combining datasets
- Notebooks execute cells independently — use "Run All" to avoid NameErrors

---

## DevOps → MLOps Connection
The server log anomaly project mirrors real AIOps work — analyzing
response times, status codes, and CPU metrics to flag incidents automatically.
This is a direct preview of Phase 5.

---

## Notebook
[day04_pandas.ipynb](../../notebooks/week-01/day04_pandas.ipynb)

---

## Tomorrow — Day 05
Mini project: download a public CSV dataset, clean missing values,
produce 3 summary statistics with Pandas.