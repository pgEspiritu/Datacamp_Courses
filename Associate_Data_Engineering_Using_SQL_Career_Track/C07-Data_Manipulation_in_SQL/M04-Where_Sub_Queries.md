# 🔎 WHERE Are the Subqueries?

## 1. WHERE Are the Subqueries?

Welcome back! 👋

In this chapter, we will learn how to use **simple subqueries** to extract, filter, and transform data.

Subqueries are especially useful when you need to perform an **intermediate calculation or transformation** before running your main query.

---

# 2. What Is a Subquery?

A **subquery** is a query nested inside another query.

You can identify a subquery because you will usually see:

- An additional `SELECT` statement
- Inside parentheses `()`
- Within another complete SQL statement

### Basic Structure

    SELECT ...
    FROM ...
    WHERE column > (
        SELECT ...
        FROM ...
    );

The inner `SELECT` is the **subquery**.

The outer `SELECT` is the **main query**.

### 🧠 Think of it as:

    Inner query
        ↓
    Get intermediate result
        ↓
    Outer query
        ↓
    Produce final result

---

# 3. Why Are Subqueries Important?

Sometimes, the information you need cannot be retrieved directly.

You may first need to:

1. Calculate something
2. Filter the result
3. Create a list
4. Transform data
5. Then use that result in your main query

A subquery allows you to perform that intermediate step **inside the same SQL statement**.

### Without a subquery

You might need to:

    1. Run Query A
    2. Look at the result
    3. Manually copy the result
    4. Put it into Query B

### With a subquery

    Query B
       ↓
    Subquery automatically produces the result
       ↓
    Query B uses the result

This makes the process more automated and reusable.

---

# 4. What Can You Do with Subqueries?

A subquery can be placed in different parts of a SQL query, including:

- `SELECT`
- `FROM`
- `WHERE`
- `GROUP BY`

Where you place the subquery depends on what you want the final result to look like.

### A subquery can return:

| Result | Description |
|---|---|
| 🔢 Scalar value | A single number or value |
| 📋 List | Multiple values used for filtering |
| 📊 Table | A result set used for further querying |

---

# 5. Why Use Subqueries?

Subqueries are useful for several reasons.

## 📊 1. Compare Summary Data with Detailed Data

For example, you could compare:

    Liverpool's performance

against:

    The overall English Premier League performance

A subquery can calculate the overall value, which the outer query can then compare against individual matches.

---

## 🏗️ 2. Reshape or Structure Data

Subqueries can help create intermediate datasets that can then be analyzed by another query.

For example:

> Determine the highest monthly average of goals scored in the Bundesliga.

You may need to:

    Match data
        ↓
    Calculate monthly averages
        ↓
    Use those averages in another query
        ↓
    Find the highest value

A subquery can handle the intermediate step.

---

## 🔗 3. Combine Information When a JOIN Isn't Available

Sometimes the tables you need don't contain the appropriate columns to directly perform a join.

A subquery can sometimes help retrieve the necessary information.

For example:

> Get both the home and away team names into the results table.

Subqueries can provide another way to retrieve information when a direct `JOIN` is not possible or convenient.

---

# 6. Simple Subqueries

A **simple subquery** is:

> A query nested inside another query that can be run on its own.

For example:

    SELECT *
    FROM match
    WHERE home_goal > (
        SELECT AVG(home_goal)
        FROM match
    );

The inner query is:

    SELECT AVG(home_goal)
    FROM match

You can run that query by itself.

It produces a single value:

    Overall average home goals

The outer query then uses that value.

---

# 7. How SQL Processes a Simple Subquery

A simple subquery is evaluated **once for the entire query**.

Consider:

    SELECT *
    FROM match
    WHERE home_goal > (
        SELECT AVG(home_goal)
        FROM match
    );

SQL conceptually processes this in two stages.

### Step 1 — Run the subquery

    SELECT AVG(home_goal)
    FROM match

Suppose it returns:

    1.54

### Step 2 — Run the outer query

SQL effectively treats the result like:

    SELECT *
    FROM match
    WHERE home_goal > 1.54;

The subquery provides the value that the outer query needs.

---

# 8. 🧠 Simple Subquery Mental Model

Think of a subquery as a **temporary answer**.

    Subquery
        ↓
    "What is the overall average?"
        ↓
       1.54
        ↓
    Outer query
        ↓
    "Show matches with home goals > 1.54"

This is one of the most important ideas when learning subqueries.

---

# 9. Subqueries in the WHERE Clause

The first type of simple subquery we'll explore is a subquery inside `WHERE`.

These are useful when you need to filter results based on a value that must first be calculated separately.

### Example Question

> Which matches in the 2012/2013 season had more home goals than the overall average number of home goals?

We could first calculate the average:

    SELECT AVG(home_goal)
    FROM match;

Then manually use the result in another query.

But we can do both steps automatically with a subquery.

---

# 10. Using a Subquery for Filtering

### Complete Query

    SELECT *
    FROM match
    WHERE season = '2012/2013'
      AND home_goal > (
          SELECT AVG(home_goal)
          FROM match
      );

The subquery:

    SELECT AVG(home_goal)
    FROM match

calculates the overall average.

The outer query then finds matches where:

    home_goal > overall_average

---

# 11. Why Put the Subquery Inside Parentheses?

The subquery is enclosed in:

    (
        SELECT AVG(home_goal)
        FROM match
    )

The parentheses clearly identify the inner query as a separate expression.

The structure is:

    WHERE column > (
        subquery
    )

This allows the result of the subquery to be used by the outer query.

---

# 12. Subquery Filtering with IN

Subqueries can also generate a **list of values**.

This is especially useful with the `IN` operator.

### Example Question

> Which teams are part of Poland's league?

Suppose:

    country_id = 15722

represents Poland.

The `team` table may contain team IDs, while the `match` table contains both:

- `country_id`
- `hometeam_id`

We can use the `match` table to generate a list of team IDs.

---

# 13. Generating a Filtering List

The subquery can be:

    SELECT hometeam_id
    FROM match
    WHERE country_id = 15722

This returns a list of team IDs associated with Poland.

We can then use that list in the outer query:

    SELECT team_long_name
    FROM team
    WHERE team_api_id IN (
        SELECT hometeam_id
        FROM match
        WHERE country_id = 15722
    );

---

# 14. Understanding `IN`

`IN` checks whether a value exists within a list.

For example:

    WHERE team_api_id IN (1, 2, 3, 4)

means:

> Keep rows where `team_api_id` is 1, 2, 3, or 4.

When combined with a subquery:

    WHERE team_api_id IN (
        SELECT hometeam_id
        FROM match
        WHERE country_id = 15722
    )

the list is generated automatically.

### 🧠 Think of it as:

    Subquery
        ↓
    Generate team ID list
        ↓
    IN
        ↓
    Find matching teams

---

# 15. Scalar Subquery vs List Subquery

An important distinction is what the subquery returns.

## 🔢 Scalar Subquery

Returns a **single value**.

Example:

    SELECT AVG(home_goal)
    FROM match

Result:

    1.54

Can be used with operators such as:

    >
    <
    =
    >=
    <=
    <>

Example:

    WHERE home_goal > (
        SELECT AVG(home_goal)
        FROM match
    )

---

## 📋 List Subquery

Returns **multiple values**.

Example:

    SELECT hometeam_id
    FROM match
    WHERE country_id = 15722

Result might look like:

    8020
    8021
    8022
    8023
    ...

This can be used with:

    IN

Example:

    WHERE team_api_id IN (
        SELECT hometeam_id
        FROM match
        WHERE country_id = 15722
    )

---

# 🔄 Simple Subquery Workflow

A useful way to visualize simple subqueries is:

    ┌─────────────────────┐
    │      Subquery       │
    │                     │
    │ Calculate / filter  │
    │ / generate a list   │
    └──────────┬──────────┘
               ↓
       Intermediate result
               ↓
    ┌─────────────────────┐
    │    Outer Query      │
    │                     │
    │ Uses the result to  │
    │ produce final data  │
    └─────────────────────┘

---

# 🎯 Key Takeaways

- A **subquery** is a query nested inside another query.
- A subquery usually appears inside parentheses.
- A simple subquery can be run independently.
- Simple subqueries are evaluated once for the entire outer query.
- A subquery can be placed in different parts of a query.
- A subquery can return:
  - 🔢 A single value
  - 📋 A list
  - 📊 A table
- `WHERE` subqueries are useful for filtering based on calculated values.
- `IN` can be used with a subquery that returns a list.
- Subqueries reduce the need for manual intermediate calculations.
- They are useful for comparing detailed data with summarized information.

---

# 🧩 Quick Reference

## 🔢 Single-value subquery

    WHERE column > (
        SELECT AVG(column)
        FROM table
    )

Use when the subquery returns **one value**.

---

## 📋 List subquery

    WHERE column IN (
        SELECT another_column
        FROM table
        WHERE condition
    )

Use when the subquery returns **multiple values**.

---

## 📊 Basic Subquery Structure

    SELECT ...
    FROM ...
    WHERE column > (
        SELECT ...
        FROM ...
    );

---

## ⭐ Remember

> **A subquery is an intermediate query whose result is used by the outer query.**

The key question to ask is:

> **"What information do I need to calculate or retrieve first before my main query can answer the question?"**

If the answer requires another query, a **subquery** may be the right tool.
