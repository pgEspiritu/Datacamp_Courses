# Multiple Joins 🔗🔗

## Overview 📚

SQL allows multiple joins to be combined in a **single query**.

Multiple joins can be **chained**, where the result of one join is joined with another table.

> **Multiple JOINs = Combine several tables in one query**

# 1. Chaining Multiple INNER JOINs

A second `INNER JOIN` can be added to the result of the first `INNER JOIN`.

### Basic Pattern

`SELECT ... FROM left_table INNER JOIN right_table ON left_table.id = right_table.id INNER JOIN third_table ON left_table.id = third_table.id;`

The second join follows the same basic syntax as the first join.

### Important

When writing the second `ON` condition, you can choose which table's field to use.

For example:

`ON left_table.id = third_table.id`

or:

`ON right_table.id = third_table.id`

The choice depends on which table contains the field that should be used for the second relationship.

# 2. World Leaders Example 🌍

The course uses the world leaders database containing:

- `presidents`
- `prime_ministers`
- `monarchs`
- `states`
- `prime_minister_terms`

The `prime_minister_terms` table contains:

- `prime_minister` → Prime minister name
- `pm_start` → Year the prime minister's term started

# 3. First JOIN

The first `INNER JOIN` connects:

`presidents`

with:

`prime_ministers`

using the `country` field.

### Concept

`presidents.country = prime_ministers.country`

This produces countries that have **both a president and a prime minister**.

The result of this first join can then be joined with another table.

# 4. Second JOIN

The result of the first `INNER JOIN` can be joined with:

`prime_minister_terms`

using the:

`prime_minister`

field.

### Concept

`prime_minister = prime_minister_terms.prime_minister`

This adds the year each prime minister assumed office.

### Result

The final result contains:

- Countries with both presidents and prime ministers.
- The corresponding prime ministers.
- The year each prime minister started their term.

# 5. Why the Number of Records Can Decrease 📉

The `prime_minister_terms` table contains **10 records**, but the final result contains only **4 records**.

This happens because `INNER JOIN` keeps only records that **match in both datasets**.

Therefore:

**10 prime minister term records**

→ Only **4 match** the result of the first join

→ Final result = **4 records**

> With multiple `INNER JOIN`s, records must continue to satisfy the matching conditions of each join to remain in the final result.

# 6. Chaining JOINs 🔗

Multiple joins can be chained as needed.

Conceptually:

`Table A → INNER JOIN Table B → INNER JOIN Table C → INNER JOIN Table D`

Each additional join follows the same pattern:

`INNER JOIN table ON matching_condition`

### Important

You can continue chaining joins and connect **as many tables as needed**, provided the relationships and join conditions are appropriate.

# 7. Multiple Joins with Aliases ✏️

Aliases can make multiple joins shorter and easier to read.

Example:

`FROM presidents AS p INNER JOIN prime_ministers AS pm ON p.country = pm.country INNER JOIN prime_minister_terms AS pmt ON pm.prime_minister = pmt.prime_minister`

Aliases:

- `p` → `presidents`
- `pm` → `prime_ministers`
- `pmt` → `prime_minister_terms`

This reduces repetition in the query.

# 8. Joining on Multiple Fields 🔑🔑

A join does not have to use only one field.

Sometimes one field is not enough to uniquely identify the matching records.

In this case, you can join using **multiple fields**.

### Example

Suppose two tables contain:

- `id`
- `date`

Instead of joining only on:

`ON left_table.id = right_table.id`

you can add another condition:

`ON left_table.id = right_table.id AND left_table.date = right_table.date`

This requires the records to match on **both**:

- `id`
- `date`

# 9. AND in the ON Clause

The `AND` keyword can be used inside the `ON` clause to add another join condition.

### Single-Key Join

`ON left_table.id = right_table.id`

Matches records based only on `id`.

### Multiple-Key Join

`ON left_table.id = right_table.id AND left_table.date = right_table.date`

Matches records only when:

`id` matches **AND** `date` matches.

### Key Concept

**Multiple join fields = All specified join conditions must match**

# 10. Why Join on Multiple Fields? 🧠

A single field may match multiple records in the other table.

For example:

`id`

might appear more than once in `right_table`.

Joining only on `id` could therefore return **multiple matching records**.

Adding another field such as `date` makes the matching condition more specific.

### Single Condition

`ON left_table.id = right_table.id`

→ Potentially multiple matches.

### Two Conditions

`ON left_table.id = right_table.id AND left_table.date = right_table.date`

→ Only records matching both `id` and `date`.

# 11. Multiple-Key Join Example 📅

Suppose:

### `left_table`

| id | date |
|---:|---|
| 1 | 2024-01-01 |
| 1 | 2024-01-02 |

### `right_table`

| id | date |
|---:|---|
| 1 | 2024-01-01 |
| 1 | 2024-01-03 |

Joining only on `id`:

`ON left_table.id = right_table.id`

can produce multiple matches because both tables contain `id = 1`.

Joining on both:

`ON left_table.id = right_table.id AND left_table.date = right_table.date`

only matches:

`id = 1 AND date = 2024-01-01`

# 12. Single-Key vs. Multiple-Key JOIN

| Join Type | Join Condition | Matching Requirement |
|---|---|---|
| **Single-key JOIN** | `ON A.id = B.id` | `id` must match |
| **Multiple-key JOIN** | `ON A.id = B.id AND A.date = B.date` | Both `id` and `date` must match |

# 13. Multiple JOINs vs. Multiple Join Keys 🧩

These are two different concepts.

### Multiple JOINs

Joining **more than two tables**.

Example:

`A INNER JOIN B ... INNER JOIN C ...`

### Multiple Join Keys

Using **more than one field** to determine whether records match.

Example:

`ON A.id = B.id AND A.date = B.date`

You can use both at the same time.

Example:

`A INNER JOIN B ON A.id = B.id AND A.date = B.date INNER JOIN C ON B.id = C.id`

# 14. Practical Query Structure 🎯

### Two Tables

`SELECT ... FROM table1 INNER JOIN table2 ON table1.field = table2.field;`

### Three Tables

`SELECT ... FROM table1 INNER JOIN table2 ON table1.field = table2.field INNER JOIN table3 ON table2.field = table3.field;`

### Multiple Join Fields

`SELECT ... FROM table1 INNER JOIN table2 ON table1.id = table2.id AND table1.date = table2.date;`

# 15. Exam / Interview Key Points 🎯

- SQL can combine **multiple joins in a single query**.
- Multiple `INNER JOIN`s can be **chained**.
- The result of one join can be joined with another table.
- Each additional join uses the same basic `INNER JOIN ... ON ...` structure.
- When chaining joins, the `ON` clause specifies how the new table should match the existing result.
- The field used for the second join can come from different tables involved in the previous join.
- The world leaders example first joins:
  - `presidents`
  - `prime_ministers`
- The result is then joined with:
  - `prime_minister_terms`
- The `prime_minister_terms` table contains:
  - `prime_minister`
  - `pm_start`
- `INNER JOIN` keeps only records that match the join condition.
- Multiple `INNER JOIN`s can reduce the final number of records because a record must match each join condition to remain in the result.
- Multiple joins can be continued as needed.
- Table aliases can simplify queries with multiple joins.
- A join can use **multiple fields**.
- `AND` can be added to the `ON` clause to require multiple fields to match.
- Joining on multiple fields can prevent unwanted multiple matches when one field alone is not sufficient.
- A common additional join field is `date`.
- Multiple join fields require **all specified conditions to match**.

# Quick Memory Aid 🚀

**Multiple JOINs = More tables**

**Multiple Join Keys = More matching conditions**

### Chained JOIN

`A → JOIN B → JOIN C`

### Multiple Join Fields

`ON A.id = B.id AND A.date = B.date`

### INNER JOIN Rule

**Only matching records survive the join.**

### World Leaders Example

`presidents → prime_ministers → prime_minister_terms`

# Most Important Concept ⭐

> **Multiple `INNER JOIN`s can be chained together to combine several tables in one query. Each join uses an `ON` condition to determine matching records. A join can also use multiple fields by adding `AND` conditions to the `ON` clause, requiring all specified fields to match and making the join more precise.**
