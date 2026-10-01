# 🧩 Nest a Subquery in FROM

## 🎯 Main Question

**What's the average number of matches per season where a team scored 5 or more goals? How does this differ by country?**

We will use a **nested, correlated subquery** to answer this question.

In some SQL problems, you may need to perform several transformations step by step. For example, you may need to:

1. Filter the matches.
2. Count the matches.
3. Group the counts by season and country.
4. Calculate an average from those counts.

Trying to do everything in one query can become difficult. Instead, you can use **nested subqueries** to perform each transformation in a separate step.

💡 **Key idea:**  
**Filter → Count → Group → Average**

---

# 📝 Instructions 1/3

### ❓ Question

**Generate a list of matches where at least one team scored 5 or more goals.**

### ✅ Answer

    -- Select matches where a team scored 5+ goals
    SELECT
        country_id,
        season,
        id
    FROM match
    WHERE home_goal >= 5
       OR away_goal >= 5;

---

## 🔍 Explanation

We want to identify matches where **at least one team scored 5 or more goals**.

The important condition is:

    WHERE home_goal >= 5
       OR away_goal >= 5

### 🏠 `home_goal >= 5`

Checks whether the **home team** scored at least 5 goals.

### ✈️ `away_goal >= 5`

Checks whether the **away team** scored at least 5 goals.

### 🔀 `OR`

We use `OR` because **either team** can satisfy the condition.

For example:

| home_goal | away_goal | Included? |
|---:|---:|:---|
| 5 | 1 | ✅ Yes |
| 1 | 5 | ✅ Yes |
| 7 | 3 | ✅ Yes |
| 2 | 2 | ❌ No |
| 4 | 5 | ✅ Yes |

---

## 📌 Why Select These Columns?

    SELECT
        country_id,
        season,
        id

These columns will be useful in the next steps:

- `country_id` → tells us **which country/league** the match belongs to.
- `season` → tells us **which season** the match occurred in.
- `id` → uniquely identifies the match and can be counted.

💡 The subquery is preparing a smaller dataset that contains only matches where **at least one team scored 5+ goals**.

---

# 🧠 Mental Model

Think of this first subquery as a **filtering step**:

    match table
        ↓
    Check home_goal >= 5
        OR
    Check away_goal >= 5
        ↓
    Keep qualifying matches
        ↓
    country_id + season + id

The next steps can then use this filtered result to perform additional calculations.

---

# 🔑 Key Takeaways

- `OR` is used when **either condition** can be true.
- `home_goal >= 5` identifies matches where the home team scored 5+.
- `away_goal >= 5` identifies matches where the away team scored 5+.
- `country_id`, `season`, and `id` are selected because they will be needed for later aggregation.
- This query is the **first layer** of the nested-subquery solution.
- The overall problem will eventually require multiple transformations.

---

# ⚡ Quick Reference

### Filter rows using OR

    SELECT column1, column2
    FROM table
    WHERE condition1
       OR condition2;

### Example

    SELECT
        country_id,
        season,
        id
    FROM match
    WHERE home_goal >= 5
       OR away_goal >= 5;

### 🧩 Nested-subquery workflow

    Step 1 → Filter qualifying matches
    Step 2 → Count matches by country and season
    Step 3 → Calculate the average number of matches per season
