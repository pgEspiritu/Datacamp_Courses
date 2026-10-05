# 🧩 Common Table Expressions (CTEs)

## 1. Common Table Expressions

Great job getting the hang of **nested and correlated subqueries**! 🎉

In the previous lessons, we used nested subqueries to break complicated SQL problems into multiple steps.

However, as queries become more complex, they can become difficult to read and maintain.

This lesson introduces **Common Table Expressions (CTEs)** as a cleaner way to organize subqueries.

---

# 2. When Adding Subqueries...

As you probably noticed, the queries we have been setting up are quickly becoming **long and complex**.

It can become difficult to clearly keep track of:

- 🔎 Each piece of the query
- ❓ Why each piece is needed
- 🧩 How the subqueries relate to each other
- 🧹 Whether a particular subquery is actually necessary

A common method for improving the **readability and accessibility** of information in subqueries is the **Common Table Expression**, or **CTE**.

---

# 3. Common Table Expressions

## 🧠 What is a CTE?

A **Common Table Expression (CTE)** is a special type of subquery that is declared **before the main query**.

Instead of placing a subquery directly inside a `FROM` statement, you:

1. Declare the subquery using `WITH`.
2. Give the subquery a name.
3. Place the subquery inside parentheses.
4. Reference the CTE later by its name.

### Basic syntax

    WITH cte_name AS (
        SELECT
            ...
        FROM table
        WHERE ...
    )
    SELECT
        ...
    FROM cte_name;

💡 A CTE can be treated like a temporary table while the query is being executed.

---

# 4. Take a Subquery in FROM

Let's rewrite a query from an earlier exercise using a CTE.

The original query used a subquery named `s` inside the `FROM` statement.

The subquery generated a list of:

- `country_id`
- Match `id`

for matches where the **total number of goals was 10 or more**.

The subquery was then joined to the `country` table, and the number of qualifying matches was counted in the main query.

The general structure was:

    SELECT
        c.name AS country_name,
        COUNT(*) AS matches
    FROM country AS c
    INNER JOIN (
        SELECT
            country_id,
            id
        FROM match
        WHERE (home_goal + away_goal) >= 10
    ) AS s
        ON c.id = s.country_id
    GROUP BY country_name;

### 🔍 What does the subquery do?

This part:

    (
        SELECT
            country_id,
            id
        FROM match
        WHERE (home_goal + away_goal) >= 10
    ) AS s

creates a temporary result containing only matches with **10 or more total goals**.

The main query then joins this result to `country`.

---

# 5. Place It at the Beginning

To rewrite the query using a CTE, take the subquery out of the `FROM` clause and place it at the **beginning of the query**.

Instead of:

    FROM (
        SELECT ...
    ) AS s

we will create:

    WITH s AS (
        SELECT ...
    )

This separates the preparation of the data from the main query.

---

# 6. Declare the CTE Using WITH

The syntax begins with:

    WITH s AS (
        SELECT
            country_id,
            id
        FROM match
        WHERE (home_goal + away_goal) >= 10
    )

The important components are:

### `WITH`

Tells SQL that we are about to define a CTE.

### `s`

The name of the CTE.

### `AS`

Connects the CTE name to the query that defines it.

### `(SELECT ...)`

Contains the query that generates the CTE.

So:

    WITH s AS (
        ...
    )

means:

> "Create a temporary named result called `s` using this query."

---

# 7. Use the CTE in the Main Query

Once the CTE has been declared, the rest of the query can treat `s` like a table.

Example:

    WITH s AS (
        SELECT
            country_id,
            id
        FROM match
        WHERE (home_goal + away_goal) >= 10
    )

    SELECT
        c.name AS country_name,
        COUNT(s.id) AS matches
    FROM country AS c
    INNER JOIN s
        ON c.id = s.country_id
    GROUP BY country_name;

Notice that the CTE is referenced here:

    INNER JOIN s
        ON c.id = s.country_id

Instead of placing the entire subquery inside `FROM`, we simply use its name:

    s

### 🎯 Result

The results are the same as the original subquery version.

The main difference is **how the query is organized**.

---

# 🔄 Subquery vs CTE

## Traditional subquery

    SELECT
        c.name AS country_name,
        COUNT(s.id) AS matches
    FROM country AS c
    INNER JOIN (
        SELECT
            country_id,
            id
        FROM match
        WHERE (home_goal + away_goal) >= 10
    ) AS s
        ON c.id = s.country_id
    GROUP BY country_name;

## CTE version

    WITH s AS (
        SELECT
            country_id,
            id
        FROM match
        WHERE (home_goal + away_goal) >= 10
    )

    SELECT
        c.name AS country_name,
        COUNT(s.id) AS matches
    FROM country AS c
    INNER JOIN s
        ON c.id = s.country_id
    GROUP BY country_name;

### 💡 Main difference

The **logic is essentially the same**, but the CTE version is often easier to read.

---

# 8. Multiple CTEs

You can create **multiple CTEs** in the same query.

Simply separate each CTE with a comma.

### Syntax

    WITH first_cte AS (
        SELECT
            ...
        FROM ...
    ),
    second_cte AS (
        SELECT
            ...
        FROM ...
    ),
    third_cte AS (
        SELECT
            ...
        FROM ...
    )

    SELECT
        ...
    FROM first_cte
    JOIN second_cte
        ON ...
    JOIN third_cte
        ON ...;

⚠️ **Important:** Do not put a comma after the final CTE.

Correct:

    WITH first_cte AS (
        ...
    ),
    second_cte AS (
        ...
    )
    SELECT
        ...
    FROM first_cte;

Incorrect:

    WITH first_cte AS (
        ...
    ),
    second_cte AS (
        ...
    ),
    SELECT
        ...

---

# 🧩 CTEs Can Reference Earlier CTEs

An important advantage of multiple CTEs is that a later CTE can reference an earlier CTE.

For example:

    WITH first_cte AS (
        SELECT
            ...
        FROM ...
    ),
    second_cte AS (
        SELECT
            ...
        FROM first_cte
    ),
    third_cte AS (
        SELECT
            ...
        FROM first_cte
        JOIN second_cte
            ON ...
    )

    SELECT
        ...
    FROM third_cte;

The dependency flows from one CTE to another:

    first_cte
        ↓
    second_cte
        ↓
    third_cte
        ↓
    main query

This can make complicated SQL much easier to organize.

---

# 9. Why Use CTEs?

Common Table Expressions have several important benefits. 🚀

## 1️⃣ Improved readability

CTEs make long queries easier to understand because each transformation can be given a meaningful name.

Instead of:

    FROM (
        SELECT ...
        FROM (
            SELECT ...
        ) AS inner_s
    ) AS outer_s

you can organize the logic as:

    WITH inner_s AS (
        SELECT ...
    ),
    outer_s AS (
        SELECT ...
        FROM inner_s
    )
    SELECT ...
    FROM outer_s;

This makes the query structure much easier to follow.

---

## 2️⃣ Organize complex queries

You can declare multiple CTEs one after another.

For example:

    WITH filtered_matches AS (
        ...
    ),
    match_counts AS (
        ...
    ),
    country_summary AS (
        ...
    )
    SELECT
        ...
    FROM country_summary;

Each CTE can perform one logical transformation.

### 🧠 Think of it as a data pipeline:

    Raw data
       ↓
    filtered_matches
       ↓
    match_counts
       ↓
    country_summary
       ↓
    final result

---

## 3️⃣ Reference earlier CTEs

A CTE can reference CTEs declared before it.

For example:

    WITH cte1 AS (
        ...
    ),
    cte2 AS (
        SELECT ...
        FROM cte1
    ),
    cte3 AS (
        SELECT ...
        FROM cte1
        JOIN cte2
            ON ...
    )
    SELECT ...
    FROM cte3;

This allows you to build a complicated analysis **step by step**.

---

## 4️⃣ Recursive CTEs

A CTE can also reference itself.

This is called a **recursive CTE**.

Recursive CTEs are useful for specialized problems such as:

- 🌳 Hierarchical data
- 👨‍👩‍👧 Organizational structures
- 🌐 Graph-like relationships
- 📁 Parent-child relationships

Recursive CTEs are an advanced application of CTEs and will be discussed separately.

---

# ⚠️ Important Performance Note

CTEs can improve readability and organization, but the exact performance behavior of CTEs depends on the SQL database system and query optimizer.

Do not assume that every database always physically executes and stores a CTE only once.

💡 The most important beginner-level benefit is **clarity and organization**.

---

# 🧠 CTE Mental Model

Think of a CTE as:

> **Name a query first, then use that name like a table.**

Instead of:

    SELECT ...
    FROM (
        SELECT ...
    ) AS subquery;

Use:

    WITH subquery AS (
        SELECT ...
    )
    SELECT ...
    FROM subquery;

---

# 🔑 Key Takeaways

- 🧩 **CTE** = Common Table Expression.
- `WITH` is used to declare a CTE.
- A CTE is given a name.
- The CTE query is placed inside parentheses.
- The CTE can then be referenced like a table.
- CTEs are especially useful for long or complicated SQL queries.
- Multiple CTEs can be declared in one query.
- Separate multiple CTEs with commas.
- Do **not** put a comma after the last CTE.
- Later CTEs can reference earlier CTEs.
- Recursive CTEs can reference themselves.
- CTEs often make complex SQL easier to read, organize, debug, and maintain.

---

# ⚡ Quick Reference

## Basic CTE

    WITH cte_name AS (
        SELECT
            ...
        FROM table
        WHERE condition
    )

    SELECT
        ...
    FROM cte_name;

## Multiple CTEs

    WITH cte1 AS (
        SELECT
            ...
        FROM table1
    ),
    cte2 AS (
        SELECT
            ...
        FROM cte1
    )

    SELECT
        ...
    FROM cte2;

## CTE + JOIN

    WITH s AS (
        SELECT
            country_id,
            id
        FROM match
        WHERE (home_goal + away_goal) >= 10
    )

    SELECT
        c.name AS country_name,
        COUNT(s.id) AS matches
    FROM country AS c
    INNER JOIN s
        ON c.id = s.country_id
    GROUP BY country_name;

---

# 🆚 Subquery vs CTE

| Feature | Subquery | CTE |
|:---|:---|:---|
| Defined | Inside main query | Before main query |
| Keyword | None | `WITH` |
| Has a name | Usually an alias | Yes |
| Can be used like a table | Yes | Yes |
| Multiple levels | Possible | Easier to organize |
| Readability | Can become difficult | Usually clearer |
| Multiple reusable steps | More difficult | Easier |
| Recursive option | ❌ | ✅ Recursive CTE |

---

# 🎯 Final Mental Model

### Subquery

    MAIN QUERY
        ↓
    SUBQUERY INSIDE QUERY

### CTE

    WITH
      ↓
    NAME THE QUERY
      ↓
    MAIN QUERY
      ↓
    USE CTE AS TABLE

### For complex SQL

    1. 🔎 Filter
    2. 🔢 Aggregate
    3. 🧩 Create CTE
    4. 🔗 Join CTEs
    5. 📊 Perform final calculation
    6. 🎯 Return final result

💡 **Remember:**

> **A CTE is a named subquery defined before the main query using `WITH`.**
