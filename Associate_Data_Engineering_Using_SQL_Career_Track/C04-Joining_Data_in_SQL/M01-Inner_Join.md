# INNER JOIN 🔗

## Overview 📚

An SQL **JOIN** combines information from separate tables into a single result set.

This lesson focuses on **INNER JOIN**, one of the two most common joins along with `LEFT JOIN`.

The course uses **PostgreSQL**, but the concepts apply to multiple SQL implementations.

# 1. INNER JOIN

`INNER JOIN` returns only the records that have **matching values in both tables** based on the specified join condition.

### Basic Concept

**Table A + Table B → Matching Records Only**

If the join field contains:

- A match in both tables → ✅ Included
- No match in one table → ❌ Excluded

## Example

Suppose two tables contain an `id` field:

- `left_table`
- `right_table`

If only IDs `1` and `4` exist in both tables, an `INNER JOIN` returns records for:

- `id = 1`
- `id = 4`

Records that do not match are excluded.

# 2. Keys 🔑

A **key** is a single column or group of columns that **uniquely identifies records in a table**.

Example:

`id`

can be a key if every record has a unique ID.

### Important

A JOIN does not necessarily have to use a key.

You can join tables using:

- A key field.
- Another field containing matching values.

# 3. INNER JOIN Syntax

The basic structure is:

`SELECT ... FROM left_table INNER JOIN right_table ON left_table.field = right_table.field;`

### Components

| Part | Function |
|---|---|
| `SELECT` | Specifies which fields to return |
| `FROM` | Specifies the first/left table |
| `INNER JOIN` | Specifies the second/right table and requests matching records |
| `ON` | Specifies the condition used to match the tables |

## Example

`SELECT presidents.country, prime_ministers.country FROM presidents INNER JOIN prime_ministers ON presidents.country = prime_ministers.country;`

This returns countries that have matching records in both tables.

# 4. JOIN Condition with ON

The `ON` keyword defines **how the two tables should be matched**.

Example:

`ON presidents.country = prime_ministers.country`

This means:

> Match records where the `country` value in `presidents` is the same as the `country` value in `prime_ministers`.

# 5. Table.Column Notation 📌

When selecting a field that exists in both tables, use:

`table.column`

This identifies exactly which table the field comes from.

Example:

`SELECT presidents.country, prime_ministers.country ...`

### Why?

If both tables contain:

`country`

SQL needs to know which table's version you want.

Using:

`presidents.country`

or:

`prime_ministers.country`

removes the ambiguity.

## General Syntax

`table_name.column_name`

Example:

`presidents.country`

# 6. Leadership Database 🌍

The course uses a database of world leaders.

The database contains:

- `presidents`
- `prime_ministers`
- `monarchs`
- `states`
- `prime_minister_terms`

### Table Information

**`presidents`**

Contains information about presidents.

**`prime_ministers`**

Contains information about prime ministers.

**`monarchs`**

Contains information about monarchs.

**`states`**

Contains information such as independence years.

**`prime_minister_terms`**

Contains the years in which prime ministers assumed office.

# 7. Finding Countries with Both Presidents and Prime Ministers 🌎

Suppose we want countries that appear in both:

- `presidents`
- `prime_ministers`

An `INNER JOIN` can identify them automatically.

Example countries in the lesson:

- Egypt
- Portugal
- Pakistan
- India

### Query Concept

`SELECT ... FROM presidents INNER JOIN prime_ministers ON presidents.country = prime_ministers.country;`

The query returns only countries with a matching `country` value in both tables.

# 8. Table Aliasing ✏️

Table names can be aliased using `AS`, just like column aliases.

This is useful when table names are long or repeatedly referenced.

Example:

`FROM presidents AS p1 INNER JOIN prime_ministers AS p2 ON p1.country = p2.country`

Now:

- `p1` refers to `presidents`
- `p2` refers to `prime_ministers`

The aliases can then be used in `SELECT` and `ON`.

Example:

`SELECT p1.country, p2.country FROM presidents AS p1 INNER JOIN prime_ministers AS p2 ON p1.country = p2.country;`

### Benefits

Table aliases:

- Make queries shorter.
- Reduce repetition.
- Improve readability.
- Make JOIN conditions easier to write.

# 9. USING Shortcut ⚡

When the join columns have **identical names in both tables**, SQL provides the `USING` shortcut.

Instead of:

`INNER JOIN prime_ministers ON presidents.country = prime_ministers.country`

you can use:

`INNER JOIN prime_ministers USING (country)`

### Requirement

`USING` can be used when the column used for joining has the **same name in both tables**.

Example:

`SELECT * FROM presidents INNER JOIN prime_ministers USING (country);`

### ON vs. USING

| Syntax | When to Use |
|---|---|
| `ON` | General join condition; can explicitly compare fields |
| `USING` | When both tables have the same join-column name |

# 10. JOIN Construction Order 🧩

The lesson notes that it is common to construct a JOIN by writing the JOIN portion first, then adding the `SELECT` fields.

Conceptually:

**FROM → INNER JOIN → ON → SELECT**

Final query structure:

`SELECT fields FROM left_table INNER JOIN right_table ON matching_condition;`

# 11. INNER JOIN Result 🔗

Suppose:

### `left_table`

| id | left_val |
|---:|---|
| 1 | A |
| 2 | B |
| 3 | C |
| 4 | D |

### `right_table`

| id | right_val |
|---:|---|
| 1 | X |
| 4 | Y |
| 5 | Z |

An `INNER JOIN` on `id` returns only:

| id | left_val | right_val |
|---:|---|---|
| 1 | A | X |
| 4 | D | Y |

IDs `2`, `3`, and `5` are excluded because they do not have matches in both tables.

# 12. INNER JOIN vs. Matching Manually 👀

For small tables, you might visually compare values to find matches.

For large tables, manually identifying matching records is impractical.

`INNER JOIN` allows SQL to automatically identify and combine matching records.

> **INNER JOIN = Automatically find and combine matching records between tables.**

# 13. Common INNER JOIN Syntax

## Using ON

`SELECT p1.country, p2.country FROM presidents AS p1 INNER JOIN prime_ministers AS p2 ON p1.country = p2.country;`

## Using USING

`SELECT * FROM presidents INNER JOIN prime_ministers USING (country);`

# Exam / Interview Key Points 🎯

- `INNER JOIN` combines data from two tables.
- `INNER JOIN` returns only records with **matching values in both tables**.
- The two tables can be joined using a **key field or another matching field**.
- A **key** is a single column or group of columns that uniquely identifies records in a table.
- `ON` specifies the condition used to match the tables.
- When the same field exists in both tables, use `table.column` notation to avoid ambiguity.
- Example:
  - `presidents.country`
  - `prime_ministers.country`
- Table aliases can be created using `AS`.
- Table aliases can be used in both `SELECT` and `ON`.
- `USING` is a shortcut when the join column has the **same name in both tables**.
- `USING (country)` replaces an explicit condition such as:
  - `ON presidents.country = prime_ministers.country`
- The lesson focuses on PostgreSQL, but the JOIN concepts apply to multiple SQL implementations.
- `INNER JOIN` is one of the two most common joins mentioned in the lesson, along with `LEFT JOIN`.

# Quick Memory Aid 🚀

**INNER JOIN = Matching rows only**

**ON = How do the tables match?**

**table.column = Which table's field?**

**AS = Shorten table names**

**USING = Shortcut when join-column names are identical**

### JOIN Pattern

`SELECT fields FROM table1 INNER JOIN table2 ON table1.field = table2.field;`

### USING Pattern

`SELECT fields FROM table1 INNER JOIN table2 USING (field);`

# Most Important Concept ⭐

> **`INNER JOIN` returns only the records that have matching values in both tables. Use `ON` to define the matching condition, `table.column` to distinguish fields with the same name, table aliases to simplify repeated table references, and `USING (column)` as a shortcut when both tables have an identically named join column.**
