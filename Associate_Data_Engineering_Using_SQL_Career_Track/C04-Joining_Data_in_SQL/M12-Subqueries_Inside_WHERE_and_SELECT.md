# 🔍 Subqueries Inside `WHERE` and `SELECT`

## 🎯 Subqueries

A **subquery** is a SQL query embedded inside another query.

This lesson covers:

- Subqueries inside `WHERE`
- Subqueries inside `SELECT`

---

# 📌 Subqueries Inside `WHERE`

The `WHERE` clause is the **most common place for subqueries** because filtering data is one of the most common data manipulation tasks.

### 🧩 Basic Syntax

SELECT some_field
FROM some_table
WHERE some_field IN (
    SELECT some_numeric_field
    FROM another_table
);

The subquery is used as the argument for the `IN` operator.

---

# ⚠️ Data Type Requirement

The result of the subquery must have the **same data type** as the field being filtered.

For example:

`some_field` → numeric  
`subquery result` → numeric ✅

If their data types do not match, the query will not work.

### 📌 Important

The subquery inside `WHERE` can come from:

- The **same table**
- A **different table**

---

# 🔢 Subqueries Inside `SELECT`

A subquery can also be placed inside a `SELECT` statement.

### 🎯 Example

Suppose we want to count the **number of monarchs for each continent** listed in the `states` table.

The continents come from `states`, while the monarch data is in `monarchs`.

We can use a subquery to perform the count for each continent.

---

# 🧩 Subquery Inside SELECT Example

SELECT DISTINCT continent,
       (
           SELECT COUNT(*)
           FROM monarchs
           WHERE monarchs.continent = states.continent
       ) AS monarch_count
FROM states;

### 🔍 How It Works

The outer query:

`SELECT DISTINCT continent FROM states`

gets the distinct continents from the `states` table.

The subquery:

`SELECT COUNT(*) FROM monarchs`

counts the monarchs.

The condition:

`monarchs.continent = states.continent`

matches the continent in the `monarchs` table with the continent currently selected from `states`.

This allows the subquery to count the monarchs for each continent.

---

# ⚠️ Alias Requirement

A subquery inside a `SELECT` statement **requires an alias**.

Example:

`AS monarch_count`

Without an alias, the result of the subquery does not have a named output field.

---

# 🆚 WHERE vs SELECT Subqueries

| Location | Purpose |
|---|---|
| `WHERE` | Filter records using values returned by the subquery |
| `SELECT` | Calculate or return a value as part of the result |

### 💡 Memory Aid

**`WHERE` subquery → Filter 🔎**  
**`SELECT` subquery → Calculate/Return ➕**
