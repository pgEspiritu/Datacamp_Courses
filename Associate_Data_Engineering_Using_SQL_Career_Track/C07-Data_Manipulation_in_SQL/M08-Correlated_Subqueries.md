# 📘 Correlated Subqueries — Markdown Notes

## 1. Correlated Subqueries

A **correlated subquery** is a special type of subquery that uses values from the **outer/main query** to produce its results.

Unlike a simple subquery, a correlated subquery depends on the current row of the outer query.

### 🔑 Key Idea

> **The outer query provides a value → the subquery uses that value → the subquery produces a result for that row.**

The subquery is generally evaluated repeatedly as the outer query processes rows.

---

## 2. Correlated Subquery vs. Simple Subquery

| Feature                 | Simple Subquery                     | Correlated Subquery                                    |
| ----------------------- | ----------------------------------- | ------------------------------------------------------ |
| Depends on outer query? | ❌ No                                | ✅ Yes                                                  |
| Can run independently?  | ✅ Usually                           | ❌ No                                                   |
| Evaluation              | Usually once                        | Repeated for outer-query rows                          |
| Performance             | Generally faster                    | Can be slower                                          |
| Main use                | Extraction, filtering, calculations | Advanced filtering, calculations, replacing some joins |

### Simple Subquery

```sql
SELECT *
FROM matches
WHERE season = (
    SELECT MAX(season)
    FROM matches
);
```

The inner query does **not** depend on the outer query.

### Correlated Subquery

```sql
SELECT
    c.name,
    (
        SELECT AVG(m.home_goal + m.away_goal)
        FROM match AS m
        WHERE m.country_id = c.id
    ) AS avg_goals
FROM country AS c;
```

The inner query refers to `c.id`.

`c` comes from the **outer query**, making this a correlated subquery.

---

## 3. How a Correlated Subquery Works

Consider:

```sql
SELECT
    c.name,
    (
        SELECT AVG(m.home_goal + m.away_goal)
        FROM match AS m
        WHERE m.country_id = c.id
    ) AS avg_goals
FROM country AS c;
```

### Outer Query

```sql
SELECT c.name
FROM country AS c
```

The outer query goes through each country.

### Inner Query

```sql
SELECT AVG(m.home_goal + m.away_goal)
FROM match AS m
WHERE m.country_id = c.id
```

The inner query calculates the average goals **for the current country**.

The important part is:

```sql
m.country_id = c.id
```

* `m.country_id` → comes from the inner query
* `c.id` → comes from the outer query

Because the subquery uses `c.id`, it is **correlated**.

---

## 4. Correlated Subquery in `WHERE`

A correlated subquery can also be used for filtering.

Example:

```sql
SELECT
    s.stage,
    AVG(m.home_goal + m.away_goal) AS avg_goals
FROM match AS m
JOIN (
    SELECT DISTINCT stage
    FROM match
) AS s
    ON m.stage = s.stage
GROUP BY s.stage
HAVING AVG(m.home_goal + m.away_goal) > (
    SELECT AVG(m2.home_goal + m2.away_goal)
    FROM match AS m2
    WHERE m2.stage = s.stage
);
```

The important concept is that the inner query refers to `s.stage` from the outer query.

The subquery is therefore **correlated with the outer query**.

---

## 5. Correlated Subqueries Can Replace Joins

A correlated subquery can sometimes accomplish something that would normally be done with a `JOIN`.

### Using a JOIN

```sql
SELECT
    c.name,
    AVG(m.home_goal + m.away_goal) AS avg_goals
FROM country AS c
JOIN match AS m
    ON c.id = m.country_id
GROUP BY c.name;
```

### Using a Correlated Subquery

```sql
SELECT
    c.name,
    (
        SELECT AVG(m.home_goal + m.away_goal)
        FROM match AS m
        WHERE m.country_id = c.id
    ) AS avg_goals
FROM country AS c;
```

Both approaches can produce the average number of goals for each country.

The correlated version replaces the explicit `JOIN` with a condition inside the subquery:

```sql
WHERE m.country_id = c.id
```

---

## 6. Scalar Correlated Subquery

A **scalar subquery** returns a single value.

Example:

```sql
SELECT
    c.name,
    (
        SELECT AVG(m.home_goal + m.away_goal)
        FROM match AS m
        WHERE m.country_id = c.id
    ) AS avg_goals
FROM country AS c;
```

The subquery returns one average value for each country.

Result conceptually:

| name    | avg_goals |
| ------- | --------: |
| England |      2.75 |
| Spain   |      2.61 |
| Germany |      2.84 |
| France  |      2.58 |

---

## 7. The Most Important Pattern

When you see this structure:

```sql
SELECT
    outer_table.column,
    (
        SELECT AGGREGATE(inner_table.column)
        FROM inner_table
        WHERE inner_table.key = outer_table.key
    )
FROM outer_table;
```

you are likely looking at a **correlated subquery**.

### Example

```sql
SELECT
    c.name,
    (
        SELECT AVG(m.home_goal + m.away_goal)
        FROM match AS m
        WHERE m.country_id = c.id
    ) AS avg_goals
FROM country AS c;
```

### Remember

```text
Outer query
     ↓
c.id
     ↓
Inner query
     ↓
WHERE m.country_id = c.id
     ↓
Calculate result for that outer row
```

---

## 8. Why Correlated Subqueries Can Be Slower

A correlated subquery may be evaluated repeatedly for different rows of the outer query.

For example:

```text
Country 1 → run subquery
Country 2 → run subquery
Country 3 → run subquery
Country 4 → run subquery
...
```

If the outer query produces many rows, the subquery may need to perform many calculations.

Therefore:

> ⚠️ **Correlated subqueries can be slower than other approaches, especially on large datasets.**

When possible, a `JOIN` with appropriate aggregation may be more efficient.

---

## 9. Simple vs. Correlated Subquery — Quick Comparison

### Simple Subquery

```sql
SELECT *
FROM match
WHERE home_goal > (
    SELECT AVG(home_goal)
    FROM match
);
```

The inner query:

```sql
SELECT AVG(home_goal)
FROM match
```

doesn't need information from the outer query.

### Correlated Subquery

```sql
SELECT
    c.name,
    (
        SELECT AVG(m.home_goal + m.away_goal)
        FROM match AS m
        WHERE m.country_id = c.id
    ) AS avg_goals
FROM country AS c;
```

The inner query needs `c.id` from the outer query.

---

# 🧠 Main Takeaways

* **Correlated subquery** = a subquery that depends on the outer query.
* It uses a value from the outer query inside the inner query.
* It is commonly used for:

  * Advanced filtering
  * Calculations
  * Comparing each row with related data
  * Replacing some joins
* A correlated subquery **cannot normally run independently** because it references the outer query.
* Simple subqueries are generally evaluated independently of the outer query.
* Correlated subqueries may be evaluated repeatedly and can therefore affect performance.
* A common pattern is:

```sql
WHERE inner_table.key = outer_table.key
```

### ⭐ Easiest Way to Identify One

Ask:

> **"Does the subquery refer to a column or alias from the outer query?"**

If **YES** → it is likely a **correlated subquery**.

If **NO** → it is likely a **simple subquery**.
