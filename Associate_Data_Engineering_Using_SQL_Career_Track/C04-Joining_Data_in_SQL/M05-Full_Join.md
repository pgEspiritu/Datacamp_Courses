# FULL JOINs 🔗

## Overview 📚

`FULL JOIN` is the **third and final type of outer join** covered in the lesson.

It combines the behavior of:

- `LEFT JOIN`
- `RIGHT JOIN`

and can be compared with:

- `INNER JOIN`

> **FULL JOIN = Keep all records from both tables, whether or not they match.**

# 1. FULL JOIN

A `FULL JOIN` returns **all records from both tables**.

It does not require a matching value in the other table.

If a record has no match:

- Fields from the other table are returned as `NULL`.

### Basic Concept

**Left-only records ✅**

**Matching records ✅**

**Right-only records ✅**

Therefore:

> **FULL JOIN keeps everything from both tables.**

# 2. FULL JOIN vs. Other Joins 📊

| Join | Records Retained |
|---|---|
| **INNER JOIN** | Only records matching in both tables |
| **LEFT JOIN** | All records from the left table + matching right records |
| **RIGHT JOIN** | All records from the right table + matching left records |
| **FULL JOIN** | All records from both tables |

### Memory Aid 🧠

**INNER = Matching only**

**LEFT = Keep left**

**RIGHT = Keep right**

**FULL = Keep both**

# 3. FULL JOIN Result

Suppose the two tables contain IDs:

**Left Table:** `1, 2, 3, 4`

**Right Table:** `1, 4, 5, 6`

A `FULL JOIN` on `id` returns:

`1, 2, 3, 4, 5, 6`

All six IDs are retained.

### Unmatched Records

For IDs that exist only in one table, fields from the other table become `NULL`.

Therefore:

- Left-only record → Right-table fields = `NULL`
- Right-only record → Left-table fields = `NULL`

### Important

Unlike `LEFT JOIN` or `RIGHT JOIN`, `NULL` values can appear on **either side** of the result.

# 4. FULL JOIN Syntax 💻

The syntax is similar to the other joins.

### Basic Syntax

`SELECT ... FROM left_table FULL JOIN right_table ON left_table.id = right_table.id;`

The key difference is the use of:

`FULL JOIN`

### Alternative Syntax

`FULL OUTER JOIN`

can also be used.

Example:

`SELECT ... FROM left_table FULL OUTER JOIN right_table ON left_table.id = right_table.id;`

`FULL JOIN` and `FULL OUTER JOIN` return the same type of result.

# 5. FULL JOIN with the Leaders Database 🌍

The lesson uses the world leaders database.

The relevant tables are:

- `prime_ministers`
- `presidents`

Suppose we want:

> **All countries in the database, and whether they have a president, a prime minister, or both.**

A `FULL JOIN` is appropriate because we want to retain **every country**, regardless of whether it appears in both tables.

# 6. FULL JOIN Query Structure

The query conceptually contains:

- `country`
- `prime_minister`
- `president`

as selected fields.

Example:

`SELECT p1.country, p1.prime_minister, p2.president FROM prime_ministers AS p1 FULL JOIN presidents AS p2 ON p1.country = p2.country LIMIT 10;`

### Query Components

**`SELECT`**

→ Selects the fields to display.

**`FROM prime_ministers AS p1`**

→ Sets `prime_ministers` as the left table and gives it the alias `p1`.

**`FULL JOIN presidents AS p2`**

→ Sets `presidents` as the right table and performs a FULL JOIN.

**`ON p1.country = p2.country`**

→ Matches records using `country`.

**`LIMIT 10`**

→ Returns the first 10 records.

# 7. Table Order Matters ⚠️

The order of the tables matters in a `FULL JOIN`.

Example:

`FROM prime_ministers AS p1 FULL JOIN presidents AS p2 ...`

is not necessarily displayed in the same record order as:

`FROM presidents AS p2 FULL JOIN prime_ministers AS p1 ...`

The lesson notes that changing the table order can change the **ordering of the resulting records**, depending on how the records are ordered in the source tables.

### Important

The goal of the FULL JOIN remains the same:

**Keep all records from both tables.**

But the resulting record order can differ.

# 8. Why Use FULL JOIN? 🎯

Use `FULL JOIN` when you need to identify:

- Records existing in both tables.
- Records existing only in the left table.
- Records existing only in the right table.

### Leaders Example

We want countries that may have:

- A president only.
- A prime minister only.
- Both a president and a prime minister.

Therefore:

**FULL JOIN = Appropriate**

# 9. NULL Values in FULL JOIN 🕳️

Because all records are retained, unmatched records produce `NULL` values.

### Country with Prime Minister Only

`prime_minister = Present`

`president = NULL`

### Country with President Only

`prime_minister = NULL`

`president = Present`

### Country with Both

`prime_minister = Present`

`president = Present`

# 10. FULL JOIN Example

Suppose:

### `prime_ministers`

| country | prime_minister |
|---|---|
| A | PM A |
| B | PM B |
| C | PM C |

### `presidents`

| country | president |
|---|---|
| B | President B |
| C | President C |
| D | President D |

A FULL JOIN on `country` produces:

| country | prime_minister | president |
|---|---|---|
| A | PM A | NULL |
| B | PM B | President B |
| C | PM C | President C |
| D | NULL | President D |

Every country from both tables is retained.

# 11. FULL JOIN vs. INNER JOIN 🔄

### INNER JOIN

Only matching records:

`B, C`

### FULL JOIN

All records:

`A, B, C, D`

### Visual Concept

**INNER JOIN → Intersection**

**FULL JOIN → Everything from both tables**

# 12. FULL JOIN vs. LEFT and RIGHT JOIN

Suppose:

**Left:** `1, 2, 3, 4`

**Right:** `1, 4, 5, 6`

### INNER JOIN

`1, 4`

### LEFT JOIN

`1, 2, 3, 4`

### RIGHT JOIN

`1, 4, 5, 6`

### FULL JOIN

`1, 2, 3, 4, 5, 6`

# 13. Practical Example 🎯

`SELECT p1.country, p1.prime_minister, p2.president FROM prime_ministers AS p1 FULL JOIN presidents AS p2 ON p1.country = p2.country LIMIT 10;`

Purpose:

> Return up to 10 countries and show whether each has a prime minister, president, or both.

# 14. Common Mistakes ⚠️

### Mistake 1: Using INNER JOIN

If the goal is to keep countries that appear in only one table, `INNER JOIN` is incorrect.

❌

`FROM prime_ministers INNER JOIN presidents ...`

✅

`FROM prime_ministers FULL JOIN presidents ...`

### Mistake 2: Expecting Unmatched Records to Disappear

With FULL JOIN, unmatched records are retained.

The unmatched side contains `NULL`.

### Mistake 3: Forgetting Which Side Can Contain NULL

In a FULL JOIN, `NULL` can occur in:

- Left-table fields.
- Right-table fields.

### Mistake 4: Confusing FULL JOIN with LEFT + RIGHT

Conceptually, FULL JOIN combines the behavior of LEFT JOIN and RIGHT JOIN into one operation.

# Exam / Interview Key Points 🎯

- `FULL JOIN` is the **third type of outer join** covered in the lesson.
- `FULL JOIN` keeps **all records from both tables**.
- Matching records are included.
- Left-only records are included.
- Right-only records are included.
- Unmatched fields are represented by `NULL`.
- `NULL` can appear on **either side** of a FULL JOIN result.
- `FULL JOIN` can also be written as `FULL OUTER JOIN`.
- The basic syntax is:

`SELECT ... FROM left_table FULL JOIN right_table ON matching_condition;`

- The join condition is specified with `ON`.
- The leaders database example uses:
  - `prime_ministers`
  - `presidents`
- The join is performed using the `country` field.
- `LIMIT 10` can be used to restrict the displayed result to the first 10 records.
- Table order can affect the **ordering of the result records**.
- FULL JOIN is useful when you need all records regardless of whether a matching record exists in the other table.

# Quick Memory Aid 🚀

**INNER JOIN → Match only**

**LEFT JOIN → Keep left**

**RIGHT JOIN → Keep right**

**FULL JOIN → Keep both**

### NULL Rule

**Left-only → Right fields = `NULL`**

**Right-only → Left fields = `NULL`**

**Both match → No missing join-side fields**

### FULL JOIN Pattern

`SELECT ... FROM A FULL JOIN B ON A.key = B.key;`

# Most Important Concept ⭐

> **`FULL JOIN` returns every record from both tables, whether or not a matching record exists. Matching records are combined, while unmatched records are retained with `NULL` values on the side where no match exists. `FULL OUTER JOIN` is an equivalent syntax, and table order can affect the ordering of the returned records.**
