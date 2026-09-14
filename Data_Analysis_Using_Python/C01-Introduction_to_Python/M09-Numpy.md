# 🔢 NumPy Basics for Data Science

## 📌 Why Use NumPy?

Python lists are powerful because they can:
- Store multiple values
- Store different data types
- Add, remove, and modify elements

However, lists have limitations when working with large datasets.

❌ Python lists cannot efficiently perform calculations on all elements at once.

Example:

```python
height = [1.73, 1.68, 1.71]
weight = [65.4, 59.2, 63.5]

# This will not work as expected
bmi = weight / height ** 2
```

For data science, we need a faster and more efficient way to perform calculations.

---

# 🚀 What is NumPy?

**NumPy (Numerical Python)** is a Python package designed for numerical computing.

It provides:

✅ Powerful array objects  
✅ Fast mathematical operations  
✅ Element-wise calculations  
✅ Tools for scientific computing and data analysis  

NumPy introduces the **NumPy array**, which is similar to Python lists but optimized for numerical operations.

---

# 📦 Importing NumPy

Before using NumPy, import the package:

```python
import numpy as np
```

The `np` alias is commonly used as a shortcut for NumPy.

---

# 🧮 Creating NumPy Arrays

NumPy arrays can be created from Python lists using `np.array()`.

Example:

```python
height = [1.73, 1.68, 1.71]
weight = [65.4, 59.2, 63.5]

np_height = np.array(height)
np_weight = np.array(weight)
```

Now the lists are converted into NumPy arrays.

---

# ⚡ Element-wise Calculations

One of NumPy's biggest advantages is performing operations on entire arrays.

Example:

```python
bmi = np_weight / np_height ** 2
```

NumPy automatically performs the calculation for each element:

```
BMI = weight[0] / height[0]²
BMI = weight[1] / height[1]²
BMI = weight[2] / height[2]²
```

No loops are required. 🚀

---

# 🔍 Python List vs NumPy Array

## Python List

```python
list_a = [1, 2, 3]
list_b = [4, 5, 6]

list_a + list_b
```

Output:

```python
[1, 2, 3, 4, 5, 6]
```

Lists combine values together.

---

## NumPy Array

```python
array_a = np.array([1, 2, 3])
array_b = np.array([4, 5, 6])

array_a + array_b
```

Output:

```python
array([5, 7, 9])
```

NumPy performs element-wise calculations.

---

# ⚠️ Important NumPy Rules

## 1. NumPy Arrays Usually Have One Data Type

Unlike Python lists, NumPy arrays usually contain values of the same type.

Example:

```python
np.array([1, True, "hello"])
```

NumPy converts everything into a common type:

```python
array(['1', 'True', 'hello'])
```

---

## 2. NumPy Arrays Are Python Objects

NumPy arrays have their own:

- Data type
- Methods
- Behaviors

They work differently from normal Python lists.

---

# 🎯 NumPy Subsetting

NumPy arrays can be accessed like Python lists.

Example:

```python
bmi[1]
```

Returns the second BMI value.

Remember:

| Index | Value |
|---|---|
| 0 | First element |
| 1 | Second element |
| -1 | Last element |

---

# ✅ Boolean Filtering

NumPy allows filtering using conditions.

Example:

```python
bmi > 23
```

Output:

```python
array([False, True, False])
```

This creates a Boolean array.

You can use it to select specific values:

```python
bmi[bmi > 23]
```

Only BMI values greater than 23 will be returned.

---

# 💡 Key Takeaways

✅ NumPy is essential for data science  
✅ NumPy arrays are faster than Python lists for numerical operations  
✅ Arrays allow element-wise calculations  
✅ NumPy supports powerful filtering techniques  
✅ Always consider data types when working with NumPy arrays  

🚀 NumPy is one of the fundamental tools for Python data analysis and machine learning.
