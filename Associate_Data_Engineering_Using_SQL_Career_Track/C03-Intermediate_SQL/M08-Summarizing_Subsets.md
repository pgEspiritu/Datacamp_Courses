# Summarizing Subsets with SQL 📊

## Overview 📚

We can combine **filtering** with **aggregate functions** to summarize only a specific subset of data.

The `WHERE` clause filters the records **before** the aggregate function is calculated.

### Key Concept

**FROM → WHERE → SELECT**

Therefore:

**Filter first → Aggregate the filtered data**

# 1. WHERE with Aggregate Functions 🔍📊

The `WHERE` clause can be combined with:

- `AVG()`
- `SUM()`
- `MIN()`
- `MAX()`
- `COUNT()`

This allows us to calculate summaries for only the records that meet a specific condition.

## Example: Average Budget from 2010 Onward

`SELECT AVG(budget) FROM films WHERE release_year >= 2010;`

This means:

1. Get records from `films`.
2. Keep only films released in **2010 or later**.
3. Calculate the average `budget` of those films.

### Logical Processing

**FROM films → WHERE release_year >= 2010 → SELECT AVG(budget)**

> The `WHERE` clause filters the records before `AVG()` calculates the result.

# 2. SUM() with WHERE ➕

Example:

`SELECT SUM(budget) FROM films WHERE release_year = 2010;`

This calculates the **total budget** of films released in 2010.

The lesson gives a total of **over 8.9 billion**.

### Important

The exact value should be interpreted carefully because the dataset contains **multiple currencies**.

# 3. MIN() with WHERE ⬇️

Example:

`SELECT MIN(budget) FROM films WHERE release_year = 2010;`

This returns the **smallest recorded budget** among films released in 2010.

The lesson gives:

**65,000**

# 4. MAX() with WHERE ⬆️

Example:

`SELECT MAX(budget) FROM films WHERE release_year = 2010;`

This returns the **largest recorded budget** among films released in 2010.

The lesson gives:

**600 million**

The value is associated with the Indian movie **"Kites"**, and the budget is represented in **Indian Rupees**.

> Be careful when interpreting financial data stored in multiple currencies.

# 5. COUNT() with WHERE 🔢

Example:

`SELECT COUNT(budget) FROM films WHERE release_year = 2010;`

This counts the number of **non-NULL budget values** among films released in 2010.

The lesson gives:

**194 recorded budgets**

### Important

`COUNT(budget)` does **not** count every film.

It only counts films where `budget` is **not NULL**.

Therefore:

**COUNT(budget) = Number of non-missing budget values**

# 6. Aggregate Functions with Filtering

| Function | Example | Purpose |
|---|---|---|
| `AVG()` | `AVG(budget)` | Average budget |
| `SUM()` | `SUM(budget)` | Total budget |
| `MIN()` | `MIN(budget)` | Smallest budget |
| `MAX()` | `MAX(budget)` | Largest budget |
| `COUNT()` | `COUNT(budget)` | Number of non-NULL budgets |

All can be combined with `WHERE` to summarize a **subset** of the table.

# 7. ROUND() 🔢✨

`ROUND()` is used to **round numerical values** to a specified number of decimal places.

This is especially useful when aggregate functions produce long decimal values.

### Basic Syntax

`ROUND(number, decimal_places)`

There are two parameters:

1. **Number** → The value to round.
2. **Decimal places** → How many decimal places to keep.

## Example

`SELECT ROUND(AVG(budget), 2) FROM films WHERE release_year >= 2010;`

This calculates the average budget and rounds the result to **2 decimal places**.

### Why Use 2 Decimal Places?

Two decimal places are commonly appropriate when displaying **currency values**.

Example:

`12345678.98765`

becomes:

`12345678.99`

# 8. ROUND() to a Whole Number 🔢

The second parameter of `ROUND()` is **optional**.

If it is omitted, SQL rounds to the nearest whole number.

Example:

`ROUND(AVG(budget))`

is equivalent to:

`ROUND(AVG(budget), 0)`

### Meaning

**No second parameter → 0 decimal places**

# 9. ROUND() with Negative Values 🔄

The second parameter of `ROUND()` can also be **negative**.

A negative value rounds digits to the **left of the decimal point**.

### Examples

`ROUND(number, -1)`

→ Round to the nearest **10**

`ROUND(number, -2)`

→ Round to the nearest **100**

`ROUND(number, -3)`

→ Round to the nearest **1,000**

`ROUND(number, -5)`

→ Round to the nearest **100,000**

### Important Example

`ROUND(1234567, -5)`

rounds the number to the nearest:

**100,000**

# 10. ROUND() Parameter Summary 📋

| Second Parameter | Result |
|---:|---|
| `2` | 2 decimal places |
| `1` | 1 decimal place |
| `0` | Whole number |
| `-1` | Nearest 10 |
| `-2` | Nearest 100 |
| `-3` | Nearest 1,000 |
| `-5` | Nearest 100,000 |

### Easy Rule

**Positive → Right of decimal**

**Zero → Whole number**

**Negative → Left of decimal**

# 11. ROUND() with Aggregate Functions 📊

`ROUND()` can be combined with aggregate functions such as `AVG()`.

Example:

`SELECT ROUND(AVG(budget), 2) AS average_budget FROM films WHERE release_year >= 2010;`

This:

1. Filters films released from 2010 onward.
2. Calculates their average budget.
3. Rounds the result to 2 decimal places.
4. Gives the result a readable alias.

### Processing Concept

**FROM → WHERE → AVG() → ROUND() → Result**

# 12. Important Data Type Rule ⚠️

`ROUND()` can only be used with **numeric values**.

Therefore, it can be used with:

- Integers
- Decimal numbers
- Numeric calculations
- Aggregate results such as `AVG()` and `SUM()`

It cannot be used directly on text fields such as:

`country`

# 13. Filtering Before Aggregating 🧠

One of the most important concepts in this lesson is that `WHERE` filters the dataset **before** the aggregate calculation.

Example:

`SELECT AVG(budget) FROM films WHERE release_year >= 2010;`

Conceptually:

**All Films → Keep 2010+ Films → Calculate Average**

It does **not** calculate the average of all films and then filter the result.

# 14. Practical Examples 🎯

## Average Budget of Films from 2010 Onward

`SELECT AVG(budget) FROM films WHERE release_year >= 2010;`

## Rounded Average Budget

`SELECT ROUND(AVG(budget), 2) AS average_budget FROM films WHERE release_year >= 2010;`

## Total Budget in 2010

`SELECT SUM(budget) AS total_budget FROM films WHERE release_year = 2010;`

## Minimum Budget in 2010

`SELECT MIN(budget) AS minimum_budget FROM films WHERE release_year = 2010;`

## Maximum Budget in 2010

`SELECT MAX(budget) AS maximum_budget FROM films WHERE release_year = 2010;`

## Number of Recorded Budgets in 2010

`SELECT COUNT(budget) AS budget_count FROM films WHERE release_year = 2010;`

# 15. Common Mistakes ⚠️

### Mistake 1: Forgetting WHERE

Without `WHERE`, the aggregate function summarizes the entire table.

`SELECT AVG(budget) FROM films;`

This calculates the average for all qualifying budget values in the table.

Adding:

`WHERE release_year >= 2010`

restricts the calculation to films released from 2010 onward.

### Mistake 2: Confusing COUNT(*) and COUNT(field)

`COUNT(*)`

→ Counts all rows meeting the `WHERE` condition.

`COUNT(budget)`

→ Counts only non-NULL `budget` values meeting the `WHERE` condition.

### Mistake 3: Rounding Text

❌

`ROUND(country, 2)`

✅

`ROUND(AVG(budget), 2)`

`ROUND()` requires a numeric value.

### Mistake 4: Misunderstanding Negative ROUND()

`ROUND(value, -5)`

does **not** mean 5 decimal places.

It means rounding to the nearest **100,000**.

# 16. Exam / Interview Key Points 🎯

- `WHERE` can be combined with aggregate functions.
- `WHERE` filters records **before** the aggregate calculation.
- The simplified processing order is:
  - **FROM**
  - **WHERE**
  - **SELECT**
- `AVG()` calculates the average of the filtered values.
- `SUM()` calculates the total of the filtered values.
- `MIN()` finds the minimum of the filtered values.
- `MAX()` finds the maximum of the filtered values.
- `COUNT(field)` counts non-NULL values among the filtered records.
- `ROUND()` rounds a numerical value.
- `ROUND(number, decimal_places)` accepts:
  - The number to round.
  - The number of decimal places.
- The second parameter of `ROUND()` is optional.
- Omitting the second parameter rounds to a whole number.
- `ROUND(number, 0)` also rounds to a whole number.
- Positive second parameters round to the **right of the decimal point**.
- Negative second parameters round to the **left of the decimal point**.
- `ROUND(number, -5)` rounds to the nearest **100,000**.
- `ROUND()` works with numerical values only.
- Aggregate functions summarize **columns/fields**, not individual rows.
- Financial data containing multiple currencies should not be directly compared or aggregated without considering currency differences.

# Quick Memory Aid 🚀

**WHERE → Filter first**

**AVG → Average**

**SUM → Total**

**MIN → Lowest**

**MAX → Highest**

**COUNT(field) → Non-NULL values**

**ROUND → Clean up numerical decimals**

### ROUND Rule

**`2` → 2 decimal places**

**`0` → Whole number**

**`-1` → Tens**

**`-2` → Hundreds**

**`-3` → Thousands**

**`-5` → Hundred-thousands**

# Most Important Concept ⭐

> **When aggregate functions are combined with `WHERE`, SQL first filters the records and then calculates the aggregate on the remaining data. `ROUND()` can then be used to control the number of decimal places in numerical results, with positive values rounding to the right of the decimal point, zero rounding to whole numbers, and negative values rounding to the left.**
