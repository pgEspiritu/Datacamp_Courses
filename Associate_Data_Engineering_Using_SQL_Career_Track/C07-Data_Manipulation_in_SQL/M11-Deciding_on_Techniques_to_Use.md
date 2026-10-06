# 🧠 Deciding on Techniques to Use

## 1. Deciding on Techniques to Use

At this point in the course, you're probably wondering why we're covering so many different methods of performing similar tasks.

The main techniques covered are:

- 🔗 **Joins**
- 🔍 **Subqueries**
- 🔄 **Correlated subqueries**
- 🪆 **Multiple/nested subqueries**
- 🧩 **Common Table Expressions (CTEs)**

The important thing to understand is that these techniques often overlap in what they can accomplish, but they are **not identical**.

---

## 2. Different Names for the Same Thing?

There is a lot of overlap between the use cases for **joins, subqueries, and common table expressions**.

Many questions can be answered using different techniques without significantly changing:

- ✅ Query accuracy
- ✅ Output
- ✅ Query performance

However, each technique has its own strengths and limitations.

### 💡 Key Idea

> Different SQL techniques can sometimes solve the same problem, but the best choice depends on the structure of the problem, readability, reusability, and database performance.

---

# 3. Differentiating Techniques

Let's compare the techniques used in this and the previous chapter.

## 🔗 Joins

Joins allow you to directly combine information from **two or more tables**.

They are mainly useful for:

- Combining related tables
- Retrieving columns from multiple tables
- Performing aggregations across related tables
- Connecting data using matching keys

### Example

    SELECT
        t.team_long_name,
        m.home_goal,
        m.away_goal
    FROM team AS t
    JOIN match AS m
        ON t.team_api_id = m.hometeam_id;

### 💡 Main idea

**JOIN = Combine tables directly**

Joins are one of the most important SQL skills when working with databases containing multiple related tables.

---

## 🔍 Correlated Subqueries

A correlated subquery allows you to combine information between:

- A subquery and a table
- A subquery and another subquery

The subquery references a column from the outer query.

### Example

    SELECT
        main.country_id,
        main.date,
        main.home_goal,
        main.away_goal
    FROM match AS main
    WHERE
        (main.home_goal + main.away_goal) >
        (
            SELECT AVG(sub.home_goal + sub.away_goal)
            FROM match AS sub
            WHERE main.country_id = sub.country_id
        );

The important part is:

    WHERE main.country_id = sub.country_id

The subquery depends on the current row from the outer query.

### 💡 Why use correlated subqueries?

They can solve situations where a regular join is difficult or cannot easily express the required relationship.

For example, in the `match` table, you may want to retrieve information for both:

- The home team
- The away team

from the same `team` table.

A correlated subquery can sometimes simplify this type of problem.

### ⚠️ Important Performance Note

Correlated subqueries can be expensive because they may need to be evaluated for many rows of the outer query.

Therefore:

> **Correlated subqueries can make queries slower, especially with large datasets.**

---

## 🪆 Multiple and Nested Subqueries

Multiple and nested subqueries are useful when your data requires **several transformation steps** before it reaches the form needed for the final query.

### Example workflow

    Step 1 → Filter the data
    Step 2 → Aggregate the data
    Step 3 → Calculate another summary
    Step 4 → Compare results
    Step 5 → Produce the final output

Instead of trying to perform everything in one complicated query, you can break the process into several subqueries.

### 💡 Main idea

**Nested subqueries = Multiple levels of data preparation**

They are especially useful when one calculation depends on the result of another calculation.

### Example structure

    SELECT ...
    FROM (
        SELECT ...
        FROM (
            SELECT ...
            FROM match
            WHERE ...
        ) AS inner_query
        ...
    ) AS outer_query;

Breaking the process into steps can improve:

- Accuracy
- Organization
- Reproducibility
- Understanding of the query logic

---

# 🧩 Common Table Expressions (CTEs)

Common Table Expressions allow you to organize subqueries by declaring them at the beginning of the query using `WITH`.

### Basic structure

    WITH cte_name AS (
        SELECT
            ...
        FROM table
        WHERE ...
    )
    SELECT
        ...
    FROM cte_name;

Instead of nesting subqueries directly inside `FROM`, you give them a name and reference them later.

### Multiple CTEs

    WITH first_cte AS (
        SELECT ...
    ),
    second_cte AS (
        SELECT ...
        FROM first_cte
    ),
    third_cte AS (
        SELECT ...
        FROM second_cte
    )
    SELECT ...
    FROM third_cte;

Later CTEs can reference CTEs created earlier.

### 💡 Main idea

**CTE = Organize complex query steps sequentially**

CTEs can serve as an alternative to deeply nested subqueries and often make complex SQL much easier to read.

---

# 📊 Comparing the Techniques

| Technique | Main Purpose | Strength | Main Consideration |
|---|---|---|---|
| 🔗 JOIN | Combine tables | Directly connects related tables | Requires appropriate join conditions |
| 🔍 Correlated Subquery | Compare/relate outer and inner data | Handles row-dependent logic | Can be slower |
| 🪆 Nested Subquery | Multi-step transformation | Handles complex calculations | Can become difficult to read |
| 🧩 CTE | Organize query steps | Readable and reusable within the query | Database-specific behavior can vary |

---

# 4. So Which Do I Use?

There is no single technique that is always the best.

The choice depends on:

- 🗄️ The database system you're using
- 🏢 The field or problem you're working on
- ❓ The question you're trying to answer
- 📊 The structure of your data
- ⚡ Query performance
- 👀 Query readability
- 🔁 Whether you need to reuse a query step

### Recommended Approach

Practice each technique with your own databases.

Then determine which technique allows you to:

1. Use the data correctly
2. Generate accurate results
3. Write readable queries
4. Reuse query logic
5. Maintain good performance

### 💡 Practical Rule

> Don't choose a technique just because it works. Choose the technique that makes the query **clear, accurate, maintainable, and appropriately efficient**.

---

# 5. Different Use Cases

Each technique is particularly useful for certain types of problems.

## 🔗 Joins — Combining Related Tables

Joins are a universally important skill when working with databases containing more than one table.

In fact:

> Understanding joins is important before learning how to work effectively with subqueries and CTEs.

### Typical question

> Which team played in each match, and what was the final score?

This requires combining information from related tables.

### Best fit

    JOIN → Combine information from related tables

---

## 🔍 Correlated Subqueries — Row-Dependent Comparisons

Correlated subqueries are useful for matching or comparing data based on the current row of the outer query.

### Example question

> Who is each employee's immediate supervisor?

The answer may require comparing information across different columns or tables where the relationship depends on the current employee.

### Best fit

    Correlated Subquery
        ↓
    Current outer row
        ↓
    Find related information
        ↓
    Return result

---

## 🪆 Multiple and Nested Subqueries — Multi-Step Analysis

Multiple and nested subqueries are useful when a question requires several transformations before the final result can be produced.

### Example question

> What is the average deal size closed by each sales representative in the last quarter?

This may require:

1. Filtering deals to the last quarter
2. Identifying completed/closed deals
3. Calculating deal sizes
4. Grouping by sales representative
5. Calculating averages
6. Producing the final result

### Best fit

    Filter
       ↓
    Transform
       ↓
    Aggregate
       ↓
    Calculate
       ↓
    Final result

---

## 🧩 CTEs — Organizing Multiple Data Sources

CTEs are excellent when you need to compare or combine many different pieces of information.

### Example question

> How did the marketing, sales, growth, and engineering teams perform on their key metrics last quarter?

You could create separate CTEs for each team.

### Example structure

    WITH marketing AS (
        SELECT ...
    ),
    sales AS (
        SELECT ...
    ),
    growth AS (
        SELECT ...
    ),
    engineering AS (
        SELECT ...
    )
    SELECT ...
    FROM marketing
    JOIN sales ...
    JOIN growth ...
    JOIN engineering ...;

Each CTE prepares one part of the analysis.

The final query then combines the prepared results.

### Best fit

    CTE 1 → Marketing performance
    CTE 2 → Sales performance
    CTE 3 → Growth performance
    CTE 4 → Engineering performance
                  ↓
             Final Query

---

# 🧠 Quick Decision Guide

Use this as a simple mental checklist:

| If you need to... | Consider using... |
|---|---|
| Combine two or more related tables | 🔗 `JOIN` |
| Retrieve related information based on the current row | 🔍 Correlated subquery |
| Calculate something using another query's result | 🔍 Subquery |
| Perform several transformation steps | 🪆 Nested subqueries |
| Make complex subqueries easier to read | 🧩 CTE |
| Create several named preparation steps | 🧩 Multiple CTEs |
| Combine information from multiple tables | 🔗 `JOIN` |
| Compare each row against a group-specific value | 🔍 Correlated subquery |
| Build a multi-step analytical query | 🧩 CTE / nested subqueries |

---

# 🔑 Important Differences

## JOIN

    JOIN → Combine tables

Think:

> "I need information from another table."

---

## WHERE Subquery

    WHERE → Filter or compare

Think:

> "I need to compare my rows against a value or list produced by another query."

---

## SELECT Subquery

    SELECT → Add a calculated/summary value

Think:

> "I want to display an additional calculated value alongside my results."

---

## FROM Subquery

    FROM → Prepare or restructure data

Think:

> "I need to create an intermediate table-like result before running my main query."

---

## Correlated Subquery

    Correlated Subquery
        ↓
    Outer row
        ↓
    Inner query depends on that row

Think:

> "The answer for the inner query changes depending on the current outer row."

---

## Nested Subquery

    Inner Query
        ↓
    Outer Subquery
        ↓
    Main Query

Think:

> "I need multiple levels of calculations."

---

## CTE

    WITH
        ↓
    Named query step
        ↓
    Another query step
        ↓
    Main query

Think:

> "I want to organize complex query steps before the main query."

---

# 🧭 SQL Technique Mental Model

A useful way to remember the major techniques:

    🔗 JOIN
        ↓
    Combine tables

    🔍 Subquery
        ↓
    Get a value/list/table from another query

    🔍 Correlated Subquery
        ↓
    Inner query depends on outer row

    🪆 Nested Subquery
        ↓
    Query inside another subquery

    🧩 CTE
        ↓
    Name and organize query steps

---

# ⭐ Key Takeaways

- 🔗 **Joins** directly combine information from multiple tables.
- 🔍 **Subqueries** allow one query to use the result of another query.
- 🔍 **Correlated subqueries** depend on values from the outer query.
- ⚠️ Correlated subqueries can be slower because they may need to execute for many outer rows.
- 🪆 **Multiple/nested subqueries** are useful for multi-step data transformations.
- 🧩 **CTEs** organize complex subqueries into named, sequential steps.
- 🔗 Understanding joins is fundamental to working effectively with relational databases.
- 💡 Several techniques can often solve the same problem.
- 🎯 The best technique depends on the problem, database, readability, maintainability, and performance.
- 🧠 Practice each technique to determine which approach works best for your specific data and questions.

---

# 📌 Quick Reference Cheat Sheet

    JOIN
    → Combine related tables.

    WHERE subquery
    → Filter or compare using another query's result.

    SELECT subquery
    → Add a calculated or summary value to each result row.

    FROM subquery
    → Prepare or restructure data before the main query.

    Correlated subquery
    → Inner query references the outer query.

    Nested subquery
    → A subquery exists inside another subquery.

    CTE
    → Name a query step using WITH and use it like a temporary table within the statement.

---

# 🏁 Let's Practice!

Now it's time to practice variations of these techniques and observe how the different approaches affect the results.

The goal is not only to make the query work, but also to understand:

- What each technique does
- When to use it
- How the techniques differ
- How to organize complex SQL
- How to choose an appropriate approach for a given problem
