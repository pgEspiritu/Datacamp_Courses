# 🔘 Boolean Operators in Python

## 📌 Combining Boolean Values

After learning how to produce Boolean values using comparison operators, the next step is to **combine Boolean expressions**.

Python provides three common Boolean operators:

| Operator | Purpose |
|---|---|
| `and` | `True` only when **both** conditions are `True` |
| `or` | `True` when **at least one** condition is `True` |
| `not` | **Negates** a Boolean value |

These operators are useful when working with multiple conditions.

---

# 1. `and` Operator

The `and` operator returns `True` **only if both conditions are `True`**.

### Truth Table

| A | B | `A and B` |
|---|---|---|
| `True` | `True` | `True` |
| `False` | `True` | `False` |
| `True` | `False` | `False` |
| `False` | `False` | `False` |

### Examples

    True and True

Result:

    True

    False and True

Result:

    False

---

## 🧮 Using `and` with Comparisons

Suppose:

    x = 12

We want to check whether `x` is **greater than 5 and less than 15**.

    x > 5 and x < 15

The two comparisons are:

    x > 5
    x < 15

Both are `True` because `x` is `12`.

Therefore:

    True and True

Result:

    True

This makes sense because `12` lies between `5` and `15`.

---

# 2. `or` Operator

The `or` operator returns `True` when **at least one condition is `True`**.

### Truth Table

| A | B | `A or B` |
|---|---|---|
| `True` | `True` | `True` |
| `False` | `True` | `True` |
| `True` | `False` | `True` |
| `False` | `False` | `False` |

### Examples

    True or True

Result:

    True

    False or True

Result:

    True

    True or False

Result:

    True

    False or False

Result:

    False

---

## 🧮 Using `or` with Comparisons

Suppose:

    y = 5

We want to check whether `y` is **less than 7 or greater than 13**.

    y < 7 or y > 13

The comparisons produce:

    y < 7
    True

    y > 13
    False

Therefore:

    True or False

Result:

    True

Only one of the conditions needs to be `True`.

---

# 3. `not` Operator

The `not` operator **negates** a Boolean value.

It changes:

- `True` → `False`
- `False` → `True`

### Examples

    not True

Result:

    False

    not False

Result:

    True

The `not` operator is especially useful when you want to **reverse the result of a Boolean expression**.

### Example

    x = 12

    not (x > 20)

Since:

    x > 20

is:

    False

Applying `not` gives:

    not False

which results in:

    True

---

# 🔢 Boolean Operators with NumPy

When working with **NumPy arrays**, regular Python `and`, `or`, and `not` should not be used to combine Boolean arrays.

For example, suppose we have:

    import numpy as np

    bmi = np.array([20.5, 21.3, 21.8, 22.4, 24.1])

We want to find the BMI values that are:

- greater than `21`
- and less than `22`

We could produce two Boolean arrays:

    bmi > 21

and:

    bmi < 22

However, trying to combine them using Python's `and` operator causes an error:

    (bmi > 21) and (bmi < 22)

### ⚠️ Why?

NumPy arrays contain multiple Boolean values. Python's `and` operator expects individual Boolean values, so it cannot determine the single truth value of the entire array.

This results in an error similar to:

    The truth value of an array with more than one element is ambiguous.

---

# 🧠 NumPy Boolean Functions

NumPy provides special functions designed to work with Boolean arrays:

| Python Operator | NumPy Function |
|---|---|
| `and` | `np.logical_and()` |
| `or` | `np.logical_or()` |
| `not` | `np.logical_not()` |

These functions operate **element-wise** on NumPy arrays.

---

## ✅ `np.logical_and()`

To find BMI values between `21` and `22`:

    np.logical_and(bmi > 21, bmi < 22)

The comparison is performed element by element.

For example:

    bmi > 21

might produce:

    [False  True  True  True  True]

while:

    bmi < 22

might produce:

    [ True  True  True False False]

Combining them with:

    np.logical_and(bmi > 21, bmi < 22)

produces a Boolean array containing `True` only where **both conditions are satisfied**.

---

## 🔍 Selecting Values with Boolean Arrays

The resulting Boolean array can be used to select only the matching values from the NumPy array.

    bmi[np.logical_and(bmi > 21, bmi < 22)]

This returns only the BMI values that are:

    > 21
    < 22

This technique is called **Boolean indexing** or **Boolean filtering**.

---

# 🔁 NumPy Boolean Operations

### Logical AND

    np.logical_and(condition1, condition2)

Returns `True` when both conditions are `True`.

### Logical OR

    np.logical_or(condition1, condition2)

Returns `True` when at least one condition is `True`.

### Logical NOT

    np.logical_not(condition)

Reverses each Boolean value.

---

# 🆚 Python vs NumPy Boolean Operators

| Purpose | Python | NumPy |
|---|---|---|
| AND | `and` | `np.logical_and()` |
| OR | `or` | `np.logical_or()` |
| NOT | `not` | `np.logical_not()` |

### Example

For individual Boolean values:

    True and False

For NumPy arrays:

    np.logical_and(array1, array2)

---

# 💡 Important Concept: Element-Wise Operations

NumPy's logical functions work **element by element**.

For example:

    np.logical_and(
        np.array([True, False, True]),
        np.array([True, True, False])
    )

Result:

    [ True False False]

Each corresponding pair is evaluated independently:

| First | Second | Result |
|---|---|---|
| `True` | `True` | `True` |
| `False` | `True` | `False` |
| `True` | `False` | `False` |

---

# 🔑 Key Takeaways

- `and` requires **both** conditions to be `True`.
- `or` requires **at least one** condition to be `True`.
- `not` reverses a Boolean value.
- Python's `and`, `or`, and `not` work with individual Boolean values.
- Do **not** use Python's `and`, `or`, or `not` to combine NumPy Boolean arrays.
- For NumPy arrays, use:
  - `np.logical_and()`
  - `np.logical_or()`
  - `np.logical_not()`
- NumPy logical operations are performed **element-wise**.
- Boolean arrays can be used inside square brackets `[]` to **filter/select values**.

### 📚 Common Pattern

    bmi[np.logical_and(bmi > 21, bmi < 22)]

This means:

> Select the values in `bmi` where the values are greater than `21` **and** less than `22`.
