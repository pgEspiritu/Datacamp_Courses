# 🚫 EXCEPT

## 🎯 What is EXCEPT?

`EXCEPT` is a **set operation** that identifies records that are:

**present in the left table but NOT present in the right table.**

### 💡 Memory Aid

**EXCEPT = Left Only** ⬅️

---

# 🧩 EXCEPT Syntax

The syntax is similar to `UNION` and `INTERSECT`.

SELECT column1, column2
FROM left_table
EXCEPT
SELECT column1, column2
FROM right_table;

### 📌 Important

`EXCEPT` does **not** use `ON` or `USING`.

---

# 🔍 How EXCEPT Works

`EXCEPT` compares the records from the left and right tables.

Only records that:

✅ Exist in the **left table**  
❌ Do **not** exist in the **right table**

are returned.

### ⚠️ Whole Record Must Match

The entire selected record must match.

For example, if:

`id = 4`

exists in both tables, but another field is different, the records are **not considered a match**.

Therefore, the record from the left table is still returned.

---

# 👑 Example: Monarchs Who Are NOT Prime Ministers

Suppose we want to find monarchs who **do not also serve as prime minister**.

SELECT monarch, country
FROM monarchs
EXCEPT
SELECT prime_minister, country
FROM prime_ministers;

The result contains only the monarchs who **do not also hold the position of prime minister**.

---

# ⚠️ EXCEPT Requirements

Like the other set operations:

- Both `SELECT` statements must have the **same number of columns**.
- Corresponding columns must have **matching data types**.
- Matching is based on the **selected fields**.
- The result uses the field names from the **first `SELECT`**.

---

# 🧠 Set Operations Comparison

| Operation | Result |
|---|---|
| `UNION` | Records from both tables, **duplicates removed** |
| `UNION ALL` | Records from both tables, **duplicates kept** |
| `INTERSECT` | Records **common to both tables** |
| `EXCEPT` | Records in the **left table but not the right table** |

### 💡 Easy Memory Aid

**UNION** ➕ → Both  
**UNION ALL** ➕📋 → Both + duplicates  
**INTERSECT** 🔗 → Common to both  
**EXCEPT** 🚫 → Left but not right
