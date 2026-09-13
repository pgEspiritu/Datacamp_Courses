# 🔗 Set Theory for SQL Joins

## 🎯 Set Operations

SQL has **three main set operations**:

- `UNION`
- `INTERSECT`
- `EXCEPT`

Set operations work differently from the joins covered earlier.

### 📌 This Lesson

Focuses on:

- `UNION`
- `UNION ALL`

---

# 🔵 UNION

`UNION` combines the records from **two tables** and returns records from both.

### ⚠️ Duplicate Records

`UNION` **removes duplicate records**.

If the same record appears in both tables, it is returned **only once**.

### 💡 Example

If:

- Table 1 = 4 records
- Table 2 = 5 records
- 2 records are duplicates

`UNION` returns:

**7 records**

---

# 🟢 UNION ALL

`UNION ALL` also combines the records from two tables, but it **keeps duplicates**.

### 💡 Example

Using the same tables:

- Table 1 = 4 records
- Table 2 = 5 records
- 2 records are duplicates

`UNION ALL` returns:

**9 records**

---

# 🧩 UNION / UNION ALL Syntax

Set operations use **two `SELECT` statements** with the set operation between them.

SELECT column1, column2
FROM table1
UNION
SELECT column1, column2
FROM table2;

For `UNION ALL`:

SELECT column1, column2
FROM table1
UNION ALL
SELECT column1, column2
FROM table2;

### 🚨 Important Difference from JOINs

Set operations **do not use `ON` or `USING`**.

Joins compare and merge tables based on matching fields.

Set operations **stack the fields/records from one result on top of the other**.

---

# ⚠️ Requirements for Set Operations

For the two `SELECT` statements:

### 1️⃣ Same Number of Columns

The number of selected columns must be **identical**.

### 2️⃣ Matching Data Types

The respective columns must have **identical data types**.

❌ Cannot stack a **number** field on top of a **character** field.

### 3️⃣ Field Names Come from First SELECT

The result uses the **field names or aliases from the first `SELECT` statement**.

---

# 👑 World Leaders Example

Using the:

- `prime_ministers` table
- `monarchs` table

We can use `UNION` to combine prime ministers and monarchs.

The `monarch` field is aliased as `leader`.

SELECT country, monarch AS leader
FROM monarchs
UNION
SELECT country, prime_minister
FROM prime_ministers;

The resulting field is named:

`leader`

because the alias comes from the **first `SELECT` statement**.

---

# 🔄 UNION vs UNION ALL

| Operation | Returns Records | Removes Duplicates? |
|---|---|---|
| `UNION` | Both tables | ✅ Yes |
| `UNION ALL` | Both tables | ❌ No |

### 👑 World Leaders Example

Some people can be both **monarch and prime minister**.

For example:

- Oman
- Brunei

With `UNION`:

`Oman` and `Brunei` appear **once** because the person is the same.

With `UNION ALL`:

`Oman` and `Brunei` appear **twice**, showing that the records exist in both tables.

Norway can appear twice with `UNION` when its monarch and prime minister are **different people**.

---

# 🧠 Exam Key Points

- `UNION` = combines results and **removes duplicates**.
- `UNION ALL` = combines results and **keeps duplicates**.
- Set operations use **`SELECT` + set operator + `SELECT`**.
- ❌ No `ON` condition.
- The two `SELECT` statements must have the **same number of columns**.
- Corresponding columns must have the **same data types**.
- Result field names come from the **first `SELECT`**.
- Set operations **stack results**, rather than joining tables based on relationships.

### 💡 Memory Aid

**UNION = Combine + Remove Duplicates** 🧹  
**UNION ALL = Combine + Keep All** 📚
