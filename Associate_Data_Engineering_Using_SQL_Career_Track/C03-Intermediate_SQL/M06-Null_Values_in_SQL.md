# NULL Values in SQL 🕳️

## Overview 📚

In SQL, **NULL** represents a **missing or unknown value**.

NULL values are common in real-world databases because information may be:

- Unavailable.
- Unknown.
- Not provided.
- Missing due to human error.

Handling NULL values correctly is important because they can affect **data analysis and conclusions**.

# 1. What Is NULL?

**NULL = Missing or unknown value**

NULL is not the same as:

- `0`
- An empty string `''`
- `FALSE`

It specifically represents the absence of a known value.

### Example

A `people` table may contain a `deathdate` field.

Some people may have:

`deathdate = 1995-06-12`

while others may have:

`deathdate = NULL`

The NULL value means the death date is **missing or unknown**.

# 2. Why NULL Values Matter ⚠️

Missing values can lead to incorrect conclusions if they are not considered.

For example, suppose we want to analyze **posthumous success** using the `deathdate` field.

We might incorrectly assume that everyone has a recorded death date simply because the table contains a `deathdate` column.

However, if many records contain NULL values, the analysis may be inaccurate.

> **Always check for missing values before interpreting or analyzing a dataset.**

# 3. IS NULL 🔍

Use `IS NULL` with `WHERE` to find records where a field contains a NULL value.

Example:

`SELECT * FROM people WHERE birthdate IS NULL;`

This returns people whose `birthdate` is missing or unknown.

### Purpose

**IS NULL = Find missing/unknown values**

# 4. Counting NULL Values 🔢

You can use `COUNT(*)` together with `IS NULL` to count records with missing values.

Example:

`SELECT COUNT(*) FROM people WHERE birthdate IS NULL;`

The lesson gives an example where the number of missing birthdates is:

**2245**

### Meaning

This indicates that **2,245 records do not have a recorded birthdate**.

# 5. IS NOT NULL ✅

Use `IS NOT NULL` when you want to find records where a value **is present**.

Example:

`SELECT * FROM people WHERE birthdate IS NOT NULL;`

This returns only records with a recorded birthdate.

### Purpose

**IS NOT NULL = Find non-missing values**

# 6. Counting Non-NULL Values

Example:

`SELECT COUNT(*) FROM people WHERE birthdate IS NOT NULL;`

The lesson gives the result:

**6152**

This counts people whose birthdate is present.

# 7. COUNT(field) vs. IS NOT NULL

These two approaches can produce the same count when counting non-missing values.

### Method 1

`SELECT COUNT(birthdate) FROM people;`

### Method 2

`SELECT COUNT(*) FROM people WHERE birthdate IS NOT NULL;`

Both count the **non-NULL birthdate values**.

### Why?

`COUNT(field)` counts only records where that field contains a non-NULL value.

Therefore:

**COUNT(field) = COUNT(*) WHERE field IS NOT NULL**

for the purpose of counting non-missing values.

# 8. NULL Filtering Summary 🧠

| SQL | Meaning |
|---|---|
| `IS NULL` | Value is missing/unknown |
| `IS NOT NULL` | Value is present/non-missing |
| `COUNT(field)` | Counts non-NULL values in the field |
| `COUNT(*)` | Counts all rows, including rows with NULL values in individual fields |

# 9. NULL vs. COUNT(*) vs. COUNT(field)

Consider a table with:

| id | birthdate |
|---:|---|
| 1 | 1990-01-01 |
| 2 | NULL |
| 3 | 1985-05-10 |
| 4 | NULL |

Then:

`COUNT(*)`

returns:

**4**

because there are four records.

`COUNT(birthdate)`

returns:

**2**

because only two records have non-NULL birthdates.

`COUNT(*) WHERE birthdate IS NULL`

returns:

**2**

because two records have missing birthdates.

`COUNT(*) WHERE birthdate IS NOT NULL`

returns:

**2**

because two records have recorded birthdates.

# 10. Important Analysis Consideration 📊

Before performing analysis, determine:

- How many values are NULL?
- How many values are non-NULL?
- Why are values missing?
- Does the missing data affect the analysis?

### Example

If a field is NULL for half of the records, analyzing only the non-NULL records may produce a result that does not represent the entire dataset.

> **Missing data is part of the data and should be understood before drawing conclusions.**

# 11. Common Mistakes ⚠️

### Mistake 1: Using `= NULL`

❌

`WHERE birthdate = NULL`

✅

`WHERE birthdate IS NULL`

SQL uses `IS NULL` to test for NULL values.

### Mistake 2: Using `<> NULL`

❌

`WHERE birthdate <> NULL`

✅

`WHERE birthdate IS NOT NULL`

### Mistake 3: Assuming an Empty Field Is Always NULL

A blank-looking value and NULL are not necessarily the same thing.

For example:

- `NULL` = Missing/unknown
- `''` = Empty string

These should not automatically be treated as identical.

# 12. Practical Examples 🎯

## Find Missing Birthdates

`SELECT name FROM people WHERE birthdate IS NULL;`

## Count Missing Birthdates

`SELECT COUNT(*) FROM people WHERE birthdate IS NULL;`

## Find People with Birthdates

`SELECT name FROM people WHERE birthdate IS NOT NULL;`

## Count People with Birthdates

`SELECT COUNT(*) FROM people WHERE birthdate IS NOT NULL;`

## Count Birthdates Using COUNT()

`SELECT COUNT(birthdate) FROM people;`

This produces the same count of non-missing birthdates as:

`SELECT COUNT(*) FROM people WHERE birthdate IS NOT NULL;`

# Exam / Interview Key Points 🎯

- **NULL represents a missing or unknown value**.
- NULL values are common in real-world datasets.
- Missing values can affect analysis and lead to inaccurate conclusions.
- `IS NULL` identifies records where a field is NULL.
- `IS NOT NULL` identifies records where a field is not NULL.
- Use `IS NULL` rather than `= NULL`.
- Use `IS NOT NULL` rather than `<> NULL`.
- `COUNT(field)` counts **non-NULL values** in the specified field.
- `COUNT(*)` counts **all rows**, regardless of NULL values in individual fields.
- `COUNT(field)` and `COUNT(*) WHERE field IS NOT NULL` produce the same count when measuring non-missing values.
- `COUNT(*) WHERE field IS NULL` counts missing values.
- It is good practice to check the amount of NULL data before performing analysis.
- A table having a field does **not** mean every record has a value for that field.
- NULL is different from:
  - `0`
  - `FALSE`
  - Empty string `''`

# Quick Memory Aid 🚀

**NULL = Missing / Unknown**

**IS NULL → Find missing**

**IS NOT NULL → Find present**

**COUNT(field) → Count non-NULL values**

**COUNT(*) → Count all rows**

### Easy Rule

> **Want missing values? → `IS NULL`**

> **Want existing values? → `IS NOT NULL`**

> **Want to count existing values? → `COUNT(field)`**

# Most Important Concept ⭐

> **NULL represents missing or unknown data. Use `IS NULL` to identify missing values and `IS NOT NULL` to identify non-missing values. `COUNT(field)` counts only non-NULL values, while `COUNT(*)` counts every row. Always consider NULL values before drawing conclusions from a dataset.**
