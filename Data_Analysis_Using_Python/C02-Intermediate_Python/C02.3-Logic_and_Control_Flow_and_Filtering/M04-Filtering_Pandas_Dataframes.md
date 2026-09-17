# 🔎 Filtering Pandas DataFrames

## 📌 Overview

In previous lessons, NumPy arrays were used for:

- Comparison operations
- Boolean operations
- Element-wise filtering

These same concepts can be applied to **Pandas DataFrames**.

Filtering allows you to keep only the rows that satisfy a specific condition.

---

# 🌍 BRICS Dataset

Suppose the `brics` DataFrame contains information about countries, including their area.

The goal is to keep only the countries whose area is **greater than 8 million square kilometers**.

There are **three main steps**:

1. Select the `area` column.
2. Compare the values in the column and create a Boolean Series.
3. Use that Boolean Series to filter the DataFrame.

---

# 1️⃣ Step 1: Select a Column

First, select the `area` column from the `brics` DataFrame.

Using square brackets:

    brics["area"]

This returns a **Pandas Series**.

You can also use `loc`:

    brics.loc[:, "area"]

or `iloc`:

    brics.iloc[:, 1]

> 💡 The important point is to select the **Series containing the area values**, rather than a DataFrame.

---

# 2️⃣ Step 2: Compare the Values

Next, compare the `area` column with `8`.

    brics["area"] > 8

This produces a **Boolean Series**.

For example:

    [True, True, False, ...]

Each value corresponds to one row in the DataFrame.

- `True` → area is greater than `8`
- `False` → area is not greater than `8`

We can store this Boolean Series in a variable:

    is_huge = brics["area"] > 8

Now `is_huge` contains the filtering condition.

---

# 3️⃣ Step 3: Filter the DataFrame

Use the Boolean Series inside square brackets:

    brics[is_huge]

Pandas keeps only the rows where `is_huge` is `True`.

For the BRICS example, this returns countries with an area greater than 8 million square kilometers:

- Brazil
- Russia
- China

---

# 🧠 Boolean Indexing

The general pattern is:

    condition = brics["column"] > value

    brics[condition]

The Boolean Series acts as a **filter** for the DataFrame.

### Example

    is_huge = brics["area"] > 8
    brics[is_huge]

This means:

> Keep only the rows where the `area` value is greater than `8`.

---

# ⚡ One-Liner Filtering

The filtering process can also be written in a single line.

Instead of:

    is_huge = brics["area"] > 8
    brics[is_huge]

You can write:

    brics[brics["area"] > 8]

The expression inside the square brackets creates the Boolean Series directly.

---

# 🔘 Filtering with Boolean Operators

Pandas is built on **NumPy**, so NumPy's logical functions can also be used with Pandas.

For example:

    np.logical_and()

can combine two conditions.

Suppose we only want countries with an area:

- greater than `8` million square kilometers
- less than `10` million square kilometers

First import NumPy:

    import numpy as np

Then create the Boolean condition:

    np.logical_and(brics["area"] > 8, brics["area"] < 10)

This produces a Boolean Series.

Use it directly to filter the DataFrame:

    brics[np.logical_and(brics["area"] > 8, brics["area"] < 10)]

---

# 🌎 Example: Area Between 8 and 10

The complete code is:

    import numpy as np

    brics[np.logical_and(brics["area"] > 8, brics["area"] < 10)]

The result contains:

- Brazil
- China

Russia is excluded because its area is approximately **17 million square kilometers**, which is greater than `10`.

---

# 🔍 Filtering Workflow

A useful way to remember DataFrame filtering is:

    DataFrame
        ↓
    Select column
        ↓
    Compare values
        ↓
    Create Boolean Series
        ↓
    Use Boolean Series to filter rows

### Example

    brics["area"]

↓

    brics["area"] > 8

↓

    is_huge = brics["area"] > 8

↓

    brics[is_huge]

---

# 📊 One Condition vs Multiple Conditions

## One Condition

    brics[brics["area"] > 8]

Keeps rows where `area > 8`.

## Multiple Conditions

    brics[np.logical_and(brics["area"] > 8, brics["area"] < 10)]

Keeps rows where:

    area > 8
    AND
    area < 10

---

# 🧠 Boolean Series

A Boolean Series is a Pandas Series containing `True` and `False` values.

Example:

    is_huge = brics["area"] > 8

Conceptually:

| Country | Area | `is_huge` |
|---|---:|---|
| Brazil | > 8 | `True` |
| Russia | > 8 | `True` |
| China | > 8 | `True` |
| Other country | < 8 | `False` |

Pandas uses these Boolean values to determine which rows should remain in the filtered DataFrame.

---

# 🔑 Key Takeaways

- Pandas DataFrames can be filtered using **Boolean conditions**.
- The basic process has three steps:
  1. Select a column.
  2. Compare the column values.
  3. Use the Boolean result to filter the DataFrame.
- A comparison such as:

      brics["area"] > 8

  produces a Boolean Series.
- Use the Boolean Series inside `[]`:

      brics[brics["area"] > 8]

- You can store the condition in a variable:

      is_huge = brics["area"] > 8
      brics[is_huge]

- NumPy logical functions can combine conditions:

      np.logical_and()
      np.logical_or()
      np.logical_not()

- DataFrame filtering is a powerful way to extract only the observations that meet specific criteria.

### 📚 Common Patterns

    brics[brics["area"] > 8]

    is_huge = brics["area"] > 8
    brics[is_huge]

    brics[np.logical_and(brics["area"] > 8, brics["area"] < 10)]

> 💡 **Core idea:** Create a Boolean condition, then use it to select the rows you want from the DataFrame.
