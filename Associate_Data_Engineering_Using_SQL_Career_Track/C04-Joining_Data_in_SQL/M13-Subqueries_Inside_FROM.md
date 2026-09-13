# 📦 Subqueries Inside `FROM`

## 🎯 Subquery in FROM

A **subquery inside a `FROM` clause** can be used as a **temporary table**.

The outer query can then `SELECT` from this subquery.

---

# 🧩 Example Problem

Suppose we want:

- All **continents with monarchs**
- The **most recent country to gain independence** in each continent

First, find the most recent independence year for each continent.

SELECT continent,
       MAX(indep_year) AS most_recent
FROM states
GROUP BY continent;

This groups records by `continent` and uses `MAX()` to find the most recent independence year for each group.

---

# 📋 Multiple Tables in FROM

Multiple tables can be included in a `FROM` clause by separating them with a comma.

SELECT ...
FROM left_table, right_table;

This can produce **duplicate records** when multiple rows match between the tables.

### ✅ Remove Duplicates

Use:

`DISTINCT`

Example:

SELECT DISTINCT id
FROM left_table, right_table;

---

# 🔍 Subquery as a Temporary Table

The previous subquery can be placed inside the `FROM` clause.

The subquery is given the alias:

`sub`

Then the outer query can use it like a table.

SELECT DISTINCT m.continent,
       sub.most_recent
FROM monarchs AS m,
     (
         SELECT continent,
                MAX(indep_year) AS most_recent
         FROM states
         GROUP BY continent
     ) AS sub
WHERE m.continent = sub.continent
ORDER BY m.continent;

---

# 🧠 How It Works

### 1️⃣ Subquery

The subquery finds the **most recent independence year for each continent**.

`MAX(indep_year) AS most_recent`

### 2️⃣ Temporary Table

The subquery is placed in `FROM` and given the alias:

`sub`

It can now be treated as a temporary table.

### 3️⃣ Match Continents

The `WHERE` clause matches:

`m.continent = sub.continent`

This keeps continents that appear in both:

- `monarchs`
- the subquery

### 4️⃣ Remove Duplicates

Because a continent can have multiple monarch records, duplicates may occur.

Use:

`SELECT DISTINCT`

to keep each continent only once.

### 5️⃣ Select the Result

`sub.most_recent`

returns the most recent independence year for each matching continent.

### 6️⃣ Sort

`ORDER BY continent`

sorts the final result by continent.

---

# 📌 Exam Key Points

- A subquery can be placed inside the **`FROM` clause**.
- A subquery in `FROM` acts as a **temporary table**.
- A subquery in `FROM` must have an **alias**.
- Multiple tables can be listed in `FROM` using commas.
- Multiple matches can create **duplicates**.
- `DISTINCT` removes duplicate results.
- The outer query can select fields from the subquery using its alias, such as:
  `sub.most_recent`

### 💡 Memory Aid

**Subquery in `WHERE` → Filter 🔎**  
**Subquery in `SELECT` → Calculate ➕**  
**Subquery in `FROM` → Temporary Table 📦**
