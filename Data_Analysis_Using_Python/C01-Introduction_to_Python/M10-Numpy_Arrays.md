# 🧮 2D NumPy Arrays

## 📌 Introduction to NumPy Dimensions

NumPy arrays are stored as:

```python
numpy.ndarray
```

`ndarray` means **N-dimensional array**.

NumPy supports arrays with different dimensions:

- 1D array → Single row of values
- 2D array → Rows and columns (table-like structure)
- 3D+ arrays → Higher-dimensional data structures

Example:

```python
np_height
```

is a **1D NumPy array**.

A 2D NumPy array contains multiple rows and columns.

---

# 🏗️ Creating a 2D NumPy Array

A 2D NumPy array can be created from a **list of lists**.

Example:

```python
family_data = [
    [1.73, 65.4],
    [1.68, 59.2],
    [1.71, 63.5]
]

np_2d = np.array(family_data)
```

Output:

```text
[
 [1.73 65.4]
 [1.68 59.2]
 [1.71 63.5]
]
```

Each inner list becomes a row in the NumPy array.

---

# 📐 Checking Array Shape

The `.shape` attribute provides information about the dimensions of an array.

Example:

```python
np_2d.shape
```

Output:

```text
(3, 2)
```

Meaning:

- `3` → Number of rows
- `2` → Number of columns

---

# ⚠️ NumPy Arrays Have One Data Type

A NumPy array can only contain one data type.

Example:

```python
np.array([
    [1.73, 65.4],
    [1.68, "59.2"]
])
```

Because one value is a string, NumPy converts all values into strings.

NumPy arrays are **homogeneous**, meaning all elements have the same type.

---

# 🔍 Subsetting 2D NumPy Arrays

A 2D array can be accessed using:

```python
array[row][column]
```

Example:

```python
np_2d[0][2]
```

Process:

1. Select row `0`
2. Select column `2`

---

# ✅ Alternative Subsetting Method

You can also use a comma:

```python
array[row, column]
```

Example:

```python
np_2d[0, 2]
```

This is the preferred NumPy style.

The value before the comma selects the row.

The value after the comma selects the column.

---

# ✂️ Selecting Multiple Rows and Columns

NumPy allows advanced slicing.

Example:

```python
np_2d[1:3, 1:3]
```

Meaning:

- Rows `1` to `2`
- Columns `1` to `2`

Remember:

✅ Start index is included  
❌ End index is excluded

---

# 📊 Selecting Entire Rows or Columns

## Select all columns from one row:

```python
np_2d[1, :]
```

Meaning:

- Select row `1`
- Select all columns

---

## Select all rows from one column:

```python
np_2d[:, 1]
```

Meaning:

- Select all rows
- Select column `1`

---

# ⚡ Calculations with 2D NumPy Arrays

Like 1D arrays, 2D arrays support element-wise calculations.

Example:

```python
np_2d * 2
```

Every value in the array is multiplied by `2`.

NumPy automatically applies calculations across the entire structure.

---

# 💻 Example: Height and Weight Data

```python
import numpy as np

height = [1.73, 1.68, 1.71]
weight = [65.4, 59.2, 63.5]

np_2d = np.array([height, weight])

print(np_2d)

print(np_2d.shape)

# Select first row
print(np_2d[0, :])

# Select second column
print(np_2d[:, 1])
```

---

# 🎯 Key Takeaways

✅ `numpy.ndarray` represents NumPy arrays  
✅ NumPy supports multiple dimensions  
✅ 2D arrays organize data into rows and columns  
✅ Use `.shape` to check array dimensions  
✅ Use `[row, column]` for efficient subsetting  
✅ NumPy arrays must contain a single data type  
✅ 2D arrays support fast element-wise calculations  

🚀 2D NumPy arrays are the foundation for working with tables, matrices, and structured datasets in data science!
