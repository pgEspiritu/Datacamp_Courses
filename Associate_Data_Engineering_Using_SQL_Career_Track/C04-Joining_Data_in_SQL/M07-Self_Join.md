# 🔄 Self Joins

## 🎯 What is a Self Join?

A **self join** is when a table is **joined with itself**.

It is used to **compare values from one part of a table with values from another part of the same table**.

### 📌 Example

Using the `prime_ministers` table, we want to find **pairs of countries that are on the same continent**.

---

## 🔑 Key Points

- A self join **joins a table to itself**.
- There is **no dedicated `SELF JOIN` syntax** in SQL.
- A self join requires **table aliases** so the two instances of the same table can be distinguished.
- A self join can also be an **INNER JOIN**.
- The important part is defining the **matching fields in the `ON` clause**.

---

## 🧩 Self Join Syntax

SELECT p1.country, p2.country, p1.continent, p2.continent
FROM prime_ministers AS p1
INNER JOIN prime_ministers AS p2
ON p1.continent = p2.continent
LIMIT 10;

### 🔍 How it works

`p1` and `p2` are **aliases for the same `prime_ministers` table**.

The join condition:

`p1.continent = p2.continent`

finds countries that belong to the **same continent**.

Because each country can match other countries in the same continent, the result produces **country pairs**.

---

## ⚠️ Problem: Countries Match Themselves

The initial self join also produces pairs such as:

`Portugal → Portugal`

This happens because a country is in the same continent as itself.

We need to exclude these records.

### ✅ Solution: Add `AND` + `<>`

ON p1.continent = p2.continent
AND p1.country <> p2.country

`<>` means **not equal to**.

This removes records where:

`p1.country = p2.country`

---

## 🧠 Final Concept

A self join can be used to create **pairs within the same table**.

For the `prime_ministers` example:

**Same continent** ✅  
**Different country** ✅

Result:

**All pairs of countries in the same continent, excluding a country paired with itself.**

---

## 📌 Exam Key Points

| Concept | Meaning |
|---|---|
| **Self Join** | Joining a table with itself |
| **Dedicated `SELF JOIN` syntax** | ❌ None |
| **Alias required** | ✅ Yes |
| **Can use `INNER JOIN`** | ✅ Yes |
| `p1` / `p2` | Aliases representing the same table |
| `<>` | Not equal to |
| `AND` in `ON` | Requires multiple join conditions |

### 💡 Memory Aid

**Self Join = Same Table + Aliases + Compare Its Rows** 🔄
