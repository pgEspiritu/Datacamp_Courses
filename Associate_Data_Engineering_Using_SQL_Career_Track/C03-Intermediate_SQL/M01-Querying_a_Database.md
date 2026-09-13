# Querying a Database

## Course Overview 📚

This course focuses on using **SQL to turn raw data into actionable insights**.

### Main Focus

Although SQL can be used to create and modify databases, this course focuses primarily on **querying databases**.

> **Query = A request for data from a database.**

### Course Topics

The course covers:

- Counting records and values.
- Viewing all or a specified number of records.
- Common SQL errors.
- SQL style guidelines.
- SQL execution order.
- Filtering data.
- Aggregate functions.
- Sorting results.
- Grouping results.
- Presenting query results clearly.

### SQL Flavor

The course uses **PostgreSQL**.

# Films Database 🎬

The course uses a films database containing four tables:

1. `films`
2. `reviews`
3. `people`
4. `roles`

The database schema shows:

- Table names
- Field names
- Data types
- Relationships between tables

# COUNT() 🔢

`COUNT()` is an aggregate function used to **count values or records**.

## COUNT() with a Field

Using `COUNT()` with a field counts the number of records that contain a value in that field.

Example:

`SELECT COUNT(birthdate) FROM people;`

This counts the number of people who have a value in the `birthdate` field.

Example result:

`6152`

### Important

`COUNT(field)` counts **non-missing values in that field**.

It does not necessarily count every row in the table.

## Aliasing COUNT() Results

A count result can be given a more readable name using an alias.

Example:

`SELECT COUNT(birthdate) AS count_birthdates FROM people;`

The alias changes the displayed column name in the result set.

> **Aliasing affects the result display, not the original table.**

# COUNT() with Multiple Fields

To count multiple fields, use `COUNT()` separately for each field.

Example:

`SELECT COUNT(name) AS count_names, COUNT(birthdate) AS count_birthdates FROM people;`

This returns:

- Number of non-missing `name` values.
- Number of non-missing `birthdate` values.

## Important

Each `COUNT()` operates independently on the specified field.

# COUNT(*) ⭐

If the goal is to count the **total number of records/rows in a table**, use:

`COUNT(*)`

Example:

`SELECT COUNT(*) FROM people;`

The `*` represents all fields.

Using `COUNT(*)` is a convenient way to count the total number of rows in the table.

### Key Difference

**`COUNT(field)` → Counts non-missing values in a specific field**

**`COUNT(*)` → Counts rows/records**

# DISTINCT 🔍

`DISTINCT` is used to return **unique values** and remove duplicates from the query result.

Example:

`SELECT DISTINCT language FROM films;`

This returns each language represented in the `films` table only once.

### Without DISTINCT

`SELECT language FROM films;`

may return:

`English, English, French, English, Spanish, French...`

### With DISTINCT

`SELECT DISTINCT language FROM films;`

returns:

`English, French, Spanish...`

## Key Concept

**DISTINCT = Unique values only**

`DISTINCT` does not delete duplicates from the underlying table. It only removes duplicate values from the query result.

# COUNT() + DISTINCT 🔢🔍

`COUNT()` and `DISTINCT` can be combined to count the number of **unique values** in a field.

Example:

`SELECT COUNT(DISTINCT birthdate) FROM people;`

This counts the number of distinct birth dates in the `people` table.

## Why Is COUNT(DISTINCT birthdate) Different from COUNT(birthdate)?

Suppose the table contains:

`1990-01-01`

`1990-01-01`

`1991-05-10`

`1992-07-15`

Then:

`COUNT(birthdate)` counts all non-missing values:

`4`

while:

`COUNT(DISTINCT birthdate)` counts unique dates:

`3`

The duplicate birthday is counted only once by `DISTINCT`.

### Key Difference

**`COUNT(birthdate)` → Counts all non-missing birthdate values**

**`COUNT(DISTINCT birthdate)` → Counts unique birthdate values**

# COUNT() Comparison 📊

| Query | What It Counts |
|---|---|
| `COUNT(field)` | Non-missing values in the specified field |
| `COUNT(*)` | Total number of rows/records |
| `COUNT(DISTINCT field)` | Unique non-missing values in the field |

# Practical Examples

## Count Birth Dates

`SELECT COUNT(birthdate) FROM people;`

**Purpose:** Count people with a recorded birth date.

## Count Records

`SELECT COUNT(*) FROM people;`

**Purpose:** Count all records in the `people` table.

## Count Names and Birth Dates

`SELECT COUNT(name), COUNT(birthdate) FROM people;`

**Purpose:** Count non-missing names and birth dates separately.

## List Unique Languages

`SELECT DISTINCT language FROM films;`

**Purpose:** List each unique language in the films table.

## Count Unique Birth Dates

`SELECT COUNT(DISTINCT birthdate) FROM people;`

**Purpose:** Count the number of different birth dates.

# Common Important Distinctions 🧠

## `COUNT(field)` vs. `COUNT(*)`

**`COUNT(field)`**

- Counts values in one specific field.
- Does not count missing/NULL values in that field.

**`COUNT(*)`**

- Counts rows in the table.
- Used when you want the total number of records.

## `DISTINCT` vs. `COUNT(DISTINCT ...)`

**`DISTINCT`**

Returns the unique values themselves.

Example:

`SELECT DISTINCT language FROM films;`

**`COUNT(DISTINCT ...)`**

Returns the number of unique values.

Example:

`SELECT COUNT(DISTINCT language) FROM films;`

# SQL Query Building Blocks 🧩

| Keyword / Function | Purpose |
|---|---|
| `SELECT` | Specifies what to retrieve |
| `FROM` | Specifies the source table |
| `COUNT()` | Counts values or rows |
| `DISTINCT` | Removes duplicate result values |
| `AS` | Creates an alias |
| `*` | Represents all fields |

# Exam / Interview Key Points 🎯

- A **query** is a request for data from a database.
- This course focuses on **querying**, not database creation or modification.
- The course uses **PostgreSQL**.
- The films database contains:
  - `films`
  - `reviews`
  - `people`
  - `roles`
- `COUNT()` is used to count values or records.
- `COUNT(field)` counts **non-missing values** in a field.
- `COUNT(*)` counts the **total number of rows/records**.
- `DISTINCT` returns only **unique values**.
- `COUNT(DISTINCT field)` counts the **number of unique values** in a field.
- `COUNT(field)` and `COUNT(DISTINCT field)` can return different results when duplicates exist.
- Aliases can make query results easier to understand.
- `DISTINCT` does not change the underlying database; it only affects the query result.
- `COUNT()` can be used multiple times in the same query to count different fields.

# Quick Memory Aid 🚀

**COUNT(field) = How many values?**

**COUNT(*) = How many rows?**

**DISTINCT = Which unique values?**

**COUNT(DISTINCT field) = How many unique values?**

**AS = Rename the result column**

### Easy Rule

> **Need the actual unique values? → `DISTINCT`**

> **Need the number of unique values? → `COUNT(DISTINCT ...)`**

# Most Important Concept ⭐

> **`COUNT(field)` counts non-missing values in a field, `COUNT(*)` counts all rows in a table, and `COUNT(DISTINCT field)` counts the number of unique values in that field. `DISTINCT` removes duplicate values from the query result without modifying the underlying data.**
