# Summarizing Data with Aggregate Functions 📊

## Overview 📚

When analyzing data, we often need to understand the **dataset as a whole**, not just individual records.

SQL provides **aggregate functions** to summarize multiple values into a single result.

> **Aggregate function = Performs a calculation on multiple values and returns a single value.**

# Aggregate Functions 🔢

The course covers five important aggregate functions:

- `COUNT()`
- `AVG()`
- `SUM()`
- `MIN()`
- `MAX()`

All aggregate functions are used after `SELECT`.

## Aggregate Function Summary

| Function | Purpose | Numeric Fields | Non-Numeric Fields |
|---|---|---:|---:|
| `COUNT()` | Counts non-NULL values | ✅ | ✅ |
| `AVG()` | Calculates average | ✅ | ❌ |
| `SUM()` | Calculates total | ✅ | ❌ |
| `MIN()` | Finds lowest/minimum value | ✅ | ✅ |
| `MAX()` | Finds highest/maximum value | ✅ | ✅ |

# 1. COUNT() 🔢

`COUNT()` counts the number of **non-NULL values** in a field.

Example:

`SELECT COUNT(budget) FROM films;`

This counts the films that have a value recorded in the `budget` field.

> `COUNT(field)` counts non-missing values.

# 2. AVG() 📈

`AVG()` calculates the **average value** of a numeric field.

Example:

`SELECT AVG(budget) FROM films;`

The lesson gives an average budget of **over 39 million per film**.

### Use

`AVG()` is appropriate for numerical data because calculating an average requires arithmetic.

Example:

**Values:** 10, 20, 30

**AVG = 20**

# 3. SUM() ➕

`SUM()` adds together the values in a numeric field.

Example:

`SELECT SUM(budget) FROM films;`

The lesson gives a total film budget of **over 181 billion**.

### Use

`SUM()` is only applicable to numerical fields because addition requires arithmetic.

Example:

**Values:** 10, 20, 30

**SUM = 60**

# 4. MIN() ⬇️

`MIN()` returns the **lowest** value in a field.

Example:

`SELECT MIN(budget) FROM films;`

For numbers, the minimum is the smallest number.

For strings, the minimum is the value that comes first alphabetically.

For dates, the minimum is the earliest date.

### Examples

Numbers:

`MIN(10, 20, 30) = 10`

Strings:

`MIN('Afghanistan', 'France', 'West Germany') = 'Afghanistan'`

Dates:

`MIN(date1, date2, date3) = Earliest date`

# 5. MAX() ⬆️

`MAX()` returns the **highest** value in a field.

Example:

`SELECT MAX(budget) FROM films;`

For numbers, the maximum is the largest number.

For strings, the maximum is the value that comes last alphabetically.

For dates, the maximum is the latest date.

### Examples

Numbers:

`MAX(10, 20, 30) = 30`

Strings:

`MAX('Afghanistan', 'France', 'West Germany') = 'West Germany'`

Dates:

`MAX(date1, date2, date3) = Latest date`

# Numerical vs. Non-Numerical Data 🔤🔢

Some aggregate functions only work with numerical data.

## Numerical Only

### `AVG()`

Requires arithmetic.

### `SUM()`

Requires arithmetic.

Therefore:

**`AVG()` and `SUM()` → Numeric fields only**

## Can Work with Non-Numerical Data

### `COUNT()`

Counts non-NULL values regardless of the field's data type.

### `MIN()`

Can return the lowest value based on the data type.

### `MAX()`

Can return the highest value based on the data type.

Therefore:

**`COUNT()`, `MIN()`, and `MAX()` → Can work with numerical and non-numerical fields**

# How MIN() and MAX() Work with Different Data Types 🧠

| Data Type | `MIN()` | `MAX()` |
|---|---|---|
| **Numbers** | Smallest number | Largest number |
| **Strings** | Alphabetically first | Alphabetically last |
| **Dates** | Earliest date | Latest date |

### Example: Countries

`SELECT MIN(country), MAX(country) FROM films;`

The lesson shows:

- `MIN(country)` → **Afghanistan**
- `MAX(country)` → **West Germany**

because:

- Afghanistan comes first alphabetically.
- West Germany comes later alphabetically.

# Important Data Quality Consideration ⚠️

The film budgets in the example are represented in **multiple currencies**.

Therefore, directly comparing or aggregating those budget values may not produce a meaningful financial comparison unless the currencies are converted using appropriate exchange rates.

> **Always understand the meaning and units of your data before interpreting aggregate results.**

# Aggregate Functions Operate on Columns 📌

Aggregate functions operate on a **field/column**, not directly on individual rows.

Example:

`AVG(budget)`

means:

> Calculate the average of the values in the `budget` column.

The function summarizes many field values into one result.

# Aliasing Aggregate Results ✏️

When using aggregate functions, SQL may automatically use the function as the result column name.

Example:

`SELECT MIN(country) FROM films;`

The output column may be named something like:

`min`

This is not very descriptive.

### Best Practice

Use an alias to make summarized results easier to understand.

Example:

`SELECT MIN(country) AS first_country FROM films;`

Another example:

`SELECT AVG(budget) AS average_budget FROM films;`

### Why Use Aliases?

Aliases make results:

- Clearer.
- Easier to understand.
- Easier to read.
- More professional.

# Multiple Aggregate Functions 📊

Multiple aggregate functions can be used in the same query.

Example:

`SELECT AVG(budget) AS average_budget, SUM(budget) AS total_budget, MIN(budget) AS minimum_budget, MAX(budget) AS maximum_budget FROM films;`

This provides a summary of the `budget` field in one query.

# Practical Examples 🎯

## Average Film Budget

`SELECT AVG(budget) AS average_budget FROM films;`

## Total Film Budget

`SELECT SUM(budget) AS total_budget FROM films;`

## Lowest Film Budget

`SELECT MIN(budget) AS minimum_budget FROM films;`

## Highest Film Budget

`SELECT MAX(budget) AS maximum_budget FROM films;`

## Count Films with Recorded Budgets

`SELECT COUNT(budget) AS films_with_budget FROM films;`

## First and Last Country Alphabetically

`SELECT MIN(country) AS first_country, MAX(country) AS last_country FROM films;`

# Aggregate Function Comparison 🧩

| Function | Question It Answers |
|---|---|
| `COUNT()` | How many non-NULL values? |
| `AVG()` | What is the average? |
| `SUM()` | What is the total? |
| `MIN()` | What is the lowest/earliest/first value? |
| `MAX()` | What is the highest/latest/last value? |

# Common Mistakes ⚠️

### Mistake 1: Using AVG() on Text

❌

`SELECT AVG(country) FROM films;`

`AVG()` requires numerical data.

### Mistake 2: Using SUM() on Text

❌

`SELECT SUM(country) FROM films;`

`SUM()` requires numerical data.

### Mistake 3: Confusing COUNT() with COUNT(*)

`COUNT(field)` → Counts non-NULL values in that field.

`COUNT(*)` → Counts all rows.

### Mistake 4: Forgetting NULL Values

Aggregate results can be affected by missing values.

For example:

`COUNT(budget)`

counts only records with a non-NULL budget.

### Mistake 5: Ignoring Units or Currency

If a numerical field combines different units or currencies, aggregate calculations may be misleading.

# Exam / Interview Key Points 🎯

- An **aggregate function** performs a calculation on multiple values and returns a single value.
- The five functions covered are:
  - `COUNT()`
  - `AVG()`
  - `SUM()`
  - `MIN()`
  - `MAX()`
- `COUNT()` counts **non-NULL values**.
- `AVG()` calculates an average and requires **numeric data**.
- `SUM()` calculates a total and requires **numeric data**.
- `MIN()` returns the lowest value.
- `MAX()` returns the highest value.
- `COUNT()`, `MIN()`, and `MAX()` can be used with non-numeric fields.
- With strings:
  - `MIN()` returns the alphabetically first value.
  - `MAX()` returns the alphabetically last value.
- With dates:
  - `MIN()` returns the earliest date.
  - `MAX()` returns the latest date.
- Aggregate functions operate on **columns/fields**.
- Aggregation summarizes multiple field values into a single result.
- Use **aliases** when summarizing data to make output clearer.
- The lesson's film budget example contains **multiple currencies**, so direct comparisons may require currency conversion.

# Quick Memory Aid 🚀

**COUNT() = How many?**

**AVG() = Average?**

**SUM() = Total?**

**MIN() = Lowest / First / Earliest?**

**MAX() = Highest / Last / Latest?**

### Data Type Rule

**AVG + SUM → Numbers only**

**COUNT + MIN + MAX → Numbers + Text + Dates**

### Interpretation Rule

**Numbers → Lowest / Highest**

**Text → Alphabetically First / Last**

**Dates → Earliest / Latest**

# Most Important Concept ⭐

> **Aggregate functions summarize multiple values into a single result. `COUNT()` counts non-NULL values, `AVG()` calculates averages, `SUM()` calculates totals, and `MIN()`/`MAX()` find the lowest/highest values. `AVG()` and `SUM()` require numerical data, while `COUNT()`, `MIN()`, and `MAX()` can also work with text and dates.**
