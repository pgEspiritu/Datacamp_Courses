# 🪟 Sliding Windows in SQL

## 1. Sliding Windows

Window functions can calculate aggregate values, rankings, and information that changes as SQL moves through a dataset row by row.

These calculations are called **sliding windows**.

A sliding window performs calculations relative to the current row, using a specified range of rows before or after it.

### What can sliding windows calculate?

- Running totals
- Moving sums
- Running counts
- Moving averages
- Other calculations based on a changing group of rows

### 🧠 Key concept

A regular window function can calculate an overall average or an average for each partition.

A sliding window can calculate a value using a **specific range of rows relative to the current row**.

For example:

    Row 1 → Calculate using Row 1
    Row 2 → Calculate using Rows 1–2
    Row 3 → Calculate using Rows 1–3
    Row 4 → Calculate using Rows 1–4

This produces a running total when used with `SUM()`.

---

## 2. Sliding Windows

Sliding windows are especially useful when the calculation must change as you move through an ordered dataset.

### Example: Running total

Suppose Manchester City scored the following number of home goals in three matches:

| Match | Home goals |
|---|---:|
| Match 1 | 2 |
| Match 2 | 1 |
| Match 3 | 3 |

A running total would look like this:

| Match | Home goals | Running total |
|---|---:|---:|
| Match 1 | 2 | 2 |
| Match 2 | 1 | 3 |
| Match 3 | 3 | 6 |

The calculation changes for each row:

    Match 1: 2
    Match 2: 2 + 1 = 3
    Match 3: 2 + 1 + 3 = 6

### General syntax

    AGGREGATE_FUNCTION(column) OVER (
        ORDER BY column
        ROWS BETWEEN start_point AND end_point
    )

The `ROWS BETWEEN` clause defines the range of rows included in each calculation.

---

## 3. Sliding Window Keywords

A sliding window uses specific keywords inside the `OVER()` clause to determine which rows participate in the calculation.

### Basic structure

    ROWS BETWEEN start_point AND end_point

For example:

    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW

This means:

> Start at the first row in the ordered window and continue through the current row.

### Important keywords

| Keyword | Meaning |
|---|---|
| `PRECEDING` | Refers to rows before the current row |
| `FOLLOWING` | Refers to rows after the current row |
| `UNBOUNDED PRECEDING` | Starts at the first row of the window |
| `UNBOUNDED FOLLOWING` | Extends to the last row of the window |
| `CURRENT ROW` | Refers to the current row |

### Examples of window frames

**1. From the beginning to the current row**

    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW

Includes every row from the beginning of the ordered window through the current row.

**2. Current row and one preceding row**

    ROWS BETWEEN 1 PRECEDING AND CURRENT ROW

Includes the previous row and the current row, when a previous row exists.

**3. Two preceding rows and the current row**

    ROWS BETWEEN 2 PRECEDING AND CURRENT ROW

Includes up to three rows: two previous rows and the current row.

**4. Current row and one following row**

    ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING

Includes the current row and the next row, when a next row exists.

**5. Entire ordered window**

    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING

Includes every row in the ordered window.

### 🧠 Mental model

    PRECEDING
    → Look backward

    FOLLOWING
    → Look forward

    CURRENT ROW
    → Include the current row

    UNBOUNDED
    → Extend to the beginning or end

---

## 4. Sliding Window Example: Running Total

Suppose we want to calculate the running total of goals scored by Manchester City when playing at home during the `2011/2012` season.

We want the calculation to:

1. Include only Manchester City's home matches.
2. Include only the `2011/2012` season.
3. Sort matches by date, from oldest to most recent.
4. Sum home goals from the beginning of the season through the current match.

### SQL query

    SELECT
        date,
        home_goal,
        SUM(home_goal) OVER (
            ORDER BY date
            ROWS BETWEEN UNBOUNDED PRECEDING
                     AND CURRENT ROW
        ) AS running_total
    FROM match
    WHERE hometeam_id = 8456
      AND season = '2011/2012'
    ORDER BY date;

*Note: `8456` is an example team ID often used for Manchester City in football datasets; verify the ID against your particular database if necessary.*

### Explanation

**Step 1: Filter the matches**

    WHERE hometeam_id = 8456
      AND season = '2011/2012'

Keeps Manchester City's home matches in the specified season.

**Step 2: Order the rows by date**

    ORDER BY date

Inside `OVER()`, this establishes the order in which the running total is calculated.

**Step 3: Calculate the running total**

    SUM(home_goal) OVER (
        ORDER BY date
        ROWS BETWEEN UNBOUNDED PRECEDING
                 AND CURRENT ROW
    )

This adds the home goals from the first match through the current match.

**Step 4: Display the result**

    AS running_total

Names the new column containing the cumulative sum.

### Example result

*Illustrative values only.*

| date | home_goal | running_total |
|---|---:|---:|
| Match 1 | 2 | 2 |
| Match 2 | 1 | 3 |
| Match 3 | 3 | 6 |
| Match 4 | 0 | 6 |
| Match 5 | 2 | 8 |

The running total never decreases because each new row adds its home goals to the previous cumulative total.

### 🧠 Mental model

    Filter matches
        ↓
    Order by date
        ↓
    Start at the first match
        ↓
    Add goals through the current match
        ↓
    Display the running total

---

## 5. Sliding Window Frame: A Limited Range

You can also use `PRECEDING` to restrict the number of rows included in each calculation.

Instead of calculating a running total from the beginning of the season, you can calculate the sum of the current match and the previous match.

### SQL query

    SELECT
        date,
        home_goal,
        SUM(home_goal) OVER (
            ORDER BY date
            ROWS BETWEEN 1 PRECEDING AND CURRENT ROW
        ) AS two_match_total
    FROM match
    WHERE hometeam_id = 8456
      AND season = '2011/2012'
    ORDER BY date;

### How it works

The window frame:

    ROWS BETWEEN 1 PRECEDING AND CURRENT ROW

includes up to two rows:

- The previous match
- The current match

### Example result

*Illustrative values only.*

| Match | Home goals | Two-match total |
|---|---:|---:|
| Match 1 | 2 | 2 |
| Match 2 | 1 | 3 |
| Match 3 | 3 | 4 |
| Match 4 | 0 | 3 |
| Match 5 | 2 | 2 |

For Match 3, the calculation is:

    Match 2 goals + Match 3 goals
    = 1 + 3
    = 4

For Match 4:

    Match 3 goals + Match 4 goals
    = 3 + 0
    = 3

For the first match, no previous row exists, so only the current match is included.

### Important clarification

The frame does not automatically mean the current row plus the previous row in every query. The rows are determined by the `ORDER BY` inside `OVER()`.

For this example, `ORDER BY date` means that the preceding row is the previous match in date order.

---

## 6. Let's Practice! 🎯

You can use sliding windows for many different calculations.

### A. Running total

Calculate the cumulative sum from the first row through the current row.

    SUM(home_goal) OVER (
        ORDER BY date
        ROWS BETWEEN UNBOUNDED PRECEDING
                 AND CURRENT ROW
    )

### B. Current row and previous row

Calculate the sum of the current row and one preceding row.

    SUM(home_goal) OVER (
        ORDER BY date
        ROWS BETWEEN 1 PRECEDING AND CURRENT ROW
    )

### C. Current row and next row

Calculate the sum of the current row and one following row.

    SUM(home_goal) OVER (
        ORDER BY date
        ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING
    )

### D. Moving average over the current and previous two rows

Calculate the average using up to three rows.

    AVG(home_goal) OVER (
        ORDER BY date
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    )

### E. Running total within each season

Calculate a separate running total for every season.

    SUM(home_goal) OVER (
        PARTITION BY season
        ORDER BY date
        ROWS BETWEEN UNBOUNDED PRECEDING
                 AND CURRENT ROW
    )

The `PARTITION BY season` clause restarts the calculation for each season.

---

## 🔑 Key Takeaways

1. **Sliding windows** calculate values using a defined range of rows relative to the current row.
2. `ROWS BETWEEN` defines the starting and ending boundaries of the window frame.
3. `PRECEDING` refers to earlier rows, while `FOLLOWING` refers to later rows.
4. `UNBOUNDED PRECEDING` means the first row of the ordered window.
5. `CURRENT ROW` includes the current row in the calculation.
6. Running totals typically use `UNBOUNDED PRECEDING` through `CURRENT ROW`.
7. Limited moving calculations can use a fixed number of preceding or following rows.
8. `PARTITION BY` can be combined with sliding windows to restart calculations within each category.
9. The `ORDER BY` inside `OVER()` determines which rows count as preceding or following.

---

## 🧠 Quick Mental Model

    PARTITION BY
    → Decide which group the current row belongs to

    ORDER BY
    → Decide the order of rows

    ROWS BETWEEN
    → Decide how many rows to include

    SUM(), AVG(), COUNT()
    → Calculate a value from those rows

    OVER(...)
    → Define the window for the calculation

**⭐ Remember:** A sliding window lets you calculate a running or moving value without removing the individual rows from your result.
