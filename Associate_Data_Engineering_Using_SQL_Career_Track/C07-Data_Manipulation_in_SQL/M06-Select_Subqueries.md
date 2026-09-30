# 📊 Subqueries in SELECT

## 🎯 Lesson Objective

So far, we have learned how to use subqueries in:

- `WHERE`
- `FROM`

Subqueries can also be placed inside the `SELECT` statement.

A subquery in `SELECT` is especially useful for:

- Bringing a summary value into detailed row-level data
- Comparing individual values against an overall value
- Performing calculations using an aggregate value
- Calculating differences from an average
- Avoiding manual calculations outside SQL

---

# 1. 🧠 What Are Subqueries in SELECT?

A subquery in `SELECT` is used to return a **single value** that can become a column in the query result.

General pattern:

    SELECT
        column1,
        (
            SELECT aggregate_function(column)
            FROM table
        ) AS summary_value
    FROM table;

The subquery produces one value, and that value can be displayed alongside every row in the main query.

---

# 2. 📌 Why Use a SELECT Subquery?

Normally, aggregate functions such as:

    COUNT()
    AVG()
    SUM()

are used with `GROUP BY` when you want one result per group.

But sometimes you want:

- Detailed rows
- Plus one overall summary value

For example:

    Match details + overall average goals

A `SELECT` subquery can provide that overall value.

---

# 3. 🔢 Example: Overall Number of Matches

Suppose we want to compare the number of matches played in each season with the **total number of matches across all seasons**.

First, calculate the overall number of matches:

    SELECT COUNT(*)
    FROM match;

This returns a single value.

In the lesson example, the overall count is:

    12,837

---

# 4. 📊 Add the Overall Count to a Query

Suppose we want the number of matches per season:

    SELECT
        season,
        COUNT(*) AS matches
    FROM match
    GROUP BY season;

This gives us a result such as:

| season | matches |
|---|---:|
| 2010/2011 | ... |
| 2011/2012 | ... |
| 2012/2013 | ... |
| 2013/2014 | ... |

But we can also add the overall match count using a subquery.

---

# 5. 💻 Subquery Inside SELECT

    SELECT
        season,
        COUNT(*) AS matches,
        (
            SELECT COUNT(*)
            FROM match
        ) AS total_matches
    FROM match
    GROUP BY season;

The subquery:

    (
        SELECT COUNT(*)
        FROM match
    )

returns one value:

    12,837

That value is then displayed alongside every season.

---

# 6. 📋 Conceptual Result

The result could look like:

| season | matches | total_matches |
|---|---:|---:|
| 2010/2011 | 380 | 12837 |
| 2011/2012 | 380 | 12837 |
| 2012/2013 | 380 | 12837 |
| 2013/2014 | 380 | 12837 |

The important observation is:

> The `total_matches` value is the same for every row because the subquery returns one overall value.

---

# 7. 🧠 Why Does the Same Value Appear on Every Row?

The subquery:

    SELECT COUNT(*)
    FROM match

does not depend on the individual season.

It calculates the overall count once and returns a single value.

The main query then places that value alongside each result row.

Think of it as:

    Main query:
    Season A → 380 matches
    Season B → 380 matches
    Season C → 380 matches

    Subquery:
    Overall → 12,837 matches

    Result:

    Season A → 380 → 12,837
    Season B → 380 → 12,837
    Season C → 380 → 12,837

---

# 8. ➗ SELECT Subqueries for Mathematical Calculations

A `SELECT` subquery can also be used in calculations.

For example, suppose we want to know:

> How much does a match's total goals differ from the overall average?

First, calculate total goals:

    home_goal + away_goal

Then calculate the overall average:

    SELECT AVG(home_goal + away_goal)
    FROM match

The lesson gives an overall average of approximately:

    2.72

---

# 9. 🧮 Calculate the Difference from the Average

We can subtract the overall average from each match's total goals.

    SELECT
        date,
        home_goal,
        away_goal,
        (home_goal + away_goal)
        -
        (
            SELECT AVG(home_goal + away_goal)
            FROM match
        ) AS difference
    FROM match;

The subquery produces one value:

    AVG(home_goal + away_goal)

The outer query subtracts that value from each match's total goals.

---

# 10. 📊 Example

Suppose the overall average is:

    2.72

And one match has:

    home_goal = 4
    away_goal = 1

Total goals:

    4 + 1 = 5

Difference:

    5 - 2.72 = 2.28

The match is therefore:

    2.28 goals above the overall average

---

# 11. 🧠 General Pattern for Mathematical Calculations

A SELECT subquery can be used inside an expression:

    SELECT
        column,
        column - (
            SELECT AVG(column)
            FROM table
        ) AS difference
    FROM table;

Other mathematical operations are also possible:

### Addition

    column + (SELECT ...)

### Subtraction

    column - (SELECT ...)

### Multiplication

    column * (SELECT ...)

### Division

    column / (SELECT ...)

---

# 12. 🎯 Example: 2011/2012 Average

An important point is that filters may need to appear in **both the main query and the subquery**.

Suppose we want to compare matches from the `2011/2012` season against the average for **that same season**.

The subquery should include:

    WHERE season = '2011/2012'

Example:

    SELECT
        date,
        home_goal,
        away_goal,
        (home_goal + away_goal)
        -
        (
            SELECT AVG(home_goal + away_goal)
            FROM match
            WHERE season = '2011/2012'
        ) AS difference
    FROM match
    WHERE season = '2011/2012';

---

# 13. ⚠️ Why Does the Subquery Need Its Own WHERE?

The subquery is evaluated separately from the main query.

Consider:

    SELECT AVG(home_goal + away_goal)
    FROM match
    WHERE season = '2011/2012'

This calculates the average for **2011/2012 only**.

If we remove the filter:

    SELECT AVG(home_goal + away_goal)
    FROM match

the result becomes the average across **all seasons**.

Therefore:

    Main query filter
    → determines which rows are displayed

    Subquery filter
    → determines which rows are used to calculate the comparison value

These are separate operations.

---

# 14. 🔄 Main Query vs. Subquery Filters

Suppose the goal is:

> Compare every 2011/2012 match with the 2011/2012 average.

We need:

    Main query:
    WHERE season = '2011/2012'

and:

    Subquery:
    WHERE season = '2011/2012'

### Why?

Because the main query controls the displayed matches.

The subquery controls the average used for comparison.

---

# 15. 🧩 Full Example

    SELECT
        date,
        home_goal,
        away_goal,
        (home_goal + away_goal)
        -
        (
            SELECT AVG(home_goal + away_goal)
            FROM match
            WHERE season = '2011/2012'
        ) AS difference
    FROM match
    WHERE season = '2011/2012';

### Processing logic

    Subquery
        ↓
    Calculate 2011/2012 average
        ↓
    Main query
        ↓
    Select 2011/2012 matches
        ↓
    Calculate each match's difference
        ↓
    Final result

---

# 16. ⚠️ Important Rule: SELECT Subquery Must Return One Value

This is one of the most important rules.

A subquery in `SELECT` must return a **single value**.

### ✅ Valid

    SELECT AVG(home_goal)
    FROM match

`AVG()` returns one value.

### ✅ Valid

    SELECT COUNT(*)
    FROM match

`COUNT()` returns one value.

### ❌ Problematic

    SELECT home_goal
    FROM match

This can return many rows.

A SELECT subquery cannot simply return multiple rows when SQL expects one value for each result row.

---

# 17. 🆚 SELECT Subquery vs. FROM Subquery

| Feature | SELECT Subquery | FROM Subquery |
|---|---|---|
| Purpose | Add a calculated/summary value | Create a temporary table |
| Expected result | **Single value** | Multiple rows/columns possible |
| Location | `SELECT` | `FROM` |
| Common use | Overall average/count | Data preparation |
| Example | `SELECT AVG(...)` | `FROM (SELECT ...) AS subq` |

### SELECT

    SELECT
        column,
        (
            SELECT AVG(column)
            FROM table
        ) AS overall_avg
    FROM table;

### FROM

    SELECT *
    FROM (
        SELECT
            ...
        FROM table
    ) AS subq;

---

# 18. 🧠 Why SELECT Subqueries Are Useful

They allow you to combine:

    Detailed data
          +
    Summary information
          ↓
    More informative results

For example:

    Individual match
          +
    Overall average
          ↓
    Difference from average

This avoids having to manually calculate the summary value and insert it into your query.

---

# 19. 📊 Common Uses

SELECT subqueries are useful for:

### Overall average

    (
        SELECT AVG(value)
        FROM table
    )

### Overall count

    (
        SELECT COUNT(*)
        FROM table
    )

### Overall sum

    (
        SELECT SUM(value)
        FROM table
    )

### Difference from average

    value - (
        SELECT AVG(value)
        FROM table
    )

### Ratio to total

    value / (
        SELECT SUM(value)
        FROM table
    )

---

# 20. 🔑 Key Takeaways

- Subqueries can be placed inside `SELECT`.
- A `SELECT` subquery should return **one single value**.
- The returned value can be displayed as a column.
- The returned value can also be used in mathematical calculations.
- `COUNT()`, `AVG()`, and `SUM()` are common inside SELECT subqueries.
- A summary value can be displayed alongside detailed rows.
- Filters in the main query and subquery operate independently.
- If the comparison value should use a specific subset of data, the appropriate filter must also be placed inside the subquery.
- A SELECT subquery is useful for comparing individual records with overall or group-specific summary values.

---

# ⚡ Quick Reference

## Overall Average

    (
        SELECT AVG(column)
        FROM table
    )

## Overall Count

    (
        SELECT COUNT(*)
        FROM table
    )

## Overall Sum

    (
        SELECT SUM(column)
        FROM table
    )

## Add Summary Value to Detailed Data

    SELECT
        column,
        (
            SELECT AVG(column)
            FROM table
        ) AS overall_average
    FROM table;

## Difference from Average

    SELECT
        column,
        column - (
            SELECT AVG(column)
            FROM table
        ) AS difference
    FROM table;

## Filtered Comparison

    SELECT
        column,
        column - (
            SELECT AVG(column)
            FROM table
            WHERE season = '2011/2012'
        ) AS difference
    FROM table
    WHERE season = '2011/2012';

---

# 🧠 Mental Model

Think of a SELECT subquery as:

**Calculate one value → Bring it into every row → Use it for display or calculation**

    Detailed row
         +
    Single summary value
         ↓
    Calculation
         ↓
    More informative result

---

# 🎯 Subquery Locations So Far

| Location | Main Purpose | Typical Result |
|---|---|---|
| `WHERE` | Filter data | Single value or list |
| `FROM` | Prepare/restructure data | Table-like result |
| `SELECT` | Add summary/calculation | **Single value** |

### Easy way to remember:

    WHERE → Filter
    FROM  → Prepare
    SELECT → Calculate / Add summary

> 🚀 **Core idea: A subquery in SELECT returns one value that can be placed beside detailed data or used in a calculation.**
