# 🪟 Window Functions in SQL

## 1. Window Functions

Great job! You now have experience transforming data using:

- Simple subqueries
- Correlated subqueries
- Common Table Expressions (CTEs)

The next technique is **window functions**, which provide another way to perform calculations while keeping the original rows of your result set.

---

## 2. Working with Aggregate Values

### ⚠️ The limitation of aggregate functions

When using aggregate functions such as:

- `AVG()`
- `SUM()`
- `COUNT()`
- `MIN()`
- `MAX()`

SQL normally requires you to use `GROUP BY` when retrieving additional non-aggregate columns.

For example:

    SELECT
        season,
        AVG(home_goal)
    FROM match;

This can produce an error because `season` is not aggregated and is not included in a `GROUP BY`.

You would normally need:

    SELECT
        season,
        AVG(home_goal)
    FROM match
    GROUP BY season;

### The problem

Grouping changes the level of detail of the result.

Instead of keeping every match, the result becomes one row per season.

This means that you cannot easily do something like:

> Show every match and compare each match's goals with the overall average goals.

You need a technique that can calculate an aggregate value **without collapsing the rows**.

That is where window functions come in.

---

# 3. Introducing Window Functions! 🪟

A **window function** performs a calculation on a result set that has already been generated.

This result set is called a **window**.

### What makes window functions useful?

Window functions allow you to perform calculations such as:

- Aggregate calculations without `GROUP BY`
- Running totals
- Rankings
- Moving averages
- Comparisons between rows
- Other calculations across related rows

### Key advantage

A normal aggregate function can reduce multiple rows into fewer rows.

A window function can calculate across multiple rows **while keeping the original rows**.

### Example

Normal aggregate:

    SELECT
        AVG(home_goal)
    FROM match;

Returns one value.

Window function:

    SELECT
        home_goal,
        AVG(home_goal) OVER ()
    FROM match;

Returns every match's `home_goal` plus the overall average.

### Mental model

Think of it this way:

    Aggregate function + GROUP BY
    → summarize rows

    Window function + OVER
    → calculate across rows while keeping the rows

---

# 4. What's a Window Function?

Let's revisit a problem from an earlier chapter:

> **How many goals were scored in each match in 2011/2012, and how did that compare to the average?**

A previous solution used a **subquery in `SELECT`**.

For example:

    SELECT
        date,
        home_goal,
        away_goal,
        (
            SELECT AVG(home_goal + away_goal)
            FROM match
            WHERE season = '2011/2012'
        ) AS overall_avg
    FROM match
    WHERE season = '2011/2012';

### What does the subquery do?

The subquery:

    SELECT AVG(home_goal + away_goal)
    FROM match
    WHERE season = '2011/2012'

calculates one overall average.

That value is then displayed alongside every match.

The important point is that the main query still returns individual matches.

---

# 5. What's a Window Function?

The same result can be generated using a window function.

The key part is the **`OVER()` clause**.

Instead of using a subquery:

    SELECT AVG(home_goal + away_goal)
    FROM match
    WHERE season = '2011/2012'

we can use:

    AVG(home_goal + away_goal) OVER ()

Example:

    SELECT
        date,
        home_goal,
        away_goal,
        AVG(home_goal + away_goal) OVER () AS overall_avg
    FROM match
    WHERE season = '2011/2012';

### Understanding `OVER()`

The `OVER()` clause tells SQL:

> Perform this calculation across the existing result set without grouping the rows.

The result still contains every match.

For example:

| date | home_goal | away_goal | overall_avg |
|---|---:|---:|---:|
| Match 1 | 2 | 1 | 2.7 |
| Match 2 | 3 | 2 | 2.7 |
| Match 3 | 1 | 1 | 2.7 |
| Match 4 | 4 | 2 | 2.7 |

The average is calculated across the result set and then shown on every row.

### Basic syntax

    AGGREGATE_FUNCTION(column) OVER ()

Examples:

    AVG(home_goal) OVER ()

    SUM(home_goal) OVER ()

    COUNT(*) OVER ()

    MAX(home_goal) OVER ()

    MIN(home_goal) OVER ()

### 🧠 Mental model

    AVG() 
        ↓
    OVER()
        ↓
    Calculate across the existing result set
        ↓
    Keep every original row

---

# 6. Generate a RANK 📊

Window functions can do more than aggregate calculations.

Another useful window function is:

    RANK()

A `RANK()` function creates a ranking based on a column that you specify.

For example, suppose we want to rank matches based on the **number of goals scored**.

First, calculate total goals:

    home_goal + away_goal

Then rank the matches according to that value.

---

# 7. Generate a RANK

The basic syntax is:

    RANK() OVER (
        ORDER BY column
    )

Example:

    SELECT
        date,
        home_goal,
        away_goal,
        RANK() OVER (
            ORDER BY home_goal + away_goal
        ) AS goals_rank
    FROM match;

### How it works

The window function:

    RANK() OVER (
        ORDER BY home_goal + away_goal
    )

does two things:

1. `RANK()` creates the ranking.
2. `ORDER BY` tells SQL what value to use for ranking.

By default, the ranking is:

    ASC

meaning:

    smallest → largest

### Example

If the total goals are:

| Total Goals |
|---:|
| 1 |
| 2 |
| 3 |
| 4 |
| 5 |

The ranking is:

| Total Goals | Rank |
|---:|---:|
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |

---

# 8. Generate a RANK — Descending Order

For football matches, ranking the smallest number of goals first may not be very useful.

We may instead want:

> Which matches had the most goals?

Use `DESC` inside the window's `ORDER BY`.

    SELECT
        date,
        home_goal,
        away_goal,
        RANK() OVER (
            ORDER BY home_goal + away_goal DESC
        ) AS goals_rank
    FROM match;

### `DESC`

`DESC` reverses the ranking:

    largest → smallest

Example:

| Total Goals | Rank |
|---:|---:|
| 6 | 1 |
| 5 | 2 |
| 4 | 3 |
| 3 | 4 |
| 2 | 5 |

### ⚠️ Important: Ties

`RANK()` automatically gives the same rank to identical values.

For example:

| Total Goals | Rank |
|---:|---:|
| 6 | 1 |
| 6 | 1 |
| 5 | 3 |
| 4 | 4 |

Notice what happens:

    6 → Rank 1
    6 → Rank 1
    5 → Rank 3

There is no Rank 2.

This is because `RANK()` skips the next ranking position after a tie.

### Example

If two rows tie for Rank 1:

    1
    1
    3

The next rank is `3`, not `2`.

### 🧠 Mental model

    RANK()
        ↓
    ORDER BY value DESC
        ↓
    Highest value = Rank 1
        ↓
    Tied values receive the same rank
        ↓
    Next rank is skipped

---

# 9. Key Differences

There are several important things to remember about window functions.

## 9.1 Window functions work on the result set

Window functions are processed after the query has produced its result set, with the final `ORDER BY` being applied later in the logical processing order.

This means the window function operates on the rows available to it from the query result.

### Example

    SELECT
        date,
        home_goal,
        away_goal,
        RANK() OVER (
            ORDER BY home_goal + away_goal DESC
        ) AS goals_rank
    FROM match;

Conceptually:

    FROM
      ↓
    WHERE
      ↓
    SELECT / result generation
      ↓
    Window function calculation
      ↓
    Final ORDER BY

The exact internal execution can vary by database optimizer, but the important concept is:

> **Window functions calculate across the rows of the query result without collapsing those rows.**

---

## 9.2 Window functions do not require GROUP BY

This is one of their biggest advantages.

### Aggregate with GROUP BY

    SELECT
        season,
        AVG(home_goal)
    FROM match
    GROUP BY season;

Result:

    One row per season

### Window function

    SELECT
        season,
        home_goal,
        AVG(home_goal) OVER ()
    FROM match;

Result:

    Every original row
    +
    The calculated average

### 🧠 Remember

    GROUP BY
    → collapses rows

    OVER()
    → keeps rows

---

## 9.3 Window functions can perform different calculations

Window functions can be used for:

### Aggregates

    AVG(value) OVER ()

    SUM(value) OVER ()

    COUNT(*) OVER ()

    MIN(value) OVER ()

    MAX(value) OVER ()

### Rankings

    RANK() OVER (
        ORDER BY value DESC
    )

Other common ranking functions include:

    ROW_NUMBER()

    DENSE_RANK()

---

## 9.4 Database support

Window functions are supported by many modern relational database systems, including:

- PostgreSQL
- Oracle
- MySQL

SQLite also supports window functions in modern versions, so the important point is to check the specific version of the database system you are using rather than assuming SQLite universally lacks them.

---

# 10. Subquery vs. Window Function

The same problem can often be solved using either a subquery or a window function.

## Using a SELECT subquery

    SELECT
        date,
        home_goal,
        away_goal,
        (
            SELECT AVG(home_goal + away_goal)
            FROM match
            WHERE season = '2011/2012'
        ) AS overall_avg
    FROM match
    WHERE season = '2011/2012';

## Using a window function

    SELECT
        date,
        home_goal,
        away_goal,
        AVG(home_goal + away_goal) OVER () AS overall_avg
    FROM match
    WHERE season = '2011/2012';

### Comparison

| Technique | Main purpose | Keeps original rows? |
|---|---|---|
| `GROUP BY` | Summarize groups | ❌ Usually no |
| SELECT subquery | Add a calculated value | ✅ Yes |
| Window function | Calculate across rows | ✅ Yes |

### 🧠 Simple rule

If you want to:

> **Calculate something across rows while keeping every row**

think:

    WINDOW FUNCTION
    +
    OVER()

---

# 🧩 Window Function Syntax Cheat Sheet

## Basic aggregate window function

    AGGREGATE_FUNCTION(column) OVER ()

Example:

    AVG(home_goal) OVER ()

---

## Window function with ordering

    FUNCTION() OVER (
        ORDER BY column
    )

Example:

    RANK() OVER (
        ORDER BY home_goal DESC
    )

---

## Ranking from highest to lowest

    RANK() OVER (
        ORDER BY value DESC
    )

---

## Ranking from lowest to highest

    RANK() OVER (
        ORDER BY value ASC
    )

---

# 🔑 Key Takeaways

1. **Window functions calculate across rows without grouping them together.**

2. The **`OVER()` clause** is the defining part of a window function.

3. Window functions can perform aggregate calculations such as:

       AVG()
       SUM()
       COUNT()
       MIN()
       MAX()

4. Window functions can also generate rankings:

       RANK()
       ROW_NUMBER()
       DENSE_RANK()

5. `GROUP BY` summarizes rows and usually reduces the number of rows.

6. Window functions keep the original rows while adding calculated information.

7. `RANK()` assigns the same rank to tied values and skips subsequent ranking numbers.

8. Use `DESC` when you want the highest values to receive Rank 1.

9. Window functions are especially useful for:
   - Rankings
   - Running totals
   - Moving averages
   - Overall averages
   - Comparisons against group or overall values
   - Calculations that should preserve row-level detail

---

# 🧠 Quick Mental Model

Think of SQL techniques like this:

    GROUP BY
    → "Summarize these rows."

    SELECT subquery
    → "Calculate one value and show it beside my rows."

    WINDOW FUNCTION
    → "Calculate across these rows but keep every row."

    RANK()
    → "Number these rows according to a value."

    OVER()
    → "Define the set of rows used by the window calculation."

---

# 🚀 Let's Practice!

The next exercises will focus on simple window functions using the `OVER()` clause.

Key syntax to remember:

    FUNCTION() OVER ()

For ranking:

    RANK() OVER (
        ORDER BY column DESC
    )

### ⭐ Most important concept

> **Window functions allow you to calculate across rows without losing the individual rows.**
