# 🔗 Correlated Subquery with Multiple Conditions

## 🎯 Objective

Correlated subqueries can use **multiple conditions** to match the current row in the main query with the appropriate rows in the subquery.

In the previous exercise, the correlated subquery compared matches with the average total goals for each country.

This time, we want to find:

> ⚽ The highest-scoring match for **each country, in each season**.

To do this, the subquery must match both:

- `country_id`
- `season`

---

# 📝 Original Question

Correlated subqueries are useful for matching data across multiple columns.

In the previous exercise, you generated a list of matches with extremely high scores for each country.

In this exercise, you're going to add an additional column for matching to answer the question:

> What was the highest scoring match for each country, in each season?

**Note:** This query may take a while to load.

### Instructions

- Complete the subquery to select the matches with the **highest** number of **total** goals.
- Match the subquery to the main query using the `country_id` and `season` columns in both tables.

---

# ✅ Answer

    SELECT
        main.country_id,
        main.date,
        main.home_goal,
        main.away_goal

    FROM match AS main

    WHERE

        -- Keep matches with the maximum total goals
        (main.home_goal + main.away_goal) =

        (
            -- Find the highest total goals
            SELECT MAX(sub.home_goal + sub.away_goal)

            FROM match AS sub

            -- Match the same country
            -- and the same season
            WHERE main.country_id = sub.country_id
              AND main.season = sub.season
        );

---

# 🔍 How the Query Works

The most important part is:

    WHERE main.country_id = sub.country_id
      AND main.season = sub.season

Previously, we matched only:

    main.country_id = sub.country_id

Now we match **two columns**.

This makes the comparison specific to:

    Country + Season

---

# 1. 📋 Main Query

The main query starts with:

    SELECT
        main.country_id,
        main.date,
        main.home_goal,
        main.away_goal
    FROM match AS main

The alias:

    main

represents the match currently being examined.

For example:

| country_id | season | date | home_goal | away_goal |
|---:|---|---|---:|---:|
| 1 | 2012/2013 | 2013-01-10 | 4 | 2 |
| 1 | 2012/2013 | 2013-02-15 | 2 | 1 |
| 1 | 2013/2014 | 2013-09-20 | 5 | 0 |

The query examines each match and asks:

> Is this match the highest-scoring match for its country and season?

---

# 2. ⚽ Calculate Total Goals

The main query calculates total goals using:

    main.home_goal + main.away_goal

For example:

    home_goal = 4
    away_goal = 2

Therefore:

    4 + 2 = 6

The query then compares this total with the maximum total goals returned by the subquery.

---

# 3. 🧮 The Subquery Uses `MAX()`

The subquery is:

    (
        SELECT MAX(sub.home_goal + sub.away_goal)
        FROM match AS sub
        WHERE main.country_id = sub.country_id
          AND main.season = sub.season
    )

The important function is:

    MAX()

It finds the **largest total-goal value** among the relevant matches.

---

# 4. 🌍 Match the Country

The first condition is:

    main.country_id = sub.country_id

This means:

> Only compare the current match with matches from the same country.

For example:

    main.country_id = 1

The subquery considers:

    sub.country_id = 1

It does not compare the match against matches from other countries.

---

# 5. 📅 Match the Season

The second condition is:

    main.season = sub.season

This means:

> Only compare the current match with matches from the same season.

For example:

    main.season = '2013/2014'

The subquery considers:

    sub.season = '2013/2014'

It does not compare the match against matches from other seasons.

---

# 6. 🔗 Two Conditions Create a Specific Group

Together:

    WHERE main.country_id = sub.country_id
      AND main.season = sub.season

means:

> Find matches belonging to the same country **AND** the same season as the current main match.

This creates a group based on:

    country_id + season

---

# 📊 Example

Suppose the data contains:

| country_id | season | total_goals |
|---:|---|---:|
| 1 | 2012/2013 | 4 |
| 1 | 2012/2013 | 7 |
| 1 | 2012/2013 | 3 |
| 1 | 2013/2014 | 5 |
| 1 | 2013/2014 | 9 |
| 2 | 2012/2013 | 8 |
| 2 | 2012/2013 | 4 |

For:

    country_id = 1
    season = 2012/2013

the subquery sees:

    4
    7
    3

Then:

    MAX(4, 7, 3) = 7

The main query checks:

    main total goals = 7

If true, the match is returned.

---

# 🧩 Why Both Conditions Are Necessary

Imagine we only used:

    main.country_id = sub.country_id

The query would find the highest-scoring match across **all seasons** for that country.

That is not what we want.

We want the highest-scoring match:

    for each country
    AND
    for each season

Therefore we need:

    main.country_id = sub.country_id
    AND
    main.season = sub.season

---

# 🆚 One Condition vs. Two Conditions

## Previous Exercise

    WHERE main.country_id = sub.country_id

Comparison:

    Country → all seasons

## This Exercise

    WHERE main.country_id = sub.country_id
      AND main.season = sub.season

Comparison:

    Country + Season

### 🧠 Think of it this way:

    country_id
        ↓
    Narrow down to country
        ↓
    season
        ↓
    Narrow down to season
        ↓
    MAX(total goals)
        ↓
    Compare with main match

---

# 🔄 Step-by-Step Processing

Suppose SQL is examining this main match:

    country_id = 1
    season = '2012/2013'
    home_goal = 5
    away_goal = 3

### Step 1 — Calculate current match total

    5 + 3 = 8

### Step 2 — Enter the correlated subquery

    SELECT MAX(sub.home_goal + sub.away_goal)

### Step 3 — Match the country

    main.country_id = sub.country_id

### Step 4 — Match the season

    main.season = sub.season

### Step 5 — Find maximum total goals

Suppose the maximum is:

    8

### Step 6 — Compare

    8 = 8

TRUE ✅

Therefore, the match is returned.

---

# 🧠 Important Difference: `AVG()` vs. `MAX()`

The previous exercise used:

    AVG()

This exercise uses:

    MAX()

### `AVG()`

Finds the average:

    AVG(home_goal + away_goal)

Used for identifying matches above an average threshold.

### `MAX()`

Finds the highest value:

    MAX(home_goal + away_goal)

Used for identifying the highest-scoring match.

---

# 🏆 What Does the Query Return?

The query returns matches where:

    total goals = maximum total goals
                  for that country
                  in that season

Therefore, the result represents the highest-scoring match or matches for each:

    country + season

---

# ⚠️ Ties Are Possible

An important point is that the query can return **more than one match** for the same country and season.

For example:

| country_id | season | home_goal | away_goal | total |
|---:|---|---:|---:|---:|
| 1 | 2012/2013 | 5 | 3 | 8 |
| 1 | 2012/2013 | 6 | 2 | 8 |

Both have:

    total_goals = 8

And:

    MAX(total_goals) = 8

Therefore, both matches satisfy:

    total_goals = MAX(total_goals)

So both can be returned.

---

# 🔗 Why This Is a Correlated Subquery

The subquery contains:

    main.country_id

and:

    main.season

These columns come from the outer query.

Therefore, the subquery depends on the current row of the main query.

That makes it a:

> **Correlated subquery**

---

# 📌 General Pattern

This exercise demonstrates a very useful pattern:

    SELECT ...
    FROM table AS main
    WHERE main.value =
        (
            SELECT MAX(sub.value)
            FROM table AS sub
            WHERE main.group1 = sub.group1
              AND main.group2 = sub.group2
        );

In this example:

    main.value
    → main.home_goal + main.away_goal

    MAX(sub.value)
    → maximum total goals

    main.group1 = sub.group1
    → country_id

    main.group2 = sub.group2
    → season

---

# 🧠 Mental Model

Think:

    MAIN MATCH
        ↓
    What country?
        ↓
    What season?
        ↓
    Find all matches from that country + season
        ↓
    Find MAX(total goals)
        ↓
    Compare with current match
        ↓
    Equal?
      ↙   ↘
    YES    NO
     ↓      ↓
    Keep   Exclude

---

# ⚡ Quick Reference

## Correlated Subquery with One Condition

    WHERE main.country_id = sub.country_id

➡️ Compare within the same country.

## Correlated Subquery with Two Conditions

    WHERE main.country_id = sub.country_id
      AND main.season = sub.season

➡️ Compare within the same country **and season**.

## Find Maximum

    MAX(home_goal + away_goal)

➡️ Finds the highest total goals.

## Find Maximum Within a Group

    SELECT MAX(sub.home_goal + sub.away_goal)
    FROM match AS sub
    WHERE main.country_id = sub.country_id
      AND main.season = sub.season

➡️ Finds the highest total goals for the current match's country and season.

---

# 🎯 Key Takeaways

- Correlated subqueries can reference **multiple columns** from the main query.
- Use `AND` when multiple columns must match.
- `main.country_id = sub.country_id` matches the country.
- `main.season = sub.season` matches the season.
- `MAX()` identifies the highest total goals.
- The query compares each match with the maximum score for its specific `country_id + season` group.
- Multiple matches can be returned if there is a tie for the highest score.
- Table aliases such as `main` and `sub` make correlated references clear.
- Adding more matching conditions makes the correlated comparison more specific.

---

# ⭐ Final Memory Trick

**Correlated subquery + multiple conditions = compare each row against a value calculated for its specific group.**

    main.country_id = sub.country_id
          +
    main.season = sub.season
          ↓
    SAME COUNTRY + SAME SEASON
          ↓
    MAX(total goals)
          ↓
    Find highest-scoring match
