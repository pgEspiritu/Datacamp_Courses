# Filtering Grouped Data with HAVING 🔍📊

## Overview 📚

SQL provides two different filtering clauses depending on **what you are filtering**:

- `WHERE` → Filters individual records **before grouping and aggregation**.
- `HAVING` → Filters groups **after grouping and aggregation**.

> **WHERE = Filter rows**

> **HAVING = Filter groups**

# 1. HAVING

`HAVING` is used when you need to filter based on the **result of an aggregate function**.

You cannot use `WHERE` to filter an aggregate result.

### Invalid Example ❌

`SELECT release_year, COUNT(title) AS title_count FROM films WHERE title_count > 10 GROUP BY release_year;`

This is invalid because `WHERE` is processed before the grouping and aggregation that produces `title_count`.

### Correct Example ✅

`SELECT release_year, COUNT(title) AS title_count FROM films GROUP BY release_year HAVING COUNT(title) > 10;`

This returns only the years in which **more than 10 films were released**.

# 2. Why HAVING Is Needed 🧠

Consider:

`COUNT(title)`

The count does not exist until SQL has:

1. Retrieved the records.
2. Grouped the records.
3. Performed the aggregation.

Therefore, filtering the aggregate result must happen **after aggregation**.

That is the purpose of `HAVING`.

### Concept

**WHERE → Filters rows before aggregation**

**HAVING → Filters groups after aggregation**

# 3. SQL Execution Order 🔄

The full simplified execution order covered so far is:

**FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT**

### Step-by-Step

1. `FROM` → Identify the source table.
2. `WHERE` → Filter individual records.
3. `GROUP BY` → Create groups.
4. `HAVING` → Filter the groups based on aggregate results.
5. `SELECT` → Select fields and create aliases.
6. `ORDER BY` → Sort the results.
7. `LIMIT` → Restrict the final number of rows.

## Example

`SELECT certification, COUNT(title) AS title_count FROM films WHERE certification IN ('G', 'PG', 'PG-13') GROUP BY certification HAVING COUNT(title) > 500 ORDER BY title_count DESC LIMIT 3;`

### Logical Processing

**FROM films**

→ Get the `films` table.

**WHERE certification IN ('G', 'PG', 'PG-13')**

→ Keep only films with these certifications.

**GROUP BY certification**

→ Create one group for each certification.

**HAVING COUNT(title) > 500**

→ Keep only groups containing more than 500 films.

**SELECT certification, COUNT(title) AS title_count**

→ Return the certification and the count.

**ORDER BY title_count DESC**

→ Sort by the count from highest to lowest.

**LIMIT 3**

→ Return only the top 3 results.

# 4. HAVING vs. WHERE ⚖️

| Clause | Filters | When It Runs |
|---|---|---|
| `WHERE` | Individual records/rows | Before `GROUP BY` |
| `HAVING` | Groups / aggregate results | After `GROUP BY` |

### WHERE Example

Question:

> What films were released in 2000?

Query:

`SELECT title FROM films WHERE release_year = 2000;`

There is no grouping or aggregation, so `WHERE` is appropriate.

### HAVING Example

Question:

> In what years was the average film duration over 2 hours?

This question requires:

- Grouping films by year.
- Calculating average duration per year.
- Filtering the resulting averages.

Therefore, `GROUP BY` and `HAVING` are required.

# 5. Translating a Business Question into SQL 🧩

## Question 1

> **What films were released in the year 2000?**

### Identify the Requirements

- Need film titles → `SELECT title`
- Source is films → `FROM films`
- Need only 2000 → `WHERE release_year = 2000`
- No grouping needed.

### Query

`SELECT title FROM films WHERE release_year = 2000;`

### Logic

**FROM → WHERE → SELECT**

# 6. Business Question Requiring HAVING 🎯

## Question 2

> **In what years was the average film duration over two hours?**

Break the question into pieces.

### Step 1 — What information do we need?

We need:

**Release year**

So:

`SELECT release_year`

### Step 2 — What calculation is required?

We need the **average film duration**.

Therefore:

`AVG(duration)`

### Step 3 — What needs to be filtered?

The question asks for years where:

**Average duration > 2 hours**

Since `AVG(duration)` is an aggregate result, we cannot filter it with `WHERE`.

Use:

`HAVING AVG(duration) > 120`

assuming duration is stored in minutes.

### Step 4 — Why GROUP BY?

We need the average duration **for each year**.

Therefore:

`GROUP BY release_year`

### Complete Query

`SELECT release_year, AVG(duration) AS average_duration FROM films GROUP BY release_year HAVING AVG(duration) > 120;`

### Logic

**FROM films**

→ Get all films.

**GROUP BY release_year**

→ Create one group for every release year.

**AVG(duration)**

→ Calculate the average duration within each year.

**HAVING AVG(duration) > 120**

→ Keep only years whose average duration exceeds 120 minutes.

**SELECT**

→ Return the release years and calculated averages.

# 7. Why GROUP BY Is Required 📌

Consider:

`SELECT release_year, AVG(duration) FROM films;`

This attempts to return:

- `release_year`
- An aggregate `AVG(duration)`

without telling SQL how the years should be grouped.

To calculate an average **per year**, we need:

`GROUP BY release_year`

Therefore:

`SELECT release_year, AVG(duration) FROM films GROUP BY release_year;`

Now SQL calculates one average duration for each release year.

# 8. Why HAVING Instead of WHERE? 🤔

This does not work:

`SELECT release_year, AVG(duration) FROM films WHERE AVG(duration) > 120 GROUP BY release_year;`

Why?

Because:

**WHERE is executed before GROUP BY and aggregation.**

At the point `WHERE` runs, the value of:

`AVG(duration)`

has not been calculated yet.

The correct approach is:

`SELECT release_year, AVG(duration) AS average_duration FROM films GROUP BY release_year HAVING AVG(duration) > 120;`

### Easy Rule

> **Filtering raw columns → `WHERE`**

> **Filtering aggregate results → `HAVING`**

# 9. HAVING and Aggregate Functions 📊

`HAVING` is especially useful with:

- `COUNT()`
- `AVG()`
- `SUM()`
- `MIN()`
- `MAX()`

### Examples

#### Count

`HAVING COUNT(title) > 10`

→ Keep groups with more than 10 titles.

#### Average

`HAVING AVG(duration) > 120`

→ Keep groups whose average duration exceeds 120 minutes.

#### Sum

`HAVING SUM(budget) > 1000000000`

→ Keep groups whose total budget exceeds 1 billion.

#### Minimum

`HAVING MIN(budget) > 100000`

→ Keep groups whose minimum budget is greater than 100,000.

#### Maximum

`HAVING MAX(budget) > 100000000`

→ Keep groups whose maximum budget exceeds 100 million.

# 10. HAVING and Aliases ⚠️

The lesson emphasizes an important difference between `HAVING` and `ORDER BY`.

Suppose:

`SELECT certification, COUNT(title) AS title_count FROM films GROUP BY certification HAVING title_count > 500 ORDER BY title_count DESC;`

The alias `title_count` is created in the `SELECT` clause.

Because of the logical execution order:

**HAVING occurs before SELECT**

the alias is **not yet available** to `HAVING`.

Therefore, use the aggregate expression directly:

`HAVING COUNT(title) > 500`

However, `ORDER BY` occurs **after SELECT**, so the alias can be used there:

`ORDER BY title_count DESC`

### Key Rule

**HAVING → Cannot generally use a SELECT alias**

**ORDER BY → Can use a SELECT alias**

# 11. WHERE + GROUP BY + HAVING + ORDER BY 🔗

These clauses often work together.

Example:

`SELECT certification, COUNT(title) AS title_count FROM films WHERE release_year >= 2000 GROUP BY certification HAVING COUNT(title) > 100 ORDER BY title_count DESC;`

### What This Does

1. `WHERE` removes films released before 2000.
2. `GROUP BY` creates groups by certification.
3. `COUNT(title)` counts films in each certification.
4. `HAVING` keeps certifications with more than 100 films.
5. `ORDER BY` sorts the results by count.

### Logic

**Filter rows → Group → Aggregate → Filter groups → Sort**

# 12. WHERE vs. HAVING Example 🧠

Suppose we want:

> Certifications with more than 500 films released from 2000 onward.

We need two different types of filtering:

### Row-Level Filter

`WHERE release_year >= 2000`

This filters individual films before grouping.

### Group-Level Filter

`HAVING COUNT(*) > 500`

This filters the certification groups after counting.

### Complete Query

`SELECT certification, COUNT(*) AS film_count FROM films WHERE release_year >= 2000 GROUP BY certification HAVING COUNT(*) > 500 ORDER BY film_count DESC;`

# 13. GROUP BY + HAVING Relationship 🔗

A common pattern is:

`SELECT group_field, AGGREGATE_FUNCTION(...) FROM table GROUP BY group_field HAVING AGGREGATE_FUNCTION(...) condition;`

Example:

`SELECT release_year, AVG(duration) AS average_duration FROM films GROUP BY release_year HAVING AVG(duration) > 120;`

### Pattern

**GROUP BY = Create groups**

**Aggregate = Calculate group summary**

**HAVING = Filter groups**

# 14. Practical Examples 🎯

## Years with More Than 10 Films

`SELECT release_year, COUNT(*) AS film_count FROM films GROUP BY release_year HAVING COUNT(*) > 10;`

## Certifications with More Than 500 Films

`SELECT certification, COUNT(*) AS film_count FROM films GROUP BY certification HAVING COUNT(*) > 500;`

## Years with Average Duration Above 120 Minutes

`SELECT release_year, AVG(duration) AS average_duration FROM films GROUP BY release_year HAVING AVG(duration) > 120;`

## Certifications with Average Budget Above 100 Million

`SELECT certification, AVG(budget) AS average_budget FROM films GROUP BY certification HAVING AVG(budget) > 100000000;`

## Filter Rows Before Grouping and Groups After Aggregation

`SELECT certification, COUNT(*) AS film_count FROM films WHERE release_year >= 2000 GROUP BY certification HAVING COUNT(*) > 100 ORDER BY film_count DESC;`

# 15. Common Mistakes ⚠️

### Mistake 1: Using WHERE to Filter an Aggregate

❌

`WHERE COUNT(*) > 10`

✅

`HAVING COUNT(*) > 10`

### Mistake 2: Using WHERE with AVG()

❌

`WHERE AVG(duration) > 120`

✅

`HAVING AVG(duration) > 120`

### Mistake 3: Forgetting GROUP BY

If the question asks for an aggregate **per group**, you need `GROUP BY`.

Example:

`AVG(duration) per release_year`

requires:

`GROUP BY release_year`

### Mistake 4: Using a SELECT Alias in HAVING

❌

`SELECT certification, COUNT(*) AS film_count FROM films GROUP BY certification HAVING film_count > 500;`

For the execution order covered here, `HAVING` happens before `SELECT`, so the alias is not available.

✅

`SELECT certification, COUNT(*) AS film_count FROM films GROUP BY certification HAVING COUNT(*) > 500;`

### Mistake 5: Confusing WHERE and HAVING

Ask:

**Am I filtering individual records or groups?**

- Individual records → `WHERE`
- Groups / aggregate results → `HAVING`

# 16. SQL Execution Order 🔄

### Written Query Order

A common query is written as:

`SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ... LIMIT ...;`

### Logical Execution Order

`FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT`

### Memory Flow

**Get data → Filter rows → Group → Filter groups → Select → Sort → Limit**

# 17. Exam / Interview Key Points 🎯

- `HAVING` is used to **filter grouped results**.
- `WHERE` filters **individual records**.
- `HAVING` is used when filtering based on an **aggregate result**.
- You cannot use `WHERE` to filter aggregate functions such as `COUNT()`, `AVG()`, or `SUM()`.
- `GROUP BY` usually comes before `HAVING`.
- `HAVING` comes after `GROUP BY`.
- The simplified SQL execution order is:

`FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT`

- `WHERE` runs before grouping and aggregation.
- `HAVING` runs after grouping and aggregation.
- A `SELECT` alias is generally not available to `HAVING` because `HAVING` is processed before `SELECT`.
- A `SELECT` alias can be used in `ORDER BY` because `ORDER BY` is processed after `SELECT`.
- `GROUP BY` is required when calculating an aggregate per group.
- `HAVING` can be used with:
  - `COUNT()`
  - `AVG()`
  - `SUM()`
  - `MIN()`
  - `MAX()`
- `WHERE` and `HAVING` can be used together:
  - `WHERE` filters rows first.
  - `HAVING` filters groups afterward.
- When solving business questions, break the question into:
  - What data is needed?
  - What rows need filtering?
  - What grouping is needed?
  - What aggregate is required?
  - Does the aggregate need filtering?
  - How should the result be sorted?

# Quick Memory Aid 🚀

**WHERE = Filter Rows**

**GROUP BY = Make Groups**

**HAVING = Filter Groups**

**SELECT = Choose / Calculate**

**ORDER BY = Sort**

**LIMIT = Restrict**

### SQL Flow

**FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT**

### Golden Rule ⭐

> **WHERE filters before aggregation; HAVING filters after aggregation.**

### Business Question Rule

> **"Which records..." → Usually `WHERE`**

> **"Which groups have an aggregate above/below..." → `GROUP BY` + `HAVING`**

# Most Important Concept ⭐

> **`WHERE` filters individual rows before grouping and aggregation, while `HAVING` filters groups after aggregation. Use `HAVING` whenever the condition depends on an aggregate such as `COUNT()`, `AVG()`, `SUM()`, `MIN()`, or `MAX()`. The simplified SQL execution order is `FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT`.**
