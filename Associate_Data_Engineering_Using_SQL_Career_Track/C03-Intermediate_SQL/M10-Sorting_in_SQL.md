# Sorting Results in SQL 🔢

## Overview 📚

**Sorting** puts query results into a specific order, making data easier to understand and analyze.

SQL uses the `ORDER BY` clause to sort results based on one or more fields.

> **ORDER BY = Sort the query results**

# 1. ORDER BY 🔄

`ORDER BY` sorts query results based on a specified field.

### Basic Syntax

`SELECT columns FROM table ORDER BY field;`

By default, `ORDER BY` sorts in **ascending order**.

### Ascending Order

Ascending can mean:

- Smallest → Largest
- A → Z
- Earliest → Latest

Example:

`SELECT title, budget FROM films ORDER BY budget;`

This sorts films by budget from **smallest to largest**.

Example:

`SELECT title FROM films ORDER BY title;`

This sorts film titles alphabetically.

### Important

The database may place titles beginning with:

- Symbols
- Numbers

before titles beginning with the letter `A`.

# 2. ASC Keyword ⬆️

The `ASC` keyword explicitly specifies **ascending order**.

Example:

`SELECT title, budget FROM films ORDER BY budget ASC;`

This produces the same result as:

`SELECT title, budget FROM films ORDER BY budget;`

### Why Use ASC?

Although ascending order is the default, including `ASC` can make your SQL:

- More explicit.
- Easier to read.
- Easier to understand.

> **ASC = Ascending**

# 3. DESC Keyword ⬇️

The `DESC` keyword sorts results in **descending order**.

Descending can mean:

- Largest → Smallest
- Z → A
- Latest → Earliest

Example:

`SELECT title, budget FROM films ORDER BY budget DESC;`

This sorts films from the **highest budget to the lowest budget**.

> **DESC = Descending**

# 4. NULL Values and ORDER BY ⚠️

Data may contain `NULL` values.

For example, some films may not have a recorded budget.

When sorting a field containing NULLs, the results may be less useful.

You can use `WHERE` before `ORDER BY` to remove NULL values.

Example:

`SELECT title, budget FROM films WHERE budget IS NOT NULL ORDER BY budget DESC;`

### Logical Written Order

`SELECT → FROM → WHERE → ORDER BY`

### Meaning

1. Get data from `films`.
2. Keep only films with a recorded budget.
3. Sort those films by budget from highest to lowest.

# 5. Sorting by a Field Not in SELECT 👀

You do **not** have to include the field being used for sorting in the `SELECT` statement.

Example:

`SELECT title FROM films ORDER BY release_year;`

This returns only:

- `title`

but sorts using:

- `release_year`

### Best Practice

Although this is valid, it is often a good idea to include the sorting field in the `SELECT` statement for clarity.

Example:

`SELECT title, release_year FROM films ORDER BY release_year;`

This makes it easier to understand why the records appear in that order.

# 6. ORDER BY Multiple Fields 🔗

`ORDER BY` can sort using **multiple fields**.

Separate the fields with commas.

Example:

`SELECT title, oscar_wins, imdb_score FROM films ORDER BY oscar_wins DESC, imdb_score DESC;`

SQL will:

1. Sort by the first field.
2. Use the second field to break ties.
3. Continue to additional fields if necessary.

## Sorting as a Tie-Breaker

Suppose two films have the same number of Oscar wins.

Sorting only by:

`oscar_wins DESC`

may result in a tie.

Add:

`imdb_score DESC`

to determine which film comes first among those tied films.

### Concept

**Primary sort → First field**

**Tie-breaker → Second field**

**Additional tie-breaker → Third field, etc.**

# 7. Different Sort Directions for Different Fields ↕️

Each field in `ORDER BY` can have its own sorting direction.

Example:

`SELECT name, birthdate FROM people ORDER BY birthdate ASC, name DESC;`

This means:

- `birthdate` → Ascending
- `name` → Descending

### Important

You can mix `ASC` and `DESC` within the same `ORDER BY`.

# 8. ORDER BY Execution Order 🔄

The simplified SQL execution order covered so far is:

**FROM → WHERE → SELECT → ORDER BY → LIMIT**

`ORDER BY` is processed **after `SELECT`** and **before `LIMIT`**.

### Example

`SELECT title FROM films WHERE budget IS NOT NULL ORDER BY budget DESC LIMIT 5;`

Logical processing:

1. `FROM films`
2. `WHERE budget IS NOT NULL`
3. `SELECT title`
4. `ORDER BY budget DESC`
5. `LIMIT 5`

This means:

> Find films with recorded budgets, select their titles, sort them from highest budget to lowest, then return the first 5.

# 9. ORDER BY vs. WHERE 🧠

These clauses perform different jobs.

### WHERE

**Filters records**

Example:

`WHERE budget IS NOT NULL`

→ Removes records that do not have a budget.

### ORDER BY

**Sorts records**

Example:

`ORDER BY budget DESC`

→ Puts records from highest budget to lowest.

### Combined

`WHERE budget IS NOT NULL ORDER BY budget DESC`

means:

**Filter first → Sort second**

# 10. Practical Examples 🎯

## Sort Budgets from Smallest to Largest

`SELECT title, budget FROM films ORDER BY budget ASC;`

## Sort Budgets from Largest to Smallest

`SELECT title, budget FROM films ORDER BY budget DESC;`

## Sort Titles Alphabetically

`SELECT title FROM films ORDER BY title ASC;`

## Sort by Release Year

`SELECT title, release_year FROM films ORDER BY release_year ASC;`

## Exclude Missing Budgets and Sort

`SELECT title, budget FROM films WHERE budget IS NOT NULL ORDER BY budget DESC;`

## Sort by Oscar Wins and Use IMDb Score as a Tie-Breaker

`SELECT title, oscar_wins, imdb_score FROM films ORDER BY oscar_wins DESC, imdb_score DESC;`

## Different Directions

`SELECT name, birthdate FROM people ORDER BY birthdate ASC, name DESC;`

## Top 5 Highest Budgets

`SELECT title, budget FROM films WHERE budget IS NOT NULL ORDER BY budget DESC LIMIT 5;`

# 11. Multiple-Field Sorting Example 📊

Suppose the data is:

| title | oscar_wins | imdb_score |
|---|---:|---:|
| Film A | 5 | 7.2 |
| Film B | 5 | 8.5 |
| Film C | 3 | 9.0 |
| Film D | 5 | 7.9 |

Query:

`ORDER BY oscar_wins DESC, imdb_score DESC`

Result order:

1. Film B → 5 Oscars, 8.5
2. Film D → 5 Oscars, 7.9
3. Film A → 5 Oscars, 7.2
4. Film C → 3 Oscars, 9.0

### Why?

The first sorting field is:

`oscar_wins DESC`

Films with more Oscars come first.

For films tied at 5 Oscars, SQL uses:

`imdb_score DESC`

as the tie-breaker.

# 12. Common Mistakes ⚠️

### Mistake 1: Using ORDER BY Before WHERE

❌

`SELECT title FROM films ORDER BY budget DESC WHERE budget IS NOT NULL;`

✅

`SELECT title FROM films WHERE budget IS NOT NULL ORDER BY budget DESC;`

### Mistake 2: Forgetting the Sort Direction

`ORDER BY budget`

defaults to ascending order.

Use:

`ORDER BY budget DESC`

when you want highest to lowest.

### Mistake 3: Assuming ORDER BY Requires SELECTing the Field

This is valid:

`SELECT title FROM films ORDER BY release_year;`

The sort field does not have to appear in the result.

### Mistake 4: Not Using a Tie-Breaker

If the first sorting field contains many duplicate values, add another field.

Example:

`ORDER BY oscar_wins DESC, imdb_score DESC`

### Mistake 5: Forgetting NULL Values

Missing values can make sorted results less useful.

Use:

`WHERE budget IS NOT NULL`

when you only want records with a budget.

# 13. SQL Clause Order 🧩

### Written Order

A common query structure is:

`SELECT ... FROM ... WHERE ... ORDER BY ... LIMIT ...;`

### Simplified Logical Execution Order

`FROM → WHERE → SELECT → ORDER BY → LIMIT`

### Example

`SELECT title FROM films WHERE release_year >= 2000 ORDER BY budget DESC LIMIT 5;`

Logical flow:

**FROM → Filter → Select → Sort → Limit**

# 14. Key Terms 🧠

### ORDER BY

Sorts query results.

### ASC

Sorts in **ascending order**.

### DESC

Sorts in **descending order**.

### Tie-Breaker

A secondary sort field used when two or more records have the same value in the primary sorting field.

### NULL

Represents a missing or unknown value and may need to be filtered out depending on the analysis.

# Exam / Interview Key Points 🎯

- `ORDER BY` is used to **sort query results**.
- By default, `ORDER BY` sorts in **ascending order**.
- `ASC` explicitly specifies ascending order.
- `DESC` specifies descending order.
- Ascending can mean:
  - Smallest → Largest
  - A → Z
  - Earliest → Latest
- Descending can mean:
  - Largest → Smallest
  - Z → A
  - Latest → Earliest
- Titles beginning with symbols or numbers can appear before titles beginning with `A`.
- A field does **not** have to be included in `SELECT` to be used in `ORDER BY`.
- Including the sorting field in `SELECT` can improve clarity.
- `ORDER BY` can sort by multiple fields.
- Multiple sorting fields are separated by commas.
- The first field is the primary sort.
- Later fields act as **tie-breakers**.
- Each sorting field can have its own direction.
- You can use `ASC` for one field and `DESC` for another.
- `WHERE` is processed before `ORDER BY`.
- `ORDER BY` is processed before `LIMIT`.
- The simplified execution order is:

`FROM → WHERE → SELECT → ORDER BY → LIMIT`

- Use `WHERE field IS NOT NULL` when you want to exclude missing values before sorting.
- Combining `WHERE`, `ORDER BY`, and `LIMIT` is useful for finding top or bottom records.

# Quick Memory Aid 🚀

**ORDER BY = Sort**

**ASC = Small → Large / A → Z**

**DESC = Large → Small / Z → A**

**Multiple fields = Primary sort + Tie-breaker**

**WHERE = Filter**

**ORDER BY = Sort**

**LIMIT = Restrict number of rows**

### Query Pattern

`SELECT columns FROM table WHERE condition ORDER BY field DESC LIMIT n;`

### Execution

**FROM → WHERE → SELECT → ORDER BY → LIMIT**

# Most Important Concept ⭐

> **`ORDER BY` sorts query results in ascending order by default. Use `ASC` for ascending and `DESC` for descending. Multiple fields can be used to create primary and tie-breaker sorting, and each field can have its own sort direction. In the simplified SQL execution order, `ORDER BY` occurs after `SELECT` and before `LIMIT`.**
