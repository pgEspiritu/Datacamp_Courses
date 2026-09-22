# 🎬 Netflix 1990s Exploratory Data Analysis

## Objective

Analyze `netflix_data.csv` to answer two questions about **movies released in the 1990s**:

1. What was the most frequent movie duration?
2. How many **short action movies** were released?

### Definitions

* **1990s** → `1990 <= release_year < 2000`
* **Movie** → `type == "Movie"`
* **Short movie** → `duration < 90` minutes
* **Action movie** → `genre == "Action"`

---

# ✅ Correct Python Solution

```
# Importing pandas and matplotlib
import pandas as pd
import matplotlib.pyplot as plt

# Read in the Netflix CSV as a DataFrame
netflix_df = pd.read_csv("netflix_data.csv")

# Filter for movies released in the 1990s
movies_1990s = netflix_df[
    (netflix_df["release_year"] >= 1990)
    & (netflix_df["release_year"] < 2000)
    & (netflix_df["type"] == "Movie")
]

# Find the most frequent movie duration
duration = int(movies_1990s["duration"].mode()[0])

# Count short action movies (< 90 minutes)
short_movie_count = (
    (movies_1990s["duration"] < 90)
    & (movies_1990s["genre"] == "Action")
).sum()

print("Most frequent movie duration:", duration)
print("Number of short action movies:", short_movie_count)
```

---

# 📊 Results

```
Most frequent movie duration: 94
Number of short action movies: 7
```

Therefore:

```
duration = 94
```

and:

```
short_movie_count = 7
```

---

# 🔍 Explanation

## 1. Filter the 1990s Movies

```
movies_1990s = netflix_df[
    (netflix_df["release_year"] >= 1990)
    & (netflix_df["release_year"] < 2000)
    & (netflix_df["type"] == "Movie")
]
```

The three conditions are:

| Condition              | Meaning                   |
| ---------------------- | ------------------------- |
| `release_year >= 1990` | Released in 1990 or later |
| `release_year < 2000`  | Released before 2000      |
| `type == "Movie"`      | Keep movies only          |

Together, they select movies released from **1990 through 1999**.

---

# 2. Find the Most Frequent Duration

```
duration = int(movies_1990s["duration"].mode()[0])
```

### `mode()`

The `.mode()` method returns the most frequently occurring value.

For example:

```
movies_1990s["duration"].mode()
```

returns a Series containing the most common duration.

Using:

```
[0]
```

selects the first mode.

Finally:

```
int(...)
```

converts the result to an integer.

Result:

```
94
```

---

# 3. Find Short Action Movies

The first condition:

```
movies_1990s["duration"] < 90
```

identifies movies shorter than 90 minutes.

The second:

```
movies_1990s["genre"] == "Action"
```

identifies action movies.

Combine them using Pandas' element-wise `&` operator:

```
(
    (movies_1990s["duration"] < 90)
    & (movies_1990s["genre"] == "Action")
)
```

This creates a Boolean Series.

---

# 4. Count the Matching Rows

The final:

```
.sum()
```

counts the `True` values.

Since:

```
True = 1
False = 0
```

the sum represents the number of short action movies.

Result:

```
7
```

---

# ⚠️ Important Python Syntax

Your original solution used:

```
&&
```

Python does **not** use `&&` for logical AND.

Use:

```
&
```

for element-wise Boolean comparisons in Pandas.

### ❌ Incorrect

```
(condition1) && (condition2)
```

### ✅ Correct

```
(condition1) & (condition2)
```

Also remember to put each comparison in parentheses:

```
(df["year"] >= 1990) & (df["year"] < 2000)
```

---

# 🧠 Alternative Way to Count

The same result can be obtained by filtering first:

```
short_action_movies = movies_1990s[
    (movies_1990s["duration"] < 90)
    & (movies_1990s["genre"] == "Action")
]

short_movie_count = len(short_action_movies)
```

This gives:

```
7
```

The `.sum()` approach is more compact:

```
short_movie_count = (
    (movies_1990s["duration"] < 90)
    & (movies_1990s["genre"] == "Action")
).sum()
```

---

# 🎯 Final Answers

| Variable            |       Answer |
| ------------------- | -----------: |
| `duration`          | `94` minutes |
| `short_movie_count` |          `7` |

### Core Pandas Pattern

```
filtered_df = df[
    (df["column1"] >= value1)
    & (df["column2"] == value2)
]
```

### Core Counting Pattern

```
count = condition.sum()
```
