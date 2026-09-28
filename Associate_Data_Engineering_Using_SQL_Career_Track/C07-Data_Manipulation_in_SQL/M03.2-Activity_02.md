# ⚽ Conditional Selection and Summation with CASE WHEN

## 📝 Overview

`CASE` statements can be placed inside aggregate functions such as `SUM()`.

This allows you to:

1. 🎯 Apply a condition
2. 🔢 Select the values that meet the condition
3. ➕ Calculate their total using `SUM()`

In this exercise, we want to calculate **Real Sociedad's total home and away goals per season**.

Real Sociedad's `team_id` is:

    8560

---

## 🎯 Instructions

**100 XP**

- Create a `CASE` statement to calculate the total number of **home goals** where `hometeam_id` is `8560`.
- Create a second `CASE` statement to calculate the total number of **away goals** where `awayteam_id` is `8560`, aliasing the column as `away_goals`.
- Group the query by `season`.

---

# 💡 Solution

    SELECT 
        season,

        -- SUM the home goals
        SUM(
            CASE 
                WHEN hometeam_id = 8560 
                THEN home_goal 
            END
        ) AS home_goals,

        -- SUM the away goals
        SUM(
            CASE 
                WHEN awayteam_id = 8560 
                THEN away_goal 
            END
        ) AS away_goals

    FROM match

    -- Group the results by season
    GROUP BY season;

---

# 🔍 Understanding the Query

## 1. Select the Season

    SELECT season

We want the results separated by season.

For example:

| season |
|---|
| 2011/2012 |
| 2012/2013 |
| 2013/2014 |
| 2014/2015 |

---

# 🏠 2. Calculate Real Sociedad's Home Goals

The important pattern is:

    SUM(
        CASE
            WHEN hometeam_id = 8560
            THEN home_goal
        END
    ) AS home_goals

Let's break it down.

### Step 1: Check the Team

    WHEN hometeam_id = 8560

This checks whether Real Sociedad was the **home team**.

### Step 2: Return the Home Goals

    THEN home_goal

If Real Sociedad was the home team, return the value from `home_goal`.

For example:

| hometeam_id | home_goal | CASE result |
|---:|---:|---:|
| 8560 | 2 | 2 |
| 8560 | 1 | 1 |
| 8455 | 3 | NULL |
| 8634 | 2 | NULL |

### Step 3: SUM the Results

`SUM()` adds the returned values:

    2 + 1 = 3

So the result is:

    home_goals = 3

---

# ✈️ 3. Calculate Real Sociedad's Away Goals

The second calculation is:

    SUM(
        CASE
            WHEN awayteam_id = 8560
            THEN away_goal
        END
    ) AS away_goals

This time, we check:

    awayteam_id = 8560

This means Real Sociedad was the **away team**.

Then we return:

    away_goal

and `SUM()` adds those values together.

---

# ⚠️ Important Correction to the Provided Code

The exercise text says to calculate **goals**, so the `THEN` clause should return the goal column:

### 🏠 Home goals

    THEN home_goal

### ✈️ Away goals

    THEN away_goal

Not:

    THEN hometeam_id

or:

    THEN awayteam_id

The team ID identifies **which team played**, while `home_goal` and `away_goal` contain the **number of goals**.

So the goal is:

    Team ID → determines whether Real Sociedad played
    Goal column → provides the value to SUM()

---

# 🧠 Why Use CASE Inside SUM()?

Think of the calculation as a filter inside the aggregation.

### Home goals

    SUM(
        CASE
            WHEN hometeam_id = 8560
            THEN home_goal
        END
    )

Conceptually:

    Is Real Sociedad the home team?
              ↓
           Yes
              ↓
      Return home_goal
              ↓
         SUM the goals

If Real Sociedad is not the home team:

    NULL

`SUM()` ignores those `NULL` values.

---

# 📊 4. GROUP BY season

The query ends with:

    GROUP BY season

This means the calculations are performed **separately for each season**.

Conceptually:

| Season | Home Goals | Away Goals |
|---|---:|---:|
| 2011/2012 | ... | ... |
| 2012/2013 | ... | ... |
| 2013/2014 | ... | ... |
| 2014/2015 | ... | ... |

Instead of calculating one total for all seasons, SQL calculates one total for each season.

---

# 🔄 Conditional Aggregation

This technique is called **conditional aggregation**.

The general pattern is:

    SUM(
        CASE
            WHEN condition
            THEN value
        END
    )

In this exercise:

    SUM(
        CASE
            WHEN hometeam_id = 8560
            THEN home_goal
        END
    )

The condition determines **which rows contribute to the sum**.

The returned value determines **what gets added**.

---

# 🧩 General Pattern

## Conditional SUM

    SUM(
        CASE
            WHEN condition
            THEN value
        END
    )

### Example

    SUM(
        CASE
            WHEN team_id = 123
            THEN goals
        END
    )

Means:

> Add the `goals` only when `team_id` equals `123`.

---

# 📌 COUNT vs SUM with CASE

These two patterns are related but do different things.

### 🔢 COUNT

    COUNT(
        CASE
            WHEN condition
            THEN id
        END
    )

Counts **how many rows** satisfy the condition.

### ➕

SUM

    SUM(
        CASE
            WHEN condition
            THEN value
        END
    )

Adds the **values** from rows satisfying the condition.

### Example

If Real Sociedad has three home matches:

| Match | Home Goals |
|---|---:|
| Match 1 | 2 |
| Match 2 | 1 |
| Match 3 | 3 |

Then:

    COUNT(CASE WHEN ... THEN id END)

returns:

    3

While:

    SUM(CASE WHEN ... THEN home_goal END)

returns:

    6

---

# 🎯 Key Takeaways

- `CASE` can be placed inside `SUM()`.
- `CASE` determines **which rows contribute** to the calculation.
- `THEN` determines **which value is aggregated**.
- For home goals, use `home_goal`.
- For away goals, use `away_goal`.
- Team IDs such as `8560` are used to identify the team.
- `SUM()` adds the selected goal values.
- If there is no `ELSE`, unmatched rows return `NULL`.
- `SUM()` ignores `NULL` values.
- `GROUP BY season` produces separate results for each season.
- This technique is called **conditional aggregation**.

---

# ⚡ Quick Reference

### 🏠 Home goals

    SUM(
        CASE
            WHEN hometeam_id = 8560
            THEN home_goal
        END
    ) AS home_goals

### ✈️ Away goals

    SUM(
        CASE
            WHEN awayteam_id = 8560
            THEN away_goal
        END
    ) AS away_goals

### 📊 Complete Pattern

    SELECT
        season,

        SUM(
            CASE
                WHEN hometeam_id = 8560
                THEN home_goal
            END
        ) AS home_goals,

        SUM(
            CASE
                WHEN awayteam_id = 8560
                THEN away_goal
            END
        ) AS away_goals

    FROM match

    GROUP BY season;

---

## ⭐ Remember

> **`CASE` decides which rows to include; `SUM()` adds the values from those rows.**
