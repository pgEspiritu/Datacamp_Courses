# ⚖️ Equality in Python

## 📌 Equality and Inequality

To check if two Python values or variables are **equal**, use the equality operator:

    ==

To check if two values are **not equal**, use the inequality operator:

    !=

Both operators return a **Boolean value**: `True` or `False`.

### ✅ Examples

    2 == (1 + 1)
    "intermediate" != "python"
    True != False
    "Python" != "python"

All of these comparisons result in `True`.

> 💡 **Important:** `==` checks whether two values are equal. It does **not** assign a value to a variable. Assignment uses `=`.

---

## 🧠 Equality Examples

| Comparison | Result | Explanation |
|---|---|---|
| `2 == (1 + 1)` | `True` | Both sides are `2` |
| `"intermediate" != "python"` | `True` | The strings are different |
| `True != False` | `True` | The Boolean values are different |
| `"Python" != "python"` | `True` | Python strings are case-sensitive |

---

## 🖨️ Using `print()`

When comparisons are written inside a Python script, use `print()` to display the result.

    print(2 == (1 + 1))
    print("intermediate" != "python")
    print(True != False)
    print("Python" != "python")

### Output

    True
    True
    True
    True

---

# 🧪 Exercise: Comparison of Values

### 🎯 Instructions

Write Python code to:

1. Check if `True` equals `False`.
2. Check if `-5 * 15` is **not equal** to `75`.
3. Check if the strings `"pyscript"` and `"PyScript"` are equal.
4. Check whether `True` and `1` are equal.

---

## ✅ Solution

### 1. Compare Booleans

    True == False

### Result

    False

`True` and `False` are different Boolean values.

---

### 2. Compare Integers

    (-5 * 15) != 75

First calculate:

    -5 * 15 = -75

Then compare `-75` with `75`.

### Result

    True

Because `-75` is not equal to `75`.

---

### 3. Compare Strings

    "pyscript" == "PyScript"

### Result

    False

Python strings are **case-sensitive**, so:

    "pyscript"

is different from:

    "PyScript"

The uppercase `P` makes the strings different.

---

### 4. Compare a Boolean with an Integer

    True == 1

### Result

    True

In Python, `True` is treated as equivalent to `1` when compared numerically, while `False` is equivalent to `0`.

    True == 1
    False == 0

Both comparisons return `True`.

---

# 🔑 Key Takeaways

- `==` checks whether two values are **equal**.
- `!=` checks whether two values are **different**.
- Comparison results are Boolean values: `True` or `False`.
- Python strings are **case-sensitive**.
- `True == 1` evaluates to `True`.
- `False == 0` also evaluates to `True`.
- Use `print()` when you want to display a comparison result in a script.
- Do not confuse `=` with `==`:
  - `=` → assignment
  - `==` → equality comparison
