# 🐼 Looping Over Pandas DataFrames — Part 2

## 📌 Overview

Pandas DataFrames are another important data structure that can be used with loops.

However, a Pandas DataFrame does **not** behave exactly like a 2D NumPy array when you use a basic `for` loop.

To iterate over the **rows** of a DataFrame, Pandas provides the:

    .iterrows()

method.

For many DataFrame transformations, however, using:

    .apply()

is a better and more efficient approach than looping row by row.

---

# 🌍 The `brics` DataFrame

The examples use the `brics` dataset loaded from a CSV file:

    import pandas as pd

    brics = pd.read_csv("brics.csv", index_col=0)

---

# 1️⃣ Basic `for` Loop on a DataFrame

You might expect this:

    for row in brics:
        print(row)

to print each row of the DataFrame.

However, that is **not** what happens.

A basic `for` loop over a Pandas DataFrame iterates over its **column names**.

Conceptually:

    for column in brics:
        print(column)

prints the column labels.

### 💡 Important

A Pandas DataFrame is not automatically iterated row by row with:

    for x in dataframe:

To iterate over rows, you need to explicitly request row iteration.

---

# 2️⃣ Using `.iterrows()`

To iterate over the rows of a DataFrame, use:

    brics.iterrows()

The general pattern is:

    for lab, row in brics.iterrows():
        print(lab)
        print(row)

On each iteration, `.iterrows()` produces:

1. The **row label**
2. The **row data as a Pandas Series**

---

# 🧠 Understanding `iterrows()`

The typical structure is:

    for lab, row in brics.iterrows():
        ...

Here:

- `lab` → row label/index
- `row` → current row as a Pandas Series

For example, during one iteration:

    lab

might contain a row label such as:

    BR

while:

    row

contains the entire row as a Pandas Series.

---

# 🔍 The Row is a Pandas Series

Because `row` is a Series, you can use the same subsetting techniques you've learned before.

For example:

    for lab, row in brics.iterrows():
        print(row["capital"])

This selects the `capital` value from the current row.

You can also print the row label together with the selected value:

    for lab, row in brics.iterrows():
        print(lab, row["capital"])

---

# 📊 What `iterrows()` Produces

Conceptually, a DataFrame such as:

    brics

can be processed row by row:

    row label + row Series

For example:

    lab = "BR"

    row = Series containing the country's data

Then:

    row["capital"]

retrieves the capital for that specific row.

---

# 3️⃣ Adding a New Column with `iterrows()`

You can use `.iterrows()` to create a new column.

Suppose you want to add a column called:

    name_length

containing the number of characters in each country's name.

The steps are:

1. Loop through each row.
2. Get the country name from the row.
3. Use `len()` to determine its length.
4. Store the result in the appropriate row of the new column.

### Example

    for lab, row in brics.iterrows():
        brics.loc[lab, "name_length"] = len(row["country"])

After the loop, the DataFrame contains a new column:

    name_length

---

# 🧠 Breaking Down the Code

### Step 1: Iterate Through Rows

    for lab, row in brics.iterrows():

`lab` contains the row label and `row` contains the current row as a Series.

### Step 2: Select the Country Name

    row["country"]

This retrieves the country name from the current row.

### Step 3: Count Characters

    len(row["country"])

The `len()` function returns the number of characters in the country name.

### Step 4: Store the Result

    brics.loc[lab, "name_length"] = len(row["country"])

`.loc[]` is label-based, so:

    lab

identifies the correct row.

---

# 📌 Why `.loc[]`?

The expression:

    brics.loc[lab, "name_length"]

means:

> Select the row labeled `lab` and the column `name_length`.

Because the column may not exist yet, Pandas can create it while assigning values.

---

# ⚠️ Efficiency Issue with `iterrows()`

Although `.iterrows()` works, it is **not especially efficient** for this kind of operation.

Why?

On every iteration:

    row

is created as a Pandas Series.

For a small DataFrame, this may not matter.

For a very large DataFrame, repeatedly creating Series objects can become inefficient.

### Basic idea

    for lab, row in brics.iterrows():
        ...

works, but may be unnecessarily slow when a vectorized operation is available.

---

# 4️⃣ Using `.apply()`

A better approach for applying a function element by element to an entire column is:

    .apply()

For example, instead of using `iterrows()` to calculate the length of every country name, you can write:

    brics["name_length"] = brics["country"].apply(len)

This performs the operation directly on the entire `country` column.

---

# 🧠 How `.apply()` Works

The expression:

    brics["country"]

selects the `country` column as a Pandas Series.

Then:

    .apply(len)

applies the `len()` function to each country name.

The result is a new Series containing the lengths.

Finally:

    brics["name_length"] = brics["country"].apply(len)

stores that Series as a new DataFrame column.

---

# 🔄 `iterrows()` vs `.apply()`

## Using `iterrows()`

    for lab, row in brics.iterrows():
        brics.loc[lab, "name_length"] = len(row["country"])

### Characteristics

- Explicit row-by-row loop
- Easy to understand when learning row iteration
- Creates a Series for each row
- Can be inefficient for large datasets

---

## Using `.apply()`

    brics["name_length"] = brics["country"].apply(len)

### Characteristics

- No explicit `for` loop
- Applies a function element-wise to a column
- More concise
- Generally more efficient for this type of operation
- Easier to read for column transformations

---

# ⚡ Vectorized Operations

The `.apply()` approach is part of a broader idea: **perform operations on entire Series or columns instead of manually looping through every row**.

Instead of thinking:

    for each row:
        calculate something

you can often think:

    apply this function to the whole column

This is one of the strengths of Pandas.

---

# 🆚 DataFrame Looping Options

| Approach | What It Does |
|---|---|
| `for x in df` | Iterates over column names |
| `df.iterrows()` | Iterates over rows as `(index, Series)` |
| `df["column"].apply(function)` | Applies a function to each element of a Series |

---

# 📚 Common Patterns

## Iterate Over Columns

    for column in brics:
        print(column)

---

## Iterate Over Rows

    for lab, row in brics.iterrows():
        print(lab, row)

---

## Select a Value from Each Row

    for lab, row in brics.iterrows():
        print(row["capital"])

---

## Create a Column with `iterrows()`

    for lab, row in brics.iterrows():
        brics.loc[lab, "name_length"] = len(row["country"])

---

## Create a Column with `.apply()`

    brics["name_length"] = brics["country"].apply(len)

---

# 🧠 Important Concept: `.iterrows()`

Remember that:

    for lab, row in brics.iterrows():

produces two things on every iteration:

    lab
    row

where:

- `lab` = row label
- `row` = row as a Pandas Series

This makes it possible to access individual values using:

    row["column_name"]

---

# 💡 Why Prefer `.apply()` Here?

When the goal is to transform an entire column using a function, `.apply()` is usually more appropriate than manually looping through rows.

For example:

    brics["name_length"] = brics["country"].apply(len)

is simpler and more efficient than:

    for lab, row in brics.iterrows():
        brics.loc[lab, "name_length"] = len(row["country"])

---

# 🔑 Key Takeaways

- A basic `for` loop over a DataFrame iterates over **column names**, not rows.
- Use `.iterrows()` when you explicitly need to iterate through DataFrame rows.
- `.iterrows()` provides:
  - row label
  - row data as a Pandas Series
- Because each `row` is a Series, you can select values with:

      row["column_name"]

- `.loc[]` can be used to assign values to a specific row and column:

      brics.loc[lab, "name_length"] = ...

- Row-by-row iteration can be inefficient for large DataFrames.
- `.apply()` is a more efficient and concise choice when applying a function element-wise to an entire column.

### 📚 Core Patterns

**Iterate over DataFrame rows:**

    for lab, row in dataframe.iterrows():
        print(lab, row)

**Select a value from each row:**

    for lab, row in dataframe.iterrows():
        print(row["column"])

**Apply a function to a column:**

    dataframe["new_column"] = dataframe["column"].apply(function)

### ⭐ Remember

> **`iterrows()` → row-by-row iteration**
>
> **`.apply()` → apply a function to a Series/column**
>
> For column transformations, `.apply()` is often the cleaner and more efficient approach.
