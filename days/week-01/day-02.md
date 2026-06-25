# Day 02 — NumPy Basics

**Phase:** 0 — Foundations | **Week:** 1  
**Roadmap Topic:** Arrays, shapes, broadcasting, vectorized operations vs Python loops + 10 problems

---

## What is NumPy?
NumPy is a supercharged Python list built for math and data.
Normal Python lists are slow — NumPy arrays are 10–50x faster
because it processes the whole array at once instead of one by one.

**Mental model:**
- Python loop = counting 1 million coins one by one
- NumPy = machine counting all coins simultaneously

---

## Core Concepts

### 1. Arrays & Shapes
```python
import numpy as np

arr1 = np.array([1, 2, 3, 4, 5])          # 1D array
arr2 = np.array([[1, 2, 3], [4, 5, 6]])   # 2D array (matrix)

print(arr1.shape)   # (5,)    → 5 elements
print(arr2.shape)   # (2, 3)  → 2 rows, 3 cols
print(arr2.ndim)    # 2       → 2 dimensions
print(arr2.size)    # 6       → total elements
print(arr1.dtype)   # int64   → type of numbers
```

---

### 2. Vectorized Operations vs Python Loop
```python
import time

big = np.arange(1000000)

# Slow — Python loop (one by one)
start = time.time()
result = [x * 2 for x in big]
print("Loop time:", round(time.time() - start, 4), "sec")

# Fast — NumPy (all at once)
start = time.time()
result = big * 2
print("NumPy time:", round(time.time() - start, 4), "sec")
```
Key insight: the bigger the data, the bigger the speed gap.
This is exactly why all ML libraries are built on NumPy.

---

### 3. Broadcasting
NumPy automatically applies an operation to every element
without needing a loop.
```python
arr = np.array([1, 2, 3, 4, 5])
print(arr + 10)    # [11 12 13 14 15]
print(arr * 3)     # [3  6  9 12 15]
print(arr ** 2)    # [1  4  9 16 25]
```

Broadcasting with matrix:
```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])
print(matrix + 10)        # adds 10 to every element
print(matrix * 2)         # multiplies every element by 2
print(matrix + np.array([10, 20, 30]))  # adds per column
```

---

## 10 Practice Problems

```python
# 1. Array 1 to 10
np.arange(1, 11)

# 2. 3x3 zeros matrix
np.zeros((3, 3))

# 3. 3x3 identity matrix
np.eye(3)

# 4. Mean, max, min
arr = np.array([4, 7, 2, 9, 1, 5, 8, 3, 6])
arr.mean(), arr.max(), arr.min()

# 5. Reshape 1D to 3x4
np.arange(1, 13).reshape(3, 4)

# 6. Multiply two arrays
np.array([1,2,3,4]) * np.array([10,20,30,40])

# 7. Filter elements > 5
arr[arr > 5]

# 8. Sort array
np.sort(arr)

# 9. Stack two arrays vertically
np.vstack([np.array([1,2,3]), np.array([4,5,6])])

# 10. 5 random numbers
np.random.rand(5)
```

---

## Advanced — Math on arrays
```python
arr = np.array([1, 2, 3, 4, 5])
np.sqrt(arr)    # square root of each
np.log(arr)     # log of each
arr * arr       # element-wise multiply
```

---

## Key Takeaways
- NumPy arrays are faster than Python lists for math operations
- `.shape` tells you the dimensions of an array
- Broadcasting applies operations to every element automatically
- No loops needed — NumPy handles it internally
- This is the foundation of Pandas, sklearn, PyTorch — everything in ML

---

## DevOps → MLOps Connection
In DevOps we process config files and logs line by line.
In ML, NumPy processes millions of data points at once.
Same data — different scale and tooling.

---

## Notebook
[day02_numpy.ipynb](../../notebooks/week-01/day02_numpy.ipynb)

---

## Tomorrow — Day 03
Pandas basics: Series, DataFrame, reading CSV/JSON, indexing, filtering.
File: `notebooks/week-01/day03_pandas.ipynb`