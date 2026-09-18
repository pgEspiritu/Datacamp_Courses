# 🗄️ SQL Courses — Cheatsheet & Sample Queries

> A practical SQL reference covering the core concepts, syntax, operators, filtering, sorting, aggregation, grouping, joins, and common SQL patterns.

---

# 📌 1. What is SQL?

**SQL (Structured Query Language)** is a language used to work with **relational databases**.

SQL can be used to:

* 🔎 Retrieve data
* ➕ Insert data
* ✏️ Update data
* 🗑️ Delete data
* 🏗️ Create tables
* 🔄 Transform data
* 📊 Aggregate and summarize data
* 🔗 Combine data from multiple tables

### SQL and Data Roles

| Role              | Common SQL Usage                              |
| ----------------- | --------------------------------------------- |
| 👷 Data Engineer  | Create, modify, transform, and manage data    |
| 📊 Data Scientist | Retrieve, filter, aggregate, and analyze data |

---

# 📋 2. Sample Database

The examples below use a fictional music-streaming database called **Spotflix**.

## `songs`

| song_id | title    | artist | genre | duration |
| ------: | -------- | ------ | ----- | -------: |
|       1 | Sunrise  | Luna   | Pop   |      210 |
|       2 | Midnight | Echo   | Rock  |      245 |
|       3 | Waves    | Luna   | Pop   |      198 |
|       4 | Fire     | Nova   | Rock  |      220 |
|       5 | Dreamer  | Echo   | Jazz  |      260 |

## `users`

| user_id | name  | country     | age |
| ------: | ----- | ----------- | --: |
|     101 | Ana   | Philippines |  25 |
|     102 | Ben   | Philippines |  31 |
|     103 | Carla | Japan       |  28 |
|     104 | David | USA         |  35 |
|     105 | Ella  | Japan       |  22 |

## `plays`

| play_id | user_id | song_id | play_count |
| ------: | ------: | ------: | ---------: |
|       1 |     101 |       1 |         10 |
|       2 |     101 |       2 |          5 |
|       3 |     102 |       1 |         15 |
|       4 |     103 |       3 |          8 |
|       5 |     104 |       4 |         20 |
|       6 |     105 |       5 |         12 |
|       7 |     102 |       3 |          7 |

---

# 🔎 3. SELECT

`SELECT` specifies which columns you want to retrieve.

## Select specific columns

```sql
SELECT title, artist
FROM songs;
```

### Output

| title    | artist |
| -------- | ------ |
| Sunrise  | Luna   |
| Midnight | Echo   |
| Waves    | Luna   |
| Fire     | Nova   |
| Dreamer  | Echo   |

---

## Select all columns

```sql
SELECT *
FROM songs;
```

### Output

| song_id | title    | artist | genre | duration |
| ------: | -------- | ------ | ----- | -------: |
|       1 | Sunrise  | Luna   | Pop   |      210 |
|       2 | Midnight | Echo   | Rock  |      245 |
|       3 | Waves    | Luna   | Pop   |      198 |
|       4 | Fire     | Nova   | Rock  |      220 |
|       5 | Dreamer  | Echo   | Jazz  |      260 |

### 💡 Remember

```text
SELECT = What do I want to see?
FROM   = Where does the data come from?
```

---

# 🎯 4. DISTINCT

`DISTINCT` returns unique values.

```sql
SELECT DISTINCT genre
FROM songs;
```

### Output

| genre |
| ----- |
| Pop   |
| Rock  |
| Jazz  |

Without `DISTINCT`, repeated genres would appear multiple times.

---

# 🔍 5. WHERE

`WHERE` filters rows based on a condition.

```sql
SELECT *
FROM songs
WHERE genre = 'Pop';
```

### Output

| song_id | title   | artist | genre | duration |
| ------: | ------- | ------ | ----- | -------: |
|       1 | Sunrise | Luna   | Pop   |      210 |
|       3 | Waves   | Luna   | Pop   |      198 |

---

# ⚖️ 6. Comparison Operators

| Operator | Meaning               | Example     |
| -------- | --------------------- | ----------- |
| `=`      | Equal to              | `age = 25`  |
| `<>`     | Not equal to          | `age <> 25` |
| `!=`     | Not equal to          | `age != 25` |
| `>`      | Greater than          | `age > 25`  |
| `<`      | Less than             | `age < 25`  |
| `>=`     | Greater than or equal | `age >= 25` |
| `<=`     | Less than or equal    | `age <= 25` |

### Example

```sql
SELECT title, duration
FROM songs
WHERE duration > 220;
```

### Output

| title    | duration |
| -------- | -------: |
| Midnight |      245 |
| Dreamer  |      260 |

---

# 🔗 7. AND

`AND` requires **all conditions** to be true.

```sql
SELECT *
FROM songs
WHERE genre = 'Pop'
  AND duration > 200;
```

### Output

| song_id | title   | artist | genre | duration |
| ------: | ------- | ------ | ----- | -------: |
|       1 | Sunrise | Luna   | Pop   |      210 |

---

# ➕ 8. OR

`OR` requires at least **one condition** to be true.

```sql
SELECT *
FROM songs
WHERE genre = 'Pop'
   OR genre = 'Jazz';
```

### Output

| song_id | title   | artist | genre | duration |
| ------: | ------- | ------ | ----- | -------: |
|       1 | Sunrise | Luna   | Pop   |      210 |
|       3 | Waves   | Luna   | Pop   |      198 |
|       5 | Dreamer | Echo   | Jazz  |      260 |

---

# 🚫 9. NOT

`NOT` reverses a condition.

```sql
SELECT *
FROM songs
WHERE NOT genre = 'Pop';
```

### Output

| song_id | title    | artist | genre | duration |
| ------: | -------- | ------ | ----- | -------: |
|       2 | Midnight | Echo   | Rock  |      245 |
|       4 | Fire     | Nova   | Rock  |      220 |
|       5 | Dreamer  | Echo   | Jazz  |      260 |

---

# 📏 10. BETWEEN

`BETWEEN` checks whether a value falls within a range.

```sql
SELECT *
FROM songs
WHERE duration BETWEEN 200 AND 250;
```

### Output

| song_id | title    | artist | genre | duration |
| ------: | -------- | ------ | ----- | -------: |
|       1 | Sunrise  | Luna   | Pop   |      210 |
|       2 | Midnight | Echo   | Rock  |      245 |
|       4 | Fire     | Nova   | Rock  |      220 |

> `BETWEEN` is inclusive of both endpoints.

---

# 📋 11. IN

`IN` checks whether a value matches one of several values.

```sql
SELECT *
FROM songs
WHERE genre IN ('Pop', 'Jazz');
```

### Output

| song_id | title   | artist | genre | duration |
| ------: | ------- | ------ | ----- | -------: |
|       1 | Sunrise | Luna   | Pop   |      210 |
|       3 | Waves   | Luna   | Pop   |      198 |
|       5 | Dreamer | Echo   | Jazz  |      260 |

Instead of:

```sql
WHERE genre = 'Pop'
   OR genre = 'Jazz'
```

you can use:

```sql
WHERE genre IN ('Pop', 'Jazz')
```

---

# 🔤 12. LIKE

`LIKE` is used for pattern matching.

## Starts with

```sql
SELECT *
FROM songs
WHERE title LIKE 'S%';
```

### Output

| song_id | title   | artist | genre | duration |
| ------: | ------- | ------ | ----- | -------: |
|       1 | Sunrise | Luna   | Pop   |      210 |

## Contains

```sql
SELECT *
FROM songs
WHERE title LIKE '%i%';
```

### Output

| song_id | title    | artist | genre | duration |
| ------: | -------- | ------ | ----- | -------: |
|       2 | Midnight | Echo   | Rock  |      245 |
|       4 | Fire     | Nova   | Rock  |      220 |

### Wildcards

| Wildcard | Meaning                 |
| -------- | ----------------------- |
| `%`      | Zero or more characters |
| `_`      | Exactly one character   |

Example:

```sql
WHERE title LIKE 'S%'
```

means the title **starts with S**.

---

# ↕️ 13. ORDER BY

`ORDER BY` sorts the result.

## Ascending

```sql
SELECT title, duration
FROM songs
ORDER BY duration ASC;
```

### Output

| title    | duration |
| -------- | -------: |
| Waves    |      198 |
| Sunrise  |      210 |
| Fire     |      220 |
| Midnight |      245 |
| Dreamer  |      260 |

`ASC` = ascending.

---

## Descending

```sql
SELECT title, duration
FROM songs
ORDER BY duration DESC;
```

### Output

| title    | duration |
| -------- | -------: |
| Dreamer  |      260 |
| Midnight |      245 |
| Fire     |      220 |
| Sunrise  |      210 |
| Waves    |      198 |

`DESC` = descending.

---

# 🔢 14. LIMIT

`LIMIT` restricts the number of rows returned.

```sql
SELECT *
FROM songs
ORDER BY duration DESC
LIMIT 3;
```

### Output

| song_id | title    | artist | genre | duration |
| ------: | -------- | ------ | ----- | -------: |
|       5 | Dreamer  | Echo   | Jazz  |      260 |
|       2 | Midnight | Echo   | Rock  |      245 |
|       4 | Fire     | Nova   | Rock  |      220 |

---

# 🧮 15. Aggregate Functions

Aggregate functions calculate a value from multiple rows.

| Function  | Purpose           |
| --------- | ----------------- |
| `COUNT()` | Count rows/values |
| `SUM()`   | Add values        |
| `AVG()`   | Calculate average |
| `MIN()`   | Find minimum      |
| `MAX()`   | Find maximum      |

---

## COUNT()

```sql
SELECT COUNT(*) AS total_songs
FROM songs;
```

### Output

| total_songs |
| ----------: |
|           5 |

---

## COUNT(column)

```sql
SELECT COUNT(artist) AS artists_recorded
FROM songs;
```

### Output

| artists_recorded |
| ---------------: |
|                5 |

### ⚠️ Important

```sql
COUNT(*)
```

counts **rows**.

```sql
COUNT(column)
```

counts **non-NULL values** in that column.

Therefore:

```text
COUNT(*) ≠ COUNT(column)
```

when the column contains `NULL` values.

---

# ➕ 16. SUM()

```sql
SELECT SUM(play_count) AS total_plays
FROM plays;
```

### Output

| total_plays |
| ----------: |
|          77 |

---

# 📊 17. AVG()

```sql
SELECT AVG(play_count) AS average_plays
FROM plays;
```

### Output

| average_plays |
| ------------: |
|          11.0 |

---

# ⬆️ 18. MIN() and MAX()

```sql
SELECT
    MIN(duration) AS shortest_song,
    MAX(duration) AS longest_song
FROM songs;
```

### Output

| shortest_song | longest_song |
| ------------: | -----------: |
|           198 |          260 |

---

# 🏷️ 19. AS — Aliases

`AS` gives a column or table a temporary name.

```sql
SELECT
    title AS song_title,
    duration AS duration_seconds
FROM songs;
```

### Output

| song_title | duration_seconds |
| ---------- | ---------------: |
| Sunrise    |              210 |
| Midnight   |              245 |
| Waves      |              198 |
| Fire       |              220 |
| Dreamer    |              260 |

---

# 📦 20. GROUP BY

`GROUP BY` groups rows with the same value.

### Count songs per genre

```sql
SELECT
    genre,
    COUNT(*) AS number_of_songs
FROM songs
GROUP BY genre;
```

### Output

| genre | number_of_songs |
| ----- | --------------: |
| Jazz  |               1 |
| Pop   |               2 |
| Rock  |               2 |

---

# 📊 21. GROUP BY with SUM()

```sql
SELECT
    user_id,
    SUM(play_count) AS total_plays
FROM plays
GROUP BY user_id;
```

### Output

| user_id | total_plays |
| ------: | ----------: |
|     101 |          15 |
|     102 |          22 |
|     103 |           8 |
|     104 |          20 |
|     105 |          12 |

---

# 📊 22. GROUP BY with AVG()

```sql
SELECT
    genre,
    AVG(duration) AS average_duration
FROM songs
GROUP BY genre;
```

### Output

| genre | average_duration |
| ----- | ---------------: |
| Jazz  |            260.0 |
| Pop   |            204.0 |
| Rock  |            232.5 |

---

# 🎯 23. HAVING

`HAVING` filters **groups** after `GROUP BY`.

### Example

```sql
SELECT
    genre,
    COUNT(*) AS number_of_songs
FROM songs
GROUP BY genre
HAVING COUNT(*) >= 2;
```

### Output

| genre | number_of_songs |
| ----- | --------------: |
| Pop   |               2 |
| Rock  |               2 |

### ⭐ WHERE vs HAVING

| Clause   | Filters                   |
| -------- | ------------------------- |
| `WHERE`  | Individual rows           |
| `HAVING` | Groups/aggregated results |

### Remember

```text
WHERE  → before grouping
GROUP BY → create groups
HAVING → filter groups
```

---

# 🔗 24. INNER JOIN

A `JOIN` combines data from multiple tables.

### Example

Get each user's name and the songs they played.

```sql
SELECT
    users.name,
    plays.song_id,
    plays.play_count
FROM users
INNER JOIN plays
    ON users.user_id = plays.user_id;
```

### Output

| name  | song_id | play_count |
| ----- | ------: | ---------: |
| Ana   |       1 |         10 |
| Ana   |       2 |          5 |
| Ben   |       1 |         15 |
| Carla |       3 |          8 |
| David |       4 |         20 |
| Ella  |       5 |         12 |
| Ben   |       3 |          7 |

---

# 🔗 25. JOIN Three Tables

You can join more than two tables.

```sql
SELECT
    users.name,
    songs.title,
    plays.play_count
FROM plays
INNER JOIN users
    ON plays.user_id = users.user_id
INNER JOIN songs
    ON plays.song_id = songs.song_id;
```

### Output

| name  | title    | play_count |
| ----- | -------- | ---------: |
| Ana   | Sunrise  |         10 |
| Ana   | Midnight |          5 |
| Ben   | Sunrise  |         15 |
| Carla | Waves    |          8 |
| David | Fire     |         20 |
| Ella  | Dreamer  |         12 |
| Ben   | Waves    |          7 |

---

# 👈 26. LEFT JOIN

`LEFT JOIN` returns **all rows from the left table**, even when there is no matching row in the right table.

```sql
SELECT
    users.name,
    plays.play_count
FROM users
LEFT JOIN plays
    ON users.user_id = plays.user_id;
```

If a user has no play record, that user's `play_count` would appear as `NULL`.

### Concept

```text
LEFT TABLE              RIGHT TABLE

ALL rows       +        matching rows
```

---

# ❌ 27. NULL

`NULL` means the value is **missing/unknown**.

Do **not** use:

```sql
WHERE column = NULL
```

Use:

```sql
WHERE column IS NULL
```

### Find missing values

```sql
SELECT *
FROM songs
WHERE artist IS NULL;
```

### Find non-missing values

```sql
SELECT *
FROM songs
WHERE artist IS NOT NULL;
```

---

# 🔄 28. CASE

`CASE` allows conditional logic.

```sql
SELECT
    title,
    duration,
    CASE
        WHEN duration < 200 THEN 'Short'
        WHEN duration <= 240 THEN 'Medium'
        ELSE 'Long'
    END AS song_length
FROM songs;
```

### Output

| title    | duration | song_length |
| -------- | -------: | ----------- |
| Sunrise  |      210 | Medium      |
| Midnight |      245 | Long        |
| Waves    |      198 | Short       |
| Fire     |      220 | Medium      |
| Dreamer  |      260 | Long        |

---

# 🧮 29. Calculated Columns

You can perform calculations directly in a query.

```sql
SELECT
    title,
    duration,
    duration / 60.0 AS duration_minutes
FROM songs;
```

### Output

| title    | duration | duration_minutes |
| -------- | -------: | ---------------: |
| Sunrise  |      210 |             3.50 |
| Midnight |      245 |             4.08 |
| Waves    |      198 |             3.30 |
| Fire     |      220 |             3.67 |
| Dreamer  |      260 |             4.33 |

---

# 🏷️ 30. String Functions

Common string functions include:

| Function   | Purpose                   |
| ---------- | ------------------------- |
| `UPPER()`  | Convert to uppercase      |
| `LOWER()`  | Convert to lowercase      |
| `LENGTH()` | Count characters          |
| `TRIM()`   | Remove surrounding spaces |
| `CONCAT()` | Combine strings           |

### Example

```sql
SELECT
    name,
    UPPER(name) AS uppercase_name
FROM users;
```

### Output

| name  | uppercase_name |
| ----- | -------------- |
| Ana   | ANA            |
| Ben   | BEN            |
| Carla | CARLA          |
| David | DAVID          |
| Ella  | ELLA           |

---

# 📅 31. Date Filtering

For a table containing dates, you can filter using comparison operators.

Example table: `service_requests`

| request_id | office_code | request_date | status |
| ---------: | ----------- | ------------ | ------ |
|          1 | O1          | 2026-01-05   | Closed |
|          2 | O2          | 2026-01-10   | Open   |
|          3 | O1          | 2026-02-15   | Closed |
|          4 | O3          | 2026-03-01   | Open   |
|          5 | O2          | 2026-03-20   | Closed |

### Query

```sql
SELECT *
FROM service_requests
WHERE request_date >= '2026-02-01';
```

### Output

| request_id | office_code | request_date | status |
| ---------: | ----------- | ------------ | ------ |
|          3 | O1          | 2026-02-15   | Closed |
|          4 | O3          | 2026-03-01   | Open   |
|          5 | O2          | 2026-03-20   | Closed |

---

# 🧠 32. SQL Query Order

Even though SQL is written like this:

```sql
SELECT ...
FROM ...
WHERE ...
GROUP BY ...
HAVING ...
ORDER BY ...
LIMIT ...
```

a useful logical processing order is:

```text
1. FROM
2. JOIN
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. ORDER BY
8. LIMIT
```

### ⭐ Memorize this

```text
FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
```

---

# 🧩 33. Complete Query Example

### Question

> Which genres have at least two songs, and what is their average duration?

```sql
SELECT
    genre,
    COUNT(*) AS number_of_songs,
    AVG(duration) AS average_duration
FROM songs
GROUP BY genre
HAVING COUNT(*) >= 2
ORDER BY average_duration DESC;
```

### Output

| genre | number_of_songs | average_duration |
| ----- | --------------: | ---------------: |
| Rock  |               2 |            232.5 |
| Pop   |               2 |            204.0 |

---

# 🏢 34. Practical Service Request Example

For data-analysis work, a table might look like this:

## `service_requests`

| request_id | office_code | status | processing_days |
| ---------: | ----------- | ------ | --------------: |
|          1 | O1          | Closed |               3 |
|          2 | O1          | Closed |               5 |
|          3 | O1          | Open   |               2 |
|          4 | O2          | Closed |               7 |
|          5 | O2          | Closed |               4 |
|          6 | O2          | Open   |               3 |
|          7 | O3          | Closed |               6 |

### Count requests per office

```sql
SELECT
    office_code,
    COUNT(*) AS n
FROM service_requests
GROUP BY office_code;
```

### Output

| office_code |  n |
| ----------- | -: |
| O1          |  3 |
| O2          |  3 |
| O3          |  1 |

---

# ⚠️ 35. Common SQL Mistake: Aggregate Function in WHERE

❌ Incorrect:

```sql
SELECT
    office_code,
    COUNT(*) AS n
FROM service_requests
WHERE COUNT(*) > 2
GROUP BY office_code;
```

`COUNT()` is an aggregate function and should not be used in `WHERE` for this purpose.

✅ Correct:

```sql
SELECT
    office_code,
    COUNT(*) AS n
FROM service_requests
GROUP BY office_code
HAVING COUNT(*) > 2;
```

### Output

| office_code |  n |
| ----------- | -: |
| O1          |  3 |
| O2          |  3 |

### ⭐ Rule

```text
WHERE  → filter rows
HAVING → filter aggregated groups
```

---

# 🔢 36. COUNT(*) vs COUNT(column)

Suppose we have:

## `employees`

| employee_id | name  | department |
| ----------: | ----- | ---------- |
|           1 | Ana   | IT         |
|           2 | Ben   | HR         |
|           3 | Carla | NULL       |
|           4 | David | IT         |

### COUNT(*)

```sql
SELECT COUNT(*) AS total_rows
FROM employees;
```

### Output

| total_rows |
| ---------: |
|          4 |

`COUNT(*)` counts **all rows**.

### COUNT(department)

```sql
SELECT COUNT(department) AS departments_recorded
FROM employees;
```

### Output

| departments_recorded |
| -------------------: |
|                    3 |

`COUNT(department)` ignores the `NULL` value.

---

# 🧠 37. SQL Cheat Sheet — Quick Reference

| Task                | SQL                               |
| ------------------- | --------------------------------- |
| Select columns      | `SELECT col FROM table;`          |
| Select everything   | `SELECT * FROM table;`            |
| Unique values       | `SELECT DISTINCT col FROM table;` |
| Filter rows         | `WHERE condition`                 |
| Multiple conditions | `AND`, `OR`, `NOT`                |
| Range               | `BETWEEN`                         |
| Multiple values     | `IN (...)`                        |
| Pattern matching    | `LIKE`                            |
| Missing value       | `IS NULL`                         |
| Non-missing value   | `IS NOT NULL`                     |
| Sort ascending      | `ORDER BY col ASC`                |
| Sort descending     | `ORDER BY col DESC`               |
| Limit results       | `LIMIT n`                         |
| Count               | `COUNT()`                         |
| Total               | `SUM()`                           |
| Average             | `AVG()`                           |
| Minimum             | `MIN()`                           |
| Maximum             | `MAX()`                           |
| Group records       | `GROUP BY`                        |
| Filter groups       | `HAVING`                          |
| Combine tables      | `JOIN`                            |
| Keep all left rows  | `LEFT JOIN`                       |
| Conditional logic   | `CASE`                            |
| Rename output       | `AS`                              |

---

# 🧪 38. SQL Query Templates

## Basic query

```sql
SELECT column1, column2
FROM table_name;
```

## Filter

```sql
SELECT *
FROM table_name
WHERE condition;
```

## Sort

```sql
SELECT *
FROM table_name
ORDER BY column_name DESC;
```

## Filter + sort

```sql
SELECT *
FROM table_name
WHERE condition
ORDER BY column_name DESC;
```

## Aggregate

```sql
SELECT
    COUNT(*) AS total
FROM table_name;
```

## Group

```sql
SELECT
    category,
    COUNT(*) AS total
FROM table_name
GROUP BY category;
```

## Group + filter

```sql
SELECT
    category,
    COUNT(*) AS total
FROM table_name
GROUP BY category
HAVING COUNT(*) > 10;
```

## Join

```sql
SELECT
    a.column1,
    b.column2
FROM table_a AS a
INNER JOIN table_b AS b
    ON a.id = b.id;
```

---

# 🎯 39. Quick Mental Model

When writing an SQL query, ask:

```text
1️⃣ What information do I need?
        ↓
2️⃣ Which table contains it?
        ↓
3️⃣ Which columns do I need?
        ↓
4️⃣ Do I need to filter rows?
        ↓
5️⃣ Do I need to combine tables?
        ↓
6️⃣ Do I need to group the data?
        ↓
7️⃣ Do I need to filter the groups?
        ↓
8️⃣ Do I need to sort the result?
        ↓
9️⃣ Do I need to limit the output?
```

This translates roughly into:

```sql
SELECT
FROM
JOIN
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT
```

---

# ⭐ 40. Most Important Rules to Remember

### Rule 1 — SELECT retrieves data

```sql
SELECT column
FROM table;
```

### Rule 2 — WHERE filters rows

```sql
WHERE condition
```

### Rule 3 — GROUP BY creates groups

```sql
GROUP BY column
```

### Rule 4 — HAVING filters groups

```sql
HAVING COUNT(*) > 10
```

### Rule 5 — COUNT(*) counts rows

```sql
COUNT(*)
```

### Rule 6 — COUNT(column) ignores NULL

```sql
COUNT(column)
```

### Rule 7 — NULL requires IS NULL

```sql
WHERE column IS NULL
```

### Rule 8 — JOIN connects related tables

```sql
JOIN table2
ON table1.id = table2.id
```

### Rule 9 — ORDER BY sorts

```sql
ORDER BY column DESC
```

### Rule 10 — SQL clauses have a logical processing order

```text
FROM
↓
JOIN
↓
WHERE
↓
GROUP BY
↓
HAVING
↓
SELECT
↓
ORDER BY
↓
LIMIT
```

---

# 🚀 41. One Complete Example

### Question

> Find the offices with more than two service requests, calculate their average processing time, and show the office with the highest average first.

```sql
SELECT
    office_code,
    COUNT(*) AS total_requests,
    AVG(processing_days) AS avg_processing_days
FROM service_requests
GROUP BY office_code
HAVING COUNT(*) > 2
ORDER BY avg_processing_days DESC;
```

### Output

| office_code | total_requests | avg_processing_days |
| ----------- | -------------: | ------------------: |
| O2          |              3 |                4.67 |
| O1          |              3 |                3.33 |

### What happened?

```text
FROM service_requests
        ↓
GROUP BY office_code
        ↓
COUNT(*) + AVG(processing_days)
        ↓
HAVING COUNT(*) > 2
        ↓
ORDER BY avg_processing_days DESC
        ↓
Final result
```

---

# 📌 SQL in One Page

```text
SELECT      → columns to retrieve
FROM        → table to retrieve from
JOIN        → combine tables
WHERE       → filter individual rows
GROUP BY    → create groups
HAVING      → filter groups
ORDER BY    → sort results
LIMIT       → restrict number of rows

COUNT()     → count
SUM()       → total
AVG()       → average
MIN()       → minimum
MAX()       → maximum

DISTINCT    → unique values
IN          → match a list
BETWEEN     → match a range
LIKE        → pattern matching
IS NULL     → missing values
CASE        → conditional logic
AS          → alias
```

## 🧠 Core SQL Pattern

```sql
SELECT
    column1,
    aggregate_function(column2) AS result
FROM table_name
JOIN another_table
    ON table_name.id = another_table.id
WHERE condition
GROUP BY column1
HAVING aggregate_function(column2) > value
ORDER BY result DESC
LIMIT 10;
```

> 💡 **The key to SQL is not memorizing every query. Learn to identify what the question is asking: retrieve → filter → combine → group → aggregate → filter groups → sort → limit.**
