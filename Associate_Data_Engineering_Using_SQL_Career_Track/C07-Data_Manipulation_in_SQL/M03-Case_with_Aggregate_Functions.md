# 📊 CASE WHEN with Aggregate Functions

## 1. CASE WHEN with Aggregate Functions

Great job so far! 🎉

Now let's take a look at how `CASE` statements can be combined with **aggregate functions** such as:

- `COUNT()`
- `SUM()`
- `AVG()`
- `ROUND()`

This allows us to create useful **summary tables** from our data.

---

## 2. In CASE You Need to Aggregate

`CASE` statements can be used for several purposes:

1. 🏷️ Create categories
2. 🔍 Filter data in the `WHERE` clause
3. 📊 Aggregate data based on a logical condition

The important idea is:

> A `CASE` statement can be placed **inside an aggregate function**.

For example:

    COUNT(
        CASE
            WHEN condition THEN column
        END
    )

---

# 🔢 COUNTing CASES

## 3. Counting Liverpool Wins

Suppose we want a summary table showing the number of **home and away games that Liverpool won in each season**.

The desired result might look conceptually like this:

| Season | Home Wins | Away Wins |
|---|---:|---:|
| 2011/2012 | ... | ... |
| 2012/2013 | ... | ... |
| 2013/2014 | ... | ... |
| 2014/2015 | ... | ... |

The question is:

> How can we count Liverpool's wins in each season?

The answer is to combine `CASE` with `COUNT()`.

---

## 4. CASE WHEN with COUNT

A `CASE` statement can be treated like another column in your query.

We can put it inside `COUNT()`.

For example, to count Liverpool's **home wins**:

    COUNT(
        CASE
            WHEN hometeam_id = 8650
                 AND home_goal > away_goal
            THEN id
        END
    )

The `WHEN` clause checks two conditions:

- Liverpool played as the **home team**
- Liverpool scored more goals than the away team

If both are true, the `CASE` returns the match `id`.

Then `COUNT()` counts the returned IDs.

### 🧠 The logic

    Liverpool home win
            ↓
    CASE returns match ID
            ↓
    COUNT() counts the ID
            ↓
    Number of Liverpool home wins

---

## 5. CASE WHEN with COUNT

We can create another `CASE` statement for Liverpool's **away wins**.

    COUNT(
        CASE
            WHEN awayteam_id = 8650
                 AND away_goal > home_goal
            THEN id
        END
    )

Then group the results by season:

    SELECT
        season,
        COUNT(
            CASE
                WHEN hometeam_id = 8650
                     AND home_goal > away_goal
                THEN id
            END
        ) AS home_wins,
        COUNT(
            CASE
                WHEN awayteam_id = 8650
                     AND away_goal > home_goal
                THEN id
            END
        ) AS away_wins
    FROM matches
    GROUP BY season;

The exact value of Liverpool's `team_api_id` depends on the database being used.

---

## 🔑 What Does COUNT() Actually Count?

Inside the `CASE`, you can return:

- 🔢 A number
- 📝 A string
- 🆔 A column
- 📊 Other values

For example:

    COUNT(
        CASE
            WHEN condition THEN id
        END
    )

`COUNT()` counts the **non-NULL values returned by the `CASE` statement**.

### Important Concept

If the condition is true:

    THEN id

returns a value.

If the condition is false and there is no `ELSE`:

    NULL

is returned.

`COUNT()` does **not** count `NULL`.

Therefore, only rows satisfying the condition are counted.

---

# ➕ CASE WHEN with SUM

## 6. CASE WHEN with SUM

`SUM()` can also be combined with `CASE`.

Suppose we want to calculate the number of **home and away goals Liverpool scored in each season**.

For Liverpool's home goals:

    SUM(
        CASE
            WHEN hometeam_id = 8650
            THEN home_goal
        END
    )

If Liverpool is the home team, the `CASE` returns `home_goal`.

Otherwise, it returns `NULL`.

`SUM()` then adds the returned values.

### 🧠 Logic

    Liverpool is home team
            ↓
    Return home_goal
            ↓
    SUM() adds the goals

---

## 💻 Example: Liverpool Home Goals

    SELECT
        season,
        SUM(
            CASE
                WHEN hometeam_id = 8650
                THEN home_goal
            END
        ) AS home_goals
    FROM matches
    GROUP BY season;

You can do the same thing for away goals:

    SUM(
        CASE
            WHEN awayteam_id = 8650
            THEN away_goal
        END
    ) AS away_goals

---

## ⚠️ Why Does `ELSE` Not Appear?

Consider:

    CASE
        WHEN hometeam_id = 8650
        THEN home_goal
    END

There is no `ELSE`.

When the condition is false, SQL assumes:

    ELSE NULL

So this:

    CASE
        WHEN condition THEN value
    END

is effectively:

    CASE
        WHEN condition THEN value
        ELSE NULL
    END

This is useful with aggregate functions because `SUM()`, `COUNT()`, and `AVG()` handle `NULL` values in ways that allow us to focus on the rows we want.

---

# 📈 CASE with AVG

## 7. The CASE is Fairly AVG...

You can also use `AVG()` with `CASE`.

The structure is almost exactly the same as `SUM()`.

Instead of:

    SUM(
        CASE
            WHEN hometeam_id = 8650
            THEN home_goal
        END
    )

use:

    AVG(
        CASE
            WHEN hometeam_id = 8650
            THEN home_goal
        END
    )

This calculates the **average number of home goals Liverpool scored per home game**.

---

## 🧠 SUM vs AVG

| Function | Purpose |
|---|---|
| `SUM()` | Adds values together |
| `AVG()` | Calculates the average |
| `COUNT()` | Counts non-NULL values |

The `CASE` determines **which rows contribute to the calculation**.

---

# 🔄 ROUNDing the AVG

## 8. A ROUNDed AVG

The average can produce many decimal places.

For example:

    1.857142857

We can use `ROUND()` to make the result easier to read.

`ROUND()` takes two arguments:

    ROUND(number, decimal_places)

Example:

    ROUND(AVG(
        CASE
            WHEN hometeam_id = 8650
            THEN home_goal
        END
    ), 2)

This rounds the average to **2 decimal places**.

---

## 💡 Function Structure

Think of the functions as being nested:

    ROUND(
        AVG(
            CASE
                WHEN condition
                THEN value
            END
        ),
        2
    )

The calculation happens conceptually from the inside out:

    CASE
      ↓
    AVG()
      ↓
    ROUND()

---

# 📊 Percentages with CASE and AVG

## 9. Calculating Percentages

One of the most useful applications of `CASE` with `AVG()` is calculating **percentages**.

Suppose we want to answer:

> What percentage of Liverpool's games did they win in each season?

We can use a special structure:

    CASE
        WHEN Liverpool won THEN 1
        WHEN Liverpool lost THEN 0
    END

Then calculate:

    AVG(CASE ... END)

---

## 🧮 Why Does AVG() Give Us a Percentage?

Suppose Liverpool has these results:

| Result | CASE Value |
|---|---:|
| Win | 1 |
| Loss | 0 |
| Win | 1 |
| Loss | 0 |
| Win | 1 |

The average is:

    (1 + 0 + 1 + 0 + 1) / 5 = 0.60

So:

    0.60 = 60%

The `1` represents a win.

The `0` represents a loss.

Therefore, the average represents the **proportion of games won**.

---

# 🎯 The Three-Part CASE Structure

## 10. Identifying Wins

The first part identifies Liverpool's wins:

    CASE
        WHEN
            (hometeam_id = 8650 AND home_goal > away_goal)
            OR
            (awayteam_id = 8650 AND away_goal > home_goal)
        THEN 1

If Liverpool won, return:

    1

---

## 11. Identifying Losses

The second part identifies Liverpool's losses:

    WHEN
        (hometeam_id = 8650 AND home_goal < away_goal)
        OR
        (awayteam_id = 8650 AND away_goal < home_goal)
    THEN 0

If Liverpool lost, return:

    0

---

## 12. Excluding Ties and Other Games

For everything else, return `NULL`.

Because there is no `ELSE`:

    ELSE NULL

is assumed.

Therefore:

- 🟢 Liverpool win → `1`
- 🔴 Liverpool loss → `0`
- 🟡 Tie → `NULL`
- ⚪ Game not involving Liverpool → `NULL`

The `NULL` values are excluded from the `AVG()` calculation.

---

## 💻 Complete Percentage Example

    SELECT
        season,
        AVG(
            CASE
                WHEN
                    (hometeam_id = 8650 AND home_goal > away_goal)
                    OR
                    (awayteam_id = 8650 AND away_goal > home_goal)
                THEN 1
                WHEN
                    (hometeam_id = 8650 AND home_goal < away_goal)
                    OR
                    (awayteam_id = 8650 AND away_goal < home_goal)
                THEN 0
            END
        ) AS win_percentage
    FROM matches
    GROUP BY season;

---

# 🔄 Making the Percentage Easier to Read

The result from `AVG()` will be a decimal such as:

    0.5833333333

We can use `ROUND()`:

    ROUND(
        AVG(
            CASE
                WHEN
                    (hometeam_id = 8650 AND home_goal > away_goal)
                    OR
                    (awayteam_id = 8650 AND away_goal > home_goal)
                THEN 1
                WHEN
                    (hometeam_id = 8650 AND home_goal < away_goal)
                    OR
                    (awayteam_id = 8650 AND away_goal < home_goal)
                THEN 0
            END
        ),
        2
    ) AS win_percentage

This produces:

    0.58

If you want the result displayed as an actual percentage:

    0.58 × 100 = 58%

---

# 🧠 The Big Idea

The most important pattern from this lesson is:

    AGGREGATE(
        CASE
            WHEN condition THEN value
            ELSE NULL
        END
    )

Different aggregate functions produce different results:

| Pattern | What it calculates |
|---|---|
| `COUNT(CASE WHEN ... THEN id END)` | Number of matching rows |
| `SUM(CASE WHEN ... THEN value END)` | Total of matching values |
| `AVG(CASE WHEN ... THEN value END)` | Average of matching values |
| `AVG(CASE WHEN ... THEN 1 WHEN ... THEN 0 END)` | Proportion/percentage |

---

# 📚 CASE + Aggregate Cheat Sheet

## 🔢 COUNT

Count rows matching a condition:

    COUNT(
        CASE
            WHEN condition
            THEN id
        END
    )

---

## ➕ SUM

Add values matching a condition:

    SUM(
        CASE
            WHEN condition
            THEN value
        END
    )

---

## 📈 AVG

Average values matching a condition:

    AVG(
        CASE
            WHEN condition
            THEN value
        END
    )

---

## 🔄 ROUND + AVG

Round an average:

    ROUND(
        AVG(
            CASE
                WHEN condition
                THEN value
            END
        ),
        2
    )

---

## 📊 Percentage Using AVG

Calculate the proportion of rows meeting a condition:

    AVG(
        CASE
            WHEN win_condition THEN 1
            WHEN loss_condition THEN 0
        END
    )

---

# 🎯 Key Takeaways

- `CASE` can be placed **inside aggregate functions**.
- `COUNT()` can count the non-NULL values returned by a `CASE`.
- `SUM()` can total values returned by a `CASE`.
- `AVG()` can calculate the average of values returned by a `CASE`.
- If there is no `ELSE`, the `CASE` returns `NULL` when no condition is met.
- Aggregate functions generally ignore `NULL` values.
- `COUNT(CASE...)` is useful for **counting conditional rows**.
- `SUM(CASE...)` is useful for **conditional totals**.
- `AVG(CASE...)` is useful for **conditional averages**.
- `AVG(CASE WHEN ... THEN 1 WHEN ... THEN 0 END)` can be used to calculate a **proportion or percentage**.
- `ROUND()` can make aggregate results easier to read.
- The general pattern is:

    AGGREGATE(
        CASE
            WHEN condition THEN value
        END
    )

---

# 🧩 Quick Mental Model

Think of the process like this:

    CASE
        ↓
    Decide which rows/values matter
        ↓
    Return a value or NULL
        ↓
    Aggregate function
        ↓
    COUNT / SUM / AVG
        ↓
    Summary result

### ⭐ Remember:

> **CASE decides what to include; the aggregate function decides what to do with it.**
