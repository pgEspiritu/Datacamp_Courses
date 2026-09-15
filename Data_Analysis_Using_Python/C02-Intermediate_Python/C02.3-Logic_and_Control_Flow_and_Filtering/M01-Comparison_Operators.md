# ⚖️ Comparison Operators - Python

## 🎯 Introduction

Comparison operators are used to determine how two Python values relate to each other.

The result of a comparison is always a **Boolean** value:

    True
    False

Comparison operators are especially useful when:

- 🔍 Checking conditions
- 📊 Filtering data
- 🧮 Comparing numerical values
- 🐍 Controlling program logic

---

# 🔢 Numeric Comparisons

Comparison operators can be used with numbers.

## Less Than `<`

Example:

    2 < 3

Result:

    True

Because `2` is smaller than `3`.

---

## Equal To `==`

To check whether two values are equal, use **two equals signs**:

    2 == 3

Result:

    False

⚠️ Remember:

- `=` → Assignment
- `==` → Comparison for equality

---

## Less Than or Equal To `<=`

Example:

    2 <= 3

Result:

    True

Also:

    3 <= 3

Result:

    True

Because `3` is equal to `3`.

---

# 📊 Comparison Operators

Python provides several comparison operators:

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `<` | Less than | `2 < 3` | `True` |
| `>` | Greater than | `3 > 2` | `True` |
| `<=` | Less than or equal | `2 <= 3` | `True` |
| `>=` | Greater than or equal | `3 >= 3` | `True` |
| `==` | Equal to | `2 == 3` | `False` |
| `!=` | Not equal to | `2 != 3` | `True` |

The `!=` operator means **not equal to**.

---

# 🔤 Comparing Strings

Comparison operators also work with strings.

Python compares strings based on their ordering.

Example:

    "carl" < "chris"

Result:

    True

Because `"carl"` comes before `"chris"` alphabetically.

Another example:

    "apple" < "banana"

Result:

    True

---

# ⚠️ Comparing Different Data Types

In general, Python cannot compare unrelated types.

Example:

    3 < "chris"

This produces an error because Python does not know how to meaningfully compare an integer with a string.

### ✅ Numeric Types Are an Exception

Python can compare different numeric types.

For example:

    3 < 4.5

Result:

    True

An `int` and a `float` can be compared because they are both numeric types.

---

# 🧠 Best Practice

When performing comparisons, make sure the values are compatible and generally belong to the same type.

Examples:

✅ Number vs Number

    10 > 5

✅ String vs String

    "apple" < "banana"

❌ String vs Number

    "apple" < 5

---

# 🔢 NumPy Comparisons

NumPy makes comparisons especially powerful.

Suppose:

    bmi = np.array([21.5, 24.3, 22.1, 26.0])

You can compare the entire array with a single value:

    bmi > 23

NumPy performs the comparison **element-by-element**.

Result:

    [False, True, False, True]

---

# 🔍 Understanding NumPy Boolean Results

For:

    bmi > 23

NumPy effectively checks:

    21.5 > 23  → False
    24.3 > 23  → True
    22.1 > 23  → False
    26.0 > 23  → True

The result is a Boolean NumPy array:

    [False, True, False, True]

---

# 📊 Boolean Filtering with NumPy

The Boolean result can be used to select matching values.

Example:

    bmi[bmi > 23]

Result:

    [24.3, 26.0]

Only the values for which the comparison returned `True` are selected.

This is one of the most useful techniques in NumPy for filtering data.

---

# ⚡ Why NumPy Comparisons Are Powerful

Without NumPy, you might need to manually compare every value.

With NumPy:

    bmi > 23

performs the comparison across the entire array automatically.

This makes the code:

- 🚀 Fast
- ✨ Concise
- 📊 Useful for data analysis
- 🔍 Excellent for filtering datasets

---

# 🧮 Common Comparison Examples

## Greater Than

    10 > 5

Result:

    True

## Less Than

    5 < 10

Result:

    True

## Greater Than or Equal

    10 >= 10

Result:

    True

## Less Than or Equal

    5 <= 10

Result:

    True

## Equal

    10 == 10

Result:

    True

## Not Equal

    10 != 5

Result:

    True

---

# ⚠️ `=` vs `==`

This distinction is very important.

## Assignment

    x = 10

This assigns the value `10` to `x`.

## Comparison

    x == 10

This checks whether `x` is equal to `10`.

Result:

    True

---

# 🧠 Key Takeaways

- ⚖️ Comparison operators determine how two values relate.
- ✅ Comparisons return Boolean values: `True` or `False`.
- 🔢 Numbers can be compared using `<`, `>`, `<=`, `>=`, `==`, and `!=`.
- 🔤 Strings can also be compared.
- ⚠️ Comparing incompatible types can result in an error.
- 🔢 Different numeric types such as integers and floats can be compared.
- 📊 NumPy allows comparisons to be performed element-by-element across arrays.
- 🔍 Boolean arrays can be used to filter NumPy data.
- 🚀 Comparison operators are fundamental tools for data analysis and programming.
