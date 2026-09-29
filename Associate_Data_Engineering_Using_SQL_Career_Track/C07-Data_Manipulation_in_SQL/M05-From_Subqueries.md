# 🧩 Subqueries in the FROM Statement

## 🎯 Lesson Objective

In this lesson, we learn how to use **subqueries inside the `FROM` clause**.

While subqueries in `WHERE` are useful for filtering, subqueries in `FROM` are especially useful for:

- Restructuring data
- Transforming data
- Pre-filtering data
- Preparing data before further calculations
- Calculating **aggregates of aggregate information**
- Creating a temporary result set that can be queried like a table

---

# 1. 🧠 Why Use Subqueries in `FROM`?

A subquery in `WHERE` generally produces a **single value or a one-column list**.

But what if you need a more complex result containing **multiple columns and rows**?

This is where a subquery in `FROM` becomes useful.

Think of a `FROM` subquery as creating a **temporary table** that the outer query can work with.

### Mental Model

    Original tables
          ↓
    Subquery in FROM
          ↓
    Temporary result
          ↓
    Outer query
          ↓
    Final result

---

# 2. 📊 Example Problem

Suppose we want to find the:

> **Top 3 teams with the highest average home goals in the 2011/2012 season.**

This requires two levels of aggregation:

### Step 1

Calculate the **average home goals for each team**.

Example:

    Team        Average Home Goals
    Barcelona          3.1
    Real Madrid        2.8
    Valencia            1.9
    Sevilla             1.7

### Step 2

Use those averages to determine the **top 3 teams**.

The subquery performs Step 1.

The outer query performs Step 2.

---

# 3. 🔨 Build the Subquery First

The first query calculates the average home goals for every team.

    SELECT
        t.team_long_name AS team,
        AVG(m.home_goal) AS home_avg
    FROM team AS t
    LEFT JOIN match AS m
        ON t.team_api_id = m.hometeam_id
    WHERE m.season = '2011/2012'
    GROUP BY t.team_long_name

### What does this query do?

It:

1. Gets the team name from `team`.
2. Gets the `home_goal` values from `match`.
3. Connects the two tables using `hometeam_id`.
4. Filters the matches to the `2011/2012` season.
5. Groups the results by team.
6. Calculates the average home goals for each team.

---

# 4. 📋 The Subquery Result

Conceptually, the subquery produces something like:

| team | home_avg |
|---|---:|
| Barcelona | 3.10 |
| Real Madrid | 2.80 |
| Valencia | 1.90 |
| Sevilla | 1.70 |
| ... | ... |

This result can now be treated like a temporary table.

---

# 5. 🏗️ Put the Subquery in `FROM`

Take the **entire query** and place it inside the `FROM` clause.

Important:

- Remove the semicolon from the subquery.
- Put parentheses around the subquery.
- Give the subquery an **alias**.

    SELECT
        team,
        home_avg
    FROM
        (
            SELECT
                t.team_long_name AS team,
                AVG(m.home_goal) AS home_avg
            FROM team AS t
            LEFT JOIN match AS m
                ON t.team_api_id = m.hometeam_id
            WHERE m.season = '2011/2012'
            GROUP BY t.team_long_name
        ) AS subquery

The alias here is:

    subquery

---

# 6. 🏆 Add `ORDER BY` and `LIMIT`

Now that the subquery behaves like a table, the outer query can sort the results.

    SELECT
        team,
        home_avg
    FROM
        (
            SELECT
                t.team_long_name AS team,
                AVG(m.home_goal) AS home_avg
            FROM team AS t
            LEFT JOIN match AS m
                ON t.team_api_id = m.hometeam_id
            WHERE m.season = '2011/2012'
            GROUP BY t.team_long_name
        ) AS subquery
    ORDER BY home_avg DESC
    LIMIT 3;

### `ORDER BY home_avg DESC`

Sorts the teams from the highest average to the lowest.

### `LIMIT 3`

Keeps only the first three results.

---

# 7. 🧩 Complete Query Structure

The important structure is:

    SELECT columns
    FROM
        (
            SELECT columns
            FROM tables
            JOIN tables
            WHERE condition
            GROUP BY columns
        ) AS subquery
    ORDER BY column DESC
    LIMIT 3;

Think of it as:

    INNER QUERY
    ─────────────────────
    Calculate average per team
              ↓
    Create temporary result
              ↓
    OUTER QUERY
    ─────────────────────
    Sort averages
              ↓
    Take top 3

---

# 8. 🔄 Why Not Do Everything in One Query?

The problem requires:

1. Calculate an average **for each team**.
2. Sort those calculated averages.
3. Select the top 3.

The `FROM` subquery allows us to separate these operations into two logical stages.

### Stage 1 — Prepare the data

    AVG(m.home_goal)
    GROUP BY team

### Stage 2 — Analyze the prepared data

    ORDER BY home_avg DESC
    LIMIT 3

This makes complex analysis easier to structure.

---

# 9. ⭐ Aggregates of Aggregates

One important use of `FROM` subqueries is calculating an **aggregate of already-aggregated information**.

For example:

### First aggregation

    AVG(home_goal)

Calculate the average home goals for each team.

### Then analyze those averages

The outer query can work with the resulting `home_avg` values.

This is useful whenever your analysis requires multiple levels of calculation.

---

# 10. 🆚 `WHERE` Subquery vs. `FROM` Subquery

| Feature | Subquery in `WHERE` | Subquery in `FROM` |
|---|---|---|
| Main purpose | Filtering | Restructuring/preparing data |
| Typical result | Single value or list | Table-like result |
| Multiple columns? | Usually no | Yes |
| Can contain multiple rows? | Yes, with `IN` | Yes |
| Needs alias? | Usually no | **Yes** |
| Can be queried by outer query? | Used as a condition | Yes |
| Useful for aggregate-of-aggregate? | Limited | **Yes** |

---

# 11. 🏷️ Why Does a `FROM` Subquery Need an Alias?

A subquery in `FROM` acts like a temporary table.

SQL therefore needs a name for it.

Example:

    FROM
        (
            SELECT ...
        ) AS subquery

Here:

    subquery

is the alias.

You can choose another name:

    ) AS team_averages

Then reference it like a table:

    SELECT
        team_averages.team,
        team_averages.home_avg
    FROM
        (
            SELECT ...
        ) AS team_averages

---

# 12. 🔗 Multiple Subqueries in `FROM`

You can have **more than one subquery** in the `FROM` clause.

For example:

    SELECT ...
    FROM
        (
            SELECT ...
        ) AS subquery1
    JOIN
        (
            SELECT ...
        ) AS subquery2
        ON subquery1.team = subquery2.team

Each subquery must have:

1. Its own alias.
2. A column that can be used to connect it to another table or subquery.

---

# 13. 🔗 Joining a Subquery to an Existing Table

A subquery can also be joined to a normal table.

Example structure:

    SELECT ...
    FROM
        (
            SELECT
                team_id,
                AVG(home_goal) AS home_avg
            FROM match
            GROUP BY team_id
        ) AS team_stats
    JOIN team
        ON team_stats.team_id = team.team_api_id

The subquery behaves much like another table.

---

# 14. 🧠 Important Rules for `FROM` Subqueries

### Rule 1 — Use parentheses

    FROM (
        SELECT ...
    ) AS subquery

### Rule 2 — Give it an alias

    ) AS subquery

### Rule 3 — Remove the inner semicolon

❌ Incorrect:

    FROM (
        SELECT ...
        ;
    ) AS subquery

✅ Correct:

    FROM (
        SELECT ...
    ) AS subquery

### Rule 4 — Make sure the outer query can use the returned columns

If the outer query needs:

    team
    home_avg

the subquery must return those columns.

---

# 15. 🎯 Main Example

### Goal

Find the top 3 teams by average home goals in the `2011/2012` season.

### Complete Query

    SELECT
        team,
        home_avg
    FROM
        (
            SELECT
                t.team_long_name AS team,
                AVG(m.home_goal) AS home_avg
            FROM team AS t
            LEFT JOIN match AS m
                ON t.team_api_id = m.hometeam_id
            WHERE m.season = '2011/2012'
            GROUP BY t.team_long_name
        ) AS subquery
    ORDER BY home_avg DESC
    LIMIT 3;

### Result

The query returns the **top 3 teams based on average home goals** for the `2011/2012` season.

---

# 🔑 Key Takeaways

- A subquery can be placed in the `FROM` clause.
- A `FROM` subquery creates a **temporary table-like result**.
- It can return **multiple rows and multiple columns**.
- `FROM` subqueries are useful for **preparing data before further analysis**.
- They are especially useful for **aggregates of aggregate information**.
- Every `FROM` subquery needs an **alias**.
- The outer query can treat the subquery result like a table.
- Multiple subqueries can be placed in `FROM`.
- A subquery can also be joined to an existing table.
- The subquery must contain the columns needed by the outer query.

---

# ⚡ Quick Reference

## Basic `FROM` Subquery

    SELECT columns
    FROM (
        SELECT columns
        FROM table
        WHERE condition
    ) AS subquery;

## `FROM` Subquery with Aggregation

    SELECT
        team,
        average_value
    FROM (
        SELECT
            team,
            AVG(value) AS average_value
        FROM table
        GROUP BY team
    ) AS subquery;

## Sort and Limit the Prepared Results

    SELECT
        team,
        average_value
    FROM (
        SELECT
            team,
            AVG(value) AS average_value
        FROM table
        GROUP BY team
    ) AS subquery
    ORDER BY average_value DESC
    LIMIT 3;

---

# 🧠 Mental Model

### `WHERE` Subquery

    Main table
        ↓
    Filter using
    another query
        ↓
    Selected rows

### `FROM` Subquery

    Original tables
        ↓
    Prepare / transform data
        ↓
    Temporary table
        ↓
    Outer query
        ↓
    Final result

---

# 🚀 Key Pattern to Remember

    SELECT ...
    FROM (
        SELECT ...
        FROM ...
        WHERE ...
        GROUP BY ...
    ) AS subquery
    ORDER BY ...
    LIMIT ...;

> **FROM subquery = prepare the data first, then query the prepared result.**
