# LEFT and RIGHT JOINs 🔗

## Overview 📚

**LEFT JOIN** and **RIGHT JOIN** are types of **outer joins**.

Unlike `INNER JOIN`, outer joins can retain records even when there is **no matching record** in the other table.

The lesson focuses on:

- `LEFT JOIN`
- `RIGHT JOIN`
- Differences between outer joins and `INNER JOIN`
- When unmatched records produce `NULL` values

# 1. INNER JOIN vs. OUTER JOIN 🔄

### INNER JOIN

Returns only records where the join field has matching values in **both tables**.

**Matching records only**

### LEFT JOIN

Returns:

- **All records from the left table**
- Matching records from the right table
- `NULL` values for right-table fields when no match exists

### RIGHT JOIN

Returns:

- **All records from the right table**
- Matching records from the left table
- `NULL` values for left-table fields when no match exists

# 2. LEFT JOIN ⬅️

A `LEFT JOIN` returns **all records from the left table**, regardless of whether a matching record exists in the right table.

Only matching records from the right table are included.

### Basic Syntax

`SELECT ... FROM left_table LEFT JOIN right_table ON left_table.id = right_table.id;`

### Example

Suppose:

**left_table**

| id | left_val |
|---:|---|
| 1 | A |
| 2 | B |
| 3 | C |
| 4 | D |

**right_table**

| id | right_val |
|---:|---|
| 1 | X |
| 4 | Y |
| 5 | Z |
| 6 | W |

A `LEFT JOIN` on `id` keeps all records from `left_table`.

Result:

| id | left_val | right_val |
|---:|---|---|
| 1 | A | X |
| 2 | B | NULL |
| 3 | C | NULL |
| 4 | D | Y |

### Important

- IDs `2` and `3` remain even though they have no match in `right_table`.
- Their `right_val` is `NULL`.
- IDs `5` and `6` from `right_table` do not appear because they are not in the left table.

> **LEFT JOIN = Keep everything from the left table.**

# 3. LEFT OUTER JOIN

`LEFT JOIN` can also be written as:

`LEFT OUTER JOIN`

These are equivalent.

Example:

`SELECT ... FROM left_table LEFT OUTER JOIN right_table ON left_table.id = right_table.id;`

# 4. World Leaders Example 🌍

The world leaders database contains:

- `presidents`
- `prime_ministers`
- `monarchs`
- `states`
- `prime_minister_terms`

Suppose we want:

> All countries with prime ministers, including presidents where they have one.

A `LEFT JOIN` is appropriate.

### Concept

**All Prime Ministers + Matching Presidents**

If a country has a prime minister but no president, the president-related fields contain `NULL`.

### Example

`SELECT ... FROM prime_ministers LEFT JOIN presidents ON prime_ministers.country = presidents.country;`

For a country such as the **United Kingdom**, where there is no president, the corresponding president field is:

`NULL`

# 5. LEFT JOIN Result 📊

Compared with `INNER JOIN`:

**INNER JOIN**

→ Keeps only countries existing in both tables.

**LEFT JOIN**

→ Keeps every country in the left table, even if the right table has no matching country.

### Example

If the left table contains:

`Egypt, Portugal, Pakistan, India, United Kingdom`

and the right table contains:

`Egypt, Portugal, Pakistan, India`

then:

**INNER JOIN**

→ Egypt, Portugal, Pakistan, India

**LEFT JOIN**

→ Egypt, Portugal, Pakistan, India, United Kingdom

For the United Kingdom:

`president = NULL`

# 6. RIGHT JOIN ➡️

A `RIGHT JOIN` works in the reverse direction of a `LEFT JOIN`.

It returns **all records from the right table**, plus matching records from the left table.

If no match exists in the left table, the left-table fields contain `NULL`.

### Basic Syntax

`SELECT ... FROM left_table RIGHT JOIN right_table ON left_table.id = right_table.id;`

### Important

The order of the tables remains:

`FROM left_table RIGHT JOIN right_table`

The keyword changes from:

`LEFT JOIN`

to:

`RIGHT JOIN`

# 7. RIGHT OUTER JOIN

`RIGHT JOIN` can also be written as:

`RIGHT OUTER JOIN`

Example:

`SELECT ... FROM left_table RIGHT OUTER JOIN right_table ON left_table.id = right_table.id;`

`RIGHT JOIN` and `RIGHT OUTER JOIN` are equivalent.

# 8. RIGHT JOIN Example 📊

Suppose:

**left_table**

| id | left_val |
|---:|---|
| 1 | A |
| 2 | B |
| 3 | C |

**right_table**

| id | right_val |
|---:|---|
| 1 | X |
| 4 | Y |
| 5 | Z |

A `RIGHT JOIN` on `id` keeps all records from `right_table`.

Result:

| id | left_val | right_val |
|---:|---|---|
| 1 | A | X |
| 4 | NULL | Y |
| 5 | NULL | Z |

IDs `4` and `5` remain because they belong to the right table, even though no matching IDs exist in the left table.

# 9. World Leaders Example with RIGHT JOIN 🌍

Suppose:

`prime_ministers` is the **left table**

and:

`presidents` is the **right table**.

Query:

`SELECT ... FROM prime_ministers RIGHT JOIN presidents ON prime_ministers.country = presidents.country;`

This retains **all countries with presidents**.

If a country has a president but no prime minister, the prime-minister fields contain:

`NULL`

# 10. LEFT JOIN vs. RIGHT JOIN ⚖️

| Feature | LEFT JOIN | RIGHT JOIN |
|---|---|---|
| **All records retained from** | Left table | Right table |
| **Matching records from** | Right table | Left table |
| **Unmatched fields** | Right-table fields become `NULL` | Left-table fields become `NULL` |
| **Common usage** | More common | Less common |

### Easy Rule

**LEFT JOIN → Keep left**

**RIGHT JOIN → Keep right**

# 11. INNER JOIN vs. LEFT JOIN vs. RIGHT JOIN 🧠

| Join | Records Retained |
|---|---|
| **INNER JOIN** | Only matching records from both tables |
| **LEFT JOIN** | All left records + matching right records |
| **RIGHT JOIN** | All right records + matching left records |

### Memory

**INNER = Match only**

**LEFT = Keep left**

**RIGHT = Keep right**

# 12. Why RIGHT JOIN Is Less Common 🤔

`RIGHT JOIN` is less commonly used than `LEFT JOIN`.

The main reason given is that any `RIGHT JOIN` can be rewritten as a `LEFT JOIN`.

### Example

This:

`FROM left_table RIGHT JOIN right_table ON left_table.id = right_table.id`

can be rewritten by reversing the table order:

`FROM right_table LEFT JOIN left_table ON right_table.id = left_table.id`

The result can represent the same relationship.

### Why LEFT JOIN Feels More Natural

SQL queries are typically constructed from **left to right**, so users often find:

**FROM → LEFT JOIN**

more intuitive than:

**FROM → RIGHT JOIN**

# 13. NULL Values in Outer Joins 🕳️

One important characteristic of outer joins is that unmatched records produce `NULL` values for the fields belonging to the table with no matching record.

### LEFT JOIN

No matching right record:

**Right-table fields → `NULL`**

### RIGHT JOIN

No matching left record:

**Left-table fields → `NULL`**

# 14. Practical Examples 🎯

## LEFT JOIN

`SELECT p.country, pm.country FROM presidents AS p LEFT JOIN prime_ministers AS pm ON p.country = pm.country;`

This keeps all records from `presidents`.

## LEFT JOIN with Prime Ministers as the Left Table

`SELECT pm.country, p.country FROM prime_ministers AS pm LEFT JOIN presidents AS p ON pm.country = p.country;`

This keeps all records from `prime_ministers`.

## RIGHT JOIN

`SELECT p.country, pm.country FROM prime_ministers AS pm RIGHT JOIN presidents AS p ON pm.country = p.country;`

This keeps all records from `presidents`.

# 15. Common Mistakes ⚠️

### Mistake 1: Forgetting Which Table Is Preserved

In:

`FROM left_table LEFT JOIN right_table ...`

the **left table is preserved**.

In:

`FROM left_table RIGHT JOIN right_table ...`

the **right table is preserved**.

### Mistake 2: Expecting Unmatched Records to Disappear

That happens with `INNER JOIN`.

With outer joins, unmatched records remain and the fields from the missing side become `NULL`.

### Mistake 3: Thinking RIGHT JOIN Is a Different Matching Concept

`RIGHT JOIN` does not use a fundamentally different matching mechanism.

It simply preserves the records from the **right table** instead of the left.

# Exam / Interview Key Points 🎯

- `LEFT JOIN` and `RIGHT JOIN` are **outer joins**.
- `INNER JOIN` returns only matching records from both tables.
- `LEFT JOIN` returns **all records from the left table** and matching records from the right table.
- If a left-table record has no matching right-table record, the right-table fields contain `NULL`.
- `RIGHT JOIN` returns **all records from the right table** and matching records from the left table.
- If a right-table record has no matching left-table record, the left-table fields contain `NULL`.
- `LEFT JOIN` can also be written as `LEFT OUTER JOIN`.
- `RIGHT JOIN` can also be written as `RIGHT OUTER JOIN`.
- In a `LEFT JOIN`, the table after `FROM` is the table whose records are all retained.
- In a `RIGHT JOIN`, the table after `JOIN` is the table whose records are all retained.
- `RIGHT JOIN` is less commonly used than `LEFT JOIN`.
- Any `RIGHT JOIN` can be rewritten as a `LEFT JOIN` by reversing the order of the tables.
- `NULL` values in outer joins indicate that no matching record was found on the other side.

# Quick Memory Aid 🚀

**INNER JOIN = Matching records only**

**LEFT JOIN = Keep ALL left records**

**RIGHT JOIN = Keep ALL right records**

### NULL Rule

**LEFT JOIN + No right match → Right fields = `NULL`**

**RIGHT JOIN + No left match → Left fields = `NULL`**

### Rewrite Rule

`A RIGHT JOIN B`

can be rewritten as:

`B LEFT JOIN A`

# Most Important Concept ⭐

> **`LEFT JOIN` preserves every record from the left table and adds matching records from the right table, using `NULL` when no match exists. `RIGHT JOIN` does the opposite by preserving every record from the right table. Because a `RIGHT JOIN` can be rewritten as a `LEFT JOIN` by reversing the table order, `LEFT JOIN` is generally more intuitive and more commonly used.**
