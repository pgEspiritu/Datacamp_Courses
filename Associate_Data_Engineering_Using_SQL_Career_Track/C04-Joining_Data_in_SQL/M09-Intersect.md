# 🎯 INTERSECT

## 🔵 What is INTERSECT?

`INTERSECT` is a **set operation** that takes two tables and returns only the **records that exist in both tables**.

### 💡 Memory Aid

**INTERSECT = Common Records** 🔗

---

# 🧩 INTERSECT Syntax

The syntax is similar to `UNION` and `UNION ALL`.

SELECT column1, column2
FROM table1
INTERSECT
SELECT column1, column2
FROM table2;

### 📌 Important

`INTERSECT` does **not** use `ON` or `USING`.

---

# ⚠️ Requirements

Like other set operations:

- Both `SELECT` statements must have the **same number of columns**.
- Corresponding columns must have **identical data types**.
- The result uses the **field names from the first `SELECT`**.
- For a record to be returned, **all selected fields must match**.

---

# 🔄 INTERSECT vs. INNER JOIN

Both can return records that have matching information, but they work differently.

| INTERSECT | INNER JOIN |
|---|---|
| Returns records common to both tables | Returns records with matching join conditions |
| All selected fields must match | Matching fields are specified with `ON` |
| Requires the same number of columns | Can join tables with different numbers of columns |
| Common records are returned only once | Can return duplicate values |
| Does not add columns from the other table | Can add columns from the other table |

### 🧠 Key Difference

**INTERSECT compares the complete selected records.**

**INNER JOIN compares the fields specified in the join condition.**

---

# 🌍 Example: Countries with Prime Ministers and Presidents

We can use `INTERSECT` to find countries that have **both a prime minister and a president**.

SELECT country
FROM prime_ministers
INTERSECT
SELECT country
FROM presidents;

The result contains the countries that appear in **both tables**.

---

# ⚠️ INTERSECT with Multiple Columns

Suppose we select:

`country, prime_minister`

instead of only:

`country`

INTERSECT now requires **both fields** to match.

SELECT country, prime_minister
FROM prime_ministers
INTERSECT
SELECT country, president
FROM presidents;

For a record to appear:

`country` must match ✅  
`prime_minister` must match `president` ✅

Since no country has a prime minister and president with the **same name**, the result is an **empty table**.

---

# 👑 Prime Ministers and Monarchs

Some monarchs also act as prime ministers.

Using both `country` and `leader`:

SELECT country, prime_minister
FROM prime_ministers
INTERSECT
SELECT country, monarch
FROM monarchs;

This can return records where **both the country and leader name match**.

---

# 📌 Exam Key Points

- `INTERSECT` = **records common to both tables**.
- All selected fields must match for a record to be returned.
- No `ON` or `USING`.
- Same number of columns is required.
- Corresponding columns need matching data types.
- Common records are returned **only once**.
- Result field names come from the **first `SELECT`**.
- Selecting more columns makes the matching requirement **more restrictive**.

### 💡 Memory Aid

**UNION** ➕ = Everything from both  
**UNION ALL** ➕📋 = Everything, including duplicates  
**INTERSECT** 🔗 = Only what both have
