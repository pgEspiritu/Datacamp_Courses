# 🔍 Subquerying with Semi Joins and Anti Joins

## 🎯 Nested SQL Queries

A **subquery** is a SQL query **embedded inside another SQL query**.

This lesson introduces:

- **Semi joins**
- **Anti joins**
- **Subqueries**

---

# ➕ Additive Joins

The six joins covered earlier are **additive** because they add columns to the original **left table**.

For example, an `INNER JOIN` can add columns from the right table to the result.

### 📌 Important

When fields have different names, they are added with their original names.

When fields have the same name, both can appear in the result, creating duplicate column names.

This can be changed using **aliasing**.

---

# ✅ Semi Join

A **semi join** chooses records from the first table when a condition is met in the second table.

Unlike regular joins:

- It does **not** use the `JOIN` keyword.
- It does **not** add columns from the second table.
- It uses the `WHERE` clause to determine which records are included.

### 💡 Basic Idea

Return values from `left_table` where `col1` exists in `col2` of `right_table`.

Conceptually:

`left_table.col1 IN right_table.col2`

Only the matching records from the **left table** are returned.

---

# 🧩 Semi Join Example

Suppose we want to determine the **presidents of countries that gained independence before 1800**.

We want:

- `country`
- `continent`
- `president`

The `indep_year` field is in the `states` table, not the `presidents` table.

First, find countries with independence year before 1800:

SELECT country
FROM states
WHERE indep_year < 1800;

The lesson's database returns:

- Spain
- Portugal

We can use this result as a filter for another query.

---

# 🧠 Subquery

A **subquery** is a query embedded inside another query.

The list of countries returned by the first query can be placed inside the `WHERE` clause of the main query.

SELECT country, continent, president
FROM presidents
WHERE country IN (
    SELECT country
    FROM states
    WHERE indep_year < 1800
);

The subquery provides the list used to filter the main query.

Since **Spain does not have a president** in the database, only the **Portuguese president** is returned.

---

# 🚫 Anti Join

An **anti join** chooses records from the first table where the value **does NOT find a match** in the second table.

Unlike regular joins:

- It does **not** add columns.
- It can be implemented using `WHERE`.
- It uses `NOT IN` to exclude matching values.

### 💡 Basic Idea

Return values from `left_table` where `col1` is **not** found in `col2` of `right_table`.

Conceptually:

`left_table.col1 NOT IN right_table.col2`

---

# 🌎 Anti Join Example

Suppose we want to find **countries in the Americas founded after 1800**.

First, filter for:

`continent = 'Americas'`

Then use `NOT IN` with the independence-year condition.

SELECT country, continent, president
FROM presidents
WHERE continent = 'Americas'
AND country NOT IN (
    SELECT country
    FROM states
    WHERE indep_year <= 1800
);

The result in the lesson includes:

- Chile
- Uruguay

The USA is excluded because it gained independence **before 1800**.

---

# 🔄 Semi Join vs Anti Join

| Type | Condition | Result |
|---|---|---|
| **Semi Join** ✅ | Match exists | Returns matching records from first table |
| **Anti Join** 🚫 | Match does not exist | Returns non-matching records from first table |

### SQL Pattern

**Semi Join:**

`WHERE column IN (subquery)`

**Anti Join:**

`WHERE column NOT IN (subquery)`

---

# 📌 Key Exam Points

- **Subquery** = query inside another query.
- **Semi join** uses `WHERE ... IN (...)`.
- **Anti join** uses `WHERE ... NOT IN (...)`.
- Semi joins return records from the **first table only**.
- Anti joins return records from the **first table only**.
- ❌ No new columns are added.
- The subquery provides the values used to filter the main query.
- Semi join = **find matches** ✅
- Anti join = **exclude matches** 🚫

### 💡 Memory Aid

**IN → Match → Semi Join** ✅  
**NOT IN → No Match → Anti Join** 🚫  
**Subquery → Query inside a Query** 🔍
